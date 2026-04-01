# Multitasking :
The concept of Multitasking is basically taken from human behaviour. For example ,sometime we do chatting on whatsapp and we talk on phone
also simultaneously.
So the same concept is use in computer for example we use vlc media player and downloading the song simultaneously.

** So performing more then one task at same time is known as Multitasking**


## Types of Multitasking :
   
### Process based Multitasking :
It means the ability to execute multiple program(process) at the same time .
For e.g. We are using vlc media player to play music and creating a java program in notepad simultaneously.

### Thread based Multitasking :
 It is the ability to execute several parts of the same program at the same time.
 For e.g. When we type in MS word at the same time the spelling checker is activates and modify if any mistake arise.Since typing and spelling
 checker and spelling modiifer perform in a single program (process) itself is known  thread based multitasking.
 

## Advantage of Multitasking :
Whether it is process based or thread based , the main objective is to reduce response time of system and to improve performance


## Main important application areas of multithreding are :
1. To develop multimedia graphics.
2. To develop animations.
3. To develop video games.

## What is thread ?
A thread is a smallest unit of execution within a process. It is like a light weight  sub-process that run independtly but share the same memory
of parent process.

## Simultaneously meaning :

Generally we think that multiple process are executing simultaneously but actually they execute one by one .Beacuse the speed of CPU is very fast
so that it appears as they are executed simultaneously. To execute a process so many process scheduling algorithms we use such as-

1. First come First Serve.
2. Shostest job-next.
3. Priority scheduling.
4. Shortest-Remaining time.
5. Round-Robin scheduling.
6. Multiple-level queues scheduling.

## Process Scheduling :
The act of determining which process is in the ready state , and should be moved to running state is known as Process scheduling. The prime
aim of process scheduling  system is to keep the CPU busy all time and to deliver minimum response time for all progress.

## Difference between process and thread -

 1. A process is an independent program in execution within its own memory space.
 1. A thread is light weight  process that share memory with other threads in same process.
 
 2. Process is heavy weight.
 2. Thread is light weight.
 
 3. Cost of communication b/w process is high  because ,switching from one process to another required some time for saving and loading
    registers.
 3. Cost of communication between thread is low.
 
 
 ## In how many ways we can create thead :
 1. By extending thread class.
 2. By implementing Runnable interface.
 
 ## Which is better way to create thread  ?
 Runnable interface is better to create thread , because here we have also a facility to apply inheritence.
 
 # Case ::
 
 ##  case 1:  Thread scheduler 
     
	 It is a part of JVM , it is responsible to schedule threads i.e.  if multiple threads are waiting to get a chance of execution then in which
	 order threads  will be executed ,is decided by scheduler.
	 We can't expect exact order followed by thread scheduler , it is varied from jvm to jvm ,hence we can't expect thread execution order and 
	 exact output .
	 
 
##   case 2:  Importance of thread  class start() method 
    
	Thread class start() method is responsible to reister thread with thread scheduler.

## 

      
 
 
