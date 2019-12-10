**Asynchronous Tasks in Django with Redis and Celery**

## requirements
As a first requirement it is required to have python 3 and Redis installed in case of not having redis installed we can download it from the official page for linux or mac and simply by doing a make install to be able to install it correctly
to verify if we really have redis installed.
We initialize our terminal and write redis-server to run our server.
We will see in our console the following

![Redis img](https://raw.githubusercontent.com/manuelorozcotoro/Computo-Distribuido/feature_branch/feature_branch/images/1.png)

To see if we really have communication with our server we open another terminal apart from where our server is. with the redis-cli command

![Redis2 img](https://raw.githubusercontent.com/manuelorozcotoro/Computo-Distribuido/feature_branch/feature_branch/images/2.png)

Once our client is initialized we will ping, if the answer is pong it means that we already have our connection to the redis server

Once verified that we have redis installed as well as python 3 We proceed to install virtualEnv and all its dependencies
We create a directory on our machine called image_parroter
`$ mkdir image_parroter`


Once created we place ourselves in it and proceed to execute the command to install virtualEnv.

```
$ cd image_parroter
$ python3 -m venv venv
```

To activate our virtualEnv and work with celery we execute the following command.

```
$ source venv/bin/activate
```
Once our venv is initialized we proceed to install Django with the necessary python packages

```
(venv) $ pip install Django Celery redis Pillow django-widget-tweaks
(venv) $ pip freeze > requirements.txt
```
Pillow is a non-Celery-related Python package for image processing
Django Widget Tweaks is a Django add-on to provide flexibility in how form entries are represented.

## Configuring the Django Project

Once our necessary packages are installed we proceed to create our Django project in this case we will call it image_parroter and our application we will put thumbnailer.

```
(venv) $ django-admin startproject image_parroter
(venv) $ cd image_parroter
(venv) $ python manage.py startapp thumbnailer
```

In order to use Celery in our project we need to create a module within our Django project, in this case the route would be the following image_parroter / image: parroter / celery.py, our celery.py file will include all the necessary packages to execute and implement celery in a correct and efficient way

```
import os
from celery import Celery

os.environ.setdefault('DJANGO_SETTINGS_MODULE', 'image_parroter.settings')
celery_app = Celery('image_parroter')
celery_app.config_from_object('django.conf:settings', namespace='CELERY')
celery_app.autodiscover_tasks()
```

in this module celery is told to use redis as the message broker, as well as where to connect to it. It is also specified that celery wait for messages to pass from one side to another between the celery and redis task queues in application / json.

```
# celery
CELERY_BROKER_URL = 'redis://localhost:6379'
CELERY_RESULT_BACKEND = 'redis://localhost:6379'
CELERY_ACCEPT_CONTENT = ['application/json']
CELERY_RESULT_SERIALIZER = 'json'
CELERY_TASK_SERIALIZER = 'json'
```
