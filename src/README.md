# Mergington High School Activities API

A super simple FastAPI application that allows students to view and sign up for extracurricular activities.

## Features

- View all available extracurricular activities
- Sign up for activities
- Sign in with a student or faculty account
- Restrict enrollment changes to the signed-in student or faculty

## Getting Started

1. Install the dependencies:

   ```
   pip install fastapi uvicorn
   ```

2. Run the application:

   ```
   python app.py
   ```

3. Open your browser and go to:
   - API documentation: http://localhost:8000/docs
   - Alternative documentation: http://localhost:8000/redoc

### Demo accounts

The development defaults are:

- Faculty: `teacher@mergington.edu` / `teacher-password`
- Student: `student@mergington.edu` / `student-password`

Set `MERGINGTON_TEACHER_PASSWORD` and `MERGINGTON_STUDENT_PASSWORD` before
starting the server to replace the demo passwords. For a custom deployment,
set `MERGINGTON_USERS_FILE` to a JSON file containing users with `role` and
PBKDF2 `password_hash` fields. Do not commit production credentials.

## API Endpoints

| Method | Endpoint                                                          | Description                                                         |
| ------ | ----------------------------------------------------------------- | ------------------------------------------------------------------- |
| GET    | `/activities`                                                     | Get all activities with their details and current participant count |
| POST   | `/activities/{activity_name}/signup?email=student@mergington.edu` | Sign up for an activity                                             |
| POST   | `/auth/login`                                                    | Create a bearer session                                              |
| GET    | `/auth/me`                                                       | Get the current signed-in user                                       |

## Data Model

The application uses a simple data model with meaningful identifiers:

1. **Activities** - Uses activity name as identifier:

   - Description
   - Schedule
   - Maximum number of participants allowed
   - List of student emails who are signed up

2. **Students** - Uses email as identifier:
   - Name
   - Grade level

All data is stored in memory, which means data will be reset when the server restarts.
