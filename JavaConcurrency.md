

# Java Threads and Concurrency


## Threads :

-	Thread is a small unit of processes ... a part of process 
-	Each process is divided in to small tasks
-	Microsoft word doc ... while typing a doc ... some threads will show errors text
-	Android Applications like Amazon and Myntra etc...
-	Web Application used servlets to serve mulitple requests

--------------------------------------------------------------------
##	Multicore processors

-	Processor having mulitple cores 

	-	quad-core, octa-core, dual-core
	
-	Every Java Program will have atleast one thread called Main Thread
-	Main Thread uses one of the 4 cores
-	Multiplying 5000 elements by 2 can be distributed across 4 Threads and 4 Threads will run on 4 different core

--------------------------------------------------------------------
## Join and isAlive 


-	isAlive() method is used to check whether Thread is alive or not
-	join() method is used to make wait Parent Thread(main) for Child Threads to complete their execution before Main Thread can continue their executions
-	join() method make Thread Main to wait till child threads combine with Main Thread
-	join() makes to wait for that particular point



	Code Snippet: 
	
		class Hello extends Thread{
			public void run()  {
				for (int i = 1; i <= 5;) {
					System.out.println("Hello");
					i++;
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
			}
		}

		class Hi extends Thread{
			public void run()  {
				for (int i = 1; i <= 5;) {
					System.out.println("Hi");
					i++;
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
			}
		}

		public class ThreadBasics {
			public static void main(String[] args) throws InterruptedException {

				Hello obj1 = new Hello();
				Hi obj2 = new Hi();
			
				obj1.start();
				obj2.start();
			
				obj1.join();
				obj2.join();
				
				Thread.sleep(1000);
				System.out.println("Bye");
			}

		}



-	In the above code join() method on t1 and t2 will makes Main Thread to wait till t1 and t2 joins with Thread Main

--------------------------------------------------------------------

## Synchronized Simple Example


	Code Snippet :
	
		class Counter {
			int counter;
			public void inc() {
				synchronized (this) {
					counter++;
				}
			}
			public int getCount() {
				return counter;
			}
		}

		public class CounterDemo {
			public static void main(String[] args) throws InterruptedException {

				Counter counter = new Counter();

				Thread t1 = new Thread(() -> {
					for (int i = 0; i < 1000; i++) {
						counter.inc();
					}
				}, "Thread 1");

				Thread t2 = new Thread(() -> {
					for (int i = 0; i < 5000; i++) {
						counter.inc();
					}
				}, "Thread 2");

				t1.start();
				t2.start();

				t1.join();
				t2.join();

				System.out.println("Counter : " + counter.getCount());
			}
		}
	
	

--------------------------------------------------------------------

## Inter Thread Communication

-	Inter Thread Communication is achieved through wait(), notify(), notifyAll() methods


--------------------------------------------------------------------

## Internal Datastructure of ConcurrentHashMap

-	ConcurrentHashMap will have Array of Segments
-	Segment is a Inner Class in ConcurrentHashMap
-	Each Segment in turn will have Array of tables of type HashEntry
-	HashEntry is a Inner Class and similar to Entry class
-	HashEntry is a Singly Linked List




--------------------------------------------------------------------

## Concurrency vs Parallelism



### Parallelism 

-	Parallelism is about doing lot of things at once
- 	3 Threads running on quad-core processor 
-	Each Thread including Thread Main will run on separate cores

Tools to enable Parallelism in Java
-	Threads
-	ThreadPool
	-	ExecutorService
	-	ForkJoinPool
	-	Custom ThreadPool (Webservers)
-	Requires > 1 CPU Core	


	Code Snippet :

		public static void main() {
		
			ExecutorService es = Executors.newFixedThreadPool(4);
			es.submit(() -> processTax(user1));
			es.submit(() -> processTax(user2));
			
			heavyCalculations();
		}


### Concurrency 

-	Concurrency is about sharing the resource and coordinating b/w Threads
	
	-	Resources can be Shared variables, instances and Collection instances
	
-	Concurrency can be applied in Single Core CPU
-	In single Core .. scheduler will do time sharing among the Threads
-	Concurrency problems will fixed by using single shared lock.lock() in the code b/w Threads
-	Concurrency is about dealing with lot of thing at once


Tools to deal with Concurrency
-	Lock/ Synchronized
-	Atomic Classes
-	ConcurrentDataStructures(ConcurrentHashMap, CopyOnWriteArrayList, ArrayBlockingQueue) 
-	Completable Future
-	CountdownLatch/Phaser/Cyclic Barrier/Semaphore

---------------------------------------------------------------------------

## Java Memory Model


-	Out of Order Execution
	
	-	Performance driver changes done by CPU, JVM and Compiler
	-	JVM, OS, Compiler may change order of statement to improve performance
	-	Output of Program and semantic remains sames 

-	Field Visibility

	-	In presence of multiple Threads a.k.a Concurrency
	-	Assume a CPU with 4 cores
	-	Processor will have Core, Registers, L1 Cache, L2 Cache, L3 Cache, Ram
	-	Registers are small area of memory and it's within the Core ... so its the fastest
	-	L1 has more memory space than Registers but its one layer farther to Core
	-	Each core will have its own L1 Cache ... so 4 L1 Cache
	-	L2 Cache will distributed two cores and farther two layers from core ... 2 L2 Cache
	-	L3 Cache will be shared across all the Cores .... 1 L1 Cache
	-	RAM shared across all the Cores farther and has lot of space
	
	-	Farther from Core ... more will be the space
	
	
	
	
		Core 1 				Core 2
		Local Cache			Local Cache
				Shared Cache
		
	Code Snippet :
	
		class FieldVisibility {
			
			int x =0;
			
			public void writerThread() {
				x = 1;
			}
			
			public void readThread() {
				r1 = x;
			}
		}

	
	
	-	When Writer Thread write the value it will write it only of Local Cache ... which is x =1
	-	Not Pushed to Shared Cache 
	-	Reader Thread while reading from Shared cache which is still x =0; ... but should be x= 1;
	
	
	Code Snippet :
	
		class VolotileFieldVisibility {
		
			volatile int x = 0;
			
			public void writerThread() {
				x = 1;
			}
			
			public void readerThread() {
				r2 = x;
			}
		}


	-	volatile Keyword make sure that latest values from Local Cache will be pushed to shared cache by JVM before Read Operation

#### JMM
	
-	JMM is a specification or set of Rules which guarantees field visibility on top of reordering of instructions
-	JMM defines a set of rules that each JVM should implement ... so that program running on different JVM results in same output

#### Happens Before Relationship

-	JMM rule that what ever fields written before volatile will be reflected to other threads after reading volatile field



	Code Snippet :
	
		class VolatileFieldVisibility {
			
			boolean isTrue = true;
			
			public void writerThread() {
				isTrue = false;
			}
			
			public void readThread() {
			
				while(isTrue) {
				}
			}
		}



---------------------------------------------------------------------------

## AtomicClass vs Volatile

###	Visibility Problem

-	Updates made by one Thread can't visible to another thread
-	To overcome visibility problem we can use volatile keyword to instance fields


### Increment Problem or Synchronization Problem

-	i++ is not atomic operation
-	
-	JVM does this is  3 steps

	-	Load i from shared cache or memory
	-	Add 1 to i
	-	Write update i to memory
	
-	This problem can be overcome by using Atomic Class like AtomicInteger, AtomicLong, AtomicDouble, LongAdder
-	This problem is also called synchronized problem since multiple threads may read and write simultaneously

	volatile int counter = 0;
	
	synchronized (this) {
		counter++;
	}
	
	
	AtmoicInteger counter = new AtomicInteger();
		
		
	counter.increment();
	

-	Atomic Class methods do compound operations in a  Atomic Manner
-	Atomic Classes are from java.util.concurrent.atomic package
-	Atomic Classes provides atomic methods like incrementAndGet(), decrementAndGet(), andAndGet(int), compareAndSet(int expectedValue, int newValue)


### Conclusion:

1.	Field Visibility problem use volatile
	
	-	volatile is used for flag
	
2.	Compound Operations use Atomic Classes

	-	AtmoicLong and AtomicInteger is used for counters
	
3.	Atomic Reference is used in Building Caches
	
	



---------------------------------------------------------------------------

## Adder and Accumulator  Classes in Java 8

### Atomic Long

-	AtomicLong increment needs to be flushed and refreshed across the Threads a.k.a Needs to be synchronized across the threads
-	This leads to contentions and performance degradations


	Code snippet :
	
```java 	
		class AtomicLong {
			AtomicLong counter = new AtomicLong(0);
			psv main() {
				ExecutorService es = Execurtors.newFixedThreadPool();
				
				for(int i=0; i<50;i++){
					es.submit(new Task(counter));
				}
				
				es.awatiTermination(3000, TimeUnit.MILLISECONDS);
				
				counter.get();// get the counter value at the end
			}
		}


		class Task implements Runnable {
			AtomicLong counter ;
			
			Task(AtomicLong counter ) {
				this.counter = counter;
			}
			
			public void run() {
				// heavyCalculations();
				
				counter.increment();
				// Each AtomicLong increment is synchornized and updates will be flused and updted across the threads
			}
		}
	````


### Adder 

-	LongAdder has different internal implementation for increment operation and finding sum across the threads
-	Each Thread will have it's own internal counter called cnt` and for each  increment it will update its internal counter cnt` and writes updated values to local cache
-	For LongAdder instance thread will not flush local cache changes to shared space for every increment ... instead it will be updated in the local  cache
-	sum will be calculated by adding all the thread local cnt` in a synchrozined manner
-	LongAdder results in High Throughput since its increment operation is not sync, done on its local counter and only sum is sync across the threads

	Code snippet :
	
	```java 	
		class LongAddedEx {
			LongAdded adder = new LongAdder(0);
			psv main() {
				ExecutorService es = Execurtors.newFixedThreadPool();
				
				for(int i=0; i<50;i++){
					es.submit(new Task(adder));
				}
				
				es.awatiTermination(3000, TimeUnit.MILLISECONDS);
				
				adder.sum();// only once synchronized 
				// At the end all the Threads local cnt` variable will added in synchronous manner
			}
		}


		class Task implements Runnable {
			LongAdder adder;
			
			Task(LongAdder adder) {
				this.adder = adder;
			}
			
			public void run() {
				// heavyCalculations();
				
				adder.increment(); // increment local cnt` variable and updates to Local Cache
				// Each thread will have its own cnt` variable 
			}
		}

	````




### Accumulator

- 	Accumulator is similar to Adder but it can do more additional and complex programs
- 	Apart from performing addition and increment it can do multiple, division and much more complex tasks
-	Accumulator constructor takes FunctionalInterface as an argument 

	public LongAccumulator(LongBinaryOperator accumulatorFunction,
                           long identity) {}

	Code Snippet of LongBinaryOperator :
	
	
		@FunctionalInterface
		public interface LongBinaryOperator {
		
			long applyAsLong(long left, long right);
		}
	
		

	LongAccumulator counter = new LongAccmulator((x,y) -> x + y, 0);
	
		x : Intermediate Value
		y :	 New Value
		0 : Intial value of x
		accumulate(1); step
	
	counter.accumulate(y:1);
	counter.get();



	Code snippet :
	
	```java 	
		class LongAddedEx {
			LongAccmulator counter = new LongAccmulator((x,y)-> x + y, 0);
			psv main() {
				ExecutorService es = Execurtors.newFixedThreadPool();
				
				for(int i=0; i<50;i++){
					es.submit(new Task(counter));
				}
				
				es.awatiTermination(3000, TimeUnit.MILLISECONDS);
				
				counter.get();// only once synchronized 
				// At the end all the Threads local cnt` variable will added in synchronous manner
			}
		}


		class Task implements Runnable {
			LongAccmulator counter;
			
			Task(LongAccmulator counter) {
				this.counter = counter;
			}
			
			public void run() {
				// heavyCalculations();
				
				counter.accumulator(); // increment local cnt` variable and updates to Local Cache
				// Each thread will have its own cnt` variable 
			}
		}

	````



Advantages of Accumulator:

-	Best Suited for Heavy Operations
-	Don't have side affects
-	Can be applied repeatedly	




---------------------------------------------------------------------------

## Fork Join Pool

- 	Similar to ExecutorService
-	Fork Join is different from ExecutorService in two ways

	1.	Task producing subtasks and joining results of each subtask to form a final result
	2.	Per Thread Queuing and Work Stealing
	
	
	1.	Forking and Joining for Fibonacci 
	
		if(n<=1) 
			return n;
		else {
			Fibonacci f1 = new Fibonacci(n-1);
			Fibonacci f2 = new Fibonacci(n-2);
			
			f1.solve();
			f2.solve();
			
			number = f1.number + f2.number;
			return number;
		}
	

		Algorithm of ForkJoin
		
		
			public Result solve(Task T) {
				
				split task T into smaller task
					for each of these tasks
						solve(t)
						
					wait or each to complete
					join results of each task
					compute final result 
				
				return finalResult;
			
			}


	2.	PerThread Queuing and Work Stealing
	
		
		a. PerThread Queuing 
		
			-	Each Thread will have its own internal Dequeue
			-	All the subtasks will placed in that Thread internal Dequeue
			-	Thread will keep taking task from its internal Dequeue and executes them ---> hence there is no synchronization b/w threads
			
		b.	Work Stealing
			
			-	When one of the Thread is idle and it can steal the tasks from deque of other Threads 
			-	Idle Thread will steal the task from back side of the deque 
			-	Original Thread continue to execute task by taking from front end of deque

		c. 	Advantages of Per Thread Queueing and Work Stealing
		
			1.	Threads picking tasks from its own internal deque
			2.	Steals tasks from other Threads when its become Idle
			3.	No Blocking unless stealing from other Threads



	Code Snippet of ForkJoin Pool :
	
	
		class Fibonacci extends RecursiveTask<Integer> {
		
			final int n;
			
			Fibonacci(int n) {
				this.n = n;
			}
			
			public Integer compute() {
				
				Fibonacci f1 = new Fibonacci(n-2);
				f1.fork();
				
				Fibonacci f2 = new Fibonacci(n-1);
				f2.fork();
				
				return f1.join() + f2.join();
			}
		}


### Ideal for ForkJoin Pools

-	No Synchronization
-	No IO operations
-	No Shared variables
-	pure functions


###	ForkJoin Task Instances are Futures with some extra Methods

-	get(), get(TimeOut)
-	cancel(), isDone(), isCancelled()

### Use Cases of ForkJoin

-	Sorting
-	Matrix multiplication
-	Tree Traversals


----------------------------------------------------------

## Synchronous Queue


### Blocking Queue

- 	Blocking Queue is queue with array of elements 
- 	Blocking is Thread Safe
-	Producer will put the elements to queue from one end and Consumer will read the elements from another end
-	When Blocking Queue is empty ... Consumer try to read an element from Queue then Consumer will be blocked untill another element in the Queue
-	Similarly Blocking Queue is full ... Producer Thread will get blocked until one of the block is free

### Synchronous Queue

-	Synchronous queue is a Blocking queue but with size of one
-	In fact ... Synchronous queue has no size
-	In Synchronous Queue there is a direct hand-off of messages b/w Producer Thread and Consumer Thread

#### That's why

-	Synchronous Queue don't have peek() methods
-	No iterate() methods
-	Perfect for Direct Handoff


----------------------------------------------------------


## 	Thread Local 

### Use-Case #1 : Per Thread Instances for Memory Efficiency and Thread Safety

	Code Snippet:
	
		1.	Two Threads Creating Separate SimpleDateFormat instances
		
			class ThreadLocalEx {
			
				public static void main(String ... args) {
					new Thread(() -> {
						String date = ThreadLocalEx.getDateOfBirth(1);
						System.out.println(date);	
					}).start();
					
					new Thread(() -> {
						String date = ThreadLocalEx.getDateOfBirth(2);
						System.out.println(date);	
					
					}).start();
				}
				
				public static String getDateOfBirth(int id) {
					Date date = getBirthDateFromDB(id);
					SimpleDateFormat df = new SimpleDateFormat("yyyy-MM-dd");
					return df.format(date);
				}
			}
			
		2.	10 Threads Creating 10 Instances of SimpleDateFormat
		
			class ThreadLocalEx {
				
				ExecutorService threadPool = Executors.newThreadFixedPool(n:5);
			
				
				public static String getDateOfBirth(int id) {
					Date date = getUserBirthDateFromDB(id);
					SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
					return sdf.format(date);
				}
				
				public static void main() {
				
					for(int i=0; i <= 10; i++){
						threadPool.submit(new Thread(() -> {
							String date = ThreadLocalEx.getDateOfBirth();
							System.out.println(date);
						}));
					}
				}
			}
			
		3.	10 Threads executing 1000 Tasks with 1000 SimpleDateFormat Instances

			class ThreadLocalEx {
				
				ExecutorService threadPool = Executors.newThreadFixedPool(n:5);
			
				public static String getDateOfBirth(int id) {
					Date date = getUserBirthDateFromDB(id);
					SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
					return sdf.format(date);
				}
				
				public static void main() {
					for(int i=0; i <= 10000; i++){
						threadPool.submit(() -> {
							id = i;
							String date = getDateOfBirth(id);
							System.out.println(date);
						});
					}
				}
			}
			
		4.	Single Global SimpleDateFormat instance Sharing across 10000 Tasks
			
			class ThreadLocalEx {
				
				ExecutorService threadPool = Executors.newThreadFixedPool(n:5);
				SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd");
			
				public static String getDateOfBirth(int id) {
					Date date = getUserBirthDateFromDB(id);
					return sdf.format(date);
				}
				
				public static void main() {
					for(int i=0; i <= 10000; i++){
						threadPool.submit(() -> {
							id = i;
							String date = getDateOfBirth(id);
							System.out.println(date);
						});
					}
				}
			}
		
				

#### Problems :

1.	Local variables inside Tasks will be created for the Tasks 
2.	Single variables or Global variables will cause Concurrency Issue or Data Integrity Issue

#### Solution

1.	Create variables per Threads and share them across Tasks

	
	-	Before Java 8
		
		class ThreadSafetyFormatter {
		
			static ThreadLocal<SimpleDateFormat> dateFormatter = new ThreadLocal<SimpleDateFormat> {
				
				@Override
				protected SimpleDateFormat initialValue() {
					return new SimpleDateFormat("yyyy-MM-dd");//	Called only once per Thread
				}
				
				
				@Override
				public SimpleDateFormat get() {
					return super.get(); // First Time for each Thread this will implicitly call initialValue
					// Once its variable is loaded into cache it will be used across Tasks
					//	1st call = initialValue()
					// 	Subsequent call will returns initialized value
				}
				
			};
		}

		class ThreadLocalEx {
		
			ExecutorService threadPool = Executors.newFixedThreadPool(n:5);
			
			public static void main() {
				for(int i=0; i<=10000; i++) {
					threadPool.submit(() -> {
						
						String date = ThreadLocalEx.getDateOfBirth(i);
						System.out.println(date);
					
					});
				}
			}
			
			public static String getDateOfBirth(int id) {
					Date date = getUserBirthDateFromDB(id);
					SimpleDateFormat sdf = ThreadSafetyFormatter.dateFormatter.get();
					return sdf.format(date);
				}
		}

-	ThreadSafetyFormatter.get() call makes Threads to have own copy SimpleDateFormat


	-	Java 8
	
		class ThreadSafetyFormatter {
		
			static ThreadLocal<SimpleDateFormatter> dateFormatter = ThreadLocal.withInitial(() -> new SimpleDateFormat("yyyy-MM-dd"));
		}



###	Use-Case #2: Per Thread Context and Performance

-	Each request needs to handle by separate Thread 
-	Each Thread needs to go through 4 separate services
-	Each Service wants to know user details
-	One way to implement this is by using HashMap or ConcurrentHashMap
-	But problem with map is that Synchronization or Performance degradation

#### Solution : ThreadLocal with User variable in it 

-	Thread Handling request will be assigned a user details in first service to its ThreadLocal
-	Subsequent Requests will get the user details from ThreadLocal

	
	class UserContextHolder {
	
		static ThreadLocal<User> userHolder = new ThreadLocal<User>();
	}
	
	class Service1 {
	
		public void process() {
			User user = getUser();
			UserContextHolder.userHolder.set(user); // Set User for this Thread
		}
	}
	
	
	class Service2 {
	
		public void process() {
			User user = UserContextHolder.userHolder.get(); // Get User for this Thread
		}
	}

#### Notes: 

-	Spring uses ThreadLocal and Context Holder concept in many of its classes
-	In Spring each request will be handled by Separate Thread
-	Spring maintains request attributes throughout scope of Request
-	Once request is processed we need to clean up ThreadLocal Context Holder manually 


class UserContexHolder {

	public static ThreadLocal<User> userContextHodler = new ThreadLocal<User>();
}

class Service1 {
	// set User
}

class Service2 {
	// get User
}

class Service3 {
	// get User
}

class Service4 {
	//	get User
	// process
	// clean up context holder
	UserContextHolder.userContextHolder.remove();
}



### Advantages of ThreadLocal 

-	Per Thread Instances + Performance 
-	Per Thread Context
-	Thread Confinement // Thread Safety


----------------------------------------------------------
## 	Phaser vs CountDownLatch vs Cyclic Barrier
##	Asynchronous Java
##	Lock Conditions Class
##	Semaphore in Java
##	Reentrant Locks 
## 	Reentrant Lock vs ReadWriteLock	
##      Spin Locks
## 	Exchanger Class 
##	Stripped Locks
## 	Java Fibers in Project Loom (coroutines) 	
##	Completable Future























































