# django-docker-starter
A simple Docker Compose workflow for local development with postgres as the database and mailgun for email testing. This config is **_NOT_** meant for production.


## Usage

To get started, make sure you have [Docker installed](https://docs.docker.com/desktop/) on your system, and then clone this repository.

- Replace `MY_PROJECT` in `docker-compose.yml` with your project name to avoid collision with other docker containers. 

- Create a Django Project in the web container `docker-compose run web django-admin startproject PROJECTNAME DIRECTORY`

- Build the other containers by running `docker-compose up -d --build`. 

The containers run on the following ports. Update the `docker-compose.yml` to change the ports:

- **postgres** - `:5432`
- **django** - `:8000`
- **mailgun** - `:8055`

To connect to the postgres container from the django container use the following:
- **HOST** - `db`
- **NAME** - `postgres`
- **USER** - `postgres`
- **PORT** - `5432`


## Running Commands
Instead of creating a virtual environment you can run everything inside the container. Running everything inside the container will probably be faster as you can avoid having to rebuild whenever you install a new package.

### Create new Django App
- `docker-compose run web python manage.py startapp APP_NAME`

### Freeze requirements
- `docker-compose run MY_PROJECT_web pip freeze > requirements.txt`

### View tail of container logs
- `docker-compose logs -f`
