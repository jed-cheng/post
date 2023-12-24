---
title: Test Post
description: there is some description
---
# Race Condition
>A situation where concurrent operations access data in a way that the outcome depends on the order (the timing) in which operations execute.

# Synchronization
>using atomic operations to ensure cooperation between multiple concurrent threads
# Mutual Exclusion
>ensuring that only one thread does a particular operation at a time

# Atomic Operation
>operations that cannot be interrupted
- On most machines, memory references and assignments (i.e., loads and stores) of words are atomic
- Many instructions are not atomic
	- Double-precision floating point store often not atomic 
	- VAX and IBM 360 had an instruction to copy whole array
# Critical section 
>piece of code that only one thread can execute at once 
- Critical section is the result of mutual exclusion 
- Critical section and mutual exclusion are two ways of describing same thing
## Lock
>prevent someone from doing something
- Lock before entering critical section, before accessing shared data 
- Unlock when leaving, after done accessing shared data 
- Wait if locked 
- Important idea: synchronization involves waiting!

acquire lock before entering critical section, release lock after exit critical section

### Implementation of lock
## Semaphores
Semaphore has non-negative integer value and 2 operations
P(): atomic operation that waits for semaphore to become positive, then decrements it by one
V(): atomic operation that increments semaphore by one, waking up a waiting P(), if any
>why P, V: In Dutch, P stands for proberen (to test) and V stands for verhogen (to increment)

- No negative values 
- Only available operations are P & V (cannot read/write value, except to set it initially) 
- Operations must be atomic 
	- Two P’s together can’t decrement value below zero 
	- Thread going to sleep in P won’t miss wakeup from V (even if they both happen at same time)

Is order of P’s important? • Yes! Can cause deadlock • 
Is order of V’s important? • No, it only might affect scheduling efficiency


# Deadlock

> starvation: lower priority thread cannot be executed, problem of scheduling
> Deadlock leads to starvation but not the other way around

Starvation can end (but doesn’t have to) •
Deadlock can’t end without external intervention

Deadlock is not always deterministic

## Requirement
- Mutual exclusion
- Hold and wait
- No preemption（不可剥夺）
- Circular wait


## Resource Allocation Graph
request
use
release

## Handling Method
- Allow system to enter deadlock and then recover
	- Requires deadlock detection algorithm
	- Technique for forcibly preempting resources and/or terminating tasks
- Ensure that system will never enter deadlock
	- Need to monitor all resources acquisitions 
	- Selectively deny those that might lead to deadlock
- Ignore problem and pretend deadlocks never occur 
	- Used by most operating systems, including UNIX
Infinite resources
No Sharing of resources
Don’t allow waiting
Make all threads request everything they’ll need at the beginning
Force all threads to request resources in fixed order preventing any cyclic use of resources