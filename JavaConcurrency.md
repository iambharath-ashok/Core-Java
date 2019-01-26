# Java-Concurrency: Java Threads and Concurrency


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
		
		
			Result solve(Problem problem) {
				if (problem is small)
					directly solve problem
				else {
					split problem into independent parts
					fork new subtasks to solve each part
					join all subtasks
					compose result from subresults
				}
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
## 	Phaser vs Count Down Latch vs Cyclic Barrier

###	Count Down Latch 

-	Count Down Latch is used when Thread Main needs to wait for Dependent Threads to initialize
-	Count Down Latch will be created and shared with tasks with Count down count
-	Once specified number of threads execute countDown() method ... Thread Main will start to execute
-	Count Down Latch can be used to initialize some resources ... 
-	Once specified number Threads completes initialization ... by calling latch.countDown() .... Thread Main will continue to proceed its execution


	Code Snippet Of Count Down Latch:
	
		public class CountDownLatchEx {
		
			ExecutorService threadPool = Executors.newFixedThreadPool(4);
			
			public static void main() {
				
				CountDownLatch latch = new CountDownLatch(3);
					
				threadPool.submit(new DependetService(latch));
				threadPool.submit(new DepedentService(latch));
				threadPool.submit(new DependentService(latch));
				
				latch.await();
			}
		}
		
		
		static class DependentService implements Runnable {
			
			CountDownLatch latch;
			
			DependentService(CountDownLatch latch) {
				this.latch = latch;
			}
			
			public void run() {
				
				// Initialized Service 
				this.latch.countDown();
				// Proceed further
			}
		
		}
		
		
### Cyclic Barrier 

-	Cyclic Barrier is a class 
-	CyclicBarrier is used when all dependent Threads will reach some barrier 
-	Dependent Threads will wait for other Threads to reach barrier and once all dependent Threads reach barrier ... 
-	Threads will continue their tasks
-	Threads will be blocked till all dependent threads reach the barrier


	Code Snippet of Cyclic Barrier:
	
		public class CyclicBarrierEx {

			static ExecutorService threadPool = Executors.newFixedThreadPool(4);
			static CyclicBarrier barrier = new CyclicBarrier(3);

			public static void main(String[] args) {

				for (int i = 0; i < 50; i++) {
					threadPool.submit(process());
				}
				
				try {
					Thread.sleep(10000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
				threadPool.shutdown();

			}

			private static Runnable process() {
				return () -> {
					try {
						while (true) {
							Thread.sleep(new Random().nextInt(6000));
							System.out.println(Thread.currentThread().getName() + " has reached Barrier");
							barrier.await();
							System.out.println(Thread.currentThread().getName() + " continued to process further tasks ");
						}
					} catch (InterruptedException e) {
						e.printStackTrace();
					} catch (BrokenBarrierException e) {
						e.printStackTrace();
					}
				};
			}
		}

		
### Phaser

-	Phaser is a class that acts both Cyclic Barrier and Count Down Latch and much more additional functionality
-	Phaser will have multiple phases with completing cycles


#### Phaser as Count Down Latch

	Code Snippet of Phaser as Count Down Latch:
		
		public class CountDownLatchPhaser {

			static ExecutorService threadPool = Executors.newFixedThreadPool(4);

			public static void main(String[] args) {

				Phaser phase = new Phaser();
				threadPool.submit(new Task(phase));
				threadPool.submit(new Task(phase));
				threadPool.submit(new Task(phase));
				
				System.out.println(Thread.currentThread().getName()+" is waiting for depending Threads to complete");
				
				phase.register();
				phase.arriveAndAwaitAdvance();
				
				
				
			}
			
			static class Task implements Runnable {

				Phaser phaser;

				Task(Phaser phaser) {
					this.phaser = phaser;
				}

				public void run() {
					try {
						Thread.sleep(new Random().nextInt(10000));
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
					System.out.println(Thread.currentThread().getName()+ " has arrived");
					phaser.arrive();
					
				}
			}
		}

#### Phaser as Cyclic Barrier


	Code Snippet of Phaser as Cyclic Barrier
	
	
		public class CyclicBarrierPhaser {

			static ExecutorService threadPool = Executors.newFixedThreadPool(4);

			public static void main(String[] args) {

				Phaser phase = new Phaser();
				threadPool.submit(new Task(phase));
				threadPool.submit(new Task(phase));
				threadPool.submit(new Task(phase));

			}

			static class Task implements Runnable {

				Phaser phaser;

				Task(Phaser phaser) {
					this.phaser = phaser;
				}

				public void run() {
						try {
							Thread.sleep(new Random().nextInt(10000));
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
						System.out.println(Thread.currentThread().getName() + " has arrived");
						try {
							Thread.sleep(1000);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
						System.out.println(Thread.currentThread().getName() + " is waiting for dependent threads");
						phaser.arriveAndAwaitAdvance();
						
						System.out.println(Thread.currentThread().getName() + " is proceeding further");
						
				}
			}

		}

		
#### Register and De-registering with Phaser

-	new Phaser(count)
-	register()
-	bulkRegister(count)


#### Methods of Phaser 

-	arrive()
-	arriveAndAwaitAdvance()
-	arriveAndDeregister()


#### Other Methods

-	gePhase()
-	getArrivedParties()
-	getUnarrivedParties()

-	onAdvance()
-	forceTerminate()
-	isTerminated()



----------------------------------------------------------
##	Asynchronous Java

- 	Each Java Thread is OS Thread or Kernel Thread
-	Every Java Thread will run on single core at a time
-	Each Java Thread will have PC, Java Stack, Stack Frames 
-	Each Java Threads will consume more memory  ... limiting the number of Threads 
-	With High computational devices also ... more number of Threads will result in slow performance
-	Scheduling Overhead, context switching around Threads and Data Locality result in slow performance


### Blocking IO Operation

-	IO Operation will block main thread till its completion and unable to process other requests
-	Blocking IO Operation not allows to utilize CPU Computation with full extent


###	Synchronous API

-	Synchronous API will block thread till its completion
-	Future<Integer>.get()


	Code Snippet of Synchronous API: 
	
		
		for(Integer id : empIds){
			
			Future<Employee> empFuture = threadPool.submit(new EmployeeFetcher(id));
			Employee emp = empFuture.get();// Main Thread will block
			
			Future<TaxRate> taxFuture = threadPool.submit(new TaxRateFetcher(emp));
			TaxRate taxRate = taxFuture.get(); // Main Thread will block
			
			
			BigDecimal tax = mputeTax(emp, taxRate);
			threadPool.submit(new MailSender(emp ,tax));
			
		} 
		
###	Asynchronous API


	Code Snippet of Asynchronous ApI
	
		for(Integer id : empIds) {
		
			CompletableFuture.supplyAsync(() -> fetchEmployee(id))
			.thenSupplyAsync(employee -> fetchTaxRate(employee));
			.thenSupplyAsync(taxRate -> computeTax(emp, taxRate))
			.acceptAsync(taxValue -> sendMail(emp, taxRate))
			
		}

### Problems is Java Threads are expensive and Blocking IO Ops

-	Expensive Thread + Blocking IO = Limited Scalability

### Solution for Blocking IO Operation and Sync ApI

-	Non-Blocking IO introduced in Java 7
-	Async API

###	Async API and Non-Blocking IO

-	NIO Non-Blocking IO will have callback methods ... 
-	Main Thread will trigger IO operation by passing a callback method .. once IO operation gets results it will call callback methods in a separate threads
-	ComplitabeFuture can be used as an Aysc API
-	ComplitableFuture is a algorithm where we specify the instructions by passing callback methods and chaining the operations


###	Servlet 3.0

-	Servlet 3.0 supports Async Calls
-	In Servlet each request will handled by a separate Thread
-	Thread will gets blocked for IO operation
-	Tomcat will have around 200 Threads ... so Tomcat only is able to serve 200 concurrent requests
-	One Solution is to make HTTP calls and IO calls in a separate Thread by passing callback method
-	In doing so Main Thread will not gets blocked and can process more number of concurrent requests


	@WebServlet(urlPatterns={"/user"}, asyncSupported=true)
	pubic class UserAsyncService extends HttpServlet {
		
		@Override
		public void doGet(HttpServletRequest request, HttpServletResponse response) {
		
			final AysncContext context = request.startAsync();
			context.start(new Runnable () {
				
				// Make Network Calls
				
				ServletResponse response = context.getResponse();
				
				
				contex.complete();
			});
		}
	}
	
	
### Servlet 3.1

-	Servlet 3.1 even went further 1 step to make read and writing attributes from request and response is non -blocking
-	Previously Read and writing of Request and response is blocking


	@WebServlet(urlPatterns ={"/user"}, asyncSupported=true)
	public class UserServicAsync_2 extends HttpServlet {
	
		@Override
		public void doGet(HttpServletRequest request, HttpServletResponse response){
			
			AsyncContext context = request.startAsync();
			ServletInputStream inputStream = response.getInputStream();
			inputStream.setReadListener(new ReadListener() {
			
				public void onAllDataRead() {
				
					// data available, process
					// Write data to output 
					
					// input and output read and write operation are non blocking
				}
			});
		} 
		
	}

	
	
### Spring Webflux 5.0

-	Reactive Programming 
-	Spring Webflux is reactive Programming under Sprig umbrella
-	Spring Webflux simplifies Non-Blocking Asynchronous programming
-	Spring uses Mono which is Future equivalent of Java 
-	Mono is push operation rather get operation
-	Whenever data or operation is ready it will push the data to Mono Object 
-	Mono Object will send response backt to client
-	In this way Servlet request will not be blocked for IO operation


### Problems with Reactive Programming

-	Difficult to debug
-	Difficult to understand
-	Different Stack Trace and difficult to trace 

### What we really want is 

1.	Light Weight Threads
2.	Synchronous Programming

-	Java is coming up with new project called Fibers which are light weight threads
-	Java Fibers are light weight threads
-	We can run millions of Java Fiber Threads on top of limited set of OS Threads
-	4 OS Thread with millions of Java Fiber Threads



----------------------------------------------------------
##	Lock Conditions Class


-	Condition is a class from java.util.concurrent Package 
-	Condition Class is used for Threads Coordination and Communication
-	Condition Class is similar to wait, notify(), notifyAll() Concepts
-	Difference b/w wait(), notify() and Condition class is that wait(), notify() methods needs to used in synchronized methods or block
-	wait(), notify(), notifyAll() methods  are from java.lang.Object class
-	wait(), notify(), notifyAll() methods are used to make any Object as MONITOR in Java


----------------------------------------------
### Use Case of Condition Class


-	Thread 1 after performing some task can't continue to perform further tasks until certain condition is met
-	Thread 1 will call await() method on Condition instance i.e coditionMet.await() ... Thread 1 will go to wait state
-	Thread 2 after performing some tasks will call conditionMet.signal() method ... which signals for Threads that are waiting for that condition to be met
-	JVM will take the Threads that are waiting for that condition to be met  ... will move from Waiting state to Runnable state



#### Code Snippets

		public class ConditionClass {

			static Lock lock = new ReentrantLock();
			static Condition condition = lock.newCondition();

			public static void main(String[] args) {
				ExecutorService threadPool = Executors.newFixedThreadPool(4);
				threadPool.submit(ConditionClass::method1);
				threadPool.submit(ConditionClass::method2);

			}

			public static void method1() {
				lock.lock();
				try {
					System.out.println(Thread.currentThread().getName() +" has Started ");
					Thread.sleep(2000);
					System.out.println(Thread.currentThread().getName()+" is awaiting for condition to be met");
					..// do some operations
					condition.await(); 				// <-----	Suspend here 
					// can do now dependent operations  <---- Resume here
					System.out.println(Thread.currentThread().getName()+" Has started execution after meeting the condition");
					
				} catch (Exception e) {
					e.printStackTrace();
				} finally {
					lock.unlock();
				}
			}
			
			public static void method2() {
				lock.lock();
				try {
					System.out.println(Thread.currentThread().getName()+" Has Started Execution");
					Thread.sleep(10000);
					System.out.println(Thread.currentThread().getName()+" Has Signal for waiting Threads");
					//do some operations
					condition.signal();
				} catch(Exception e) {
					e.printStackTrace();
				}		finally {
					lock.unlock();
				}
			}

		}

		
		
	Output :
	
		pool-1-thread-1 has Started 
		pool-1-thread-1 is awaiting for condition to be met
		pool-1-thread-2 Has Started Execution
		pool-1-thread-2 Has Signal for waiting Threads
		pool-1-thread-1 Has started execution after meeting the condition

----------------------------------------------

### Same semantics as wait-notify

-	Condition Class serves same semantics as wait-notify methods
-	Only difference is that wait-notify methods can be on any Java object and can be used as Monitor object
- 	Wait-Notify methods can be used only inside the synchronized blocks and methods
-	Monitor is nothing but a simple object ... that is used for Thread communication using wait and notify methods
-	Monitor can be any object i.e String, Object, or any Object
-	siganlAll() works on basis of FIFO and follows fairness 



	// wait-notify semantics
	public synchronized void execute() {
		
		try {
			monitor.wait();
		} catch(InterruptedException e) {
			e.printStackTrace();
		} 
		
		// notify only one Thread
		monitor.notify();
		
		...// notifyAll Threads
		monitor.notifyAll();
	}
	
	
	// condition class semantics
	
	this.lock.lock();
	try{
		condition.await();
	} finally {
		this.lock.unlock();
	}
	 
	 // Notify only one Thread
	 condition.signal();
	 
	 // Notify only All Thread
	 condition.signalAll();
	
----------------------------------------------
###	Perform await() in while loop

-	condition.await() method should be used and invoked in the while loop
-	Thread can do spurious wakeup even though no one has waked it up
-	In order to do avoid spurious wakeup we needs to put that in while loop ... again it will go in to await state
-	Some Threads may do spurious Wakeup in order to avoid that ... condition.await() method needs to be invoked in the while loop


#### Code Snippets


	public void consume() {
	
		this.lock.lock();
		try {
		
			while(count == 0) {
				condition.await();  // Spurious wake-up
			}

			return getData();
		} finally {
			this.lock.unlock();
		}
	}
	
	
----------------------------------------------

###	 Condition Class Best fit for Producer and Consumer  Problem


#### Code Snippet 

	Lock lock = new ReentrantLock();
	Condition added = lock.newCondition();
	Condition removed = lock.newCondition();
	

	class Producer {
	
		public void producer() {
			this.lock.lock();
			try {
				while( count == MAX_COUNT ) {
					removed.await();
				}		
				addData();
				added.signal(); // Sending Added Signal to Consumer Thread
			} finally {
				this.lock.unlock();
			}
		}
	}
	
	
	class Consumer {
		
		public void consume() {
			this.lock.lock();
			try {
				while(count == 0) {
				added.await();
			}	
				String message = getData();
				removed.signal(); // Sending Removed Signal to Producer Thread
			} finally {
				this.lock.unlock():	
			}
			
		}
	}

	




----------------------------------------------------------
##	Semaphore in Java Concurrency


-	Semaphore is class from java.util.concurrent package
-	Semaphore is used to manage or restrict access to resource( i.e External Resources)
-	Semaphore has a concept of permits that every Thread should acquire before access the resources or performing some tasks
-	Semaphore needs to be initialized with number of Permits 
-	Once Thread acquired a permit from Semaphore ... Semaphore count will be decremented
-	Once all Threads acquired permits from Semaphore and count of Semaphore becomes 0 ... then all the remaining Threads that were try to get Permits will be blocked at that point till one of the Thread release the permit
-	Once existing Thread releases the Permit ... then First Thread that is waiting for Permit will be given permit ... Thread can continue to perform the tasks
-	Semaphore at any point in time ... depending on permit count will allow only limited set(Number) of Threads to access or perform the operation



### Use Case #1: Making call to Slow External Service

-	Our Service needs to consume service from External Service ... which is Slow can handle limited set of Requests
-	In this case we need to allow only 3 Threads at a time to consume service from External Service
-	Our application is having 50 Threads ... but only 3 Threads should be allowed to consume the service from external system
-	This use case can be achieved by using Semaphore with 3 permits


#### Code Snippets of Semaphore:

	class Main {
	
		public static void main(String ... args) {
			
			ExecutorService threadPool = Executors.newFixedThreadPool(50);
			Semaphore semaphore = new Semaphore(3);
			
			
			IntStream.rangeClosed(1, 100).forEach(threadPool.execute(new Task(semaphore)));
		
		}
	}

	
	class Task implements Runnable {
		
		Semaphore semaphore;
		
		Task(Semaphore semaphore) {
			this semaphore = semaphore;
		}
		
		public void run() {
		
			this.semaphore.acquire(); // Throws InterruptedException
					or
			this.semaphore.acquireUninterruptbly();
			
			// After performing operation Threads should release the Permits 
			// Otherwise Semaphore permits will run out ... resulting in Threads blocked for Permit will never come out
			
			this.semaphore.release();
			
			// Number of permit acquired by thread should be equals to Thread releasing Permits
			
			
		}
	}

-----------------------------------------------------------
##	Reentrant Locks 


-	Lock allows to restrict access to shared resources 	... so that only one thread will allowed to access the Shared Resources
-	Lock allows only one Thread at a time access SHARED RESOURCE
-	Use case: Multiple Threads simultaneously modifying the Shared Resource DB

### Difference B/w ReentrantLock and Synchronized Keyword

-	Synchronized is a implicit lock
-	Lock are explicit
-	Lock allows locking and unlocking in any scopes and in any order
-	Ability to tryLock and tryLock(timeout) 


###	Why the name is Reentrant 

-	ReentrnantLock allows to call block multiple times
-	Thread wants to execute same or different code with same lock
-	No needs to wait Thread for Lock ... it already has and can reenter the lock
-	There is a method called getHoldCount() that gives #number of times that Thread has reentered the lock
-	Behind the screen Thread doesn't needs to reacquire the lock because it already holds the lock
-	Only hold count will gets incremented


###	Fairness Lock

-	ReentrantLock has a overloaded constructor that allows to create a fairness lock
-	ReentrantLock constructor has to pass a boolean value true to make it fairness lock
-	Fairness Lock try to ensure Threads in a FIFO order 
-	Fairness Lock allows to get hold of Lock for a Thread that has waited for longest duration
-	Fairness Lock will push the Threads that trying to get a lock on the Queue
-	Unfair Lock will may result in performance improvement but it leads some thread to STARVATION



### TryLock with ReentrantLock

-	boolean tryLock() is a method on the ReentrantLock 
-	lock() method will push the Thread in to waiting state if lock is not available
-	tryLock() method will try to acquire the lock if lock is not hold by any other Threads
-	tryLock() returns true or false depending on Lock status
-	If lock is not free then we can continue to perform other operations
-	Even if ReentrantLock is Fair Lock tryLock doesn't ensure fairness
-	To tryLock() to fairness we need to use overloaded tryLock(2, TimeUnit.SECONDS) method



###	Other Methods of Reentrant Lock

-	isHeldByCurrentThread
-	getQueueLength
-	getHoldCount
-	newCondition

#### Code Snippet of ReentrantLock with tryLock():

	public static void accesResource() {
		boolean lockAcquired = lock.tryLock();
		
		if(lockAcquried) {
			try {
				
				// Access Resource
				
			} finally {
				lock.unlock();
			}
		} else {
			// Do something else 
		}
	
	}


#### Code Snippet of ReentrantLock:


	
		public static void accessResource() {
			
			this.lock.lock();
			
			// Access to Shared Resource
			
			this.lock.unlock():
		
		}	
	
	
	
	public class MainClass {
	
		public  static void main() {
			
			ExecutorService threadPool = Executors.newFixedThreadPool(4);
				
			threadPool.submit(() -> accessResource());
			threadPool.submit(() -> accessResource());
			threadPool.submit(() -> accessResource());
			threadPool.submit(() -> accessResource());
		}
	}

	
####	Code Snippet of Synchronized Block:


	public static void accessResource() {
	
		synchronized(this) { // this.lock.lock()
			// access shared resources
		}                   // this.lock.unlock()
	
	}
	
	public class MainClass {
		
		public static void main(String ... args ) {
			ExecutorService threadPool = Executors.newFixedThreadPool(4);
				
			threadPool.submit(() -> accessResource());
			threadPool.submit(() -> accessResource());
			threadPool.submit(() -> accessResource());
			threadPool.submit(() -> accessResource());
		}
	}
	

### Use Case #1 : Booking a Seat on Movie App

-	Movie App allows to multiple users to book a ticket
-	Each user is a Single Thread
-	Allowing Multiple Threads simultaneously to book same ticket will result in to issues
-	To overcome this issue ... we allow only one Thread at a time to book the ticket

-----------------------------------------------------------
## 	Reentrant Lock vs ReentrantReadWriteLock	

1.	Reentrant Lock 

-	Normal Lock and only one Thread at a time
-	Good for general purpose locking

2.	ReadWriteLock

-	Good for Frequent Reads and Infrequent Writes
-	Much more performant than Reentrant Lock
-	ReentrantReadWriteLock has two functionality
-	Separate Read and Write locks per lock instance
-	Allows Write Lock owner Thread to also acquire read lock
-	One Writer Thread at a time and multiple Read Threads at a time
-	Even though ReadLock and WriteLock though are separate instances .... only one is allowed at a time
-	Either READ LOCK to be hold by N number of Threads or WRITE LOCK to be hold by 1 Thread at a time
-	But never both at same time


### Waiting Queue of ReentrantReadWriteLock 


-	When one of the Write Thread is holding write lock then both Read and Write Threads will blocked and put them in waiting queue
-	When one or more than one Thread holds the Read lock then ... if another Thread comes for Reading Shared resource then that Thread will be allowed to hold Read Lock ... will not put them in waiting queue
-	When Read Threads holds the Lock then all Write Thread will put in waiting state in waiting queue
-	When Read Threads release the lock ... then only one Write lock is allowed to hold the write lock 
-	Both Read and remaining write threads will be put on waiting queue



#### Code Snippet of ReadWriteLock: 

	class MainClass {
	
		private ReentrantReadWriteLock lock = new ReentrantReadWriteLock();
		private ReentrantReadWriteLock.ReadLock readLock = lock.readLock();
		private ReentrantReadWriteLock.WriteLock writeLock = lock.writeLock();
	
	
		public static void main() {
		
			Resource resource = new Resource():
			
			Thread t1 = new Thread(() -> resource.readResource()); t1.start();
			Thread t2 = new Thread(() -> resource.readResource()); t2.start();
			Thread t3 = new Thread(() -> resource.writeResource()); t3.start();
			Thread t4 = new Thread(() -> resource.writeResource()); t4.start();
		
		}
	}

	class Resource {
	
		public void readResource() {
			readLock.lock();
			
			//	View the Resource 
			
			readLock.unlock():
		}
		
		public void writeResource() {
			writeLock.lock();
			
			//	update the Resource
			writeLock.unlock();
		}
	
	}



### Use Case #1 : Booking a Seat on Movie App with Read and Write Lock

-	Using single lock across all the Threads will result in Performance Issue
-	When Threads wants to read the data ... it will have to wait for other Threads ... since only one Thread to allowed to hold the Lock
-	Some Thread may just want to read the Seat Chart ... some Threads may wants to update the data 
-	Threads wants to read the Seat Chart may hold the Read Lock ... and any number of Threads can hold of Read Lock
-	N number of Threads holding READ LOCK can view SEAT CHART at same time
-	While Read Threads hold the read lock ... Write Threads will in blocked status
-	Once all Read Threads release READ LOCK then Write Threads from WAIT QUEUE will to moved from Blocked status to Runnable Status
-	ONLY one WRITE Thread will be allowed to hold lock at a time

-----------------------------------------------------------

## 	Exchanger Class 

-	Exchanger Class is a class from java.util.concurrent package
-	Exchanger class is similar to Synchronous Queue ... which allows direct handoff of messages b/w producer and consumer
-	Exchanger class allows direct handoff b/w Producer and Consumer in both direction
-	Since both Producer and Consumer is getting Something in return it's Data Structure is called Exchange
-	When either of the Thread wants to exchange the items ... if one of the Thread is not available then Thread will get blocked
-	Whenever Thread is available ... then Threads will exchange the messages


### Use Case #1: Producer and Consumer exchanging with Full and Empty Buffer

-	Producer Thread initially will have Full Buffer (i.e contains data) which is ready to exchange
-	Consumer on the other hand has already read all the data and has Empty Buffer
-	At this point in time both Producer and Consumer can perform exchange of Buffers by calling Exchange method
-	After exchange ... Producer will have Empty buffer and Consumer will have empty buffer
-	Again Producer can fill the Buffer and Consumer can read the Buffer


---------------------------------------------------------
##	Stripped Locks

-	Stripped is a class from java.util.concurrent package 
-	Stripped Locks is used to handle number of locks while working with large set of Objects
-	Less Locks => Better Memory, more contention
-	More Locks => More Memory but High Throughput 
-	Stripped Locks will somewhere will fit in with middle and comes with limited set of Locks that can work with Thousands of objects
-	Stripped => Middle ground
-	Needs to have hashcode and equals method 
-	Choose Object to retrieve the lock
	

### Use case #1: Adding Candy's to 10000 bags with limited set of Threads 

-	We needs to add Different Colored Candy's to 10000 bags with 20 Threads
-	Thread 4 and 7 may tries to add Blue Candy to Bag 3 
-	bag.hasBlueCandy() method for both Threads result in false ... resulting in both Threads will add candy's twice to bag instead of one
-	Having Single Lock for 10000 bags will result in more Contention b/w Threads
-	Having 10000 Locks will result in More Memory Consumption ... => Inefficient Solution
-	We need middle ground or ideal of set of Locks to deal with 10000 Bags 
-	Striped Lock provides set of specified number of Locks ... that are passed to parameter to Stripped.lock(number: 10)
-	Stripped lock = Stripped.lock(10) will return 10 Locks ... that can be used to handle 10000 Bag Objects
-	One Lock will be assigned to Handle Set of Bags

### Code Snippet of Use Case #1:  Adding Candy's to 10000 bags with limited set of Threads 

	private Stripped<Lock> strippedLocks = Stripped.lock(10); // Total Number of Locks
	
	public void updateBag(Bag bag) {
			
		Lock lock = strippedLocks.get(bag.getId()); // Get a Lock for this Bag
		lock.lock();
		if(!bag.hasBlueCandy()) {						// Use like a Normal Lock
			bag.add(new Candy(color: blue));			// Perform Operations
		}
		lock.unlock();				
	}

	Code Snippet 
	
		Lock lock = strippedLock.get(bag.getId());
		// getId is a String ... and String Class has valid equals and hashcode method implementation
		
		
		Lock lock = strippedLock.get(bag);
		// In order to use Custom Object as key to get Lock from strippedLocks
		// valid implementation of hashcode and equals method needs to provided on Bag Class

	
##### No matter how many bag instances we have all will be resolved with these 10 Locks


### How Locks are mapped to an Object

-	Lock will assigned based on Object hashcode value % Number of Locks 
-	Lock# = Object HashCode % 10

			   Hashcode    Total Locks	  #Lock to be used
		Lock # = 2432    %    10 	    =   2
		Lock # = 433     %    10	    =   3
		Lock # = 99437   %    10 	    =   7
		Lock # = 82      %    10 	    =   2



### Code Snippet of Stripped Locks 

		
	if(!bag.hasBlueCandy()) {
		bag.add(new Candy(color: blue));
	}


	Solution with Lock 

	lock.lock();
	if(!bag.hasBlueCandy()) {
		bag.add(new Candy(color: blue));
	}
	lock.unlock();
		
---------------------------------------------------------

##  Spin Locks

-	Keep trying to acquire the lock without going into wait state
-	Assumption: Most locks are used for short period of time
-	Spin Locks are also called Busy Loop, Busy Wait, Spinning
-	

### Trade Off of Spin Lock

							    Spinning 							Wait State 
						
Lock Available Quickly 		Improves perf 				      cost of Thread Switches
						  by avoiding Thread Swich	

Locks Taking More Time 		Thread Starvation 			      Improves CPU utilization





###	Adaptive Spinning

-	Try spinning for some time, if still not available then go into wait state 
-	JVM Profiles the code and decides how much time to spin for 


###	Use case #1: Update a Bid 

-	Suppose we want to update a Bid with latest Bid value
-	Bid Request will come with Bid ID 
-	Fetch Bid 
-	Increment Bid
-	Save Item
-	Concurrent updates by multiple Threads can be avoided by Lock
-	To improve performance Threads can run across multiple Cores
-	Thread 1 will try to perform operation by acquiring a lock 
-	Instead of saving item back to DB ... we will save it in in-memory 
-	This is going to be very quick operation ...  Thread 2 will keep on trying to acquire the lock
-	Thread 2 instead of going to waiting state by doing context switching will keep trying to acquire the lock



#### Code Snippet of Use Case:

	public void update(int id) {
	
		Lock lock = getLock():
		lock.lock();
		
		try {
			BidItem item = getItem(id);
			Item item = incrementBid(item);
			saveItem(item);
			
		} finally {
			lock.unlock();
		}
	
	}





---------------------------------------------------------
## 	Coroutines and Java Fibers in Project Loom (coroutines) 	


### Use Case #1: Getting 10000 Products from External Service

-	In this use case we needs to fetch 10000 products from external Service and update then and save it into our DB
-	We created 10000 tasks for each of the operations and submit them for ThreadPool
-	A ThreadPool of 10 Threads can perform handle 10000 tasks
-	Since Use Case #1 contains HTTP call and DB IO call ... Threads will gets blocked for IO and HTTP operations
-	Blocking Threads will result in inefficient CPU utilization
-	One solution is to use CacheThreadPool ... that will creates as many Threads as required
-	But CachedThreadPool will result in JVM crash or OutOfMemoryException


	Code Snippet of Use Case :
	
		ExecutorService threadPool = Executors.newFixedThreadPool(10);
		
		
		for(int i = 1; i <= 100_000; i++) {
			
			int productId = i;
			
			Runnable task = new Runnable() {
						
				@Override
				public void run() {
					Product p = getProduct(productId);
					updatePrice(p);
					saveProduct(p);
				}
			};
			
			threadPool.submit(task);
		}
	
		


###	What's the Core Problem
-	waiting Threads don't allow scaling(CPU sits Idle)
-	Threads are too expensive ... 1 MB STACK ... Can't create too many of them
-	Task waiting for IO Operations ... blocks the Thread itself


### Using Reactive Programming to solve  Core, Thread and Blocking IO Operations

-	Event or Callback method based approach 
-	Threading is handled efficiently in Reactive Framework
-	Threads will not wait for IO Operation to complete ... instead will provide a callback method ... which will be called operation is completed
- 	Main Threads will submit a task in separate Thread and pass a callback method to call ... once operation is completed


### Problems with Reactive Programming

-	Needs to learn huge number of APIs to work with it
-	Not easy to learn and understand the code
- 	Nor easy to debug the Code




### Java Fibers 

-	Java Fibers is a upcoming project from Java
-	Millions of Threads will run on top limited set of OS Threads 
-	Java Fiber uses millions of Light Weight Threads that can be used with existing APIs

	Advantages of Fibers over Threads
	
	-	Very light weight .. only 1 KB of Stack .. compared to 1 MB of Stack of Thread
	-	Do not block the underlying Threads
	-	Can use same API as used with Threads
	-	Can run millions of Fibers in an Application
	-	Will enable servers handling thousands of Concurrent Requests





---------------------------------------------------------
##	Completable Future


-	Performing Non-Blocking Operation is very easy in Java 
-	Create a new task and submit that task for new separate Thread ... so that Main Thread will not gets blocked
-	Runnable Thread will call run method and once run method is completed ... Thread will gets destroyed
-	To return a value from the Thread we can use Callable and Future 
-	Callable will returns a value from Thread and Future will be used to fetch the value from Future Instance
-	Future is like a container that holds the value whenever value is ready 
-	future.get() method call is a Blocking call ... i.e Thread will gets blocked until value will be available



### Use Case #1: Order Management

-	Below is the set of operations for processing an Orders 

-	Fetch an Orders
-	Enrich an Order
-	Payment for an Order
-	Dispatch an Order
-	Send an Email 


### Code Snippet for Processing an Orders using Future and Callable

-	Below code is not scalable 
-	Thread will gets blocked for each future.get() call


	Code Snippet:
	
		public void processOrders() {
			
			try {
		
				Future<Order> orderFuture = threadPool.submit(fetchOrder());
				Order order = orderFuture.get(); // Blocking Operation
				
				Future<Order> enrichFuture = threadPool.submit(enrichOrder(order));
				Order enrichedOrder =  enrichFuture.get();
				
				Future<Order> paymentFuture = threadPool.submit(performPayment(enrichOrder));
				order = paymentFuture.get();// 
				
				Future<Order> future = threadPool(dispatchTask(order));
				order = future.get();
				
				Future<Order> future = threadPool(sendEmail(order));
				order = future.get();
			} catch(InterruptedException | ExecutionException e) {
				e.printStackTrace();
			}	
		}

### Code Snippet for Processing an Orders using Completable Future

-	CompletableFuture is a class from java.util.concurrent package
-	CompletableFuture is used perform blocking operations in a most efficient way
-	CompletableFuture takes a callback method ... performs operations on the callback methods
- 	CompletableFuture class provides a static method called supplyAsync ... for which we provide a task or method 
-	In CompletableFuture class we can chain the dependent tasks ... like an Algorithm


	Code Snippet:
	
		for(int i =0; i<=100_00; i++) {
			
			CompletableFuture.supplyAysnc(() -> fetchOrder())
				.thenApply(order -> enrichOrder(order))
				.thenApply(o -> performPayment(o))
				.thenApply(order -> dispatch(order))
				.thenAccept(order -> sendEmail(order));
		}


-	thenApply() will be executed same Thread
-	thenApplyAsync() method is used to supply other Thread pool to execute the task
-	supplyAsync() method will have a overloaded methods	that will take other ThreadPool 


	Code Snippet thenSupplyAsync:
		
		ExecutorService cpuBound = Executors.newFixedThreadPool(5);
		ExecutorService ioBound = Executors.newCachedThreadPool();
		
		for(int i =0; i<=100_00; i++) {
			
			CompletableFuture.supplyAysnc(() -> fetchOrder(), ioBound)
				.thenApplyAsync(order -> enrichOrder(order), cpuBound)
				.thenApplyAsync(o -> performPayment(o), ioBound)
				.thenApplyAsync(order -> dispatch(order))
				.thenAccept(order -> sendEmail(order));
		}

-	For CompletableFuture doesn't need any ThreadPool to submit task 
-	All tasks scheduling will be managed Automatically by JVM
-	CompletableFuture by default internally uses Fork Join Pool to manage the task


		for(int i =0; i<=100_00; i++) {
			
			CompletableFuture.supplyAysnc(() -> fetchOrder(), ioBound)
				.thenApplyAsync(order -> enrichOrder(order), cpuBound)
				.thenApplyAsync(o -> performPayment(o), ioBound)
				.exceptionally(e -> new FailOrder())
				.thenApplyAsync(order -> dispatch(order))
				.thenAccept(order -> sendEmail(order));
		}
		

-	exceptionally)() methods is used to handle any exception in the CompletableFuture operations		
	
---------------------------------------------------------
##	DeadLocks

-	DeadLocks occurs when Thread is waiting for a lock held by another Thread and vice versa
-	DeadLocks are difficult to detect due to multiple types of locks and Thread Sources
-	DeadLockds can be detect at runtime using ThreadDumps
-	Consistent ordering of Locks helps in avoiding DeadLock
-	Using Timeouts on Lock Acquisition will also helps

### What is a DeadLock

-	Thread 1 acquiring Lock A will wait for Lock B
-	Thread 2 acquiring Lock B will wait for Lock A 


#### Code Snippet of DeadLock

	class DeadLockEx {
	
		Lock lockA = new ReentrantLock();
		Lock lockB = new ReentrantLock();
		
		private void execute() {
		
			new Thread(this::processThis).start();
			new Thread(this::processThat).start();
		}
		
		
		// Thread 1 Executing processThis method
		public void processThis() {
			lockA.lock();
				
				// some operations
			
				lockB.lock(); // DeadLock
			
			
			
				lockB.unlock();
			lockA.unlock();
		}
		
		public void processThat() {
			lockB.lock();
				
				// some operations
			
				lockA.lock(); // DeadLock
			
			
			
				lockA.unlock();
			lockB.unlock();
			
		}
	
	}

### How to Detect DeadLocks at Runtime?

-	There are tools for detecting DeadLocks at runtime
-	ThreadDump is tool that is used to detect DeadLocks at runtime
-	Commands to detect DeadLocks at runtime

	1.	jstack 11475 > ./threadDump.txt
	
		-	jstack is a command to print the Threads stack that are in DeadLock 
		-	For jstack we needs to pass the Process_Id
		-	Above command will redirect Thread Dump log to file
		
		
	2.	kill -3 12704
	
		-	Above Command will print the Threads that are in DeadLock status at Runtime
		
	3.	Java Provides an API to detect DeadLock at runtime

		-	Java provides an API which constantly run in background 
		-	Where JVM will tell at any point in time ... there is an DeadLock 
		
	
### How to prevent DeadLocks?

-	Creating and acquiring Locks by providing a TimeOut a Param
-	Acquiring Lock in same order across different methods



#### Code snippets of Acquiring Locks with TimeOut 


	public void execute() {
		
		Lock lock = new ReentrantLock();
		boolean isAvailable = lock.tryLock(2 , TimeUnit.SECONDS);
		
		
		BlockingQueue queue = new ArrayBlockingQueue(16);
		queue.poll(2, TimeUnit.SECONDS);
		
		
		Semaphore semaphore = new Semaphore(1);
		semaphore.acquire(2, TimeUnit.SECONDS);
	
	}

	
###	Global Ordering can be Tricky


	Code snippet:
	
		public void transfer(Account acct1, Account acc2, int amount) {
		
			synchronized(acct1) {
				synchronized(acct2) {
					acc1.deduct(amount);
					acc2.add(amount);
				}
			}
		}
		
		
		public void execute() {
		
			new Thread(this::transfer(john, marlie, 2000)).start();
			new Thread(this::transfer(marlie, john, 3000)).start();
		
		}
		
		
		public void transfer(Account from, Account to, BidDecimal amount) {
		
			Account acc1 = getLarger(from, to);
			Account acc2 = getSmaller(from, to);
			
			synchronized(acct1) {
				synchronized(acct2) {
					acc1.deduct(amount);
					acc2.add(amount);
				}
			}
		}
		
		
		// Updated code to avoid DeadLock
		
		public void execute() {
		
			new Thread(this::transfer(john, marlie, 2000)).start();
			new Thread(this::transfer(marlie, john, 3000)).start();
		
		}
		
		
		
---------------------------------------------------------
## How to TimeOut a Thread - Interview Question


-	A task is Running in Separate Thread. Stop the task if it exceeds 10 mins
-	We needs to break this into two parts
	
	-	How we can stop or interrupt signal to Thread
	-	And termination after 10 minutes

1. 	Stopping the Thread/ Task
2.	Timeout Condition


### Part 1. Stopping the Thread/ Task or How to Stop



#####	Executor ThreadPool shutdown methods to force stop the Task

-	shutDown()
	
	-	No new tasks will be accepted 
	-	Previously submitted tasks are executed
	
-	shutDownNow()

	-	No new tasks will be accepted
	-	Previously submitted tasks waiting in queue will be returned
	-	Tasks being run by Threads are attempted to stop 
	
	
- No Guarantee to stop the Threads



#####	Future and Callable 

- 	future.cancel(true); // Methods will only attempt to stop the Threads
-	Java Threads can't be killed 
-	They are cooperative
-	We needs to ASK THREADS POLITELY



####	How to ASK POLITELY for Threads

##### 1.	Interrupts

-	Calling interrupt method on Thread
-	In TASK we needs check whether any body wants interrupt the Thread
-	We needs to write a logic to check Interruption frequently in the while loop


	Code Snippet: 
	
	
		public static void main(String ... args) {
			
			Thread t1 = new Thread(() -> {
			
				while(!Thread.currentThread().isInterrupted()) {  // Keep checking for Interrupts
					//	Next Step
				}
			});
			
			t1.start();
			
			// 2.	TODO: Timeout for 10 Minutes
			
			// 3.	stop or interrupt the Thread
			t1.interrupt();
				or
			t1.shutDownNow(); // This internally calls Thread.interrupt
		}
		
		
		
		
		// Future 
		
		public static void main(String ... args) {
		
			ExecutorService threadPool = Executors.newFixedThreadPool(3);
			
			Future<?> future = threadPool.submit(() -> {
			
				while(!Thread.currentThread().isInterrupted()) {
					
				}
			});
			
			future.cancel(true); // Calls Thread.interrupt() method for Currently Running Thread
		}
		

##### 2.	Volatile/ AtomicBoolean


-	Stopping Thread using AtomicBoolean and Volatile Keyword

	
###### Code Snippet showing Stopping Thread using volatile keyword

	
		Code Snippet:
			
			public static void main(String ... args) {
				
				MyTask task = new MyTask();
				Thread thread = new Thread(task); // Same will work for ThreadPool also  
				
				thread.start();
				
					
				// 2.	TODO: Timeout for 10 Minutes
				
				// 3.	stop or interrupt the Thread
				
				task.keepRunning = false;
				
			}
			
			public class MyTask implements Runnable {
			
				public volatile boolean keepRunning = true;
				
				@Override
				public void run() {
					
					while(KeepRunning) {
						//Threads will keeps on running
					}
						
				}
			
			}


###### Code Snippet showing Stopping Thread using AtomicBoolean



	Code Snippet:
			
			public static void main(String ... args) {
				
				MyTask task = new MyTask();
				Thread thread = new Thread(task); // Same will work for ThreadPool also  
				
				thread.start();
				
					
				// 2.	TODO: Timeout for 10 Minutes
				
				// 3.	stop or interrupt the Thread
				
				task.stop();
				
			}
			
			public class MyTask implements Runnable {
			
				public AtomicBoolean keepRunning = new AtomicBoolean(true);
				
				@Override
				public void run() {
					
					while(keepRunning.get() == true) {
						//Threads will keeps on running
					}
						
				}
				
				public void stop() {
					keepRunning.set(false);
				}
			
			}

------------------------------------

### Part 2. Conditional Timeout

-	Once we setup ways to stop Threads ... we can stop the Thread only after certain timeout



#### Code Snippets


-	Thread.sleep(10* 60 * 1000)

	
		public static void main() {
		
		
			// 1.	Create a Task and Submit it to a Thread
			MyTask task = new MyTask();
			Thread thread1 = new Thread(task);
			
			thread1.start();
			
			//	2.	 TimeOut for 10 Minutes
			try {
				Thread.sleep(10 * 60 * 1000);
			} catch(Exception e) {
				e.printStackTrace();
			}
			
			// 3.	Stop the Thread
			task.stop();
		}



-	Scheduler Executor Service


		public static void main() {
			MyTask task = new MyTask();
			Thread thread1 = new Thread(task);
			
			thread1.start();
			
			ScheduledExecutorService scheduler = Executors.newScheduledThreadPool(1);
			scheduler.schedule(() -> {
				task.stop();
			}, 10, TimeUnit.MINUTES);
		
		}

-	Future cancel with a TimeOut


	
		public static void main() {
		
			ExecutorService threadPool = Executors.newFixedThreadPool(2);
			
			//	1.	Create a task and submit to a Thread	
			MyTask task = new MyTask();
			final Future<?> future = threadPool.submit(task);
			
			try {
				// 2.	Wait for 10 Minute to get Response
				future.get(10, TimeUnit.MINUTES);
			} catch(InterruptedException | ExecutionException e) {
				e.printStackTrace();
			} catch(TimeoutException e) {
				future.cancel(true); // If using interrupts
				task.stop(); // If using volatile
			}
			
		
		
		}

--------------------------------------
## Java Interrupts

-	Threads can't be forced to Shutdown in Java
-	We can only Request Thread to stop ... politely 
-	A Thread can be Requested to stop by another Thread using interrupt method
-	thread.interrupt() method ... will send a interrupt signal to Running thread
-	Thread may or may not get interrupted(stopped) based on it's stage
-	There are two methods Thread class to check whether Thread is interrupted or not 


	boolean interrupted() - reset the interrupted flag and returns boolean value
	boolean isInterrupted() -	returns interrupted flag value based on whether Thread is interrupted or not
	
-	Thread.sleep(long millis) and thread.wait() method will throw InterruptedException when Thread got Interrupted while Thread is in waiting or sleeping state
-	Thread.sleep(long millis) and thread.wait() needs to have try and catch block for interrupted exception
-	We should throw InterruptedException from Running Thread to Main Thread ... to intimate problem in Running Thread

--------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
##----------------------------------------------------------
