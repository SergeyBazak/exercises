# Exercise #1

## Simple Python RESTful API Application

In this section, our goal is to create a simple RESTful API application.\
The purpose of this application is to provide access to a database of users.

For simplicity, the database will be stored as a simple JSON file in the following format:\
`users.json`:
```json
{
    "duncan_long": {
        "id": "drekaner",
        "name": "Duncan Long",
        "favorite_color": "Blue"
    },
    "kelsea_head": {
        "id": "wagshark",
        "name": "Kelsea Head",
        "favorite_color": "Ping"
    },
    "phoenix_knox": {
        "id": "jikininer",
        "name": "Phoenix Knox",
        "favorite_color": "Green"
    },
    "adina_norton": {
        "id": "slimewagner",
        "name": "Adina Norton",
        "favorite_color": "Red"
    }
}
```

The application should expose 3 endpoints:
| URI | HTTP METHOD | COMMENT |
|-----|:-----------:|---------|
| `/` | GET | Return [Swagger](https://swagger.io/) documentation page (OPTIONAL) |
| `/users` | GET  | Return a JSON list of all the users excluding the `id` of the user |
| `/user/{username}` | GET | Return a JSON object describing the requested user |

The application can be built using any webserver, but the simple [Flask](https://palletsprojects.com/p/flask/) is recommended.

## Containers

Once we have a working application, we should containerize it.\
Write a `Dockerfile` and using Docker or Podman build a container so users can run the following two commands:
```shell
$ docker build -t app:latest /path/to/Dockerfile
$ docker run -d -p 5000:5000 app
```

1. You can use any base image you would like.
1. Containerize only what you need for running the application, nothing else.

## Unit Tests

Now we should write a simple unit-test for testing the functionality of the application.\
The unit-test should create a mock JSON database file (`users.json`) with predefined data, and validate that the application returns the correct information.

For example, given the following input file:
```json
{
    "test_user": {
        "id": "test",
        "name": "Test User",
        "favorite_color": "Black"
    }
}
```

(Test #1) Accessing the `/users` URI should return:
```json
{
    "test_user": {
        "name": "Test User",
        "favorite_color": "Black"
    }
}
```

(Test #2) Accessing the `/user/test_user` URI should return:
```json
{
    "test_user": {
        "id": "test",
        "name": "Test User",
        "favorite_color": "Black"
    }
}
```

(Test #3) Accessing the `/user/test_user123` URI should return HTTP code 404 as the user does not exist in the database.

## CI

Now that we have a working app that can also run inside a container, we should setup CI for it, so it won't break in the future.\
Use the following guidelines for setting up the CI:
1. Choose whatever CI system or service you prefer (e.g. Jenkins, GitHub Actions, GitLab CI etc.)
1. Clone the application source code from a GitHub repository. 
1. Run `flake8` linting on the source code.
1. Run the unit-test and make sure all the tests pass.
1. `BONUS:` Automatically execute the CI on every new pull request.
