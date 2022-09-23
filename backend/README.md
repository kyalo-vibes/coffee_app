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

- Updates an existing drink in the database by changing either the title, recipe, or parts fields.
- Request Arguments: id
- Returns: An object with a success message after updating.
- Try: `curl -H "Authorization: Bearer <token>"  http://127.0.0.1:5000/drinks/1 -PATCH -H "Content-Type: application/json" -d '{"title": "juice", "recipe": [{"color": "yellow", "parts": 1}]}'`


```json
{
   "drinks":[{
      "id":1,
      "recipe":[{
         "color":"yellow",
         "parts":1}],
      "title":"juice"}]
   ,"success":true
}
```

