Here is a comprehensive README.md file tailored to the web application code you
provided.

Uthsav - TDTTI Thuravoor (Registration System)

A lightweight, responsive, single-page web application designed to manage
student registrations for school festivals and cultural events (Kalothswom,
Science Fests, Sports Fests, etc.).

This system features a dual-role architecture (Student & Official), robust
registration validation rules, an admin dashboard, and relies on Google Apps
Script (Google Sheets) as its backend database.

🌟 Key Features

For Students:

  - Phone Number Login: Quick and easy access using a registered phone number.
  - Smart Registration: Auto-populates event details (Category, Duration, Max
    Participants) based on the selected Fest and Item.
  - Rule Enforcement: Automatically prevents students from registering for the
    same item twice and enforces participation limits (e.g., max 3 individual
    items, max 2 group items per fest).
  - Group Events: Allows the selection of multiple participants and assignment
    of a "Team Leader".
  - Personalized Dashboard: Students only see their own registration records.

For Officials / Admins:

  - Secure Login: ID and Password based authentication with a "Keep me logged
    in" feature.
  - Comprehensive Records: View all registrations in sortable tables divided
    into "Individual" and "Group" items.
  - Advanced Filtering: Filter records by Class, Division, or a global search
    text.
  - Admin Dashboard:
      - Global Registration Control: Open or Close global registration with a
        custom display message.
      - Fest Management: Enable or disable specific fests dynamically.
      - User Management: Create, Edit, and Delete Official user accounts
        directly from the UI.
  - Session Tracking: Tracks active session time and logs login/logout
    timestamps to the database.

System-wide:

  - Responsive Design: Works seamlessly on desktops, tablets, and mobile
    devices.
  - Auto-Complete Search: Easily search for students by Admission Number, Name,
    or Phone Number during registration.
  - UI Notifications: Custom toast notifications for errors and success
    messages, plus a loading overlay.

🛠️ Tech Stack

  - Frontend: HTML5, CSS3, Vanilla JavaScript (ES6+).
  - Backend / Database: Google Apps Script (doPost and doGet) connected to
    Google Sheets.

🚀 Setup & Installation

Because this application relies on Google Sheets as its backend, you must have a
corresponding Google Apps Script deployed as a Web App to make it fully
functional.

1. Update the Execution URL

Open the index.html file.

Replace the URL with the Web App URL generated from your Google Apps Script
deployment.

2. Required Database Structure (Google Sheets)

Your connected Google Sheet should contain the following tables/sheets to match
the frontend expectations:

  - Students: Admission Number, Name, Gender, Class, Division, Phone No
  - Fests: Fest Name, Item, Item Code, Category (e.g., Boy/Girl/General), No of
    Participants, Duration
  - Registrations: Timestamp, Admission Number, Name, Class, Division, Name of
    Fest, Item, Category, No of Participants, Role in Event
  - Users: User ID, Name, Password, Role (Set to "Official")
  - Settings: Key, Value (Keys like Global_Registration, Global_Message,
    Fest_Art Fest, etc.)

📖 Usage Guide

Logging In

1.  Student Login: Navigate to the "Student" tab, enter the registered phone
    number, and click Login.
2.  Official Login: Navigate to the "Official" tab, enter the User ID and
    Password provided by the administrator.

Making a Registration

1.  Ensure you are on the Registration tab.
2.  Select the Fest and the specific Event Item.
3.  The system will automatically display the required number of participant
    slots.
4.  Use the search bar in the participant block to find a student by Name, Admn
    No, or Phone.
5.  If it is a group item, select one student to be the Team Leader.
6.  Click Register Student(s).

Viewing Records (Officials)

1.  Go to the View Records tab.
2.  Use the dropdowns at the top to filter by Class and Division.
3.  Type in the search box to find specific students or event names.
4.  Click on any table header (e.g., "Name ↕") to sort the data alphabetically
    or numerically.

⚠️ Security Notes

  - Client-Side Validation: The current app uses client-side validation to
    prevent exceeding participation limits. Ensure your Google Apps Script
    backend also re-verifies these rules before writing to the Google Sheet to
    prevent API abuse.
  - Passwords: Official passwords currently appear to be stored and transmitted
    in plain text. For production use in a sensitive environment, consider
    implementing hashing on the backend.

📄 License

This project is open-source and free to modify for educational and institutional
use. Customizations specific to TDTTI Thuravoor have been integrated.
