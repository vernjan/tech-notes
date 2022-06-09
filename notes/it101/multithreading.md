# Multithreading

## Sources
- [Java Multithreading for Senior Engineering Interviews](https://www.educative.io/courses/java-multithreading-for-senior-engineering-interviews) (Educative course)
- [System Design — Other Topics](https://medium.com/must-know-computer-science/system-design-other-topics-b93b22828608)

## Thread vs. process
- processes have separate address spaces
- inter-process communication - files, pipes, sockets
- threads exist within a process
- threads have its own registers and stack
- inter-thread communication - shared heap memory

## Concurrency vs. parallelism
- **concurrency**
    - operations running seemingly at the same time (1 CPU doing context switching)
    - operations are independent of each other
        - e.g. web server processing HTTP requests
    - we measure **throughput**
- **parallelism**
    - operations running truly at the same time (requires multiple cores/machines)
    - splitting a big task into smaller parts
        - e.g. cracking a hash, encoding video
    - we measure **latency**

## Cooperative vs. preemptive
- **cooperative** - threads coordinate each other (a thread decides when to give up the control)
- **preemptive** - scheduler coordinates threads (threads have no control over CPU time)

## Synchronous vs. asynchronous
- **synchronous** - line-by-line execution of code, blocking
- **asynchronous** - form of parallel programming
    - non-blocking calls return _futures_ or _promises_
    - another pattern - callbacks

## Critical sections & race conditions
- **critical section** is any piece of code that has the possibility of **being executed concurrently** by more than one thread
  and **exposes any shared data** or resources used
- **race conditions** happen when threads run through critical sections without thread synchronization

## Deadlocks
- **starvation** - resource is not getting enough CPU
- deadlock will only occur if the four **Coffman conditions** hold true
    1. **Mutual Exclusion**: it implies there should be a resource that can only be held by one process at a time. This means that the resources should be non-sharable.
    2. **Hold and Wait**: A process can hold multiple resources and still request more resources from other processes that are holding them.
    3. **No preemption**: A resource cannot be preempted from a process by force. A process can only release a resource voluntarily.
    4. **Circular wait**: A process is waiting for the resource held by the second process, which is waiting for the resource held by the third process, and so on, till the last process is waiting for a resource held by the first process.
       This forms a circular chain.

### Preventing deadlocks
- break any of the Coffman conditions
- example
    - threads declare in what order they will need the resources (locks)
    - create a graph of resources, edges are made by transitions between resources
    - the prevention algorithm checks for cycles

## Livelock
- occurs when two threads continuously react in response to the actions by the other thread without making any real progress
- consequence is the same as for a deadlock

## Reentrant lock
- one thread can acquire the same lock multiple times

## Mutex vs. semaphore
- kernel synchronization primitives
- **mutex** (mutual exclusion) - locking mechanism
    - once a thread acquires a mutex, all other threads attempting to acquire the same mutex are blocked until the first thread releases the mutex
    - guarantees only one thread in a critical section
    - the same thread locks and unlocks the mutex -> **purpose is locking**
- **semaphore** - signaling mechanism
    - has a limited number of permits
    - any thread can acquire/release permits -> **purpose is signaling** (coordination)

## Monitor
- language level construct (mutex and semaphore are low-level OS primitives)
- mutex with **condition variables**
- enable testing for a predicate (for example _queue is not empty_)
- `wait()` and `signal()`
- keeps **entry set** (holds threads waiting for mutex) and **wait set** (holds thread which called `wait()`)
    - calling `signal()` moves one thread from the wait set into the entry set

```
void waitForPredicate() {
  mutex.acquire()
  while (predicate == false) {
    condVar.wait()
  }
  // Do something useful
  mutex.release()     
}
  
void changePredicate() {
  mutex.acquire()
  set predicate = true
  condVar.signal()
  mutex.release()
}
```
- in Java, condition variable is any object (inherits `wait()` and `notify()`)

## Amdahl's law
- specifies the cap on the maximum speedup that can be achieved when parallelizing the execution of a program
- some parts of the code must always run serially

## Moore's law
- number of transistor doubles every 2 years
- it still kind of holds but CPU clocks is not increasing for a long time, what is increasing nowadays is the number of cores