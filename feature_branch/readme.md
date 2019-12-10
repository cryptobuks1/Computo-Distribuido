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

Subsequently we must ensure that the celery module that we just created is injected directly into our Django application when it is executed, this is done by the app within the initial configuration of our Django project and explicitly registering it as a namespace symbol inside the Django package “image_parroter”.

```
# image_parroter/image_parroter/__init__.py

from .celery import celery_app

__all__ = ('celery_app',)
```

We add a new module called tasks.py inside the "thumbnailer" application. Inside the tasks.py module I import the shared function decorator and is used to define a celery task function called adding_task.

```
from celery import shared_task
@shared_task
def adding_task(x, y):
    return x + y
```

Finally, I need to add the thumbnail application to the INSTALLED_APPS list in the settings.py module of the image_parroter project.

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'thumbnailer.apps.ThumbnailerConfig',
    'widget_tweaks',
]
```

Now as the redis server is running, the celery program started in a second terminal.

![Redis3 img](https://raw.githubusercontent.com/manuelorozcotoro/Computo-Distribuido/feature_branch/feature_branch/images/3.png)

In the third and final terminal, again with the Python virtual environment active, I can start the Django Python shell and try my adding_task.

```
(venv) $ python manage.py shell
Python 3.6.6 |Anaconda, Inc.| (default, Jun 28 2018, 11:07:29)
>>> from thumbnailer.tasks import adding_task
>>> task = adding_task.delay(2, 5)
>>> print(f"id={task.id}, state={task.state}, status={task.status}")
id=86167f65-1256-497e-b5d9-0819f24e95bc, state=SUCCESS, status=SUCCESS
>>> task.get()
7
```

## Create thumbnails of images within a celery task

Back in the tasks.py module, I import the Image class from the PIL package, then added a new task called make_thumbnails, which accepts an image file path and a list of width and height dimensions of 2 tuples to create thumbnails

```
import os
from zipfile import ZipFile

from celery import shared_task
from PIL import Image

from django.conf import settings

@shared_task
def make_thumbnails(file_path, thumbnails=[]):
    os.chdir(settings.IMAGES_DIR)
    path, file = os.path.split(file_path)
    file_name, ext = os.path.splitext(file)

    zip_file = f"{file_name}.zip"
    results = {'archive_path': f"{settings.MEDIA_URL}images/{zip_file}"}
    try:
        img = Image.open(file_path)
        zipper = ZipFile(zip_file, 'w')
        zipper.write(file)
        os.remove(file_path)
        for w, h in thumbnails:
            img_copy = img.copy()
            img_copy.thumbnail((w, h))
            thumbnail_file = f'{file_name}_{w}x{h}.{ext}'
            img_copy.save(thumbnail_file)
            zipper.write(thumbnail_file)
            os.remove(thumbnail_file)

        img.close()
        zipper.close()
    except IOError as e:
        print(e)

    return results
```

With the celery task defined, he went on to build Django views to serve a template with a file upload form.
To begin, I give the Django project a MEDIA_ROOT location where image files and zip files can reside (I used it in the previous example task), as well as specify MEDIA_URL where the content can be served.

```
STATIC_URL = '/static/'
MEDIA_URL = '/media/'

MEDIA_ROOT = os.path.abspath(os.path.join(BASE_DIR, 'media'))
IMAGES_DIR = os.path.join(MEDIA_ROOT, 'images')

if not os.path.exists(MEDIA_ROOT) or not os.path.exists(IMAGES_DIR):
    os.makedirs(IMAGES_DIR)
    ```

Inside thumbnailer / views.py we import the django.views.View class and we will use it to create HomeView that contains the get and post methods
