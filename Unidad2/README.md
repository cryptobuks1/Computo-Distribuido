**AN INTRODUCTION TO ASYNCHRONOUS PROGRAMMING IN PYTHON**

**INDEX**

* [1.-Introduction to asynchronous programming in python](#item1)
* [1.1.-Multiple Processes](#item2)
* [1.2.-Multiple threads](#item3)
* [1.3 performance corutins](#item4)
* [1.2.-Multiple threads](#item3)
* [1.2.-Multiple threads](#item3)
* [1.2.-Multiple threads](#item3)
* [1.2.-Multiple threads](#item3)


<a name="item1"></a>
## TOPIC 1

**1.-Introduction to asynchronous programming in python.**
Asynchronous programming gives us the ability to "defer" the execution of a function while waiting for an operation to be completed, usually I / O (network, hard disk, ...), and thus avoid blocking the execution until it has been completed. completed the task in question This is possible because the functions are first-class citizens and can be passed as arguments of other functions as we would with the variables.

<a name="item2"></a>
## TOPIC 2
**1.1 Multiple Processes**
The way in which multiprocesses work is to execute the same script several times, after this the scripts can be executed individually or together, the operating system is responsible for distributing the resources of the PC in all instances.
Multiple processes or multiple threads can be executed within a single process.
Additionally, the multiprocessing library can be used in which it supports generation processes as in the following example.

Example:

from multiprocessing import Process
  #Import the process library of the multiprocessing package.
  # The multiprocessing package supports generation processes offering local concurrency
  # and remote.


def print_func(continent='Asia'): # The print_func function is created by sending as parameter the variable continent equal to "ASIA".
    print('The name of continent is : ', continent) # Print the continent variable of the function


if __name__ == "__main__":  # confirms that the code is under main function
    """With this code we see if the module has been imported or not.
    If it has not been imported (it has been run as the main program)
    Run the code inside the conditional."""
    # Therefore the code below makes it our main program to run it without problems
    names = ['America', 'Europe', 'Africa']
    procs = []
    proc = Process(target=print_func)  # instantiating without any argument
    procs.append(proc)
    proc.start()

    # instantiating process with arguments
    for name in names:
        # print(name)
        proc = Process(target=print_func, args=(name,))
        procs.append(proc)
        proc.start()

    # The processes are completed by joining the 2 arrangements with our main function
    # Obtaining the name of content is: "the name of the continent declared in the arrangement depending on the position"
    # complete the processes
    for proc in procs:
        proc.join()

<a name="item3"></a>
## TOPIC 3
**1.2 Multiple threads**
One way to execute several things at once is to use threads in this way multiple tasks are executed.
Here is an example of how this type of programming works in python:

  "" "A python library is imported here that allows you to perform
  multiprocesses using threads "" "
import threading

def print_cube(num):
  #define the function print_cube that takes as argument the variable num
    """
    function to print cube of given num
    """
    print("Cube: {}".format(num * num * num))

def print_square(num):
  #define the square square function that takes as argument the variable num
    """
    function to print square of given num
    """
    print("Square: {}".format(num * num))

if __name__ == "__main__":
  # threads are created
    "" "functions are accessed here through target, and
    assign the value of the number 10 for the argument that these functions will take "" "

    t1 = threading.Thread(target=print_square, args=(10,))
    t2 = threading.Thread(target=print_cube, args=(10,))

    # starting thread 1
    t1.start()
    # starting thread 2
    t2.start()

    # wait until thread 1 is completely executed
    t1.join()
    # wait until thread 2 is completely executed
    t2.join()

    # both threads completely executed
    print("Done!")


<a name="item4"></a>
## TOPIC 4
**1.3 performance corutins**
Corutins are generalizations of subroutines. They are used for cooperative multitasking where a process voluntarily yields (gives away) control periodically or when it is inactive to allow multiple applications to run simultaneously. Corutins are similar to generators but with few additional methods and a slight change in the way we use the declaration of performance. Generators produce data for iteration, while corutins can also consume data.
Courutinas Code

def print_name (prefix): # create the print_name function with the prefix parameter
print ("Searching prefix: {}". format (prefix)) # The parameter is converted.
    
try: # we create a try which will make us exit the courutina at the end of the while
    while True:
            # we use yield to create our corutina
            name = (yield)
            if prefix in name:
                print (name)
except GeneratorExit:
        print ("Closing coroutine !!") # initialize
 
corou = print_name ("Dear") # we send as prefix the word dear to the function to execute the corutina
corou .__ next __ () #with next we send parameters through yield to the function print_name
corou.send ("James")
corou.send ("Dear James")
corou.close () # we finally close the courutina.

<a name="item5"></a>
## TOPIC 5
**1.4 Asynchronous programming**
In this form of programming the operating system does not participate. The way Python works in this way is thanks to the new module module introduced in the Python 3.4 version that makes the code simpler.
Asyncio uses different constructions:
* Event loop: Manage and distribute tasks.
* Routines: Release the control flow back to the event loop.
* Futures: It is the result of a task that may or may not have been executed.

import signal  
import sys  
import asyncio  
import aiohttp  
import json

loop = asyncio.get_event_loop()  
client = aiohttp.ClientSession(loop=loop)

async def get_json(client, url):  
    async with client.get(url) as response:
        assert response.status == 200
        return await response.read()

async def get_reddit_top(subreddit, client):  
    data1 = await get_json(client, 'https://www.reddit.com/r/' + subreddit + '/top.json?sort=top&t=day&limit=5')

    j = json.loads(data1.decode('utf-8'))
    for i in j['data']['children']:
        score = i['data']['score']
        title = i['data']['title']
        link = i['data']['url']
        print(str(score) + ': ' + title + ' (' + link + ')')

    print('DONE:', subreddit + '\n')

def signal_handler(signal, frame):  
    loop.stop()
    client.close()
    sys.exit(0)

signal.signal(signal.SIGINT, signal_handler)

asyncio.ensure_future(get_reddit_top('python', client))  
asyncio.ensure_future(get_reddit_top('programming', client))  
asyncio.ensure_future(get_reddit_top('compsci', client))  
loop.run_forever()  
