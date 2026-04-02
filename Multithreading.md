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

##  case 3 : overloading of run() method 

      Overloading of run()   method  is always  possible , but thread class Thread class start() method can invoke no arguement run() method 
	  the other overloaded method we have to call explicitly like a normal method call.
	  
## case 4 : If we not overriding run method -
       
	   If we not overriding run() method , then thread class run() method  will be executed which  has emplty implemnetation.Hence we won't get
	   any output .
	   
##  case 5 : overriding of start() method 
        If we override start() method, then our start() method will be executed  just like a normal method call and new thread won't be created.
		
		
## case 6  : After starting a thread if we are trying to restart the same thread then we will get RuntimeException saying :

        IllegalThreadStateException.
		

#  Methods :
 
 1 . start() method 
         
		  public void start()->
		  
		  When we call a start() method , a new thread is started and the run() method is executed.

2.  sleep() method 

   a. public static native void sleep(long millisec)  throws InterruptedException <br>
   b. public static native void sleep(long miilisec , int nanosec)  throws InterruptedException
   
    If a thread don't want to perform any operation for a particular amount of time then we should go for sleep() method.
	
3. stop() method  - It is depcreated

          Synatx: 
          public final void stop()
		 
		 In java , the stop() method belongs to the Thread class and was originally used to forcefully terminate a thread
		 
		 ⚠️ Why is stop() deprecated
		 stop() is considered unsafe and was deprecated because:

			1. ❌ Unsafe termination
			It kills the thread instantly.
			The thread may be in the middle of critical work.
			
			2. ❌ Leaves objects in inconsistent state
			If a thread is modifying shared data and gets stopped:
			Data may become corrupted.
			Leads to unpredictable behavior.
			
			3. ❌ Releases locks abruptly
			If the thread holds locks, they are released suddenly.
			Other threads may access half-updated data.
			

4.    suspend method() -It is deprecated 
       
     
		  Syntax :
		  public final void suspend()
		  
		  Temproarily pauses the execution of a thread without terminating it.
		  
		  
		  Why  it is deprecated :
		  
		    ❌ 1. Deadlock risk
			If a thread is suspended while holding a lock:
			Other threads cannot access that resource
			Leads to deadlock
			
			❌ 2. No control over where it pauses
			Thread may pause in the middle of critical code.
			
			❌ 3. Program can freeze
			If the suspended thread is never resumed → application may hang.
			
			
5 .      resume() method - It is  deprecated 

           Syntax :
		   public final void resume()
		   
		   It resumes execution of a thread that was paused using suspend().
		   
		   Why  it is deprecated :
		   
		    ❌ 1. Deadlock issue
			If a thread is suspended while holding a lock:
			Other threads are blocked
			Even after resume(), program behavior becomes inconsistent
			❌ 2. Timing problems
			If resume() is called before suspend(), it has no effect
			Thread may remain suspended forever → ❌ program freeze
			❌ 3. No proper control
			No guarantee when the thread will resume safely
			

6        join() method :

            Syntac :
           a. public final void join()  throws InterruptedException
		   b. public final void join(long millisec)  throws InterruptedException
		   c. public final void join(long millisec, int nanosec)  throws InterruptedException
		   
		   
		   If a thread want to wait untill completing some other thread , then we should go for join() method.
		   
		   If a thread t1 wants to wait untill completing t2 then t1 has to call t2.join().If t1 executes t2.join() then immediately t1 will
		   be entered into the waiting state untill t2 completes.Once t2 completes then t1 can continue its execution.
		   
		   

7.      yield() method :

          Syntax 
		  public static void yield()
		  
		  yield() method causes to pause current executing thread to give the chance for waiting threads of same priority.If there is no waiting
		  thread or all waiting threaad have low proirity then same thread can continue its execution.If multiple threads are waiting wiht same 
		  priority then which thread will get chance  we can't expect it depends on thread scheduler.The thread which is yielded, when 
		  it will get chance once agin it depends on thread scheduler and we can't expect exatly.
		  
		  NOTE :  Some platforms won't  provide proper support for yield method .
		  
		 
# Thread Priorities :
   Every thread in java has some priority it mat be default priority generated by JVM or customized priority provided by programmer.
   The valid range of thread priority is 1 to 10 where  1 is min prioirty adn 10 is max prioirty.

## Methods :

1 .   public static Thread currentThread() :  
         
		 It returns a reference to the currently executing thread.
		 
		 -> What happend when we print currenThread Object 
		   Thread[Name of Thread , Priority of Thread, Group of Thread]


2.  public final int getpriority()

3. public final void setPriority(int p)

4. public final String getName()

5. public final void setName(String name)

### What happens when we use thread priorities less than 1 and greater then 10

    IllegalArgumentException


## Default Priority :

The default priority only for the main thread is five but for all remaining threads default priority will be inherited from parent to child
i.e. whatever priority parent thread has the same prioirty will be there fro child thread.

Note :  Some platform won't provide proper support for thread safety



		 
 






































     
   
   
		  
		  
				   
		   
		   
 
		
		

      
 
 
