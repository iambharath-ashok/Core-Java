# Java Executor Service

### 1. Introduction


	Code Snippet of Creating a Thread in Java: 

		public class MainClass {

			public static void main(String ... args) {
				Thread thread = new Thread(new Task())
				thread.start();
				System.out.println("Thread Name : "+ Thread.currentThread().getName());
			}

			static class Task implements Runnable {
				
				@Override
				public void run() {
					System.out.println("Thread Name : "+ Thread.currentThread().getName());
				}
			}
		}	


#### 1.	Main Thread will continue to run till the end of the execution

#### 2.	When t1.start() is executed then a new thread will be created with name thread-0
	
- 	Once thread has been created its start to work asynchronously 
-	At same time Main thread also continue its execution
-	Once thread task is completed Java will delete that Thread

#### 3. 	In Java, 1 Java Thread = 1 OS Thread

#### 4.	Creating Threads is a Expensive task
	
-	Creating 100 threads to perform 100 task is an very Expensive task
-	Instead we need to create a pool of Threads - this pool of threads is called Thread Pool
-	We will assign 100 task to Thread pool of 10 

	-	Each thread will start with one task at a time
	-	Once task is completed on particular thread then it will pick up another task
	
#### 5.	Executor Service
	
-	Executors has 4 static methods to get the pool of threads
-	Executors will return ExecutorService that is used to execute or submit the task to Blocking queue
-	Instead of creating a thread, now a task is submitted to ExecutorService



		
	### Thread Pool Executor
	
	-	Thread Pool Executor internally uses Blocking Queue
	-	All the task that are submitted to ExecutorService are stored in a Blocking Queue
	-	All Threads within Thread Pool Executor will perform 2 steps
		
		1.	Fetch next Tasks from Queue
		2.	Execute the Tasks

	-	Since all the threads with in Thread Pool Executor pick up tasks at same time - Concurrently
		
		-	Queue should be able to handle Concurrent Operations	
		- 	Thread Pool Executor uses Blocking Queue which is Thread Safe	

		
		
	### Code Snippet of submitting a Tasks to ThreadPool: 
	
		public class MainClass {
		
			public static void main(String [] args) {
				ExecutorService  executorService = Executor.newFixedThreadPool(nThreads:5);
				
				for (int i=0; i < 10; i++) {
					executorService.execute(new Task()); // Submitting 10 Tasks to ThreadPool of 5 Threads
				}
				
			}
			
			
			static class Task implements Runnable {
				
				public void run() {
					System.out.println("Thread Name: "+ Thread.currentThread().getName());
				}
			}
		}




#### 6.	Ideal Size of Thread Pool
	
-	Ideal size of Thread Pool depends on the Task that we going to perform inside the run methods
-	Tasks can be CPU Intensive or IO Intensive Tasks	
	
	### 1.  CPU Intensive Task
	
	-	If Tasks were CPU intensive then Thread Pool Size depends on the number of CPU cores
		
		-	If tasks is CPU intensive like algorithm to create hash function or Cryptography then it consumes more CPU

	-	If CPU is having only 4 cores, then we can run only 4 threads at a time irrespective of number of Threads
		
		-	A CPU with 4 cores and 1000 threads will use the Time Split Scheduling Algorith
				
			-	It will give some time to one of the thread and bump it off
			-	This will result in performance degradations
			-	In this case, Ideal Pool size is to have the same number of cores in the CPU
				
					
					
					
	#### Code Snippet of having Ideal number of Threads depending on number of Cores:
						
			public class MainClass {
				
				public static void main(String ... args) {
					int coreCount = Runtime.getRuntime().availableProcessors();
					ExecutorService executorService = Executors.newFixedThreadPool(coreCount);
					
					for ( int i=0; i < 10; i++ ) {
						executorService.execute(new CPUIntensiveTask());
					}
				}
				
				
				static class CPUIntensiveTask implements Runnable {
				
					public void run() {
						// Code to be Executed as Part of Thread
					}
				
				}
			}
				
		
	
	
	### 2.	IO Intensive Task
		
	-	I/O Intensive Task are like DB call or HTTP call,  N/w calls
	-	For I/O Intensive Tasks, we can have large Thread Pool Size
	-	Ideally for I/O calls Threads will be in a Waiting State 
		
		-	So we can have a other threads to continue the tasks				
			
	
	#### Code Snippet of IO Intensive Task: 
	
			public class MainClass {
						
				public static void main(String ... args) {

					ExecutorService executorService = Executors.newFixedThreadPool(nThreads:50);
					
					for ( int i=0; i < 10; i++ ) {
						executorService.execute(new IOIntersiveTask());
					}
				}
				
				
				static class IOIntersiveTask implements Runnable {
				
					public void run() {
						// Code to be Executed as Part of Thread
					}
				
				}
			}
	
	
	
	
### Summary 
	
-	Thread Pool Size depends on the Task that we are going to perform
-	Ideal Thread Pool Size for CPU Intensive task will depends on the Number of Cores on CPU
	-	How many other Executors or Threads are running on the same CPU
	
-	Ideal Thread Pool Size for I/O Intensive task will be higher like 100
	-	Exact number of threads depends on 
		-  Rate of task submission
		-  Average task wait time
	-	Too many threads will increase Memory Consumption leading JVM crash or OutOfMemoryError
			
-------------------------------------------------------------	
	
## 2. Types of Thread Pools

	###	1. Fixed Thread Pool
	
	### 2. Cached Thread Pool
	
	### 3. Scheduled Thread Pool
	
	### 4. Single Threaded Executor
	
	
	
	###	1. Fixed Thread Pool
	
	-	Has Fixed Number of Threads
	-	N number of Tasks can be submitted to Threads
	- 	All Tasks will be stored in Queue called Blocking Queue
	-	Queue should be Thread Safe ... 
	-	Thread Pool will fetch tasks from queue and execute on Thread
	
	###	2. Cached Thread Pool
	
	-	Doesn't have Fixed Number of Threads
	-	Doesn't have queue that holds the Number of Tasks
	-	Queue used in Cached Thread Pool is Synchronous Queue ... which can hold only one Item or Task at a Time
	-	When task is submitted ... Cached Thread Pool will search for if any IDLE Threads
	
		-	If no IDLE Threads found it will create a new Thread and assign Task to that Thread
		
	-	Life Cycle: 	Cached Thread Pool has ability to create 1000 Threads to meet demands
	-	Cached Thread Pool also has ability to Kill Threads once no Further Tasks are available
	-	If Thread is idle for more 60 Seconds then ... Thread will be killed
	
	
	###	3. Scheduled Thread Pool
	
	-	Schedule Thread Pool is for Tasks that should after certain amount of delay
	-	Life Cycle: More Threads are created if Required
	-	Delay Queue is used to store the Tasks
	
		#### Different types of Scheduling
	
		### 1. schedule() 
			
		-	Schedule a Task to run after certain delay ... i.e 10 Seconds

		### 2. scheduleAtFixedRate()
			
		-	Perform some Task every 10 Seconds
		-	Tasks will be stored in Delay Queue
		-	Tasks will be stored in Queue according to their Delay Period
		-	10 Seconds tasks will at front and 10 Minutes Task will be next to 10 Second Delay Task
		
		### 3. scheduleAtFixedDelay()
		
		-	Will run after some fixed delay from completion of task 
		-	Fixed deley is 5 Second and Task will run for 15 Seconds ... then Task will Schedule to run after 5 Seconds from completion of Task
		
		#### Code Snippet of ScheduledThreadPool
		
		
			Code Snippet: 
			
				public void main(String ... args) {
				
					ScheduledExecutorService scheduledThreadPool = Executors.newScheduledThreadPool(5);
					
					
					// Tasks to run after 10 Seconds Delay
					scheduledThreadPool.schedule(new Task(), 10, TimeUnit.SECONDS);
					
					// Tasks to run repeatedly after 10 Seconds with initial delay of 10 Seconds
					scheduledThreadPool.scheduleAtFixedRate(new Task(), initialDelay: 10, period: 10, TimeUnit.SECONDS);
					
					
					// Task to run repeatedly after 10 Seconds after previous Task Completion
					scheduledThreadPool.scheduleAtFixedDelay(new Task(), initialDelay: 10, delay: 10, TimeUnit.SECONDS);
				
				
				}
			
	###	4. 	Single Threaded Executor

	-	Size of the Pool will be only one 
	-	Life Cycle: Only one Thread will fetch Task from Blocking Queue and Executes it
	-	If Thread got killed due any exception ... then Thread Pool will recreate a new Thread
	-	Thread Pool will make sure that at least 1 Thread will be executing tasks at a time
	-	There will be only one Thread
	-	Since only 1 Thread ... only 1 Task will executed at a time
	-	This Thread Pool type will used to make sure that Task1, Task2, Task3 ... be executed in sequentially
	
	
-------------------------------------------------------------	
	
## 3. Callable and Future
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
	
