# Udacity_Trivia_API_Project2
## Trivia  API Documentation

### Getting Started
- Base URL: This app can only be run locally and it isn't hosted as a base URL. The backend app is hosted at the default, `http://127.0.0.1:3000/questions`, which is set as a proxy in the frontend configuration. 
- Authentication: This version of the application does not require authentication or API keys.

### Error Handling
Errors are returned as JSON objects in the following format:
```
{
    "success": False, 
    "error": 400,
    "message": "bad request"
}
```
The API will return four error types when requests fail:
- 400: Bad Request
- 404: Resource Not Found
- 422: Not Processable
- 405: Method not allowed


### Expected Endpoints And Behaviours
### 1. GET '/categories'

- Fetches a dictionary of categories containing 'id' and the corresponding category value
- Request Arguments: None
- Returns: An object with a single key, categories, that contains an object of id: category_string key:value pairs.

```json
{
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  }
}
```

---

### 2. GET '/questions?page=${integer}'

- Fetches a paginated set of questions, a total number of questions, all categories and current category string.
- Request Arguments: `page` - integer
- Returns: An object with 10 paginated questions, total questions, object including all categories, and current category string

```json
{
  "questions": [
    {
      "id": 1,
      "question": "This is a question",
      "answer": "This is an answer",
      "difficulty": 4,
      "category": 1
    }
  ],
  "totalQuestions": 100,
  "categories": {
    "1": "Science",
    "2": "Art",
    "3": "Geography",
    "4": "History",
    "5": "Entertainment",
    "6": "Sports"
  },
  "currentCategory": "Sports"
}
```

---

### 3. `GET '/categories/${id}/questions'`

- Fetches questions for a cateogry  through specific id request argument
- Request Arguments: `id` - (integer)
- Returns: An object with questions for the specified category, total questions, and current category string

```json
{
  "questions": [
    {
      "id": 1,
      "question": "This is a question",
      "answer": "This is an answer",
      "difficulty": 5,
      "category": 3
    }
  ],
  "'number_of_total _questions": 100,
  "current_category": 3,
  "currentCategory": "Geography"
}
```

---

### 4.`DELETE '/questions/${id}'`

- Deletes a specific question via the id of the question
- Request Arguments: `id` - (integer)
- Returns: Returns the id of the question delete and shows the number of questions left. 
```json
{
    "success": true,
    "deleted": "${id}",
    "questions": "${Number of questions left}"
}
```
---

### 5. `POST '/quizzes'`

- A post request is sent in order to get the next question
- Request Body:

```json
{
    "previous_questions": [1, 4, 20, 15],
    "quiz_category": "current category"
 }
```

- Returns: a single new question object which is not among the "previous_questions"

```json
{
  "question": {
    "id": 1,
    "question": "This is a question",
    "answer": "This is an answer",
    "difficulty": 5,
    "category": 4
  }
}
```

---

### 6. `POST '/questions'`

- A post request is sent in order to add a new question
- Request Body:

```json
{
  "question": "A new question string",
  "answer": "A new answer string",
  "difficulty": 1,
  "category": 3
}
```

- Returns: Returns the view of the currenr question added and total number of questions.
```json
{
    "success": true,
    "question": "current_questions",
    "total_questions": "len(questions)"
}
```

---

### 7. `POST '/questions'`

- A post request is sent in order to search for a specific question by search term
- Request Body:

```json
{
  "searchTerm": "this is the term the user is looking for"
}
```

- Returns: any array of questions, a number of totalQuestions that met the search term and the current category string. An error is returned if the search does not exist amongst the bank of existing questions.

```json
{
  "questions": [
    {
      "id": 1,
      "question": "This is a question",
      "answer": "This is an answer",
      "difficulty": 5,
      "category": 5
    }
  ],
  "totalQuestions": 100,
  "currentCategory": "Entertainment"
}
```
