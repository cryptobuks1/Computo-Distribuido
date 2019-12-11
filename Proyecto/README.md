# Dockerize Our Django Project
Requirements
- Install Docker on our operating system in this case linux
- Asynchronous Tasks in Django with Redis and Celery Project
- Internet connection to download the requirements

## Developing
![Imagen1](https://raw.githubusercontent.com/manuelorozcotoro/Computo-Distribuido/Unidad4/Unidad4/images/tete.png)
Creation of our dockerFile file
We create a file at the root of our project called dockerfile with the following parameters.

In the content of our `dockerfile` we will have the following
```
FROM python:3.6

ENV PYTHONUNBUFFERED 1
ENV DJANGO_ENV dev
ENV DOCKER_CONTAINER 1

COPY ./requirements.txt /code/requirements.txt
RUN pip install -r /code/requirements.txt

COPY . /code/
WORKDIR /code/

EXPOSE 8000
```

In the same way we create a requirements.txt file that will contain the requirements that we will need for our container to run our django application

We start by specifying the name of the add-on and its version.
```
celery==4.2.1
redis==3.2.0
Django>=2.0,<3.0
psycopg2>=2.7,<3.0
django-extensions==1.9.8
django-widget-tweaks==1.4.1
Pillow==2.6.1
```



and finally we create our `docker-compose.yml` file that will execute all the images defined in the container requirements.
```
version: '3'

services:
  db:
    image: postgres:9.6.5
    volumes:
      - postgres_data:/var/lib/postgresql/data/
  redis:
    image: "redis:alpine"
  web:
    build: .
    command: bash -c "python /code/manage.py migrate --noinput && python /code/manage.py runserver 0.0.0.0:8000"
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    depends_on:
      - db
      - redis
  celery:
    build: .
    command: celery -A image_parroter worker -l info
    volumes:
      - .:/code
    depends_on:
      - db
      - redis
  celery-beat:
    build: .
    command: celery -A image_parroter beat -l info
    volumes:
      - .:/code
    depends_on:
      - db
      - redis

volumes:
  postgres_data:
 ```
 To run our docker container we move to the folder through the terminal where our files are.

Once in the folder we execute the following command to build our container

`sudo docker-compose build`

Once you have built our container we can execute it using the following command.

`sudo docker-compose up`

![Imagen1](https://raw.githubusercontent.com/manuelorozcotoro/Computo-Distribuido/Unidad4/Unidad4/images/3.png)
