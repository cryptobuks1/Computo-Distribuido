**AN INTRODUCTION TO ASYNCHRONOUS PROGRAMMING IN PYTHON**

**INDEX**

* [1.-Introduction to asynchronous programming in python](#item1)
* [1.1.-Multiple Processes](#item2)

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

from multiprocessing import Process """Import the process library of the multiprocessing package.
The multiprocessing package supports generation processes offering local concurrency
and remote."""


def print_func(continent='Asia'): # The print_func function is created by sending as parameter the variable continent equal to "ASIA".
    print('The name of continent is : ', continent)# Print the continent variable of the function


if __name__ == "__main__":  # confirms that the code is under main function # Therefore the code below makes it our main program to run it without problems

    names = ['America', 'Europe', 'Africa']
    procs = []
    proc = Process(target=print_func)  # instantiating without any argument  # the array is initialized without any arguments
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
    for proc in procs:
        proc.join()

<a name="item3"></a>
## TOPIC 3
**1.1 Multiple Processes**
