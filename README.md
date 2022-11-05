# Basic Flask Backend Setup
This project is built on initial work done by https://github.com/miguelgrinberg/microblog-api


### Setup

Follow these steps if you want to run this application on your computer, either
in a Docker container or as a standalone Python application.

```bash
clone the repo and from the root of the project run
copy .env.example .env
```

Open the new `.env` file and enter values for the configuration variables.

### Run with Docker

To start:

```bash
docker-compose up -d
```

The application runs on port 5000 on your Docker host. You can access the API
documentation on the `/docs` URL (i.e. `http://localhost:5000/docs` if you are
running Docker locally).

To populate the database with some randomly generated data:

```bash
docker-compose run --rm microblog-api bash -c "flask fake users 10 && flask fake posts 100"
```

To stop the application:

```bash
docker-compose down
```

### Run locally

Set up a Python 3 virtualenv and install the dependencies on it:

```bash
python3 -m venv venv
venv\scripts\activate.bat
pip install -r requirements.txt
```

Create the database and populate it with some randomly generated data:

```bash
flask db upgrade
flask fake users 10
flask fake posts 100
```

Run the application with the Flask development web server:

```bash
flask run
```

The application runs on `localhost:5000`. You can access the API documentation
at `http://localhost:5000/docs`.

## Troubleshooting

On macOS Monterey and newer, Apple decided to use port 5000 for its AirPlay
service, which means that the Microblog API server will not be able to run on
this port. There are two possible ways to solve this problem:

1. Disable the AirPlay Receiver service. To do this, open the System
Preferences, go to "Sharing" and uncheck "AirPlay Receiver".
2. Move Microblog API to another port:
    - If you are running Microblog API with Docker, add a
    `MICROBLOG_API_PORT=4000` line to your *.env* file. Change the 4000 to your
    desired port number.
    - If you are running Microblog API with Python, start the server with the
    command `flask run --port=4000`.
