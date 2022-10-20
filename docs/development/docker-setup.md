---
title: Docker dev setup
reviewers:
---

In order to simplify the development environment setup and provide greater consistency between development and production environments, we have packaged the application as a Docker image. This means that you don't need to worry about conflicts of Python versions, Python library versions, or Python virtual environments. Everything is inside the Docker container.

## Setup for development using Docker Compose

Install Docker on your development machine. Instructions for all supported platforms are here <https://docs.docker.com/get-docker/>

Clone this repository to your code folder:  
`git clone https://github.com/rcpch/rcpch-audit-engine.git`

Navigate into the folder  
`cd rcpch-audit-engine`

Start the development environment  
`docker compose up`

!!! tip
    Note that the command changed from `docker-compose` to `docker <space> compose` with more recent Docker versions.

This should create a `db` container for the database and another `web` container for the Django app. The `web` container is built with the correct Python version, all development dependencies are automatically installed, the database connection is created, migrations applied and seed data added to the database. The entire process takes less than 30 seconds.

View the application in a browser at <http://0.0.0.0:8000/>

Changes you make in your development folder are **automatically synced to inside the Docker container**, and will show up in the application right away. This Docker setup is quite new so please do open an issue if there is anything that doesn't seem to work properly. Suggestions and feature requests welcome.

## Executing commands in the context of the `web` container

You can run commands in the context of any of the containers.

The below command will execute `<command>` inside the `web` container.

```console
docker compose exec web <command>
```

For example, to create a superuser

```console
sudo docker compose exec web python manage.py createsuperuser
```

## Running the test suite

```console
sudo docker compose exec web coverage run manage.py test
```

## Shutting down the Docker Compose environment

++ctrl+c++ will shut down the `web` and `db` containers but will leave them built. You can restart them rapidly with `docker compose up`.

To shut down and destroy the containers so that you can start again from scratch (for example if you want to rebuild and re-seed the database) then use

```console
docker compose down
```

## Tricks and tips.

* Although the `docker compose` setup is very convenient, and it installs all the runtime development dependencies _inside_ the `web` container, one thing it can't do is install any _local_ Python packages which are required for text editing, linting, and similar utilities _outside_ the container. Examples are `pylint`, pylint_django`, etc. You will still need to install these locally, ideally in a virtual environment.