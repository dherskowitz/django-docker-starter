# django-docker-starter
A simple Docker Compose workflow for local development with postgres as the database and mailgun for email testing. This config is **_NOT_** meant for production.


## Usage

To get started, make sure you have [Docker installed](https://docs.docker.com/desktop/) on your system, and then clone this repository.

- Replace `MY_PROJECT` in `docker-compose.yml` with your project name to avoid collision with other docker containers. 

- Create a Django Project in the web container `docker-compose run web django-admin startproject PROJECTNAME DIRECTORY`. On first run the containers will build and install the requirements.

- If on Linux/Mac update ownership, otherwise files created inside the container will not be editable. You will have to do this whenever you create a new file or folder in the container. 
    
    ```sudo chown -R $USER:$USER .```

- Build the other containers by running `docker-compose up -d`. You can pass ` --build` if you need to re-build.

The containers run on the following ports. Update the `docker-compose.yml` to change the ports:

- **postgres** - `:5432`
- **django**   - `:8000`
- **mailgun**  - `:8055`

To connect to the postgres container from the django container use the following:
- **HOST** - `db`
- **NAME** - `postgres`
- **USER** - `postgres`
- **PORT** - `5432`


## Running Commands
Instead of creating a virtual environment you can run everything inside the container. Running everything inside the container will probably be faster as you can avoid having to rebuild whenever you install a new package.

### Create new Django App
```
# Create app in container
docker-compose exec web python manage.py startapp APP_NAME

# Update ownership
sudo chown -R $USER:$USER .
```

### Freeze requirements
- `docker-compose exec web pip freeze > requirements.txt`

### View tail of container logs
- `docker-compose logs -f`
