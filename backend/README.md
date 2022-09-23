# Coffee Shop Backend

## Getting Started

### Installing Dependencies

#### Python 3.7

Follow instructions to install the latest version of python for your platform in the [python docs](https://docs.python.org/3/using/unix.html#getting-and-installing-the-latest-version-of-python)

#### Virtual Environment

We recommend working within a virtual environment whenever using Python for projects. This keeps your dependencies for each project separate and organized. Instructions for setting up a virtual environment for your platform can be found in the [python docs](https://packaging.python.org/guides/installing-using-pip-and-virtual-environments/)

#### PIP Dependencies

Once you have your virtual environment setup and running, install dependencies by naviging to the `/backend` directory and running:

```bash
pip install -r requirements.txt
```

This will install all of the required packages we selected within the `requirements.txt` file.

##### Key Dependencies

- [Flask](http://flask.pocoo.org/) is a lightweight backend microservices framework. Flask is required to handle requests and responses.

- [SQLAlchemy](https://www.sqlalchemy.org/) and [Flask-SQLAlchemy](https://flask-sqlalchemy.palletsprojects.com/en/2.x/) are libraries to handle the lightweight sqlite database. Since we want you to focus on auth, we handle the heavy lift for you in `./src/database/models.py`. We recommend skimming this code first so you know how to interface with the Drink model.

- [jose](https://python-jose.readthedocs.io/en/latest/) JavaScript Object Signing and Encryption for JWTs. Useful for encoding, decoding, and verifying JWTS.

## Running the server

From within the `./src` directory first ensure you are working using your created virtual environment.

Each time you open a new terminal session, run:

```bash
export FLASK_APP=api.py;
```

To run the server, execute:

```bash
flask run --reload
```

The `--reload` flag will detect file changes and restart the server automatically.

# API Documentation

## Endpoints

|Method   | API Endpoints                                              | Purpose                                          |                             
|--------------| -------------------------------------------------------|:-------------------------------------------------------:|
|    GET       |```/drinks```                                   |```Fetches all the drinks from the server```                 |      
|    GET      |```/drink-details```                                    |```Fetches the recipe of the selected drink```                             |
|    DELETE    |```/drinks/<int:id>```           |```Deletes a particular drink```              |
|    POST      |```/drinks```                                    |```Creates a new drink```           |
|    PATCH      |```/drinks/<int:id>```                             |```Updates the title, recipe or parts of a drink```| 


### `GET '/drinks'`

- Fetches a JSON of all the drinks in the database and displays them all.
- Request Arguments: None
- Returns: An object with a three keys, `tile`, `recipe` and `parts`.
- Try: `curl -H "Authorization: Bearer <token>"  http://127.0.0.1:5000/drinks`

```json
{"drinks":[
   {"id":1,
   "recipe":[
      {"color":"blue",
      "parts":1}
            ],
"title":"water"}
         ],
   "success":true}


```

### `GET '/drink-details'`

- Fetches a JSON of all the drinks in the database and displays them all and allows for editing.
- Request Arguments: None
- Returns: An object with a three keys, `tile`, `recipe` and `parts`.
- Try: `curl -H "Authorization: Bearer <token>"  http://127.0.0.1:5000/drinks`

```json
{"drinks":[
   {"id":1,
   "recipe":[
      {"color":"blue",
      "name":"water",
      "parts":1}],
   "title":"water"}]
   ,"success":true}
```

### `DELETE '/drinks/<int:id>'`

- Deletes the drink that corresponds to the given ID. 
- Request Arguments: id
- Returns: An object with success message after deletion.
- Try: `curl -H "Authorization: Bearer <token>"  http://127.0.0.1:5000/drinks/1 -DELETE`


```json
{
   "delete":1,
   "success":true
}
```

### `PATCH '/drinks/<int:id>'`

- Posts a new question into the database with question, answer, category and difficulty fields.
- Request Arguments: None
- Returns: An object with a success message and the list of new questions after insertion.
- Try: `curl http://127.0.0.1:5000/trivia/questions -X POST -H "Content-Type: application/json" -d '{"question": "Who is Chelsea's most prolific striker?", "answer": "Didier Drogba", "category": 6, "difficulty": 2}'`


```json
{
  "1": "Science",
  "2": "Art",
  "3": "Geography",
  "4": "History",
  "5": "Entertainment",
  "6": "Sports"
}
```

### `POST '/trivia/questions/search'`

- Searches for questions that match the search word provided.
- Request Arguments: search word
- Returns: A dictionary of questions that matched with the search term.
- Try: `curl http://127.0.0.1:5000/trivia/questions/search?search=Taj -X POST`

```json
{
  "questions": [
    {
      "answer": "Agra",
      "category": 3,
      "difficulty": 2,
      "id": 15,
      "question": "The Taj Mahal is located in which Indian city?"
    }
  ],
  "success": true,
  "total_questions": 1
}
```

### `GET '/trivia/categories/<category_id>/questions'`

- Fetches a dictionary of questions belonging to the category specified.
- Request Arguments: category_id
- Returns: A dictionary of questions under the given category_id.
- Try: `curl http://127.0.0.1:5000/trivia/categories/1/questions`

```json
{
  "current_category": 1,
  "questions": [
    {
      "answer": "The Liver",
      "category": 1,
      "difficulty": 4,
      "id": 20,
      "question": "What is the heaviest organ in the human body?"
    },
    {
      "answer": "Alexander Fleming",
      "category": 1,
      "difficulty": 3,
      "id": 21,
      "question": "Who discovered penicillin?"
    },
    {
      "answer": "Blood",
      "category": 1,
      "difficulty": 4,
      "id": 22,
      "question": "Hematology is a branch of medicine involving the study of what?"
    }
  ],
  "success": true,
  "total_questions": 3
}
```

### `POST '/trivia/play'`

- Starts the quiz by fetching randoming questions for the user to post answers.
- Request Arguments: search word
- Returns: A dictionary of that has not already been used.
- Try: `curl http://127.0.0.1:5000/trivia/play -X POST -H "Content-Type: application/json" -d '{"previous_questions": [], "quiz_category": {"type": "sports", "id": "6"}}'`

```json
{
  "question": {
    "answer": "Uruguay",
    "category": 6,
    "difficulty": 4,
    "id": 11,
    "question": "Which country won the first ever soccer World Cup in 1930?"
  },
  "success": true
}
```

