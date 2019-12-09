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
