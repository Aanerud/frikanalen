Creating a local development environment
========================================

Let's start by installing some of the dependencies by running the
`install-debian-deps.sh`.

Create virtual env:

    $ virtualenv env

Activate your new python environment:

    $ source env/bin/activate
    (env)$

Use pip to install the rest of the requirements:

    (env)$ pip install -r requirements.txt

Open fkbeta/settings.py in your editor and edit paths and database-settings.
You should set SECRET_KEY to a random string.

Initialize the database:

    (env)$ cd fkbeta
    (env)$ python manage.py migrate
        ...

Load some default data (fixtures) into the database:

    (env)$ python manage.py loaddata frikanalen
        ...

Create a new admin user:

    (env)$ python manage.py createsuperuser

Start the webserver:

    (env)$ python manage.py runserver

Point your browser to http://127.0.0.1:8000/admin and log in.

## Docker

If you want to use docker, the following commands should set you up:

    $ docker build -t "frikanalen" .
    $ docker run -p 8000:8000 frikanalen

Alternatively you can pull down a image from Docker Hub:

    $ docker run -p 8000:8000 frikanalen/frikanalen
   
Adding a super user in Pyton

    $ docker ps -a

Grabbing process ID 

CONTAINER ID        IMAGE               COMMAND                  CREATED             STATUS                        PORTS                    NAMES
246237e83e21        frikanalen          "python manage.py run"   2 minutes ago       Up 2 minutes                  0.0.0.0:8000->8000/tcp   loving_poincare

Grabb "246237e83e21" and use in following command

   $ sudo docker exec -i -t 246237e83e21 /bin/bash
   
Then you shuld see " root@****:/srv/frikanalen/fkbeta# " where **** is the ID from pre step. 
run then command 

   $ python manage.py createsuperuser
   
Create youre user 

and log then into : http://localhost:8000/admin/login/?next=/admin/
