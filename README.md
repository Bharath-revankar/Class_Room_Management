# Classroom Management System

A simple, full-stack classroom management system built with Node.js, Express, MongoDB, and vanilla JavaScript. This application provides role-based access for students, teachers, and admins to manage classroom activities.

## Tech Stack

**Backend:**

- **Node.js** with **Express** for the server
- **MongoDB** with **Mongoose** for the database
- **JSON Web Tokens (JWT)** for authentication
- **Socket.io** for real-time WebSocket messaging
- **bcrypt** for secure password hashing
- **crypto** for field-level encryption of sensitive data
- **dotenv** for managing environment variables
- **multer** for handling file uploads

**Frontend:**

- **HTML5**
- **CSS3**
- **Vanilla JavaScript**

## Features

- **User Authentication:** Secure sign-up and login system with JWT.
- **Role-Based Access Control:**
  - **Student:** View announcements, submit assignments, view grades, and chat.
  - **Teacher:** Post announcements, create assignments, view submissions, grade assignments, and chat.
  - **Admin:** Manage all users and their roles, and chat.
- **Assignment Handling:** Teachers can post assignments, and students can upload their solutions.
- **Academic Records:** Securely store and manage student grades and attendance with encryption.
- **Real-time Messaging:** A global chat room for all users, powered by WebSockets.

## Project Structure

```
.
├── client/
│   ├── index.html
│   ├── login.html
│   ├── register.html
│   ├── dashboard.html
│   ├── style.css
│   └── app.js
│   └── dashboard.js
├── server/
│   ├── config/
│   │   ├── db.js
│   │   └── crypto.js
│   ├── controllers/
│   │   ├── authController.js
│   │   ├── announcementController.js
│   │   ├── assignmentController.js
│   │   ├── academicController.js
│   │   └── adminController.js
│   ├── middleware/
│   │   └── authMiddleware.js
│   ├── models/
│   │   ├── User.js
│   │   ├── Announcement.js
│   │   ├── Assignment.js
│   │   └── AcademicRecord.js
│   ├── routes/
│   │   ├── auth.js
│   │   ├── announcements.js
│   │   ├── assignments.js
│   │   ├── academics.js
│   │   └── admin.js
│   ├── uploads/
│   ├── .env
│   ├── package.json
│   └── server.js
└── .gitignore
└── README.md
```

## Setup and Installation

To run this project locally, follow these steps:

1.  **Clone the repository:**

    ```bash
    git clone <repository-url>
    cd <repository-directory>
    ```

2.  **Install backend dependencies:**

    ```bash
    cd server
    npm install
    ```

3.  **Set up environment variables:**

    - Create a `.env` file in the `server` directory.
    - Add the following variables:
      ```
      PORT=8090
      MONGO_URI=mongodb://localhost:27017/classroom
      JWT_SECRET=your_super_secret_jwt_key
      ```

4.  **Ensure MongoDB is running:**

    - Make sure you have a local MongoDB instance running or update the `MONGO_URI` to point to your database.

5.  **Start the server:**

    ```bash
    node server.js
    ```

6.  **Open the application:**
    - Open your web browser and navigate to `http://localhost:8090`.

## How to Use

1.  **Register Users:** Create accounts for a student, a teacher, and an admin.
2.  **First Admin:** To create the first admin user, register a new user and then manually update their `role` in the MongoDB `users` collection to `"admin"`.
3.  **Explore:** Log in with each user to explore their respective dashboards and functionalities.

## visual
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Classroom Management System - Documentation</title>
    <style>
      body {
        font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
          "Helvetica Neue", Arial, sans-serif;
        line-height: 1.6;
        color: #333;
        max-width: 1200px;
        margin: 0 auto;
        padding: 20px;
        background-color: #f9f9f9;
      }
      h1,
      h2,
      h3,
      h4 {
        color: #2c3e50;
        border-bottom: 2px solid #3498db;
        padding-bottom: 10px;
      }
      h1 {
        font-size: 2.5em;
      }
      h2 {
        font-size: 2em;
      }
      h3 {
        font-size: 1.5em;
      }
      code,
      pre {
        background-color: #ecf0f1;
        border-radius: 4px;
        padding: 2px 6px;
        font-family: "Courier New", Courier, monospace;
      }
      pre {
        padding: 15px;
        overflow-x: auto;
        border: 1px solid #ddd;
      }
      .container {
        background-color: #fff;
        padding: 25px;
        border-radius: 8px;
        box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
        margin-bottom: 20px;
      }
      .flow-diagram {
        display: flex;
        align-items: center;
        justify-content: space-around;
        margin: 30px 0;
        flex-wrap: wrap;
      }
      .flow-box {
        background-color: #eaf5ff;
        border: 2px solid #3498db;
        border-radius: 8px;
        padding: 15px;
        text-align: center;
        min-width: 150px;
        box-shadow: 0 2px 5px rgba(0, 0, 0, 0.05);
        margin: 10px;
      }
      .flow-arrow {
        font-size: 2em;
        color: #3498db;
        margin: 10px;
      }
      .file-path {
        font-weight: bold;
        color: #c0392b;
      }
      table {
        width: 100%;
        border-collapse: collapse;
        margin-bottom: 20px;
      }
      th,
      td {
        border: 1px solid #ddd;
        padding: 12px;
        text-align: left;
      }
      th {
        background-color: #f2f2f2;
        font-weight: bold;
      }
    </style>
  </head>
  <body>
    <div class="container">
      <h1>Classroom Management System: Project Documentation</h1>
      <p>
        This document provides a comprehensive overview of the project's
        architecture, code structure, and the end-to-end flow of its core
        functionalities.
      </p>
    </div>

    <div class="container">
      <h2>1. Technology Stack</h2>
      <table>
        <thead>
          <tr>
            <th>Category</th>
            <th>Technology</th>
            <th>Purpose</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td><strong>Backend</strong></td>
            <td>Node.js / Express.js</td>
            <td>API Server and Routing</td>
          </tr>
          <tr>
            <td><strong>Database</strong></td>
            <td>MongoDB with Mongoose</td>
            <td>Data storage and object modeling</td>
          </tr>
          <tr>
            <td><strong>Authentication</strong></td>
            <td>JSON Web Tokens (JWT)</td>
            <td>Secure, stateless user authentication</td>
          </tr>
          <tr>
            <td><strong>File Handling</strong></td>
            <td>Multer</td>
            <td>
              Middleware for handling file uploads (e.g., assignment
              submissions)
            </td>
          </tr>
          <tr>
            <td><strong>Frontend</strong></td>
            <td>HTML / CSS / Vanilla JavaScript</td>
            <td>User interface and client-side logic</td>
          </tr>
          <tr>
            <td><strong>Real-time</strong></td>
            <td>Socket.IO</td>
            <td>Live global chat functionality</td>
          </tr>
        </tbody>
      </table>
    </div>

    <div class="container">
      <h2>2. Project Structure</h2>
      <p>
        The project is organized into two main directories:
        <code>client</code> for all frontend assets and <code>server</code> for
        all backend logic.
      </p>
      <pre>
/github_classroom
|
|-- /client/
|   |-- dashboard.html      # Main application SPA (Single Page Application)
|   |-- dashboard.js        # Frontend logic for the dashboard
|   |-- login.html          # User login page
|   |-- login.js            # Frontend logic for login
|   |-- register.html       # User registration page
|   |-- register.js         # Frontend logic for registration
|   `-- style.css           # Global stylesheet
|
`-- /server/
    |-- /controllers/       # Business logic for API routes
    |-- /middleware/        # Authentication and authorization checks
    |-- /models/            # Database schemas (Mongoose)
    |-- /routes/            # API endpoint definitions
    |-- /uploads/           # Storage for submitted assignment files
    |-- .env                # Environment variables (DB URI, JWT Secret)
    `-- server.js           # Main backend server entry point
</pre
      >
    </div>

    <div class="container">
      <h2>3. Code Explanation: File by File</h2>

      <h3>Frontend (`/client`)</h3>
      <p>
        The frontend is built without a framework, using HTML templates and
        vanilla JavaScript to create a dynamic experience.
      </p>

      <h4><span class="file-path">client/login.html & register.html</span></h4>
      <p>
        Standard HTML forms for user authentication. They link to their
        respective JavaScript files.
      </p>

      <h4><span class="file-path">client/login.js & register.js</span></h4>
      <p>
        These files handle form submissions. They gather user input, send it to
        the backend API using <code>fetch()</code>, and handle the response. On
        successful login, <code>login.js</code> saves the received JWT to
        <code>localStorage</code> and redirects the user to the dashboard.
      </p>

      <h4><span class="file-path">client/dashboard.html</span></h4>
      <p>
        This is the core of the user interface. It's a single page that contains
        HTML <code>&lt;template&gt;</code> tags for each user role (Student,
        Teacher, Admin). This allows the UI for each role to be defined in one
        place.
      </p>

      <h4><span class="file-path">client/dashboard.js</span></h4>
      <p>
        This is the most important frontend file. On page load, it performs
        these key actions:
      </p>
      <ol>
        <li>
          Checks for a JWT in <code>localStorage</code>. If none exists, it
          redirects to the login page.
        </li>
        <li>
          Decodes the JWT to get the user's <strong>role</strong> and
          <strong>username</strong>.
        </li>
        <li>
          Selects the correct HTML <code>&lt;template&gt;</code> based on the
          user's role and injects it into the page.
        </li>
        <li>
          Makes API calls to the backend (e.g., <code>/api/assignments</code>,
          <code>/api/announcements</code>) to fetch data.
        </li>
        <li>
          Dynamically renders the fetched data into the appropriate lists and
          sections on the page.
        </li>
        <li>Sets up all event listeners for buttons, forms, and the chat.</li>
      </ol>

      <h3>Backend (`/server`)</h3>

      <h4><span class="file-path">server/server.js</span></h4>
      <p>
        The entry point for the Node.js application. It sets up the Express
        server, connects to MongoDB, configures middleware (like serving the
        `client` and `uploads` directories statically), and mounts the API
        routes.
      </p>

      <h4><span class="file-path">server/models/</span></h4>
      <p>
        This directory contains the Mongoose schemas that define the structure
        of data in MongoDB.
      </p>
      <ul>
        <li>
          <code>User.js</code>: Defines the schema for users, including
          username, password (hashed), role, and roll number.
        </li>
        <li>
          <code>Assignment.js</code>: Defines assignments, including title,
          description, the teacher who created it, and an array of submissions
          (which includes student, file path, and grade).
        </li>
        <li>
          <code>Announcement.js</code>: Schema for announcements made by
          teachers.
        </li>
        <li>
          <code>AcademicRecord.js</code>: Stores a student's grades across all
          assignments.
        </li>
      </ul>

      <h4>
        <span class="file-path">server/middleware/authMiddleware.js</span>
      </h4>
      <p>Crucial for security. It provides functions to protect API routes.</p>
      <ul>
        <li>
          <code>isLoggedIn</code>: Checks for a valid JWT in the request header.
          If valid, it decodes the user info and attaches it to the request
          object (<code>req.user</code>).
        </li>
        <li>
          <code>isTeacher</code>, <code>isStudent</code>, <code>isAdmin</code>:
          These functions first call <code>isLoggedIn</code> and then check if
          the <code>req.user.role</code> matches the required role for the
          route.
        </li>
      </ul>

      <h4><span class="file-path">server/routes/</span></h4>
      <p>
        Defines the API endpoints. Each file maps HTTP methods (GET, POST, PUT)
        for a specific resource to controller functions and protects them with
        authentication middleware.
      </p>
      <pre>
// Example from server/routes/assignments.js
// Protects the route, ensuring only a logged-in student can access it.
router.post(
  "/:id/submit",
  authMiddleware.isStudent, 
  assignmentController.submitAssignment
);</pre
      >

      <h4><span class="file-path">server/controllers/</span></h4>
      <p>
        Contains the core business logic. These functions are executed by the
        router when an API endpoint is hit. They interact with the database
        models to perform CRUD (Create, Read, Update, Delete) operations.
      </p>
      <ul>
        <li>
          <code>authController.js</code>: Handles user registration and login
          logic.
        </li>
        <li>
          <code>assignmentController.js</code>: Manages creating assignments,
          retrieving them, handling submissions (using Multer), and grading.
        </li>
      </ul>
    </div>

    <div class="container">
      <h2>4. End-to-End Project Flow</h2>
      <p>
        This section illustrates the complete lifecycle of a user interaction,
        from registration to logout.
      </p>

      <h3>Flow 1: User Registration and Login</h3>
      <div class="flow-diagram">
        <div class="flow-box">
          <strong>1. Frontend</strong><br />User fills Register/Login Form
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>2. Frontend JS</strong><br /><code>fetch()</code> API call
          to<br /><code>/api/auth/register</code>
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>3. Backend Router</strong><br />Route matches in
          <code>auth.js</code>
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>4. Backend Controller</strong><br /><code
            >authController</code
          >
          hashes password, saves user to DB
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>5. Database</strong><br />New User document created
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>6. Backend Controller</strong><br />Generates JWT
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>7. Frontend JS</strong><br />Receives JWT, saves to
          <code>localStorage</code>, redirects to <code>dashboard.html</code>
        </div>
      </div>

      <h3>Flow 2: Authenticated Action (e.g., Student Views Assignments)</h3>
      <div class="flow-diagram">
        <div class="flow-box">
          <strong>1. Frontend</strong><br /><code>dashboard.js</code> loads
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>2. Frontend JS</strong><br /><code
            >fetch('/api/assignments')</code
          >
          with JWT in Header
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>3. Backend Middleware</strong><br /><code
            >authMiddleware.isLoggedIn</code
          >
          verifies JWT
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>4. Backend Controller</strong><br /><code
            >assignmentController</code
          >
          fetches assignments from DB
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>5. Database</strong><br />Returns assignment data
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>6. Frontend JS</strong><br />Receives JSON data and renders it
          as HTML
        </div>
      </div>

      <h3>Flow 3: Student Submits an Assignment</h3>
      <div class="flow-diagram">
        <div class="flow-box">
          <strong>1. Frontend</strong><br />Student selects file and clicks
          "Submit"
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>2. Frontend JS</strong><br />Sends <code>FormData</code> to
          <code>/api/assignments/:id/submit</code>
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>3. Backend Middleware</strong><br /><code
            >authMiddleware.isStudent</code
          >
          checks role
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>4. Backend Controller</strong><br /><code>multer</code>
          middleware processes the file upload
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>5. Server File System</strong><br />File is saved to
          <code>/server/uploads/</code>
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>6. Backend Controller</strong><br />Saves file path and
          student ID to the Assignment in DB
        </div>
      </div>

      <h3>Flow 4: Logout</h3>
      <div class="flow-diagram">
        <div class="flow-box">
          <strong>1. Frontend</strong><br />User clicks "Logout" button
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>2. Frontend JS</strong><br /><code
            >localStorage.removeItem('token')</code
          >
        </div>
        <div class="flow-arrow">&rarr;</div>
        <div class="flow-box">
          <strong>3. Frontend</strong><br /><code
            >window.location.href = 'login.html'</code
          >
        </div>
      </div>
    </div>
  </body>
</html>
