

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
	
	```java 
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
	````


-	In the above code join() method on t1 and t2 will makes Main Thread to wait till t1 and t2 joins with Thread Main

--------------------------------------------------------------------

## Synchronized Simple Example


Code Snippet :

```java 
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
````
	

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

	```java 
		public static void main() {
		
			ExecutorService es = Executors.newFixedThreadPool(4);
			es.submit(() -> processTax(user1));
			es.submit(() -> processTax(user2));
			
			heavyCalculations();
		}
	````

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
	
	```java 
		class FieldVisibility {
			
			int x =0;
			
			public void writerThread() {
				x = 1;
			}
			
			public void readThread() {
				r1 = x;
			}
		}
	````
	
	
	-	When Writer Thread write the value it will write it only of Local Cache ... which is x =1
	-	Not Pushed to Shared Cache 
	-	Reader Thread while reading from Shared cache which is still x =0; ... but should be x= 1;
	
	
	Code Snippet :
	
	```java 
		class VolotileFieldVisibility {
		
			volatile int x = 0;
			
			public void writerThread() {
				x = 1;
			}
			
			public void readerThread() {
				r2 = x;
			}
		}

	````
	-	volatile Keyword make sure that latest values from Local Cache will be pushed to shared cache by JVM before Read Operation

#### JMM
	
-	JMM is a specification or set of Rules which guarantees field visibility on top of reordering of instructions
-	JMM defines a set of rules that each JVM should implement ... so that program running on different JVM results in same output

#### Happens Before Relationship

-	JMM rule that what ever fields written before volatile will be reflected to other threads after reading volatile field



	Code Snippet :
	
	```java 
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

	````

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

	```java
		volatile int counter = 0;

		synchronized (this) {
			counter++;
		}
	````
	
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


### AtomicLong
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



















































































