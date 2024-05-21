# ProjectSpring

## Functional Requirements

### Academic Program Management

- **Create Faculty**: System administrators can create new faculties by specifying the faculty ID and name.
- **Create Course**: Administrators can add new courses by specifying the course ID, name, description, and linking them to a specific faculty.
- **Create Student**: Administrators can add new students by providing personal details such as first name, last name, date of birth, gender, email, phone, and address. Each student is also associated with a specific course.

### Conducting Surveys

- **Create General Survey Info**: Administrators can create new surveys by specifying the title, description, and date of the survey.
- **Add Questions to Survey**: Administrators can add questions to a survey by providing the question text and type (text, multiple-choice, etc.).
- **Collect Answers to Questions**: The system collects student responses to survey questions and stores them for further analysis.

## System Behaviors

### Academic Program Management

- **Create Faculty**: The system verifies the entered data and creates a new faculty in the database.
- **Create Course**: Upon verification of the entered data, the system adds a new course to the database, linking it to the appropriate faculty.
- **Create Student**: The system verifies student data and adds them to the database, associating them with a specific course.

### Conducting Surveys

- **Create General Survey Info**: After verifying the entered data, the system saves survey information in the database.
- **Add Questions to Survey**: The system verifies the entered data and adds questions to the survey in the database.
- **Collect Answers to Questions**: The system collects student responses to survey questions and stores them in the database for analysis.

## REST API Endpoints

### Academic Program Management

- **POST /api/faculties**: Create a new faculty.
- **POST /api/courses**: Add a new course.
- **POST /api/students**: Add a new student.

### Conducting Surveys

- **POST /api/surveys**: Create a new survey.
- **POST /api/questions**: Add a new question to a survey.
- **POST /api/answers**: Collect answers to survey questions.
