# flask_app
## Introduction
Application for playing tic tac toe game. Player plays with computer (ai based on negamax - simplified minmax algorithm). Enjoy!

## Images from website

Home page before logging

![image](https://github.com/Arthemyst/flask_app/assets/59807704/252bf596-5045-4177-8a5a-4efe0c08b4ad)

Login page

![image](https://github.com/Arthemyst/flask_app/assets/59807704/22b9b20c-39d6-49bc-a75c-fb3f5a7bc328)

Register page

![image](https://github.com/Arthemyst/flask_app/assets/59807704/41e1f96e-f29b-45de-934a-1a6cd6c9c9a9)

Profile page after logged in

![image](https://github.com/Arthemyst/flask_app/assets/59807704/2ea659ba-103d-4d09-b91f-60b6c0453a6d)

Game page

![image](https://github.com/Arthemyst/flask_app/assets/59807704/b37ee28c-0d39-4f2e-aef8-ea918fbfa56f)

Statistics Page

![image](https://github.com/Arthemyst/Football_analysis/assets/59807704/f943770d-3324-44f9-ba33-464eb875cc16)


## Setup
The first thing to do is to clone the repository:
```sh
$ git clone https://github.com/Arthemyst/flask_app.git
$ cd flask_app
```

This project requires Python 3.8 or later.

Create a virtual environment to install dependencies in and activate it:

Linux:
```sh
$ python3 -m venv env
$ source env/bin/activate
```

Please create file .env in docker directory. The file format can be understood from the example below::

```sh
SECRET_KEY=your_secret_key
DATABASE_IP=localhost-ip_of_docker_database_1_found_by_below_command
DATABASE_PASSWORD=postgres
DATABASE_USER=postgres
DATABASE_NAME=postgres
INITIAL_CREDITS=10
ADDITIONAL_CREDITS=10
CREDITS_FOR_WIN=4
```

### Start docker:

Application runs on docker. To run app you need to install docker on your machine. Please run docker-compose to install dependiences and run application:

First terminal:
```sh
$ docker-compose -f docker/docker-compose.yaml up --build
```
Second terminal run pararallel to first:
```sh
$ docker cp create_table.sql docker-database-1:/create_table.sql
$ docker exec -it docker-database-1 psql -U postgres -d postgres -f /create_table.sql
```
Check docker-database-1 ip and put it inside .env variable for DATABASE_IP:
```sh
$ docker inspect -f '{{range .NetworkSettings.Networks}}{{.IPAddress}}{{end}}' docker-database-1
```


tip: if docker-database-1 or docker-web-1 occured error message, please replace it with docker_database_1 and docker_web_1

### tests

To test management commands during application running:

first terminal:
```sh
$ docker-compose -f docker/docker-compose.yaml up --build
```
second terminal run pararallel to first:
```sh
$ docker exec -it docker-web-1 /bin/bash
$ python3 -m pytest tests/tests_for_flask_pages_responses.py
```

## app running

After successfully starting application you should be able to work in web environment.

You can register and than log in to your account. You will be redirected to Profile page, but if you go to home page you can back to profil page by clicking on Profile button.
On profile page you can choose to play game or check statistics from your profile. Page with statistics show you information about chosen day. After all you can log out and close session.

