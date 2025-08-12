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
