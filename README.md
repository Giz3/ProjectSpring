# ProjectSpring

## Functional Requirements

### Academic Program Management

- **Create Faculty**: System administrators can create new faculties by specifying the faculty ID and name. This involves providing unique identifiers for each faculty and assigning them appropriate names. Faculties represent academic departments or divisions within the institution.
- **Create Course**: Administrators can add new courses by specifying the course ID, name, description, and linking them to a specific faculty. Each course should have a unique identifier, a descriptive name, and an optional description. Additionally, courses should be associated with a particular faculty to indicate their departmental affiliation.
- **Create Student**: Administrators can add new students by providing personal details such as first name, last name, date of birth, gender, email, phone, and address. Each student should be associated with a specific course to facilitate academic tracking and management. Student records should also include unique identifiers to distinguish between individual students.

### Conducting Surveys

- **Create General Survey Info**: Administrators can create new surveys by specifying the title, description, and date of the survey. Surveys serve as the primary instrument for collecting feedback or data from students. They should have informative titles, descriptive descriptions, and scheduled dates for administration. Additionally, surveys should be assigned unique identifiers for tracking purposes.
- **Add Questions to Survey**: Administrators can add questions to a survey by providing the question text and type (text, multiple-choice, etc.). Questions form the basis of the survey instrument and should be carefully crafted to elicit the desired responses from students. Each question should be associated with a specific survey to maintain survey integrity and coherence.
- **Collect Answers to Questions**: The system collects student responses to survey questions and stores them for further analysis. Responses should be recorded accurately and securely, preserving the integrity of the data throughout the collection process. Each response should be linked to the corresponding question and survey to facilitate analysis and interpretation.

## System Behaviors

### Academic Program Management

- **Create Faculty**: The system verifies the entered data and creates a new faculty in the database. It performs validation checks to ensure that each faculty has a unique identifier and that all required fields are provided. Upon successful creation, the system generates a confirmation message and assigns a unique identifier to the new faculty.
- **Create Course**: Upon verification of the entered data, the system adds a new course to the database, linking it to the appropriate faculty. It checks for the existence of the associated faculty and ensures that the course ID is unique. After successful addition, the system provides feedback to the user and assigns a unique identifier to the new course.
- **Create Student**: The system verifies student data and adds them to the database, associating them with a specific course. It validates input fields to maintain data integrity and checks for the existence of the associated course. Upon successful addition, the system generates a confirmation message and assigns a unique identifier to the new student.

### Conducting Surveys

- **Create General Survey Info**: After verifying the entered data, the system saves survey information in the database. It ensures that all required fields are provided and performs checks to prevent duplicate survey titles or IDs. Upon successful creation, the system provides feedback to the user and assigns a unique identifier to the new survey.
- **Add Questions to Survey**: The system verifies the entered data and adds questions to the survey in the database. It validates question text and type to ensure consistency and accuracy in data collection. Upon successful addition, the system provides feedback to the user and assigns a unique identifier to the new question.
- **Collect Answers to Questions**: The system collects student responses to survey questions and stores them in the database for analysis. It maintains the association between responses, questions, and surveys to facilitate data retrieval and analysis. Upon successful collection, the system generates a confirmation message and assigns a unique identifier to each response.

## REST API Endpoints

### Academic Program Management

- **POST /api/faculties**: Create a new faculty.
  - Request: `{ "facultyName": "Engineering", "facultyCode": "ENG" }`
  - Response: `{ "success": true, "message": "Faculty created", "faculty": { "id": 1, "facultyName": "Engineering", "facultyCode": "ENG" } }`

- **POST /api/courses**: Add a new course.
  - Request: `{ "courseName": "Intro to CS", "courseCode": "CS101", "description": "Introductory course", "facultyId": 1 }`
  - Response: `{ "success": true, "message": "Course created", "course": { "id": 1, "courseName": "Intro to CS", "courseCode": "CS101", "description": "Introductory course", "facultyId": 1 } }`

- **POST /api/students**: Add a new student.
  - Request: `{ "firstName": "John", "lastName": "Doe", "dateOfBirth": "1995-08-25", "gender": "Male", "email": "john.doe@example.com", "phone": "123-456-7890", "address": "123 Main St", "courseId": 1 }`
  - Response: `{ "success": true, "message": "Student created", "student": { "id": 1, "firstName": "John", "lastName": "Doe", "dateOfBirth": "1995-08-25", "gender": "Male", "email": "john.doe@example.com", "phone": "123-456-7890", "address": "123 Main St", "courseId": 1 } }`

### Conducting Surveys

- **POST /api/surveys**: Create a new survey.
  - Request: `{ "title": "Satisfaction Survey", "description": "Feedback collection", "dateConducted": "2024-05-31" }`
  - Response: `{ "success": true, "message": "Survey created", "survey": { "id": 1, "title": "Satisfaction Survey", "description": "Feedback collection", "dateConducted": "2024-05-31" } }`

- **POST /api/questions**: Add a new question to a survey.
  - Request: `{ "surveyId": 1, "questionText": "How satisfied are you?", "questionType": "Multiple Choice", "options": ["Very satisfied", "Satisfied", "Neutral"] }`
  - Response: `{ "success": true, "message": "Question added", "question": { "id": 1, "surveyId": 1, "questionText": "How satisfied are you?", "questionType": "Multiple Choice", "options": ["Very satisfied", "Satisfied", "Neutral"] } }`

- **POST /api/answers**: Collect answers to survey questions.
  - Request: `{ "questionId": 1, "studentId": 1, "answerText": "Very satisfied" }`
  - Response: `{ "success": true, "message": "Answer submitted", "answer": { "id": 1, "questionId": 1, "studentId": 1, "answerText": "Very satisfied" } }`
