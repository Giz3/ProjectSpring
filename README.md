# ProjectSpring

## Functional Requirements

### Survey Management
- Create new surveys with a title and description.
- Edit existing surveys.
- Delete surveys.
- View a list of all surveys.

### Question Management
- Add questions to a survey.
- Edit questions.
- Delete questions from a survey.
- Define the type of question (text question, multiple-choice question, etc.).

### Option Management
- Add options for multiple-choice questions.
- Edit options.
- Delete options.

### Student Survey Participation
- Students can view available surveys.
- Students can answer survey questions.
- Student responses are saved in the database.

### Response Collection and Analysis
- Collect student responses to survey questions.
- View survey results for each survey.
- Filter and sort responses by various criteria (e.g., by student, by question).

### Authentication and Authorization
- The system should support user registration and login (students).
- Administrators can create, edit, and delete surveys and questions.
- Students can only respond to surveys.

## System Behaviors

### Survey Management
- **Create Survey**: When an administrator creates a survey, the system should validate the title and description. If valid, the survey is saved to the database and a confirmation message is displayed.
- **Edit Survey**: When an administrator edits a survey, the system should retrieve the current survey data, allow modifications, validate the changes, and update the database. A success message is shown upon completion.
- **Delete Survey**: When an administrator deletes a survey, the system should confirm the action, remove the survey and its associated questions and responses from the database, and display a confirmation message.
- **View Surveys**: The system should display a list of all surveys, including their titles and descriptions, to administrators and students. 

### Question Management
- **Add Question**: When an administrator adds a question to a survey, the system should validate the question text and type, associate it with the correct survey, and save it to the database.
- **Edit Question**: When an administrator edits a question, the system should retrieve the question data, allow modifications, validate the changes, and update the database.
- **Delete Question**: When an administrator deletes a question, the system should confirm the action, remove the question and its associated options and responses from the database, and display a confirmation message.
- **Define Question Type**: The system should allow administrators to select the question type (e.g., text, multiple-choice) and ensure that the appropriate validation and storage mechanisms are applied.

### Option Management
- **Add Option**: When an administrator adds an option to a multiple-choice question, the system should validate the option text, associate it with the correct question, and save it to the database.
- **Edit Option**: When an administrator edits an option, the system should retrieve the option data, allow modifications, validate the changes, and update the database.
- **Delete Option**: When an administrator deletes an option, the system should confirm the action, remove the option from the database, and display a confirmation message.

### Student Survey Participation
- **View Surveys**: Students should be able to view a list of available surveys, including titles and descriptions.
- **Answer Survey Questions**: When a student answers survey questions, the system should validate the responses, associate them with the correct survey and student, and save them to the database.
- **Save Responses**: The system should ensure that all responses are stored correctly in the database, maintaining the association between students, questions, and surveys.

### Response Collection and Analysis
- **Collect Responses**: The system should collect and store all student responses in the database.
- **View Survey Results**: Administrators should be able to view the results of each survey, including aggregated data and individual responses.
- **Filter and Sort Responses**: The system should allow administrators to filter and sort responses by various criteria (e.g., by student, by question) to facilitate analysis.

### Authentication and Authorization
- **User Registration**: The system should support new student registrations, including validation of email addresses and other required information.
- **User Login**: The system should authenticate students and administrators based on their credentials, providing appropriate access levels.
- **Administrator Actions**: The system should restrict survey creation, editing, and deletion to administrators.
- **Student Actions**: The system should allow students only to view available surveys and submit responses.

## REST API Endpoints

### Authentication
- **POST /api/register**: Register a new user.
  - Request body: `{ "name": "string", "email": "string", "password": "string" }`
  - Response: `{ "message": "User registered successfully" }`
- **POST /api/login**: Authenticate a user and return a token.
  - Request body: `{ "email": "string", "password": "string" }`
  - Response: `{ "token": "jwt-token" }`

### Survey Management
- **GET /api/surveys**: Get a list of all surveys.
  - Response: `[ { "survey_id": "int", "title": "string", "description": "string", "created_date": "date" }, ... ]`
- **POST /api/surveys**: Create a new survey.
  - Request body: `{ "title": "string", "description": "string" }`
  - Response: `{ "message": "Survey created successfully", "survey_id": "int" }`
- **PUT /api/surveys/{id}**: Edit an existing survey.
  - Request body: `{ "title": "string", "description": "string" }`
  - Response: `{ "message": "Survey updated successfully" }`
- **DELETE /api/surveys/{id}**: Delete a survey.
  - Response: `{ "message": "Survey deleted successfully" }`

### Question Management
- **POST /api/surveys/{survey_id}/questions**: Add a question to a survey.
  - Request body: `{ "text": "string", "type": "string" }`
  - Response: `{ "message": "Question added successfully", "question_id": "int" }`
- **PUT /api/questions/{id}**: Edit a question.
  - Request body: `{ "text": "string", "type": "string" }`
  - Response: `{ "message": "Question updated successfully" }`
- **DELETE /api/questions/{id}**: Delete a question.
  - Response: `{ "message": "Question deleted successfully" }`

### Option Management
- **POST /api/questions/{question_id}/options**: Add an option to a multiple-choice question.
  - Request body: `{ "text": "string" }`
  - Response: `{ "message": "Option added successfully", "option_id": "int" }`
- **PUT /api/options/{id}**: Edit an option.
  - Request body: `{ "text": "string" }`
  - Response: `{ "message": "Option updated successfully" }`
- **DELETE /api/options/{id}**: Delete an option.
  - Response: `{ "message": "Option deleted successfully" }`

### Student Survey Participation
- **GET /api/surveys/{id}**: Get details of a survey including questions.
  - Response: `{ "survey_id": "int", "title": "string", "description": "string", "questions": [ { "question_id": "int", "text": "string", "type": "string", "options": [ { "option_id": "int", "text": "string" }, ... ] }, ... ] }`
- **POST /api/surveys/{survey_id}/responses**: Submit responses to survey questions.
  - Request body: `[ { "question_id": "int", "answer": "string" }, ... ]`
  - Response: `{ "message": "Responses submitted successfully" }`

### Response Collection and Analysis
- **GET /api/surveys/{id}/results**: Get the results of a survey.
  - Response: `{ "survey_id": "int", "title": "string", "description": "string", "responses": [ { "question_id": "int", "text": "string", "type": "string", "answers": [ { "student_id": "int", "answer": "string" }, ... ] }, ... ] }`
- **GET /api/surveys/{id}/responses**: Get all responses for a survey.
  - Response: `{ "survey_id": "int", "responses": [ { "student_id": "int", "question_id": "int", "answer": "string" }, ... ] }`

### User Management
- **GET /api/users/{id}**: Get user details.
  - Response: `{ "user_id": "int", "name": "string", "email": "string", "role": "string" }`
- **PUT /api/users/{id}**: Update user details.
  - Request body: `{ "name": "string", "email": "string", "password": "string" }`
  - Response: `{ "message": "User updated successfully" }`
- **DELETE /api/users/{id}**: Delete a user.
  - Response: `{ "message": "User deleted successfully" }`
