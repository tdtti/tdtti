# Teacher Subject Distribution & Timetable System

A single-page school scheduling tool for nine divisions (`5B`–`7D`) and 15 faculty members. It stores teacher allocations in Cloud Firestore, generates weekly class and teacher timetables, identifies unplaced lessons, and prepares WhatsApp-ready schedule messages.

## What it supports

- **Teacher allotment** — assign class/subject workloads and class-in-charge responsibilities, with live weekly-load totals.
- **Allocation views** — teacher-by-class and subject-by-class matrices with per-class totals against the required **35 periods/week**.
- **Timetable engine** — creates a five-day, seven-period timetable (315 class periods) while applying teacher collision, daily-load, P7, IT/PE, SV/LIB, P1, and language-elective rules.
- **Fixed language matrix** — places the prescribed Standard 5, 6, and 7 language electives at their mandated synchronized slots and keeps ANM free in each of those slots.
- **Operational tools** — Firestore live sync, local diagnostic fixes, printable A4 landscape reports, substitute availability, and WhatsApp sharing for allocations and timetables.

## Run locally

This is a static application. Serve the repository directory with any web server, for example:

```bash
python3 -m http.server 8080
```

Then open `http://localhost:8080` in a browser.

## Firebase configuration

Firebase is initialized in `index.html`. The app uses these document paths:

- `teacher_allocations/{teacherCode}`
- `school_data/weekly_timetable`
- `school_data/teacher_phones`

Use Firebase Security Rules appropriate to your school before deploying. API keys embedded in frontend code identify a Firebase project but do not replace access-control rules.

## Scheduling assumptions

- Week: Monday–Friday; P1–P7 (09:20–15:20) for each division.
- Core 5-period subjects are distributed at most once per day by the solver.
- P7 excludes `ENG`, `BS`, `SS`, `MM`, `HIN`, `MI`, and `MII`; `SV/LIB` is P7-only.
- Only one IT lab and one PE ground lesson may run in a P2–P7 slot.
- Teachers must teach at least four periods per day, with at most two consecutive teaching periods and one consecutive free period.
- The available allocations must add up to 35 periods per division for a complete timetable. The diagnostic panel identifies shortages or lessons that cannot be placed.

## Teacher workload rules

A timetable is published only when every class has exactly 35 allocated periods and every teacher has 20–25 allocated periods for the week. The generated timetable must also give each teacher at least four teaching periods on every school day, with no run longer than two consecutive teaching periods or one consecutive free period. If a configuration or generated draft cannot meet these requirements, the diagnostic panel lists the rule violations and preserves the last valid timetable.
A timetable is only reported as conflict-free when every teacher has at least four teaching periods on each school day, has no run longer than two consecutive teaching periods, and has no run longer than one consecutive free period. If the configured allocations cannot meet these requirements, the diagnostic panel names every teacher/day violation instead of reporting a false success.
