# django-docker-starter
A simple Docker Compose workflow for local development with postgres as the database and mailgun for email testing. This config is **_NOT_** meant for production.


## Usage

To get started, make sure you have [Docker installed](https://docs.docker.com/docker-for-mac/install/) on your system, and then clone this repository.

Replace `MY_PROJECT` with your project name to avoid collision with other docker containers. 

Next, navigate in your terminal to the directory you cloned this, and spin up the containers for the web server by running `docker-compose up -d --build`. 

This will also install the latest version of Django and psycopg2 in the container. To specify a version create a requirement.txt before running build. 


The containers run on the following ports. Update the `docker-compose.yml` to change the ports:

- **postgres** - `:5432`
- **django** - `:8000`
- **mailgun** - `:8055`

To connect to the postgres container from the django container use the following:
- **HOST** - `db`
- **NAME** - `postgres`
- **USER** - `postgres`
- **PORT** - `5432`

You can run create a virtual environment (`python3 -m venv ENV_NAME`) or you can run everything inside the container. 

For example create a new django project
- `docker-compose run MY_PROJECT_web django-admin startproject PROJECT_NAME`
- `docker-compose run MY_PROJECT_web python manage.py startapp APP_NAME`

Running everything inside the container will probably be faster as you can avoid having to rebuild whenever you install a new package.

If you choose to run commands inside if the container, you can run `docker-compose run MY_PROJECT_web pip freeze > requirements.txt` to get all the requirements from the container. 
