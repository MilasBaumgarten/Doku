# Multithreading
## What not to do
- don't modify, create or delete UObjects
- don't use the TimeManager
- don't draw debug lines

source: [Rama: Multi-Threading: How to Create Threads in UE4](https://www.ue4community.wiki/Legacy/Multi-Threading:_How_to_Create_Threads_in_UE4)

## FRunnable
Using a FRunnable class is an easy way to handle multithreading for a small number of tasks. But when great number of tasks will be used, it is better to use a Thread Pool and Tasks.

<iframe width="560" height="315" src="https://www.ue4community.wiki/Legacy/Multi-Threading:_How_to_Create_Threads_in_UE4"></iframe>

aditional infos:
- thread management
- sleeping
- what not to do
- single threaded plattform support

source: [Rama: Multi-Threading: How to Create Threads in UE4](https://www.ue4community.wiki/Legacy/Multi-Threading:_How_to_Create_Threads_in_UE4)

## Tasks
Tasks can be used to run calculations in a separate thread. They can also be handled by a thread pool. By default the global thread pool will be used to run the task ```Task->StartBackgroundTask();```. To use a custom thread pool, you can pass it as a parameter ```Task->StartBackgroundTask(MyThreadPool);```. (source: AsyncWork.h)

<iframe width="560" height="315" src="https://www.orfeasel.com/implementing-multithreading-in-ue4/"></iframe>

source: [Orfeas Eleftheriou: Implementing Multithreading in UE4](https://www.orfeasel.com/implementing-multithreading-in-ue4/)

## Using Thread Pools
Tasks can be run by using a thread pool. By default the global thread pool will be used ```Task->StartBackgroundTask();```. To use a custom thread pool, you can pass it as a parameter ```Task->StartBackgroundTask(MyThreadPool);```. (source: AsyncWork.h)  
Aparently the global thread pool only has one thread. This means that it is not recommended to use it for more than simple concurrent tasks. Instead a custom thread pool should be created.

<iframe width="560" height="315" src="https://www.programmersought.com/article/6978151078/"></iframe>

source: [ProgrammerSought: "Exploring in UE4" multi-threading mechanism detailed [principle analysis]](https://www.programmersought.com/article/6978151078/)

## Callbacks
When you want to make a callback from within a multithreaded task or runnable, you have to take care of some things. Firstly you shouldn't just call the relevant functions as this will execute them in the separate thread. Instead you should create a new taks that runs on the game thread: ```AsyncTask(ENamedThreads::GameThread, [this]() { YourLambdaCallback });```. Inside the lambda you can e.g. call a function on a "listener" who was passed as a reference when creating the thread ```Listener->MyCallback();```.

source: [Forum Thread: How to callback function in game thread after FRunnableThread finish?](https://answers.unrealengine.com/questions/494119/how-to-callback-function-in-game-thread-after-frun.html)