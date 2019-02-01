

# Java Collections 

# How HashMap works in Java

##  Associative Data Structure:
	-	Map is a Associative Array Data Structure: Key1: -> Value1, Key2: -> Value2
	
	
##	Hashing:
	-	Transformation of String representation data to shortened form of fixed data with Integer Value
	-	Shortened Integer Value helps in indexing and faster searches

## public int hashcode():

	-	Every Java will have hashCode() method that returns the hashcode value for an invoked instance
	
	
## High Level Implmentation of HashMap:

-	HashMap class implements clonable and serializable and extends AbastractMap


## HashMap Low Level Implementation:

-	HashMap has a Table or Array of Nodes that in-turn will have set of LinkedList
-	Each index in table is called bucket which basically a Node which in turn is a List of LinkedList
		 			
-	Node:
	-	Node itself is a LinkedList
	-	A Node has key, hashcode, value, pointer to next Node
	
		Node<K,V>:
		
			int hash;
			K Key;
			V Value;
			Node<k, V> next;//pointer to next Node<K,V>

### Size of HashMap Table

-	By default the size of the HashMap table is 16 range from 0 to 15

### put(K k, V v)

	Code Snippet:
		
		put(K k, V v) {
			
			hash(K)
			
			index = hash & n-1
		
		}

### get(K v)


	Code Snippet:
	
		get(K k) {
			hash(k)
			
			index = hash % n-1
			
			equals
		}
-	HashMap allows Nulls as keys and 
-	HashMap with Null key will always have hashcode value of 0		
-	HashMap with Null key will always go to 0th bucket of HashMap

## 	Java 8 Changes for HashMap

-	When we have lot of unequal key with same which gives same index - all the keys will go to same bucket
-	Java 8, introduced a TREEIFY_THRESHOLD, when number of items exceeds Threshold LinkedList will be converted to Balanced Tree
-	Balanced Tree is better performance than LinkedList i.e O(n) vs O(log n)
-	In Balanced Tree, smaller hashcode will go to left and higher hashcode will be moved to right part of the tree
-	Performance of Balanced Tree depends on implementation of hashcode and Comparable result for the keys
------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------

## Types of Maps in Java 

1.	HashMap
2.  LinkedHashMap
3.	TreeMap
4.	Hashtable
5.	WeakHashMap
6.	IdentityHashMap
7.	ConcurrentHashMap
8.	Collections.SynchronizedMap
9.	EnumMap
10.	ConcurrentSkipListMap


### 1.	java.util.HashTable

-	Legacy and very first ... even before collection package was introduced
-	All methods are Thread Safe
-	Synchronized keyword on each public Method such as put, get, remove
-	10000 Threads Reading is also very costly 



### 2.	java.util.HashMap


- 	MOst Popular implementation of Map
-	Not Thread Safe
-	Doesn't allow duplicate keys
-	Allows Null Keys only once
-	Doesn't follow insertion order


###	3.	java.util.LinkedHashMap

- 	Popular implementation of Map
-	Not Thread Safe
-	Doesn't allow duplicate keys
-	Allows Null Keys only once
-	Follow insertion order
-	Internally use DoublyLinkedList
-	Takes more memory space as it used DoublyLinkedList DS


###	4.	java.util.TreeMap

- 	Popular implementation of Map
-	Not Thread Safe
-	Doesn't allow duplicate keys
-	Not Allows Null and Throw NullPointer
-	Follow some sorting technique
-	Keys should implement Comparable or we need provide Comparator Impl  .... otherwise Throws ClassCastException
-	Internally use Red-Black Tree based implementaion




### 5.	java.util.IdentityHashMap


-	Uses Identity to store and retrieve Keys
-	Uses reference equality : r1 == r2 rather than r1.equals(r2)
-	For hashing, System.identityHashCode(givenKey) is invoked rather than givenKey.hashCode()
-	Used is serializationa and deep copying



### 6.	EnumMap<K extends Enum<K>,V>

-	EnumMap takes Enum as key 
-	EnumMap key should come from same Enum Type
-	Iterator is not fail-fast
-	Null Keys not permitted and Not synchronized
-	Not Thread Safe
-	EnumMap is ordered collection and they are maintained in the natural order of their keys
-	Natural order of keys means the order on which enum constant are declared inside enum type
-	It’s a high performance map implementation, much faster than HashMap
-	All keys of each EnumMap instance must be keys of a single enum type.
-	EnumMap doesn’t allow null key and throw NullPointerException, at same time null values are permitted.


	Code Snippet: 
	
		public class MapIterator {

			public static void main(String[] args) {

				Map<String, Integer> map = new HashMap<>();

				map.put("user1", 7);
				map.put("user2", 7);
				map.put("user3", 7);
				map.put("user4", 7);
				map.put("user5", 7);
				map.put("user6", 7);
				map.put("user7", 7);
				map.put("user8", 7);

				/*
				  // Throws ConcurrentModificationException
				  
				 Iterator<Entry<String, Integer>> iterator = map.entrySet().iterator();

				while (iterator.hasNext()) {
					System.out.println(iterator.next());
					map.put("dddd", 99);
				}*/
				
				Map<Car,Integer> enumMap = new EnumMap<>(Car.class);
				enumMap.put(Car.AUDI,3);
				enumMap.put(Car.BENZ,6);
				enumMap.put(Car.BMW,5);
				enumMap.put(Car.ROYCE,13);
				
				Iterator<Entry<Car, Integer>> iterator2 = enumMap.entrySet().iterator();
				
				while (iterator2.hasNext()) {
					System.out.println(iterator2.next());
					enumMap.put(Car.ROYCE, 99);
				}
			}
		}

		enum Fruit {
			BANANA, MANGO, GRAPES
		}
		enum Car {
			BMW, BENZ, AUDI, ROYCE
		}

	Output :
	
		BMW=5
		BENZ=6
		AUDI=3
		ROYCE=99



### 7.	WeakHashMap

-	WeakHashMap is the Hash table based implementation of the Map interface, with weak keys.
-	An entry in a WeakHashMap will automatically be removed when its key is no longer in ordinary use.
-	When a key has been discarded its entry is effectively removed from the map
-	Both null values and null keys are supported in WeakHashMap.
-	It is not synchronised.
-	This class is intended primarily for use with key objects whose equals methods test for object identity using the == operator.
-	Key inserted gets wrapped in java.lang.ref.WeakRef
-	Best Suitable for Cache Implementation


	Code Snippet :
	
		Map<Pizza, Integer> weakHashMap = new WeakHashMap<>();
		
		Pizza p1 = new Pizza();
		Pizza p2 = new Pizza();
		Pizza p3 = new Pizza();
		
		weakHashMap.put(p1, 2);
		weakHashMap.put(p2, 2);
		weakHashMap.put(p3, 2);
		
		
		System.out.println(weakHashMap);
		p1 = null;
		
		System.gc();
		
		System.out.println(weakHashMap);
		
	
		
	OutPut :

		{Pizza@1c6b6478=2, Pizza@6a38e57f=2, Pizza@5577140b=2}
		{Pizza@6a38e57f=2, Pizza@5577140b=2}


### 8.	Collection.synchronizedMap(aMap)


-	The synchronizedMap() method of java.util.Collections class is used to return a synchronized (thread-safe) map backed by the specified map.
-	Returns a implementation of type SynchronizedMap 
-	All methods in SynchonizedMap is Synchronized
-	Similar to Hashtable and prefered to use in application


	Code Snippet:
	
		Collections.synchronizedMap(map);
		
		


### 9.	ConcurrentHashMap

-	ConcureentHashMap is enhancement of HashMap and Thread Safe
-	The underlined data structure for ConcurrentHashMap is Hashtable.
-	ConcurrentHashMap class is thread-safe i.e. multiple thread can operate on a single object without any complications.
-	At a time any number of threads can perform read operation without locking the ConcurrentHashMap object which is not there in HashMap.
-	In ConcurrentHashMap, the Object is divided into number of segments according to the concurrency level.
-	Default concurrency-level of ConcurrentHashMap is 16.
-	In ConcurrentHashMap, at a time any number of threads can perform read operation but for updation in object, thread must lock the particular segment in which thread want to operate. 
-	This type of locking mechanism is known as Segment locking or bucket locking.Hence at a time 16 updation operations can be performed by threads.
-	null insertion is not possible in ConcurrentHashMap as key or value.
-	Provides Some Atomic Operations from java 8 computIfAbsent(),compute(), computIfPresent()
-	Iterations do not throw ConcurrentModificationException
-	All Operations in ConcurrentHashMap is not Atomic
	
	
	
	Code Snippet showing ConcureentHashMap operations are not Atomic :
	
		public class ConcurrentHashMapEx {

			static ConcurrentMap<String, Long> orders = new ConcurrentHashMap<>();

			private static void processOrders() {
				for (String city : orders.keySet()) {
					for (int i = 0; i < 50; i++) {
						Long oldCount = orders.get(city);
						orders.put(city, oldCount+1);
					}
				}
			}

			public static void main(String[] args) throws InterruptedException {

				orders.put("Bombay", 0l);
				orders.put("New York", 0l);
				orders.put("London", 0l);
				orders.put("Tokyo", 0l);

				ExecutorService es = Executors.newFixedThreadPool(2);

				es.submit(ConcurrentHashMapEx::processOrders);
				es.submit(ConcurrentHashMapEx::processOrders);

				es.awaitTermination(1000, TimeUnit.MILLISECONDS);
				es.shutdown();
				
				System.out.println(orders);
				
			}
		}
		
		Output :
		
			{New York=100, Bombay=100, Tokyo=95, London=100}
			{New York=64, Bombay=60, Tokyo=64, London=54}
			{New York=50, Bombay=95, Tokyo=89, London=100}
			{New York=100, Bombay=100, Tokyo=100, London=100}


	
	Code Snippet showing ConcurrentHashMap with AtomicInteger:

		public class ConcurrentHashMapEx {

			static ConcurrentMap<String, AtomicInteger> orders = new ConcurrentHashMap<>();

			private static void processOrders() {
				for (String city : orders.keySet()) {
					for (int i = 0; i < 50; i++) {
		//				Long oldCount = orders.get(city);
		//				orders.put(city, oldCount+1);
						orders.get(city).incrementAndGet();
					}
				}
			}

			public static void main(String[] args) throws InterruptedException {

				orders.put("Bombay", new AtomicInteger());
				orders.put("New York", new AtomicInteger());
				orders.put("London", new AtomicInteger());
				orders.put("Tokyo", new AtomicInteger());

				ExecutorService es = Executors.newFixedThreadPool(2);

				es.submit(ConcurrentHashMapEx::processOrders);
				es.submit(ConcurrentHashMapEx::processOrders);

				es.awaitTermination(1000, TimeUnit.MILLISECONDS);
				es.shutdown();
				
				System.out.println(orders);
				
			}
		}
		
	Output :
	
		{New York=100, Bombay=100, Tokyo=100, London=100}
		{New York=100, Bombay=100, Tokyo=100, London=100}
		{New York=100, Bombay=100, Tokyo=100, London=100}
		{New York=100, Bombay=100, Tokyo=100, London=100}


	

###	10.	ConcurrentSkipListMap
	
	
- 	It provides a scalable and concurrent version of NavigableMap in Java. 
-	Keys in ConcurrentSkipListMap are sorted by default in their natural ordering.
-	ConcurrentSkipListMap is equivalent of TreeMap
-	Provides natural ordering on Keys
-	Concurrent Implementation of TreeMap
-	Writes are rarely blocked and Reads are never Blocked








































