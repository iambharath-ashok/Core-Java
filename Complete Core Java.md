# Complete Core Java


## 1.	JDK

-	JDK Stands for Java Developement Kit
-	JDK comes with Compiler and JRE
	### JRE - Java Runtime Environment

	-	JRE contains JVM and API 
	-	JVM uses JIT Compiler - Just In Time compiler to run the application efficiently 
	-	JRE provides runtime environment for compiled code or byte code to run
	-	JRE is like a duplicate OS or Virtual Machine
	-	JRE interprets the bytecode and converts it to the machine code for the underlying OS

		#### JVM - Java Virtual Machine

		-	In Java, Compiled code will be run on the JVM and directly on the OS


		#### API - Application Programming Interface

		-	Predefined and can use without knowing much background or how its been implemented
		-	Reading and writing files

			-	Java IO Library


	### Compiler

	-	Compiler converts .java source file to .class byte code
	-	Byte code is a binary file and understood by JVM and will be run on the JVM
			
----------------------------------------------------------------------------		
			
## 2.	Java Platform Independent

-	We can't run c program compiled on Windows  to run on Mac OS
-	In java .java file will be coverted to .class file which is a intermediate file by compiler called Bytecode
-	Bytecode is not a machine code for particular OS 
-	Bytecode can be interpreted by Linux JVM for Linux OS .... Windows JVM will interpret the bytecode to Windows OS


-	Platform independent will comes from this additional step
-	JVM uses JIT Compiler to translate the Bytecode to machine code
		
		
#### Java is a platform independent language ... once compiled it can be run on any OS
----------------------------------------------------------------------------
		
## 3. Object Oriented Programming

	
-	Each object has properties and behavior
-	Properties are represented by fields 
-	Behavior is represented by methods or functions

	-	Objects will communicate with each other through methods
	-	Information is exchanged through variables or fields and properties
			
### Java is a object oriented programming language

-	Advantage -> Easy to map real world problems
			
----------------------------------------------------------------------------

##  4.	Principles of Object Oriented Programming

1.	Encapsulation
2.	Abstraction
3.	Polymorphism
4.	Inheritance
		
		
### 1. Encapsulation

-	Encapsulation is about protecting properties and functionalities from other objects
-	Binding together properties and methods together
-	In Java we achieve encapsulation using class

		Ex:	
			
			class { 
				fields
				methods
				blocks
			 }
			

### 2.	Inheritance 

-	Inheritance is a process creating a new object using an existing object
-	New object will inherit the properties and functionalities from existing object and can provide the new functionalities
-	IS- A and Reusability is a terms used to represent inheritance

Ex :

	Vehicle -> Car and Bus 
			Car -> Audi and BWM
			Bus -> Benz and Volvo

##### In Java inheritance will done using extends keyword 
#####  Advn of Inheritance is code reusability			

### 3.	Abstraction 

-	Abstraction is a principle of hiding the unnecessary details of the object from another object 
-	And showing only essential features in-order to communicate with that object


##### In Java we achieve abstraction using an interface


	Ex: 

		-	We just focus on how to use the functionalities or objects 
		-	We dont needs to care how this has been implemented

			TV, Car, Laptop, Pen, Paper,CellPhone



### 4.	Polymorphism

-	Polymorphism is showing different behaviors at point-in time

##### Polymorphism is achieved using method overloading and overriding 

----------------------------------------------------------------------------		
				
##  5.	Building blocks of Java

-	Class
-	Properties
-	Methods
-	Blocks
----------------------------------------------------------------------------			
			
## 6.	Static Members and their Execution Control Flow

		
-	Static - 	Class Level
-	Non Static -	Object Level
		
	
1. Static Blocks

	-	Static Blocks will be executed before main method 
	-	Static Blocks will executed at the time of loading the class to memory

	-	Static blocks will be used to initialize the variables
	-	Static blocks will be Executed from top to bottom and order is imp

	Code Snippet:

	```java
		private static void method1(String name) {
			System.out.println("Static Method 1 calling from" + name);
		}

		static {
			System.out.println("Static Block1");
			method1("Block 1");
		}

		public static void main(String[] args) {
			System.out.println("Main method");
			method1("Main Method");
		}


		static {
			System.out.println("Static Block2");
			method1("Block 2");
		}
	```


2.	Static Variables 

	-	Static Variables are initialized at the time of class loading at first time
	-	Only one copy of Static variable is created per class
			
----------------------------------------------------------------------------
			
## 6.	Non-Static Members and their Execution Control Flow
			
			
1.	Non-static Variables
2.	Non-static Methods
3.	Non-static blocks
4.	Constructor
	
	- 	Instance blocks will get executed whenever a new instance will be created
	-	Instance block will get executed before the constructor
		
	```java
		public class NonStaticMembers {

			private NonStaticMembers() {
				System.out.println("Insid Constructor");
			}

			{
				System.out.println("Inside Instance Block");
			}

			public static void main(String[] args) {
				System.out.println("Inside Main Method");
				System.out.println(staticInt);
				System.out.println(new NonStaticMembers().nonStaticInt);

				for(int i=0 ; i<5; i++ ) {
					new NonStaticMembers();
				}
			}

			private int nonStaticInt;
			private static int staticInt;

		}
	````		
	
Output:

	Inside Main Method
	0
	Inside Instance Block
	Insid Constructor
	0
	Inside Instance Block
	Insid Constructor
	Inside Instance Block
	Insid Constructor
	Inside Instance Block
	Insid Constructor
	Inside Instance Block
	Insid Constructor


##### Difference b/w Static and Non-static Blocks

1. 	Static block will gets executed only once per the class - while loading class to memory
2.	Non-static block will gets executed every time a new object will gets created
			

	-	Object reference in static block
		
		```java
			class SimpleClass {

			}
			public class ObjectReferenceInStaticBlock {

				private SimpleClass scInstance;
				private static SimpleClass scStatic;

				public static void main(String[] args) {
				}

				static {
					SimpleClass sc = new SimpleClass();
					//scInstance = new SimpleClass();  // gives compilation error
					scStatic = new SimpleClass();
					System.out.println(sc);
				}
			}
		````	
		
#### this keyword


-	this keyword is used to refer to the current object that is being invoking
-	this keyword points to current object address
-	When we invoke Constructor using new operator then Object address will be assigned to this keyword

				
				
Code Snippet:

```java
	ExperimentalClass() {
		System.out.println(Constructor: "+ this);
	}

	public static void main(String[] args) {
		ExperimentalClass experimentalClass = new ExperimentalClass();
		System.out.println("Main method : " + experimentalClass);
		experimentalClass.method1();
	}
````

Output:

	Constructor: com.bharath.nonstatic.ExperimentalClass@71be98f5
	com.bharath.nonstatic.ExperimentalClass@71be98f5
	Main method : com.bharath.nonstatic.ExperimentalClass@71be98f5
	Method 1: com.bharath.nonstatic.ExperimentalClass@71be98f5

----------------------------------------------------------------------------					
			
## 6.	Static vs Non-Static Members

	
### Static 

-	Belongs to Classes
-	Accessed using Class name
-	Static blocks are executed at the time of Class loading
-	Memory is allocated and initialized at the time of class loading

### Non-Static

-	Belongs to Instances
-	Accessed via Instance name
-	Blocks are executed at the time of object creation
-	Memory is allocated and initialized at the time of Object creation

			
----------------------------------------------------------------------------


## 7.	Data Type

	
1. Primitive Data Types

	-	byte

		-	1 byte = 8 bits = 1 1 1 1 1 1 1 1
		-	2^8 = 256 = 256/2 = -128 to +127

		- 	
			byte b= 120;
			byte a = 12;

			int i = a + b;

		- 	Always assign the bytes sum to int			

	-	short

		-	2 bytes
	-	int 

		-	4 bytes
	- 	long

		-	8 bytes

	-	boolean

		-	2 bit

	- 	float

		-	4 bytes

	-	double

		- 	8 bytes

	-	char

		-	2 bytes




2.	Type Casting


	1.	Primitive Type Casting 

		-	Implicit Up-casting

			-	Assigning lower data type to higher data type
			-	Lower -> Higher
			-	Will be handled implicitly by Compiler
			-	Ex: 
					1.	Byte to Int
					2.	Int to Long 

		-	Explicit down-casting

			-	Assigning higher Data type to lower data type
			-	Higher -> Lower
			-	Needs to handled by Developer manually - by casting
			-	Ex:

					1.	Int to Byte
					2. 	Long to Int

						static int i = (int) 99999999l;

	2.	Reference (Object) Type-casting


		- Implicate Up-casting

			-	Assigning Child class instance to parent class reference
			-	Child -> Parent

		-	Explicit Down-casting

			-	Parent class instance to Child Class
			-	Parent -> Child
			-	Down-casting needs to done explicitly

			-	Ex:

				int i = (int)999999l;
				byte b = (byte) 128; // Output -127 
				//byte b = 129---> Compilation Error can't convert from int to byte
	
----------------------------------------------------------------------------

## 8.	Wrapper Classes with  AutoBoxing and unboxing
	
-	Wrapper Classes are used to convert primitive types to Object types
-	Wrapper Classes are mainly required when we are working with Collection API	

	-	Each primitive type in Java has corresponding Wrapper class
		
		
			Primitive Type 						   Wrapper Class
		   -------------------------------------------------------------------------------
			 byte								Byte
			 short								Short
			 int								Integer
			 long								Long
			 float								Float
			 double								Double
			 char								Character
			 boolean							Boolean
			
			
1.	Boxing 	-> Converting primitive type to Object type
2.	Un-boxing ->	Converting Object type to primitive type

Code Snippet : 	

--------------------------
	1.  Integer
		int i = 10;
		Integer integer = Integer.valueOf(i); //Boxing
		i = integer; //Un-Boxing
		i = integer.intValue(); //Un-Boxing
		
--------------------------		
	2.  Short 
		short s = 200;
		Short sh1 = Short.valueOf(s); // Short short = Short.vauleOf(s); ---> Gives Compilation Error ... since short is a reserved keyword
		s = shortValue.shortValue();
		
--------------------------
	3.  String and Primitives

		long l = 20000000;
		String longString = Long.toString(l); // primitive to String
		l = longString.parseLong(longString); // String to Primitive
		
---------------------------		
	4.  Wrapper Class Constructors
	
	-	Each Wrapper classes provided overloaded constructors
	-	One takes the primitive type and another as string as the argument to Wrapper class constructor
		
	Ex: 

		double d = 2999.553;
		Double dd = new Double(d);

		String s = "67584493.4232";
		Double dString = new Double(s);

----------------------------------------------------------------------------			
			
## 9.	Operators and Assignments

1.	Unary Operators	- ++, --

	-	works on single operand
	-	Increment (++) and  Decrement (--)

		-	y = x++ - PostIncrement
		-	y = ++x - PreIncrement

		-	y = x-- - PostDecryment
		-	y = --x - PreDecryment


2.	Arithmetic Operators

	- 	Binary operators multi , +, -, /, % 


3.  String concatination - + 

	-	Only operator that overloaded in Java is the + 
	-	When used + operator with integer then it adds the numbers
	-	When used + operator with String it will appends the strings

		Ex:

			int i = 30 + 43 = 73 
			String newString = abc + xyz = abcxyz


4.	Relational Operators - <= , < , >, =>


	-	Comparison Operators <= , < , >, => 
		-	Will be uses only on Primitive types

	-	Equality Operators ==, !=

		-	Will used for both Primitives and Objects 
		-	If we used equality operators for Objects types then if verifies whether both objects are referring to same memory locations

			String s = "someString";
			String s2 = "someString";

			s1 == s2 // true

				##### Equality operator "==" checks whether both references points to same memory locations


5.	Bitwise Operators - &, | , ^

	-	&, |, ^ are the Bitwise operators


	- 	& --> returns true if both arguments are true
	-	| --> returns false if either one of the arguments are true
	-	^ --> returns true if both are arguments are different



		Code Snippet :

					System.out.println(true & true);// true
					System.out.println(true & false); //false
					System.out.println(true | false);// true
					System.out.println(false | false);// false


					System.out.println(true ^ true);//false
					System.out.println(false ^ false);//false

					System.out.println(false ^ true);//true


					System.out.println(4 & 5);//4 100 & 101 = 100
					System.out.println(4 | 5);//5 100 | 101 = 101
					System.out.println(4 ^ 5);//1 100 ^ 101 = 001 


6.	Short Circuit Operators	- &&, ||

	-	&&, || are the Short Circuit Operators
	-	Main advantage of Short Circuit Operators are they increase the performance
	-	Second argument is optional

		-	If either one of the operand values matches the criteria then it not evaluates the whole expression


7.	Assignment Operators - =

	-	Used to assign the values and reference of objects 

8.	Ternary Operators ? :

	-	Test Expression ? value 1 : value 2

----------------------------------------------------------------------------
		
	
## 9.	Flow Control Statement


1.	Selection Statements

	-	if-else
	-	switch

2.	Iteration Statements

	-	while
	- 	do-while
	- 	for
	-	for-each

3.	Transfer Statements

	-	break
	- 	continue
	-	return
	-	try-catch-finally
	- 	assert
			
			
#### Labelled Blocks and Break
			
```java			
	main() {
		l1 : {
			System.out.println("Block Begins");
			if(x == 20) {
				break l1; // Comes out of the l1 block 
				//	break can be used switch and looping blocks
			}
		}
	}
````					
----------------------------------------------------------------------------


## 10. Access Modifiers

-	Applicable for - Class, Methods, Constructors, Variables
-	Private, Protected, Package, Public
-	Access modifiers can't be used with blocks ... because blocks are executed by JVM 
-	If no access specifier is specified then its by default will package level

	
-	Classes

	-	Classes can only have Public and Package
	-	Classes can't mark with private ... because application or any other class can't access the private class
	-	Protected is used in inheritance ... used with methods and variables


```java
	package p1;									

		class A {
			private int a;
					int b;
			protected int c;
			public int d;
		}

	package p1;

		class B {

			main() {
				A a = new A();
				a.a; // Not possible // error
				a.b;// possible
				a.c; //possible
				a.d;// possible
			}
		}

	package p2;

		class C extends A {

			main() {
				A a = new A();
				a.a; //Not possible //private error
				a.b; //Not possible // package level error
				a.c; //Not possible // protected error
				a.d;// possible

				C c = new C();
				c.a; // Not Possible
				c.b; //Not possible
				c.c; // Possible --> inherited to C and able to access
				c.d; // Possible 
			}
		}
````


-	Private 

	-	Can be accessed by only with in the class

-	Package or default

	-	Can be accessed within the class and in its package

-	Protected

	-	Can be accessed in class and package and inherited class
	-	Can't be access to the protected member of the parent class by creating the Parent Object

##### Can only accessed in the inherited class by creating the child class instance

-	public 

-	available publicly 
		
	
----------------------------------------------------------------------------	
	
## 10. Packages

	
-	Packages are the folders used to place the related java files together
-	Packages can have sub packages 
	
	
----------------------------------------------------------------------------


## 11. Event Management Use Case

-	Entities

	-	Organizer
	-	Event
	-	Participants
	-	Venue

----------------------------------------------------------------------------		
	
## 12. Inheritance

		
1.	Single Inheritance
2.	Multi-Level Inheritance
3.	Hierarchical Inheritance
4.	Method Overloading
5.	Super Keyword
6.	super() method
7.	Constructor Chaining
	
----------------------------------------------------------------------------
1.  Single Inheritance 

	-  Child Class Inheriting from Single Parent Class
	-  toString and hashCode methods are inherited from object class
	-  SingleInheritance Class inherits from java.lang.Object Class

	```java	
		public class SingleInheritance {
			void method1() {
				System.out.print("Method 1");
			}
			public static void main(String[] args) {
				SingleInheritance si = new SingleInheritance();
				si.method1();
				si.toString();
				si.hashCode();
			}
		}
	````	
2.  Multi-Level Inheritance

	-  Inheritance by multiple level

	```java	
		public class Parent {
			Parent() {
				System.out.println("Parent Constructor " + this);
			}
			void parentMethod() {
				System.out.println("Parent Method");
			}
		}
		public class Child extends Parent {
			Child() {
				System.out.println("Child Constructor "+this);
			}
			void childMethod() {
				System.out.println("Child Method");
			}
		}
		public class InheritanceTest {
			public static void main(String[] args) {
				Child c = new Child();
				c.parentMethod();
				c.childMethod();
			}
		}
	````	

3.  Memory Allocation and Inheritance

	-  Two instances are created - one for parent and child 
	-  Both Child and Parent Instances share the same memory location

#### Output for the above Program :

		*Parent Constructor* com.bharath.inheritance.*Child@71be98f5*
		*Child Constructor* com.bharath.inheritance.*Child@71be98f5*
		Parent Method
		Child Method

4.  Hierarchical Inheritance

	-  Inheritance by Hierarchy and at several level

	```java

		public class Vehicle {
			String fuel() {
				return "petrol";
			}
		}
		public class Bike extends Vehicle {

		}
		public class Bus extends Vehicle {
			@Override
			String fuel() {
				return "CNG";
			}
		}
		public class Car extends Vehicle{
			String fuel(){
				return "Disel";
			}
		}

	````	
5.  Method Overriding

	-  fuel method has been overridden in the above examples

6.  super Keyword 

	-  super keyword is used to access the parent class members

	```java	

		public class Child extends Parent {
			Child() {
				System.out.println("Child Constructor "+this);
			}
			void childMethod() {
				*super.parentMethod();*
				System.out.println("Child Method");
			}
		}

	````
7.  super() method

	-  super() is used in the constructor of child class to invoke the parent class constructor explicitly
	-  super() can also be used for constructor chaining


8.  Constructor Chaining

	```java

		public class JDK6 {
			JDK6() {
				super();
				System.out.println("JDK6");
			}
		}
		public class JDK7 extends JDK6 {
			JDK7() {
				super();
				System.out.println("JDK7");
			}
		}
		public class JDK8 extends JDK7 {
			JDK8(){
				super();
				System.out.println("JDK8");
			}
		}

	````	

----------------------------------------------------------------------------


## 13. Abstraction

	
-	Abstraction is a process of hiding the implementation details of the object from the object thats using that object
-	Using Object should know how to use the object's functionality and should not worry about its implementation
	
1. Abstract Class

	-	In Java, Abstraction is achieved through Abstract class and Interface
	-	Abstract is partial abstraction and interface is complete abstract

	-	We cant create an instance of Abstract Class

	-	Abstract class can have main method and will be to run the Abstract class main method

	####	Abstract class is mainly used to achieve the Runtime Polymorphism and loose coupling
	####	abstract keyword can't used with static and final as combination... compiler will give the error

		Code Snippet: 

				public abstract class AbstractClass {
					public abstract void method();
					public String method1() {
						return "value";
					}
					public static void main(String... args) {
						System.out.println("Inside Main Method");
					}
				}

		Output:

			-	Inside Main Method

2.	Interface

	-	Interface in Java is used to achieve loose coupling and runtime polymorphism
	-	Interface is a specification or an idea that represents the functionalities


3.	Interface Vs Abstract Class


	Interface 
		-	methods are by default public abstract
		-	variable are by default public static final
		-	Interface can have only abstract and default methods

			-	default methods in interface will have concrete implementation

		-	From Java 8, multiple inheritance with interface is not supported if two interface has same default method signature
		-	Or if child interface or class doesn't provide its own impl at its level
		- 	Interface in java cant have constructor and hence cant create an instance of an interface

	Abstract Class

		-	Abstract class is marked with abstract keyword
		-	abstract methods needs to be marked with abstract keyword
		-	Abstract class can have both concrete and abstract methods
		-	Abstract class can have constructors
		-	Abstract can have main method and can run as java program


4.	final Keyword

	-	final keyword can be used at Class, Method and Variables level

		1.	final Class 
			-	Class marked with final cant be inherited

		2.	final Variables 

			-	Variables can be initialized at only once and at beginning

		3.	final Methods

			-	final Methods can't be inherited and overridden



5.	Marker Interface

	-	Marker Interface are the interface that doesn't have any methods
	-	By implementing marker interface classes will have special ability 

		-	Cloneable 
		-	Serializable
		-	Randoms access
				
----------------------------------------------------------------------------					
	
## 14. Polymorphism

	
	
	-	Polymorphism is a principle of showing different behavior at different stage or level
	-	An object showing different behaviors for communicating objects then its a polymorphism
	
	
		- 	There are two types of polymorphism 
		
			1. 	Compile-Time or Static Binding
			2.	Runtime or Dynamic Binding
			
			
			1. 	Compile-Time or Static Binding

				-	Static Binding is achieved through *method overloading*
				-	Compiler selects or link which specific method needs to invoke at compile time
				-	In compile time polymorphism method that needs to invoke or link will be done based on method signature
				
				
					sum(int a, int b);
					sum(float a, float b);
					sum(long a, long b);					
			
			
			2.	Runtime or Dynamic Binding
				
				-	Runtime polymorphism is achieved through *method overriding*
				-	In Runtime polymorphism child class instance will assign to Parent Class variable and invoking the child class implementation with parent class reference
				
						
						interface MacBook {
							void start();
							void stop();
						}
						
						public class MacBookPro  implements MacBook {
							void start(){}
							void stop() {}
						}
						
						public class MacBookAir  implements MacBook {
							void start(){}
							void stop() {}
						}
						
						
						MacBook macBook = new MacBookPro();
						macBook.start();
						macBook.stop()
						
						MacBook macBook = new MacBookAir();
						macBook.start();
						macBook.stop();
						
----------------------------------------------------------------------------				
				
## 15. Encapsulation


	-	Encapsulation is a process of binding the properties and methods together 
	-	Encapsulation is a process of protecting the fields and functionalities from other objects
	
	-	Advantage of Encapsulation is security and maintainability
	-	Encapsulation is data binding and abstraction
	
	-	Encapsulation is achieved by making the fields private and providing the setters methods to set the values for the fields
		
		-	using setter methods we can provide validation on the values of the fields
		
		
		public class Customer {
			private String name;
			
			public void setName(String name){
				if(name == null) {
					throw new NullPointerException();
				} 
				this.name = name;
			}
			
			public String getName(){
				return this.name;
			}
		}
			
----------------------------------------------------------------------------	
	
## 16. Exceptions

	1. Types of Errors
		
		1.	Compile Time Error
		
			-	Type Incompatible Errors
			-	Static Context Error
			-	Invalid method error and params type error
			
		2.	Logical Error
			
			- 
			
		3.	Runtime Error
			
			-	NullPointerException
			-	ArrayIndexOutOfBoundException
			-	NumberFormatException
			-	Improper shutdown of resources like DB etc
			
	 
	2.	Types of Exceptions
		
		1.	Compile time Exceptions or Checked Exception
		2.	Runtime Exception	or Unchecked Exception
		
		
			1.	Compile Time or Checked Exception
			
				-	Compile exceptions are exceptions that needs to be handled at compile time
				-	Compile time exceptions can be handled by throws keyword or by surrounding with try-catch-finally block
				-	Custom Checked exceptions are created by extending with Exception class - it needs to handled at compile time
			
			2.	Runtime Exception or Unchecked Exceptions
			
				-	Runtime Exception are exceptions that are thrown at runtime
				-	Needs to be handled at runtime either by throwing or surrounding with try-catch-finally
				
				
	3.	Java Exception Hierarchy	
	
		-	Throwable is the parent class of both Error and Exception
		-	Throwable has child classes Error and Exception
		
		
		-	Throwable
			
			-	Error
				
				-	OutOfMemoryError
				-	NoClassDefFoundError
				-	NoSuchMethodError
				-	VirtualMachineError
				-	StackOverFlowError
								
				
			-	Exception
				
				-	IOException
					
					-	FileNotFoundException
					
				-	RuntimeException
				
					-	ClassNotFoundException
					-	NullPointerException
					-	ArrayIndexOutOfBoundException
					-	DivideByZeroException
			
				-	SQLException
							
	
		4.	Handling Exceptions
		
			-	Exception can be handled by using throws, throw, try-catch-finally blocks
			
		5.	throw
		
			-	throw keyword is used to throw Exception Explicitly
			-	using throw we can throw Checked or RuntimeException 
			-	if throw is used to throw Checked Exception then it needs to surround with try-catch or throws keyword
		
		6.	throws
		
			-	throws keyword mainly used to make the calling method to handle the exception
			-	throws keyword is used mark that method may throw Checked Exception
			-	throws keyword is used to handle checked exceptions
			-	throws keyword is used on method so that user can handle exception better at compile time
			
		
		7.	Try-catch-finally
		
			-	try block is used to write code that may throw exceptions
			-	if an exception occurred then it can handled in the catch block
			
			-	catch block will gets executed only if there is a exception 
			-	catch block is not mandatory block - we can skip the catch
			
			
			-	finally will be used to close any resource intensive objects
			
				-	finally will be executed irrespective of exception occurred or not in the try block
				-	finally block get executed always
				-	all the resource closing statements
				
			-	try-catch-finally can be used handled both compile and runtime exceptions

----------------------------------------------------------------------------

## Threads

	1. 	Creating Threads in Java
	
		-	Threads in Java can be created in two ways 
			
			1.	By extending Thread class
			2.	By implementing Runnable Interface
			
		-	Implementation Thread class needs to provide an implementation by defining a method
		
		
			class Thread1 extends Thread {
				
				@Override
				public void run() {
					
				}
			}
				
			public class Test{
				
				public static void main(String ... args) {
					Thread1 t1 = new Thread1();
					t1.start();
				}
			} 	

	2.	Thread.sleep(millis)
	
		-	Thread.sleep() is a static method used to send the thread in sleeping mode for specified amount of time
		-	sleep method is used to make processor time for other threads 
		-	sleep is used to increase the performance
		
			-	Reading the data from webservice every second can slow down the application
			-	Instead we can read this periodically ... when the data is available 
		
	3.	join()
	
	
		-	join() method is used to make sure that thread on which join is invoked will complete its execution and enter to dead state
			
			-	Until that JVM will make sure that other threads will not able to execute the below line of code
		
		-	join() method make sure that other threads will not start executing below lines until join() invoked thread enters dead state
		-	join() is a instance method	 from java.lang.Thread Class
		
				public class ThreadJoinDemo {

					static int sum, num;

					public static void main(String[] args) throws InterruptedException {
						System.out.println("Sum of first N numbers ");
						System.out.println("Enter the Number");
						Scanner s = new Scanner(System.in);

						ThreadJoinDemo.num = s.nextInt();
						
						SumThread st = new SumThread(ThreadJoinDemo.num);
						st.start();
						
						MultiplyThread mt = new MultiplyThread(ThreadJoinDemo.num);
						mt.start();
						
						st.join();
						mt.join();
						
						System.out.println("===========Sum of "+ThreadJoinDemo.num +" is : "+st.sumResult);
						System.out.println("=============Multi of "+ThreadJoinDemo.num +" is : "+mt.mulResult);
						System.out.println("==================Main method ended====================");
					}
				}
				
				public class SumThread extends Thread {
					int num;
					int sumResult;
					SumThread(int num) {
						this.num = num;
					}
					public void run()  {
						Thread currentThread = Thread.currentThread();
						currentThread.setName("Sum Thread");
						currentThread.setPriority(MIN_PRIORITY);
						System.out.println(Thread.currentThread().getName() + " Caluculating Sum. ");

						for (int i = 0; i < num; i++) {
							sumResult += i;
							System.out.println("Caluculating Sum of "+ i+ " is "+ sumResult);
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
					}
				}
				
				public class MultiplyThread extends Thread {
					int num;
					int mulResult = 1;
					MultiplyThread(int num) {
						this.num = num;
					}
					public void run()  {
						Thread currentThread = Thread.currentThread();
						currentThread.setName("Multiplication Thread");
						currentThread.setPriority(MIN_PRIORITY);
						System.out.println(Thread.currentThread().getName() + " Caluculating Multiplication. ");


						for (int i = 1; i <= num; i++) {
							mulResult *= i*;
							System.out.println("Caluculating Multiplication of "+ i+ " is "+ mulResult);
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
					}
				}

 	4.	Thread Identity
	
		-	Each thread will by default will have some names like Thread-0, Thread-1, Thread-2
		-	We can change the threads explicitly 
		
		
				Thread currentThread = Thread.getCurrentThread();
				currentThread.setName("Some Name");

	5.	Thread Priority
	
		-	Thread Priority is used to set priority in which certain threads needs to execute in the Priority
		-	1 is the Min Priority and 10 is the Highest Priority
		
	
	6.	Runnable Interface
	
		-	RunnableInterface is a functional interface from Java 8
		-	RunnableInterface has only one method run 
		####  -	We can use LambdaExperssion , Method Reference, Anonymous Inner Class as impl to Runnable reference
	
	
		class RunnableThread1 implements Runnable {
			@Override
			public void run() {
			}
		 }
		
		class Test {
			void main() {
				RunnableThread1 rt = new RunnableThread1(); // Impl runnable interface
				RunnableThread1 rt = () -> {
				}; // LambdaExperssion
				RunnableThread1 rt = RunnableThread1::run;
				##### Thread t = new Thread(rt); // We needs to create new Thread and pass RunnableInterface Impl as param to Thread
			}
		}

	7.	yield() method
	
		-	yield() methods will yield for another Thread
		-	yield means letting another thread to continue execution 
		-	yield() is a static method in Thread class
		-	once control come to run() method of Thread it will yield so that main will complete execution first
			
			class Thread1 implements Runnable {
				@Override
				public void run() {
					for(int i=0;i<=100;i++){
						System.out.println(Thread.currentThread().getName());
						Thread.yield();
					}
				}
			}
			
			public class TestYield {
			
				main() {
					
					Runnable r = new Thread1();
					Thread t = new Thread(r);
					t.start();
					
					for(int i=0;i<=100;i++){
						System.out.println(Thread.currentThread().getName());
					}
				}
			}


	8.	interrupt() method
	
		-	interrupt() method is used to interrupt or kill the thread
		-	interrupt will stop thread immediately 
		-	Code below interrupt() call will continue to execute
		-	interrupt() method is from java.lang.Thread Class
		
		
		Code Snippet :
			
			class Thread1 implements Runnable {
				public void run() {
					for(int i=0; i<10;i++) {
						System.out.println("Executing Thread " + Thread.currentThread().getName());
						try{
							Thread.sleep(10000);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
						
					}
				}
			}
			
			public class TestInterrupt {
							main() {
					Runnable r = new Thread1();
					Thread t = new Thread(r);
					t.start();
					
					t.interrupt(); // Interrupting Thread by called interrupt on the thread instance
					
					System.out.println("Main Method has ended");
				}
			}


	9.	Synchronization

		-	When multiple Threads working on same object simultaneously ... there might me chances that each others data got corrupted
			
			-	Thread dirty reading 
			
		-	Synchronization 
			
			-	Is used to make sure that only Thread can execute that particular method at a time
			-	Only one Thread holding the lock at a time
			-	Method marked with synchronize will be accessed by only one thread at  time
			-	First Thread that access the method will acquire a lock on the object
			-	Acquiring and releasing Lock will handled by JVM
			-	Other threads trying to acquire lock will go to waiting state
			-	Synchronization is done at object level and not at method level
			
		-	Locks

			-	synchronized instance method
			-	static method
			-	instance
			-	static synchronized method
		
		
		Code Snippet :
			
			class Booking {
				
				Payment p;
			
				Booking() {}
				
				public synchronize void bookTicket(String name) {
					System.out.println("Booking for user "+ name);
					p.makePayment();
					Thread.sleep(4000);
				}
			}
		
			class AndroidUser implements Runnable {
				Booking booking;
				AndroidUser(Booking booking) {
					this.booking = booking;
				}
				public void run() {
					this.booking.bookTicket("RailwayAdmin");
				}
			}
			
			class RailwayAdmin implements Runnable {
				Booking booking;
				RailwayAdmin(Booking booking) {
					this.booking = booking;
				}
				public void run() {
					this.booking.bookTicket("RailwayAdmin");
				}
			}
			
		
			public class TestSynchronize {
				main() {
					Booking booking = new Booking();
					
					Runnable user1 = new AndroidUser(booking);
					Runnable user2 = new RailwayAdmin(booking);
					Runnable user3 = new RailwayAdmin(booking);
					
					Thread t1 = new Thread(user1);
					Thread t2 = new Thread(user2);
					Thread t3 = new Thread(user3);
					
					t1.start();
					t2.start();
					t3.start();
				}
			}
			
	10.	Class Level Lock


		-	If thread want to execute static synchronized method it will first gets a Class Level Lock
		-	Once Thread has Class Level Lock then ... all other threads can't execute static synchronized methods
		
		- 	But other threads can still execute instance and static non-synchronized methods and synchronized instance methods
		
	
	11.	Synchronized Block
	
		-	Synchronized block is used when we want few lines of code to synchronize instead of making whole method as synchronize
		-	Multiple threads can enter the method but only one thread can execute synchronized block at a time
		-	synchronized block will increase the performance
		
		
		Types of Synchronized Blocks
			
			-	synchronized blocks can be defined in 3 ways
			
			method() {
				
				synchronize(this) {} // Instance Level Lock
				
				synchronize(any other object){} // Object Level Lock
				
				synchronize(Booking.class) {} // Class level lock
				
			}
		
	12.	InterThread Communication
	
	
		-	wait(), notify(), notifyAll() all method used for InterThread Communication
		-	above methods are available from java.lang.Object class and available to all the class
		
		-	Invoking wait() method from Main Thread will make Main Thread to wait for Child thread to complete its execution
		-	Child Thread once complete its execution should notify the Main Thread to continue its execution
			
			-	Child Thread will notify main thread using notify() method
				
			
			class SumThread implements Runnable {
				int sum;
				public void run() {
					synchronize {
						for (int i=0; i < 100; i++) {
							sum+=i;
						}
						this.notify();
					}
				}
			}
		
			public class ThreadCommunicationTest {
				main() {
					SumThread st = new SumThread();
					st.start();
					synchronize{
						try{
							st.wait();
							System.out.println("Notified Main Thread");
							System.out.println("Sum of numbers is "+ st.sum);
						} catch(InterruptedException e) {
							e.printStackTrace();
						}
					}
				}
			}
		
		
			Execution Flow of above program :
			
			
				1.	Main Thread will be created by JVM
				2.	Main Thread will create a Child Thread and start the child Thread
				3.	Main thread will gets a lock on the instance an SumThread st and invokes wait() method on the Main Thread
				4.	So that main thread will go for waiting state
				5.	Child Thread in the mean time will get a lock on its own object 
				6.	Will calculate sum and notifies Main Thread by invoking notify() method
				7.	notify() will release the lock and invokes the waiting thread
				7.	Main Thread will get notified and continue its rest of the execution
				
				
				Note: 
					
					-	wait(), notify(), notifyAll() methods should be executed in synchronized context 
					-	Otherwise we will get IllegalMonitarStateException
				
----------------------------------------------------------------------------				
				
## Executor Service


	1. Limitations of using Threads in real-time Scenarios and managing thread life-cycle by ourselfs
	
	
		1.	Time Consuming
		2.	Poor Resource Management
		3.	Application is not Robust
		
	
	2. Java Executor Framework

	-	Executor Framework Introduced in Java 1.5 overcomes traditional approach of creating and using Threads
	-	Executor Provides a Pool of Thread called - Thread Pool
	-	Once we submit task ... one of the Thread from Thread pool will pickup the task ... executes and Thread goes back to Thread pool instead of dying ... so that Threads can be reused in Future
	-	Executor Framework will manage the life-cycle of the of Thread
		
		
		Steps to ExecutorService 
		
			1.	Create a instance of ExecutorService with specific type of Thread Pool
				
				- Executors Class provides factory methods that provides implementation of ExecutorService
				
			2.	Create a Thread and needs to perform actual Task
			3.	Assign Thread task to ExecutorMethod
			
				Executor e = ExecutorService.newCachedThreadPool();
				Runnable task = new CheckProcessor();
				e.execute(task);
				
		Advantages of ExecutorService:
		
			1.	Time Consuming
				
				-	No more Time-Consuming because we have pool of Threads waiting to process the Incoming tasks
			
			2.	Poor Resource Management
				
				-	We can limit the Number of Threads that can be created by providing the upper bound
				-	Based on the volume we can use the number of Threads
				-	No excess Threads will created ... so that system may not crash
				
			3.	More Robust
				
				-	System will not crash and as there is a limit on the Number of Threads that can be created
				-	100 Threads can handle millions of Transactions
				
			
		
		
		
	3.	Code Snippet for ExecutorService of CheckProcessor Use Case
		
		
					class ChechProcessor implements Runnable {
					
						String name;
						ChechProcessor(String name) {
							this.name = name;
						}
						public void run() {
						
							System.out.println(name + " Check Processor has began processing the check");
							
							try{
								Thread.sleep(3000);
							} catch(InterruptedException e){
							}
							
							System.out.println(name+ " Check Processor Has Completed execution")
							
						}
					}
					
					public class ExecutorTest {
					
						main() {
						
							CheckProcessor[] checkProcessors = { new CheckProcessor("ATM"), new CheckProcessor("Bank"), new CheckProcessor("Mobile"), new CheckProcessor("Web")};
						
							ExecutorService es =  ExecutorService.newFixedThreadPool(2);
							
							for(CheckProcessor checkProcessor : checkProcessors) {
								es.submit(checkProcessor);
							}
							
							es.shutdown();
						}
					}
		
	4.	Callable and Future
		
		1. Callable Interface
		
			-	Callable and Future are two features or interfaces in Executor Framework that powerful and useful
			
				Runnable interface can't return any value - return type is void
				
				To return value of task we need to use Callabe<V> interface
					
				
				Runnable - void run()
				
				Callable<V> -	V call()
				
				
			-	Callable interface is a Generic interface we can provide what type of value we want to return
			-	We need provide an implementation for Callable call method and needs to submit that Callable task to ExecutorService
			-	ExecutorService will return a Future instance  containing value
			
		2.	Future Interface
			
			-	Future Instance will returned by Executor Service
			-	Future Interface will methods using which we can extract the values
		
		
		3. Code Snippet and Output
		
			class SumProcessor implements Callable<Integer> {
				int num = 0;
				SumProcessor(int num) {
					this.num = num;
				}
				public Integer call() {
					System.out.println(Thread.currentThread().getName() + " is Calculation sum of " + this.num);
					int sum =0;
					for (int i = 0; i <=this.num; i++) {
						sum += i;
					}
					return sum;
				}
			}

			public class CallabelSumProcessorTest {
				public static void main(String[] args) {
					SumProcessor [] callables = {new SumProcessor(20), new SumProcessor(100), new SumProcessor(60), new SumProcessor(10)};
					ExecutorService es = Executors.newFixedThreadPool(2);
					for(SumProcessor sp : callables) {
						Future<Integer> future = es.submit(sp);
						try {
							Integer integer = future.get();
							System.out.println("Sum of "+sp.num +" is  "+integer);
						} catch (InterruptedException e) {
							e.printStackTrace();
						} catch (ExecutionException e) {
							e.printStackTrace();
						}
					}
					es.shutdown();
				}
			}

----------------------------------------------------------------------------			
		
## Garbage Collection
	
	
1.	In Java, each threads will have its own Stack Space and Heap Space
2.	In Stack space local primitive types are stored 
3.	In Heap Space ... objects are allocated memory and reference from Stack Space will point to that Memory on the Heap Space
	
###	Garbage Collection is a process in which JVM will automatically clears them memory for unreachable objects from the Heap Space
	
-	Garbage Collection is done by Garbage Collector
-	Garbage Collector is a daemon thread that runs within JVM in background
-	We cant force Garbage Collector to Clean the Heap Space 
-	We can only request Garbage Collector to Clean Heap Space by calling System.gc() method


#### Code Snippet For Garbage Collector 
		
	public class GarbageCollectorTest {

		GarbageCollectorTest() {
			System.out.println("Creating Instance through Constructor");
		}

		public static void main(String[] args) {

			for (int i = 0; i < 200000; i++) {
				new GarbageCollectorTest();
				new GarbageCollectorTest();
			}
		}

		@Override
		protected void finalize() {

			System.out.println("Executing Finalize Method");
			System.gc();
		}
	}
----------------------------------------------------------------------------

## Inner Classes

				
1.	Static Inner Classes with Static Members
2.	Static Inner Classes with Non-static Members
3.	Non-Static Inner Classes
4.	Accessing Outer Class Members
5.	Local Inner Class 
6.	Anonymous Inner Class
7.	Anonymous Runnable Class

		
	---------------------------
	-	In java we can define 4 types of inner class

		1.	Instance Inner Class
		2.	Static Inner Class
		3.	Local Inner Class
		4.	Anonymous Inner class - declared and defined at same place
		
		
----------------------------------------------------------------------------		
		
## String Handling


### 1.	Different ways to create String 

-	An  object of String can be created in 2 ways
-	String and Wrapper class has overridden Object class toString method  ... so that it will print the object content not the object address with has code value

	1.	Assigning String Literal
	2.	Using new operator with String Overloaded Constructors
		

			```java
			
					String s1 = "Bharath";// Will be created String constant pool
					
					String s2 = new String("Bharath"); // Will be created in Heap Area
									
					char [] chars = { 'a', 'b', 'c' }; 
					String s3 = new String(chars); // Will be created in Heap Area
					
					byte [] bytes = { 63, 64, 65 };
					String s4 = new String(bytes); // Will be created in Heap Area
			`````
			
	3.	String Pooling
	
		-	String pool is a special area on the Heap Area
		-	Reuse String values in the application 
		

			-	String is immutable
			
				-	Whenever we tries to assign a new value to String reference it will not reuse existing memory or doesn't remove the previous value
				-	Instead it will create a new String with another memory location and make reference point to that location
				
			-	String is Thread Safe
			
				-	When Thread wants to change the value it will be created with new location 
				-  	No dirty reads will made as each thread will point to two different string values
				
			-----------------------
			Advantages of String Immutability is :
			
				1.	Performance 
				
					-	JVM will reuse the existing constants from the String Constant pool
				
				2.	Thread Safe
				
					-	Multiple Threads can work with String 
					-	Threads updating value will point new different location
					
		-	String Pool Proof


			public class StringPooling {
				main() {
					String a = "xyz";
					String b = "xyz";
					String c = "xyz";
					String d = new String("xyz");
					
					System.out.println(a.hashCode());
					System.out.println(b.hashCode());
					System.out.println(c.hashCode());
					
					System.out.println(System.identityHashCode(a));
					System.out.println(System.identityHashCode(c));
					System.out.println(System.identityHashCode(d));
					System.out.println(System.identityHashCode(e));
				}
			}
			
			Output :
				45689
				45689
				45689
				
	4.	String Comparison and Object Comparison
		
		
			-	== operator will check for object memory location
			-	equals method in String checks for String content
			-	== operation on objects uses Object Class equals() method - Object Class equals() method compares Objects with == operator as its implementation
	
	5. String Class Methods
	
	
		- Instance Methods
		
			1.	length() - 	Number of Character in String
			2.	indexOf('Characther') - Returns Position of that character in the string
			3.	charAt(3) - Returns the character at that location
			4. 	substring(Beginning Index, Ending Index) - substring(2) or substring(2, 6)
			5.	split(" ") - Split the sentence with delimiter and returns String Array
			6.	replace('Character To Be Replaced','Newly Replacing Char') - Replaces existing Chars in the String with new Chars
			7. 	toUpperCase()
			8.	toLowerCase()
			
			
		String Class doesn't have append method as it's a immutable 
	
	
	6.	StringBuffer and StringBuilder
	
		-	StringBuffer is mutable -  We can change the values of StringBuffer
		-	When we append the another String or StringBuffer to StringBuffer
		-	Initial capacity of StringBuffer is 16 chars
		
			StringBuffer sb = new StringBuffer();
				
			sb.append("All Power is with in You");
			sb.append("You can do Anything or Everything");
			
			sb.reverse(); // Reverses the given String
			 
			sb.capacity();  
			sb.charAt(10);
			
			sb.insert();
			
			sb.delete('Starting Index','Ending Index')
					


	7. StringBuffer vs StringBuilder
		
		1.	Similarities
		
			-	Both StringBuffer and StringBuilder is mutable
			
		2.	StringBuffer 
		
			-	StringBuffer is thread Safe - multiple threads can work on this without any issues
			-	StringBuffer is less efficient and consume more time than StringBuilder
			-	StringBuffer should be used -> when we need mutable and working with Multiple Threads
			
		3.	StringBuilder
		
			-	StringBuilder is not Thread Safe - Multiple Threads can't work on StringBuilder
			-	StringBuilder is faster than StringBuffer
			-	StringBuilder should be used -> when we need mutable and working with Single Thread
			
	

----------------------------------------------------------------------------		
		
## IO Streams

	
-	Stream is a logical handler of DATA from Input Source to Output Source
-	Input Source is used to Read Data and Output Source is used to Write Data
-	Server will use Output Stream to send data and Browser will will use Input Stream to receive the Data

	
### Java Supports 4 Types of Streams

1. 	Byte Streams

-	Reads and write 1 byte at a time
-	Byte Streams are used to read and write binary data

2.	Character Streams
	
-	Character streams uses Unicode to write and read data
-	Character Streams Reads and Writes 1 character at a time
-	Character are represented in Unicode in Java
-	Character Streams will read and write 2 bytes at a time
-	Using unicode we can read and write any language in Java
-	Character Streams will be used when we needs deals to Textual information

3.	Buffered Streams

-	Buffered Streams are wrapper for Byte and Character Streams 
-	Buffered Streams allows to read more data at a time
-	Using Buffered Streams we can read and write lines of data instead of one byte or character at a time
	
	
4.	Object Streams
	
-	Objects Streams allows us to read and write Objects to File or Network Streams
-	Objects Streams writing Objects to File or Network is called Serialization 
-	Objects Streams reading Objects from File or Network is called De-serialization

	
####	java.io package

-	All the Streams will fall under java.io package
-	InputStream and OuputStream are used for dealing with ByteStream
-	FileOutputStream and FileInputStream is implementation of OutputStream and InputStream
-	Reader and Writer are used to dealing with CharacterStream
-	FileWriter and FileReader are the Implementation of Reader and Writer
-	File is a Handler class used to deal with files and folders
-	Classes of java.io package throws a checked exception IOException and FileNotFoundException
	
	
									java.io 
									
				InputStream(AC)				Reader(AC) 		  		File - Handler Class used to handle Files and folders
				OuputStream(AC) 			Writer(AC)
				FileInputStream				FileReader
				FileOutputStream			FileWriter

		

	1.	FileInputStream	
		
		-	Reads 1 Byte at a time
	
			try {
				FileInputStream inputStream = new FileInputStream(new File("/FilePath"));
			
				int data =0; // 
				
				while((data = inputStream.read())!= -1) {
					System.out.print((char)data);
				}
			} catch(FileNotFoundException){}
			catch(IOException) {}
			finally {
				try{
					inputStream.close();
				}catch(IOException){}
			}	

	2. 	FileOutputStream  - copying file using FileOutputStream
	
		-	Writes 1 Byte at a time
		-	FileOutputStream and FileInputStream is used for Reading and Writing Binary Files 
		
		
			try {
				FileInputStream inputStream = new FileInputStream(new File("/FilePath"));
				FileOutputStream outputStream = new FileOutputStream(new File("/FilePath"));
			
				int data =0; // 
				
				while((data = inputStream.read())!= -1) {
					System.out.print((char)data);
					outputStream.write(data);
				}
			} catch(FileNotFoundException){}
			catch(IOException) {}
			finally {
				try{
					inputStream.close();
					outputStream.close();
				}catch(IOException){}
			}	



	3.	FileReader and FileWriter 
		
		-	FileReader and FileWriter will used and good for reading and writing textual data
		
			try {
				FileReader fileReader = new FileReader("/FilePath");
				FileWriter fileWriter = new FileWriter("/FilePath");
			
				int data =0; // 
				
				while((data = fileReader.read())!= -1) {
					System.out.print((char)data);
					fileWriter.write(data);
				}
			} catch(FileNotFoundException){}
			catch(IOException) {}
			finally {
				try{
					fileReader.close();
					fileWriter.close();
				}catch(IOException){}
			}	


	4.	StringTokenizer - A Utility Class
	
		-	StringTokenizer is a utility Class to work with String or Handling String Lines
		-	StringTokenizer is mainly used when reading data from Input Streams 
		-	StringTokenizer has overloaded constructor that can be used to split and manipulate the strings
		
		
		Code Snippet 
		
			class StringTokenizerTest {
				main() {
					String string = "You all the power within you";
					
					StringTokenizer st = new StringTokenizer(string);
					
					while(st.hasMoreTokens()) {
						System.out.println(st.nextToken());
					}
				}
			}
			
		-	StringTokenizer("String");
		-	StringTokenizer("String", "Delimeter");
		-	StringTokenizer("String", "Delimeter","booleanValue");		
			
	
	
	5.	Try With Resources
	
		-	Try with Resources has been introduced in Java 7
		-	Try with Resources handles auto-closable - Resources that can be AutoClosable 
		-	To use with Try-Resources, resource class should implements AutoClosable interface
		-	Finally Block is optional in Try-Resources 
			
		Code Snippet 
			
		
			try(FileReader fileReader = new FileReader("/FilePath");
					FileWriter fileWriter = new FileWriter("/FilePath");){
					
					int data =0; // 
					
					while((data = fileReader.read())!= -1) {
						System.out.print((char)data);
						fileWriter.write(data);
					}
			
			}catch(FileNotFoundException) {	}
			catch(IOException) {}
		
		
	6.	Serialization and Deserialization

		-	Serialization is a process of writing Object to Stream
		-	Streams can be File or Network
		-	For an object to be serialize it should implement Serializable Interface
		-	Serializable is a Marker Interface that doesn't have any methods .... but JVM treat that differently by adding additional capabilities
		-	Serializable tells JVM that Objects from this class be Serializable
		-	Transient Keyword is used that mark or make few critical fields to be not part of Serialization and written to OutputStream
	
	
	7.	ObjectInputStream and ObjectOutputStream
	
		
		-	ObjectInputStream is used to Read the Serialized data from file to Object - Deserialization
		-	ObjectOutputStream is used to Write Data to File or Stream - Serialization
		
		
				
		Code Snippet :
		
			class Hosting implements Serializable {
				int id;
				String name;
				Long websites;
				transient String domainName;

				public Hosting(int id, String name, Long websites, String domainName) {
					super();
					this.id = id;
					this.name = name;
					this.websites = websites;
					this.domainName = domainName;
				}
				@Override
				public String toString() {
					return "Hosting [id=" + id + ", name=" + name + ", websites=" + websites + "]";
				}
			}

			public class Serialization {

				public static void main(String[] args) {
					try (FileOutputStream fos = new FileOutputStream(
							"C:\\Bharath_Courses\\Java\\CoreJava\\IOStreams\\HostingDetails.ser");
							ObjectOutputStream oos = new ObjectOutputStream(fos);) {
						oos.writeObject(new Hosting(1, "aws.amazon.com", 90000l, "iambharath.guru"));
					} catch (FileNotFoundException e) {
						e.printStackTrace();
					} catch (IOException e) {
						e.printStackTrace();
					}
				}
			}
			
			
			public class Deserialization {
				public static void main(String[] args) {
					try (FileInputStream fis = new FileInputStream(
							"C:\\\\Bharath_Courses\\\\Java\\\\CoreJava\\\\IOStreams\\\\HostingDetails.ser");
							ObjectInputStream ois = new ObjectInputStream(fis);) {
						Hosting hosting = (Hosting) ois.readObject();
						System.out.println(hosting);
					} catch (FileNotFoundException e) {
						e.printStackTrace();
					} catch (IOException e) {
						e.printStackTrace();
					} catch (ClassNotFoundException e) {
						e.printStackTrace();
					}
				}
			}

		

		Output :
				
			Hosting [id=1, name=aws.amazon.com, websites=90000]
	
		
		

----------------------------------------------------------------------------		
		
## Arrays

-	Array is a Data Structure that hold similar type of elements or homogeneous elements
-	Array in Java can hold Primitive or an Objects type of same kind
-	Object Class Array can hold different kind of elements --> Object[]
-	In Java, Arrays are static .... ie Arrays size can't be grown at runtime --> to overcome that problem we can use Collection Types
-	Once Array is initialized with some size ... we cant increase the size at runtime
-	Accessing elements is very easy and fast ... but inserting and deleting operations will be slow


----------------------------------------------------------------------------		
		
## Object Class Methods

### hashCode() 

-	Collection classes like HashMap and HashSet will internally use hashCode() to store and retrieve objects from a particular buckets 
- 	JVM by default will use some integer value as the hashCode value
-	We can use our own hashcode value by providing implementation to hashCode() method
-	hashCode() method returns int value


	Code Snippet of Providing Custom hashCode() Impl :
	
		class Passenger {
			private String firstName;
			private String lastName;
			private int id;
			
			public int hashCode() {
			
				return this.id + this.firstName.length() + this.lastName.length();
			}
		
		}


### equals()

-	equals is a Object class method inherited all the child class
-	Object class equals() method uses ==(Object Address of HashCode value) operator to check whether two Objects are equals are not
-	For custom Object we need override equals() method and provide implementation for it



	Code Snippet of equals() method
	
	
			class Passenger {

				String firstName;
				String lastName;
				int id;

				public Passenger(String firstName, String lastName, int id) {
					super();
					this.firstName = firstName;
					this.lastName = lastName;
					this.id = id;
				}

				public int hashCode() {
					System.out.println("Hash Code has been invoked");
					return this.id + this.firstName.length() + this.lastName.length();
				}
				
				public boolean equals(Passenger p) {
					return this.firstName.equals(p.firstName) && this.lastName.equals(p.lastName) && this.id == p.id;
				}
			}

			public class HashCodeVerifier {

				public static void main(String[] args) {
					
					Passenger p1  = new Passenger("BHarath", "AShok",1);
					Passenger p2  = new Passenger("BHarath", "Ashok",1);
					
					System.out.println(p1.equals(p2));
				}
			}

### Contract b/w equals() and hashCode()

-	For given two objects

	1.	If equals() method returns true then their hashCode values must be same
	2.	If equals() method returns false then hashCode value may or may not be same
	3.	If hashCode value is True then equals() method may or may return true
	
-	Whenever we implement equals() method and returns true then we need to make sure that hashcode values will be same
-	Override both equals and hashCode method
		
		
		
----------------------------------------------------------------------------		
		
## Collections and Generics


###	Collection Framework


### Main Interfaces of Collection API

	1.	Most interface and classes of CollectionAPI are from java.util package
	2.	java.util.Collection is One of the Parent Interface of Iterable Collection API 
	3.	Collection Interface extends Iterable Interface ---> Data Structure that can be Iterable with Iterator
	3.	java.util.List, Set, Queue are the child interface of Collection Interface
	4.	Java Collections are dynamic, Collections size can grow dynamically at runtime
	 
	 
	1. List 
		
		-	List is a Data Structure allows duplicates and maintains order of insertion
		-	List Implementations
			
			1.	ArrayList
			2.	LinkedList
			3.  Vector
	
				-	Vector is legacy class
				-	All the methods on the vector class are synchronized
			

	2.	Set
		
		-	Set is a Data Structure that doesn't allows duplicates
		-	Set Implementations
			
			1.	HashSet 
				
				1.	LinkedHashSet -	 Maintains the order of insertion
			
			2.	SortedSet

				1.	NavigableSet
					
					1.	TreeSet	-	Elements will be sorted in some order
					
	3.	Queue 

		-	Queue is FIFO Data Structure 
		
		1. Queue 
		
			1.	Priority Queue
			2.	LinkedList
			
	4.	Map
	
		-  	Map is Parent Interface in Collection API
		-	Map is a key value pair Data Structure
		
		1. Map Implementations
		
			1.	HashMap
				
				1. LinkedHashMap
				
			2.	SortedMap
				
				1.	NavigableMap
				
					1.	TreeMap - Sorting on elements will performed
			
		
			3.	HashTable - Thread Safe 
			
				-	All the methods on the HashTable are Thread Safe
				-	Due to Synchronized methods performance will be slower than HashMap
				-	HashTable is legacy classes
		
		
		
		
#### List Interface and its Implementations

1.	List 

	-	List(I) interface extends Collection(I) Interface
	-	List Interface some utility methods like sort(), subList(), toArray(), listIterator(), iterator()

2.	ArrayList
	
	-	Initial capacity will 10 
	-	Faster access and read 
	-	Slow for deleting and inserting at middle
	
		list.add('index', item to be insert);
		list.add(3, 100); // Inserting at middle
		
		list.set(3,200); // Replacing an Item

		list.get(5); // Retrieving based on the Index
		list.remove(5); // Deleting an Item

3.	LinkedList

	-	LinkedList is Ordered Collection in which elements are stored in form of Nodes
	-	A Node has three fields data, Next and Previous
	-	Each Node knows about Next and Previous Node
	-	Insertion and deletions at middle of List are very fast but consumes more memory than ArrayList
	-	Index based search will be slower
	
---------------------------------------------------------
	 	
#### Set Interface and its Implementations

	
1.	Set 

	-	Set is Data Structure where duplicates are not allowed
		
		
2.	HashSet

	-	null is allowed but only once
	-	Duplicated are not allowed 
	-	No order of insertion is maintained
	
3.	LinkedHashSet

	-	Maintains order of Insertion
	-	Duplicates will be removed and null values are allowed --> only one null value
		
		
4.	TreeSet 
	
	-	TreeSet implements Sorted and Navigable set
	-	TreeSet sorts the elements in some order either natural, reverse or custom order based on Comparable and Comparator
	-	Null Values are not at allowed --> Throws NullPointerException
	-	Removes Duplicates and maintains Some Order on the Elements
	-	TreeSet Elements should either implement Comparable or Provide Comparator Interface as impl for TreeSet Constructor
	
5.	NavigableSet
	
	-	NavigableSet is a child interface of SortedSet has methods
	-	NavigableSet is implemented by TreeSet
	-	Important Methods of NavigableSet are ceiling(), higher(), floor(), lower(), pollFirst(), pollLast(), descendingSet()
	
---------------------------------------------------------
	 	
#### Iterable Interface
	
	
-	Iterable is an interface  and has only one method iterator() that returns an Iterator Implementation Interface
-	Collection Implementations like List, Set, Queue will return a iterator instance according to their structure and Implementation


	Code Snippet : 
	
		Set<Integer> setInteger = new HashSet<>();
		
		setInteger.add(1);
		setInteger.add(2);
		
		
		Iterator<Integer> iterator = setInteger.iterator();
		
		while(iterator.hasNext()) {
			System.out.println(iterator.next());
			iterator.remove();
		}


---------------------------------------------------------
	 	
#### Iterator

-	Iterator is an interface that its implementation instance is used to traverse the Collection Implementation items
-	Iterator provides methods hasNext(), next(), remove() to traverse the elements 
-	Collection Implementation classes like ArrayList, HashSet, PriorityQueue will provide an implementation of Iterator Interface

---------------------------------------------------------
	 	
#### ListIterator

-	ListIterator can traverse in both forward and backward direction
-	ListIterator Interface extends Iterator and provides additional methods on top of Iterator interface
-	hasPrevious(), previous(), nextIndex(), previousIndex() --> additional methods


	
	Code Snippet : 

		List<Integer> integerArray = new ArrayList<>();
		
		integerArray.add(1);
		integerArray.add(2);
		
		
		ListIterator<Integer> iterator = integerArray.listIterator();
		
		while(iterator.hasNext()) {
			System.out.println(iterator.next());
			iterator.remove();
		}
		
		while(iterator.hasPrevious()) {
			System.out.println(iterator.previous());
			iterator.remove();
		}


---------------------------------------------------------
	 	
#### Comparable and Comparator

-	Comparable and Comparator is used to provided sorting order on the elements of Data Structure
-	Comparable and Comparator is used mostly in TreeSet and TreeMap 
-	Comparable is from java.lang package
-	Comparator is from java.util package
	
		
	Code Snippet for Sorting String based on length using Comparator:		
		
			public class SortingStringsBasedOnLength {
				public static void main(String[] args) {
					
					String [] stringArray = new String[10];
					stringArray[0] = "aadfd";
					stringArray[1] = "dfd";
					stringArray[2] = "";
					stringArray[3] = "afadfa";
					stringArray[4] = "dfhrtrtdfgs";
					stringArray[5] = "aa";
					stringArray[6] = "erecv";
					stringArray[7] = "dfdsafda";
					stringArray[8] = "geg";
					stringArray[9] = "gegdfdfd";
					
					List<String> stringList = new ArrayList<>(Arrays.asList(stringArray));
					System.out.println(stringList);
					
					List<String> sortedStringList = stringList.stream().sorted(Comparator.comparingInt(String::length)).collect(Collectors.toList());
					sortedStringList.forEach(System.out::println);
				}
			}


---------------------------------------------------------
	 	
### Map Interface

-	Map Interface is used to represent key values type of objects
-	Map is parent interface in Collection API
-	Map is implemented by HashMap, WeakHashMap, IdentityHashMap, TreeMap


1. HashMap 

	-	Allows both null as key and values
	-	Removes Duplicated keys
	-	Doesn't maintain insertion order 
	
2.	LinkedHashMap

	-	Allows null values and keys
	-	Removes duplicates or duplicates are not allowed
	-	Maintains insertion order 

3.	TreeMap

	-	DoesNot allow null values by Default --> Throws NullPointerException
	-	DoesNot allow duplicates
	-	Sorts the elements in Map on Keys or Values
	
	Code Snippets:
	
		public class MapDemo {
			public static void main(String[] args) {
				Map<String, Integer> map = new HashMap<>();

				map.put(null, 23);
				map.put("ddd", 24);
				map.put("ddd", null);
				map.put(null, null);

				System.out.println("HashMap : "+map);

				Map<String, Integer> linkedMap = new LinkedHashMap<>();

				linkedMap.put(null, 23);
				linkedMap.put("ddd", 24);
				linkedMap.put("ddd", null);
				linkedMap.put(null, null);
				linkedMap.put(null, 243);

				System.out.println("LinkedHashMap : "+linkedMap);

				Map<String, Integer> treeMap = new TreeMap<>();

				treeMap.put(null, 23);
				treeMap.put("ddd", 24);
				treeMap.put("ddd", null);
				treeMap.put(null, null);
				treeMap.put(null, 243);

				System.out.println("LinkedHashMap : "+treeMap);
				
				
				
				 // NullFriendly Comparator to Avoid NullPointerExceptions
				
					Map<String, Integer> treeMap = new TreeMap<>(Comparator.nullsFirst(Comparator.naturalOrder()));

					treeMap.put(null, 23);
					treeMap.put("ddd", 24);
					treeMap.put("ddd", null);
					treeMap.put(null, null);
					treeMap.put(null, 243);

					System.out.println("LinkedHashMap : "+treeMap);
					}
				}



	Output :
	
		HashMap : {null=null, ddd=null}
		LinkedHashMap : {null=243, ddd=null}
		Exception in thread "main" java.lang.NullPointerException
			at java.base/java.util.TreeMap.compare(TreeMap.java:1291)
			at java.base/java.util.TreeMap.put(TreeMap.java:536)
			at map.HashMapDemo.main(HashMapDemo.java:34)
			
				
	Output of Null Friendly Comparator : 
	
			HashMap : {null=null, ddd=null}
			LinkedHashMap : {null=243, ddd=null}
			LinkedHashMap : {null=243, ddd=null}	
			
			




4.	IdentityHashMap
	
	Code Snippet
			public class IdentityHashMapDemo {
				public static void main(String[] args) {
					Map<Integer, String> map = new HashMap<>();
					
					Integer i1 = Integer.valueOf(10);
					Integer i2 = Integer.valueOf(20);
					
					map.put(i1, "aaaa");
					map.put(i1, "bbbb");
					
					System.out.println("HashMap : "+map); //HashMap used equals() and hashCode() method to compare the Keys
											// If Keys contents are equals then it will replace the existing key with new value
					
					Map<Integer,String> identityHashMap = new IdentityHashMap<>();
					identityHashMap.put(i1, "aaaa");
					identityHashMap.put(i2, "aaaa");
					
					System.out.println("Identity HashMap : "+identityHashMap);//IdentityHashMap will Compare the keys with == Operators
																		//== (Double equal to operator) will check whether two keys are pointing to same objects or not using hashcode values rather than content
																		//
				}
			}
			
		
	Output :

		HashMap : {10=bbbb}
		Identity HashMap : {10=aaaa, 20=aaaa}

			



5.	WeakHashMap 
	
	Code Snippet :
	
		public class WeakHashMapDemo {

			public static void main(String[] args) throws InterruptedException {
				Map<User, String> hashMap = new HashMap<>();
				System.out.println(" .................. HashMap ..................");
				User u = new User();
				
				hashMap.put(u, "aaaa");
				System.out.println(hashMap);
				
				u = null;
				System.gc();
				Thread.sleep(5000);
				
				System.out.println(hashMap);
				
				/*
				 * WeakHashMap
				 /
				System.out.println(" .................. WeakHashMap ..................");
				
				Map<User, String> weakHashMap = new WeakHashMap<>();
				User u2 = new User();
				
				weakHashMap.put(u2, "bbbb");
				
				System.out.println(weakHashMap);
				
				u2 = null;
				System.gc();
				Thread.sleep(5000);
				
				System.out.println(weakHashMap);
			}
		}


	Output :
	
		 .................. HashMap ..................
		{User=aaaa}
		{User=aaaa}
		 .................. WeakHashMap ..................
		{User=bbbb}
		Finalize Called
		{}

	
---------------------------------------------------------
	 	
### Queue Interface
		
-	Queue Interface extends Collection interface
-	Queue Interface is implemented by LinkedList, PriorityQueue and BlockingQueue
-	Blocking Queue falls under concurrent collections 

1.	LinkedList 


	-	LinkedList is a Strict FIFO Data Structure 
	-	LinkedList allows null and duplicate values
	-	Maintains Insertion order

2.	PrioritQueue

	-	We can change the Order of Priority Queue using Comparator
	-	Priority Queue allows duplicates but doesn't allow null values -> Throws NullPointerException on addition of Queue
	-	Important methods are 
	
	
		offer(Object o) // used to add elements to Queue
		Object peek() // Returns first element or head element of the queue if queue is empty then return null
		Object element() // Similar to peek but throws NoSuchElementException if Queue is empty
		Object poll() // Removes Head element of the Queue .. if empty returns null
		Object remove() // Similar to poll but if queue is empty then throws NoSuchElementException
		
		
	Code Snippets :

		public class PriorityQueueDemo {

			public static void main(String[] args) {

				Queue<Integer> queue = new PriorityQueue<>();

				System.out.println(queue.offer(23));// used to add elements to Queue

				for (int i = 0; i <= 100; i += 10) {
						queue.offer(i);
				}
				
				System.out.println("Priority Queue After Insertion : "+queue);
				
				System.out.println(queue.offer(11));
				System.out.println("After inserting 11 : "+queue);
				System.out.println(queue.peek());// Returns first element or head element of the queue if queue is empty then return null
				System.out.println(queue.element());// Similar to peek but throws NoSuchElementException if Queue is empty
				System.out.println(queue.poll());// Removes Head element of the Queue .. if empty returns null
				System.out.println(queue.remove());// Similar to poll but if queue is empty then throws NoSuchElementException
				System.out.println(queue.remove(89));
			}
		}
		
	Output :
	
		true
		Priority Queue After Insertion : [0, 20, 10, 23, 30, 40, 50, 60, 70, 80, 90, 100]
		true
		After inserting 11 : [0, 20, 10, 23, 30, 11, 50, 60, 70, 80, 90, 100, 40]
		0
		0
		0
		10
		false
		
		
---------------------------------------------------------
	 	
### Arrays and Collections Classes

-	Arrays and Collections classes are utility Classes that has several static utility methods 
-	Both Arrays and Collections class from java.util package
-	Collections 

	-	sort(List l)
	-	reverse(List l)
	-	int binarySearch(List l, I i) // Performs Binary Search of the list	and returns the index of the item in the list

-	Arrays

	-	sort(T[] t) // Arrays.sort() we can also pass custom comparator for Sort Method
	-	parrelSort(T[] t)
	-	asList(T... t)
	- 	stream()
	-	toString(T[] t)
	-	fill()


---------------------------------------------------------
	 	
##	Generics

-	Generics was introduced in Java 1.5
-	Generics mainly introduced for Type Safety and Type Casting Problems while working with Collection API
	
	1.  Type Safety
	2.	Type Casting --> Avoid ClassCastException at runtime
	

	Code Snippet :

		public class MyGenericClass<T> {

			T t;

			MyGenericClass(T t) {
				this.t = t;
			}

			public void displayObjectType() {
				System.out.println(t.getClass().getName());
			}

			public T getObject() {
				return this.t;
			}

		}
		
		
		public class TestGeneric {
			
			public static void main(String[] args) {
				System.out.println("==============================");
				MyGenericClass<String> stringGeneric = new MyGenericClass<String>(new String("Bharath"));
				stringGeneric.displayObjectType();
				System.out.println(stringGeneric.getObject());
				
				System.out.println("==============================");
				
				MyGenericClass<Integer> integerGeneric = new MyGenericClass<Integer>(Integer.valueOf(10));
				integerGeneric.displayObjectType();
				System.out.println(integerGeneric.getObject());
				System.out.println("==============================");
				
				MyGenericClass<Float> floatGeneric = new MyGenericClass<Float>(Float.valueOf(999.99f));
				floatGeneric.displayObjectType();
				System.out.println(floatGeneric.getObject());
			}
		}
	
	Output : 
		
		==============================
		java.lang.String
		Bharath
		==============================
		java.lang.Integer
		10
		==============================
		java.lang.Float
		999.99


1. 	Restricting Generic Type Parameters

	Code Snippet : 
	
		public class MyRunnable<T extends Runnable> {

		}
		class Test {
			public static void main(String[] args) {
				MyRunnable<Thread> m = new MyRunnable<>();
				MyRunnable<Runnable> m2 = new MyRunnable<>();
			}
		}
	
2.	Using Multiple Restrictions
	
	Code Snippet : 
	
		class MyGeneric<T extends Runnable & Comparable<?>> {
		}

		class MyThreadClass<T> extends Thread implements Comparable<T> {
			@Override
			public int compareTo(T o) {
				return 0;
			}
		}

		class MyRunnableClass<T> implements Comparable<T>, Runnable {
			@Override
			public void run() {
			}

			@Override
			public int compareTo(T o) {
				return 0;
			}
		}

		public class TestClass {
			public static void main(String[] args) {
				MyGeneric<MyThreadClass<String>> m = new MyGeneric<>();
				MyGeneric<MyRunnableClass<Integer>> m2 = new MyGeneric<>();
			}
		}
	
3.	Using Generic Method Parameters and wild cards
	
	Code Snippet :
		
		public class WildCardParams {
	
			public <T> void myMethod(List<T> l) {
				l.add(null);
				l.add("ddd"); // Compilation Error
				l.add(3);// Compilation Error
			}
			
			public void myMethod2(List<?> l) {
				l.add(null);
				l.add("ddd");// Compilation Error
				l.add(3);// Compilation Error
			}
			
			
			public static void main(String[] args) {
				WildCardParams wcp = new WildCardParams();
				wcp.myMethod(new ArrayList<Integer>());
				wcp.myMethod2(new ArrayList<String>());
			}
		}

4.	Wildcard and extends
	
-	We can't add values using extends keyword in the calling method and gives compilation error
	
	
	Code Snippet:
	
		public class WildCardParams {
		
			public <T extends Integer> void myMethod(List<T> l) {
				l.add(null);
				l.add("ddd"); // Compilation Error
				l.add(3);// Compilation Error
			}
			
			public void myMethod2(List<?> l) {
				l.add(null);
				l.add("ddd");// Compilation Error
				l.add(3);// Compilation Error
			}
			
			
			public static void main(String[] args) {
				WildCardParams wcp = new WildCardParams();
				wcp.myMethod(new ArrayList<Integer>());
				wcp.myMethod(new ArrayList<String>());// Gives Compilation Due to Argument Mismatch
			}
		}


	
5.	Wildcard and super

-	We can add values using super keyword in the calling method and doesn't gives any compilation error

	Code Snippet :
	
		public class WildCardParams {
			
			public void myMethod(List<? super Integer> l) {
				l.add(null);
				l.add("ddd"); // Compilation Error due to type Mismatch
				l.add(3);
			}
			
			public void myMethod2(List<? super String> l) {
				l.add(null);
				l.add("ddd");
				l.add(3);// Compilation Error due to type Mismatch
			}
			
			
			public static void main(String[] args) {
				WildCardParams wcp = new WildCardParams();
				wcp.myMethod(new ArrayList<Integer>());
				wcp.myMethod2(new ArrayList<String>());
			}
		}

6.	Type Erasure

-	Generics in Java are Compile Time Generics and not Runtime Generics
-	Compiler will uses Type specified on the Generic Class at only Compile time
-	Once Type Check on the Generic Class is done at Compile time 

	-	Compiler will remove the Types at the end of compilation phase 
	-	This will be applicable for all the inbuilt class like List, Set, Queue and Map
	-	At the end of Compilation Phase, Java Compiler will remove the Type Check at runtime
	-	Type erasure is done backward Compatibility issues with Java 1.4, 1.3 

	
-----------------------------------------------

## Enums

-	Enums are used to represent group of Named Constants
-	Enums were introduced in Java 1.5
-	Enums in Java is represented as a class
-	Enums by default extends an abstract class called java.lang.Enum class
-	Properties in Enums are by default public  static final and constants
-	Constants in Enum can be easily accessible by Enum Class Name
-	Enums cant extends other classes but can implement any number of interfaces



	Code Snippets :
	
		public enum PaymentType {

			CREDITCARD(5), DEBITCARD(0), CASH(10, 3.99F), CHECK(5);

			private int fee;
			private float otherChargers;

			PaymentType(int fee) {
				this.fee = fee;
			}
			
			PaymentType(int fee, float otherCharges) {
				this.fee = fee;
				this.otherChargers = otherCharges;
			}

			public int getFee() {
				return this.fee;
			}
			
			public float getOtherCharges() {
				return this.otherChargers;
			}
			
			public float getTotalCharges() {
				return this.getFee() + this.getOtherCharges();
			}

		}
		
		
		public class EnumTest {

			public static void main(String[] args) {
				PaymentType[] paymentValues = PaymentType.values();
				for (PaymentType pt : paymentValues) {
					System.out.println("=======================");
					System.out.println("PaymentType: " + pt.name());
					System.out.println("Ordinal Value: " + pt.ordinal());
					System.out.println("Fee: " + pt.getFee());
					System.out.println("OtherCharges: " + pt.getOtherCharges());
					System.out.println("TotalCharges: " + pt.getTotalCharges());
				}
			}
		}




	Output :
		
		=======================
		PaymentType: CREDITCARD
		Ordinal Value: 0
		Fee: 5
		OtherCharges: 0.0
		TotalCharges: 5.0
		=======================
		PaymentType: DEBITCARD
		Ordinal Value: 1
		Fee: 0
		OtherCharges: 0.0
		TotalCharges: 0.0
		=======================
		PaymentType: CASH
		Ordinal Value: 2
		Fee: 10
		OtherCharges: 3.99
		TotalCharges: 13.99
		=======================
		PaymentType: CHECK
		Ordinal Value: 3
		Fee: 5
		OtherCharges: 0.0
		TotalCharges: 5.0


----------------------------------------------------------------------

## JVM Architecture

1.	What is a Virtual Machine?

	-	VMs are S/w simulation of Real Machines - that performs same functions as real one
	-	Two types of VM 
		1.	Hardware Based
			
			-	Divides given machine into logical systems which are isolated from each other
			-	Hardware resources will be shared b/w VMs
			-	Cloud S/w like AWS, GCP, PCF
			-	Oracle Virtual Box, VMWare Workstations
			
		2.	Application Based
			
			-	Provides runtime engine for Programs to run 
			- 	JVM Provides runtime engine for Java Programs
			
			
		
2.	Components of a JVM

	1.	Class Loader Subsystem 
			
		-	Responsible for loading class to memory
			
	2.	Memory Areas 
		
		-	Heap Area
		-	Method Area
		-	Stack Area
		-	PC Registers
		-	Native Method Stacks
		
	3.	Execution Engine 
	
		-	Runs programs
	
	4.	Java Native Interface (JNI)
	5.	Native Method Libraries
	
	
	
3.	How Class Loaders Work

	-	When JVM came across the class it will check whether the class is already in the Method Area
	-	If not ... it will ask Class Loader System to load the class to Method Aread
	-	ClassLoader Subsystem is ask Application ClassLoader to load the Class
	-	Application ClassLoader in turn delegate request to Extension ClassLoader
	-	ExtensionClass Loader in turn will delegate request to BootStrap ClassLoader
	-	BootStrap ClassLoader is in the top of hierarchy and checks jre/lib/rt.jar and loads it
	-	If class is  not there then again it will delegate the request to Extension ClassLoader
	-	Extension ClassLoader will checks in jre/lib/ext/.jar ... if not found then it will delegate request to Application ClassLoader
	-	Application ClassLoader will checks application Class and all of its jar like hibernate.jar, jdbc.jar
	-	If Class is not found in Application ClassPath also then it will Throw NoClassDefFoundError or ClassNotFoundException
	
	
4.	Types of class loaders

	-	There are 3 types of ClassLoaders
	
		1.	BootStrap ClassLoader
		2.	Extension ClassLoader
		3.	Application ClassLoader
	
	1.	BootStrap ClassLoader

		-	Also know as Primordial Class Loader 
		-	Is responsible loading API classes that comes with JDK 
		-	These Classes will be under JDK/JRE/lib/rt.jar
		-	Written in Low level Language like C and C++
	
	2. 	Extension ClassLoader

		-	Loads class from JDK/JRE/lib/ext/security.jar ... many others
	
	3.	Application ClassLoader
	
		-	Child of Extension Class Loader
		-	Responsible for loading all the Application Related Jars
		
		
5. 	Dynamic Class Loading In Action
	
	-	Class can be loaded dynamically to memory using Class.forName() method
	-	Class.forName() will take overloaded methods 
	
6.	Class is loaded only once

	-	Class will be loaded to Memory only once
	
	Code Snippet :
		
		class User {
			Stirng name;
		}
		
		public class ClassLoaderTest {
		
			main() {
				User u1 = new User();
				Class c1 = u1.getClass();
				
				User u2 = new User();
				Class c2 = u2.getClass();
				
				System.out.println(c1);
				System.out.println(c2);
				
				System.out.println(c1 == c2);
			}
		}
		
7.	Display the class loaders
	
	-	this.class.getClassLoader() will  display the ClassLoader
	-	String.class.getClassLoader() will be loaded by BootStrap ClassLoader hence those information will not be provided
	
8.	Class Loading Sub System and Loading Class

	-	Class Loading Sub System is one of the important part of JVM
	-	Class Loading Sub System is responsible for Loading, Linking and initialization of Class 
	
	1.	Loading 
		
		-	Loading is a process of Loading a class from Hard Disk to JVMs Method Area 
		-	.class file be loaded to JVM Method Area 
		-	JVM does this for every class in the Application
		-	Once .class file is loaded in to Method Area, JVM will an Instance of that class of type java.lang.Class in the Heap Area
		-	Its not actually an Instance of that class but a Class representation of that class - A class object of that class
		-	Using that class instance we can access all the other information related to class
		
	2.	Linking
	
		-	Linking is divided into sub activities 
			
			1.	Verification
				
				-	Its a process of verifying that byte code of class is correct and not corrupted
				-	Byte Code Verifier will do this check
				-	If there are any error or misamatch in .class bytecode ... then JVM will throw java.lang.VerifyError
				
			2.	Preparation
			
				-	In this process ... JVM will allocate memory for all the static, global variables and assigns default values for them
				
			3.	Resolution
				
				-	In this process ... reference will be replaced with actual memory location on the method area
	
	
	
	3.	Initialization
		
		-	In this phases all the static variables are executed
		-	All the static blocks will be executed from parent to child class ... top to bottom
	
9.	Method Area

	-	When classes are loaded into memory ... all the binary information will be stored in Method Area
	-	Method Area is shared across all the threads 
	-	Started right from JVM Start Up

10. Stack Area
	
	- 	When JVM creates a Threads ... JVM will creates Stack for each Thread
	-	Each Thread will gets its own Stack Area and Thread can't access Stack of another Thread
	-	All the method calls and local variables are stored in Stack Area
	-	Each Method call will have a Stack Frame 
	-	Once Method execution completes then Method Stack Frame will be removed
		
		Each Method Stack Frame will have three 3 areas
		
			1.	Variable Array - all the method params and local variable will be stored
			2.	Operand Stack - pushes and pops the statements in to operand stack
			3.	Frame Data - Points to Runtime Constant Pool and Exception Table
		
	-	Once Thread execution completes whole Stack Area will removed by  JVM
	
	
	
11. Heap Area

	-	All the Objects of application are stored in Heap Area - Objects are allocated memory in Heap Area
	-	All the Threads can and will share the Heap Area
	-	Will be initialized at JVM Start up
	
	
12.	PC Registers Area

	-	PC - Program Counter Register 
	-	PC Register Area will always point to current executing statements
	-	Each Thread will gets its own PC Registers Area
	-	PC Register will point next instruction once current execution completed


Native Method Stack Area

	-	This area is used to store the information to call the native langauges



----------------------------------------------------------------------------

## Java Reflection API

-	Reflection is a API that can be used to change the behavior of Class Dynamically at Runtime
-	Using Reflection we can create an Object, invoke methods and change private fields


### Key Reflection API Classes


	-	java.lang.Class is the Starting Point to use Reflection 
	-	All the classes that are loaded Method Area or Memory will be created an instance of java.lang.Class
	-	java.lang.Class has the all Reflection Methods to access class Constructors, Methods, Fields, Annotations
	-	Using java.lang.Class ... we can access all the Constructors, Methods, Fields and Annotations
	
	
	1.	Listing all the Constructor and Methods
	
		Code Snippet :
			
			public class Calculator {

				private double num1;
				private double num2;

				public Calculator(double num1, double num2) {
					this.num1 = num1;
					this.num2 = num2;
				}

				public Calculator() {
					System.out.println("Defalut Constructor Called");
				}

				public double getNum1() {
					return num1;
				}

				public void setNum1(double num1) {
					this.num1 = num1;
				}

				public double getNum2() {
					return num2;
				}

				public void setNum2(double num2) {
					this.num2 = num2;
				}

			}
			
			import java.lang.reflect.Constructor;
			import java.lang.reflect.Method;
		
			public class ReflectionAPITest {
				public static void main(String[] args) throws ClassNotFoundException {
					Class<?> clazz = Class.forName(Calculator.class.getName());
	
					Constructor<?>[] constructors = clazz.getConstructors();
					Method[] methods = clazz.getMethods();

					for (Constructor<?> constructor : constructors) {
						System.out.println(constructor);
					}

					for (Method method : methods) {
						System.out.println(method);
					}
				}
			}
	
			Output :
			
				public Calculator(double,double)
				public Calculator()
				public double Calculator.getNum2()
				public void Calculator.setNum1(double)
				public void Calculator.setNum2(double)
				public double Calculator.getNum1()
				public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
				public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
				public final void java.lang.Object.wait() throws java.lang.InterruptedException
				public boolean java.lang.Object.equals(java.lang.Object)
				public java.lang.String java.lang.Object.toString()
				public native int java.lang.Object.hashCode()
				public final native java.lang.Class java.lang.Object.getClass()
				public final native void java.lang.Object.notify()
				public final native void java.lang.Object.notifyAll()
		
		
	2.	How to create an instance by Constructor with Reflection API

		Code Snippet :
		
			try {
				
				//Param Constructor
				Constructor<?> paramConstructor = clazz.getConstructor(double.class, double.class);
				Object paramInstance = paramConstructor.newInstance(20,30);
				System.out.println(paramInstance);
				
				//Default Constructor
				Constructor<?> defaultConstructor = clazz.getConstructor(null);
				Object calInstance = defaultConstructor.newInstance(null);
				System.out.println(calInstance);
				
			} catch (NoSuchMethodException | SecurityException e) {
				e.printStackTrace();
			} catch (InstantiationException e) {
				e.printStackTrace();
			} catch (IllegalAccessException e) {
				e.printStackTrace();
			} catch (IllegalArgumentException e) {
				e.printStackTrace();
			} catch (InvocationTargetException e) {
				e.printStackTrace();
			}
		
		Output :
		
			Calculator@1055e4af
			Defalut Constructor Called
			Calculator@277c0f21
			
			
	3.	Invoke the Getter 

			Code Snippet : 
			
				try {
					
					//Creating Instance with Constructor 
					
					Constructor<?> paramConstructor = clazz.getConstructor(double.class, double.class);
					Object paramInstance = paramConstructor.newInstance(20,30);
					System.out.println("Getting Instance to invoke Method : "+paramInstance);
					
					
					// Invoking Method with Instance got from above
					
					Method getNum1Method = clazz.getMethod("getNum1", null);
					Object doubleInstance = getNum1Method.invoke(paramInstance, null);
					System.out.println("Value after invoking getter method getNum1 : "+doubleInstance);
					
				} catch (NoSuchMethodException | SecurityException e) {
					e.printStackTrace();
				} catch (InstantiationException e) {
					e.printStackTrace();
				} catch (IllegalAccessException e) {
					e.printStackTrace();
				} catch (IllegalArgumentException e) {
					e.printStackTrace();
				} catch (InvocationTargetException e) {
					e.printStackTrace();
				}
		
			Output : 
			
				
				Getting Instance to invoke Method : Calculator@1055e4af
				Value after invoking getter method getNum1 : 20.0





	4.	Invoking Setter Method

		Code Snippet :

			try {
				Constructor<?> paramConstructor = clazz.getConstructor(double.class, double.class);
				Object paramInstance = paramConstructor.newInstance(20,30);
				System.out.println("Getting Instance to invoke Method : "+paramInstance);
				
				Method getNum1Method = clazz.getMethod("getNum1", null);
				Object doubleInstance = getNum1Method.invoke(paramInstance, null);
				System.out.println("Num1 Value before invoking setter method setNum1 : "+doubleInstance);
				
				
				Method setNum1Method = clazz.getMethod("setNum1", double.class);
				Object setNum1ReturnValue = setNum1Method.invoke(paramInstance, 100);
				System.out.println("Setter Method setNum2 Return will null since its a setter : "+setNum1ReturnValue);
				doubleInstance = getNum1Method.invoke(paramInstance, null);
				System.out.println("Num1 value after invoking setter from ReflectionAPI : "+doubleInstance);
			} catch (NoSuchMethodException | SecurityException e) {
				e.printStackTrace();
			} catch (InstantiationException e) {
				e.printStackTrace();
			} catch (IllegalAccessException e) {
				e.printStackTrace();
			} catch (IllegalArgumentException e) {
				e.printStackTrace();
			} catch (InvocationTargetException e) {
				e.printStackTrace();
			}

			
			
			
		Ouptut :

			Getting Instance to invoke Method : Calculator@1055e4af
			Num1 Value before invoking setter method setNum1 : 20.0
			Setter Method setNum2 Return will null since its a setter : null
			Num1 value after invoking setter from ReflectionAPI : 100.0

			
			
	5.	Modifying Private Fields 

		Code Snippet :
			
			try {
				Constructor<?> paramConstructor = clazz.getConstructor(double.class, double.class);
				Object paramInstance = paramConstructor.newInstance(20,30);
				System.out.println("Getting Instance to invoke Method : "+paramInstance);
				
				Method getNum1Method = clazz.getMethod("getNum1", null);
				Object doubleInstance = getNum1Method.invoke(paramInstance, null);
				System.out.println("Num1 Value before invoking setter method setNum1 : "+doubleInstance);
				
				
				Method setNum1Method = clazz.getMethod("setNum1", double.class);
				Object setNum1ReturnValue = setNum1Method.invoke(paramInstance, 100);
				System.out.println("Setter Method setNum2 Return will null since its a setter : "+setNum1ReturnValue);
				doubleInstance = getNum1Method.invoke(paramInstance, null);
				System.out.println("Num1 value after invoking setter from ReflectionAPI : "+doubleInstance);
				
				Field num1Field = clazz.getDeclaredField("num1");
				num1Field.setAccessible(true);
				
				num1Field.set(paramInstance, 800);
				
				Object updatedNum1Value = num1Field.get(paramInstance);
				System.out.println("Updated Num1 Value : "+updatedNum1Value);
				
			} catch (NoSuchMethodException | SecurityException e) {
				e.printStackTrace();
			} catch (InstantiationException e) {
				e.printStackTrace();
			} catch (IllegalAccessException e) {
				e.printStackTrace();
			} catch (IllegalArgumentException e) {
				e.printStackTrace();
			} catch (InvocationTargetException e) {
				e.printStackTrace();
			}
			
		Ouptut : 	
			Getting Instance to invoke Method : Calculator@1055e4af
			Num1 Value before invoking setter method setNum1 : 20.0
			Setter Method setNum2 Return will null since its a setter : null
			Num1 value after invoking setter from ReflectionAPI : 100.0
			Updated Num1 Value : 800.0

			
			
			
			
	6.	Accessing Annotations and Annotation Fields and methods
		
		Code Snippet :
		
			@Retention(RetentionPolicy.RUNTIME)
			public @interface MyAnnotation {
				
				public abstract String value1();
				public String value2();
				public static final Integer value=500;
				public int integerValue();
			}
			
			@MyAnnotation(value1 = "123", value2 = "bharath", integerValue = 100)
			public class Calculator {

			}
			
			
			import java.lang.annotation.Annotation;
			import java.util.Arrays;

			public class ReflectionAPITest {

				public static void main(String[] args) throws ClassNotFoundException, NoSuchFieldException {
					Class<?> clazz = Class.forName(Calculator.class.getName());

					Annotation[] annotations = clazz.getAnnotations();
					System.out.println("Annotations List : " + Arrays.toString(annotations));

					MyAnnotation annotation = clazz.getAnnotation(MyAnnotation.class);
					System.out.println("Annotation Instance : "+annotation);
					System.out.println("Calling Annotation integerValue Method : "+annotation.integerValue());
					System.out.println("Calling Annotation Value() method"+annotation.value1());
					System.out.println("Calling Public Static Final Variable of Annotation: "+MyAnnotation.value);
				}
			}

	Output:
		
		RetentionPolicy.RUNTIME	
			
			Annotations List : [@MyAnnotation(value1="123", value2="bharath", integerValue=100)]
			Annotation Instance : @MyAnnotation(value1="123", value2="bharath", integerValue=100)
			Calling Annotation integerValue Method : 100
			Calling Annotation Value() method123
			Calling Public Static Final Variable of Annotation: 500
				
		RetentionPolicy.CLASS

			Annotations List : []
			Exception in thread "main" java.lang.NullPointerException
				at ReflectionAPITest.main(ReflectionAPITest.java:14)
			Annotation Instance : null

			
			
			
----------------------------------------------------------------------------

## Java Annotations


-	Annotations are metadata -> Provides details about methods, classes and variables or fields
-	Annotations adds special meanings, capabilities and functionalities to Classes --> JPA, Spring, Hibernate and WebServices Annotations
-	Annotations are followed by @ Symbol
-	Annotation makes code cleaner and easy to understand
-	Annotations are used to get rid of lot of XML based configuration	
-	In Java ... there are 3 types of Annotations 

	1.	CLASS --> Compile Time	---> Used Compiler for Compile Time Validations
	2. 	SOURCE	-->	Build Time  ---> Used By Build tools like Maven, Gradle and Ant
	3.  RUNTIME  --> Runtime 	---> Used By JVM at Runtime
		
-	There are lot of Built-in Annotations and we can define our own Custom Annotations
			
			@Override
			@Deprecated
			@SuppressWarnings


-	@Target Annotation is used to specify where this Annotations can be used or applicable
				
			Constructor, Fields, Types, Methods, Package, Parameters, and Local Variables 	

----------------------------------------------------------------------------

## Java Internationalization

## Regular Expressions

----------------------------------------------------------------------------

## Race Conditions


-	Race Conditions is a situation where Two or more Threads intervene each other and each Thread will read the values modified by other Threads 
-	Race Conditions will result Inconsistent results
-	Each Thread will have its own Stack Area and all the local variables are allocated in the Thread Stack Area

#### Reasons for Race Conditions are :

-	Multiple Threads sharing same Object or Resource
-	Multiple Threads Reading and Writing Shared Object 
-	Multiple Threads will sharing instance variable of Object that are allocated Memory on the Heap Area


#### How to avoid Thread Race Conditions

-	By Providing Threads different Objects or Resource - Not ideal Solution
-	Avoiding instance variables and Static variables that are allocated memory on the Heap Area
-	Through Synchronization


##### 1. Synchronization of Method
	
-	Synchronization is a process in which Threads are allowed to access the Heap area in controlled Manner
-	Synchronization can be applied to Methods are blocks of code
-	Once Thread executing Synchronized method other Threads can't intervene the executing Thread - Other Threads have to wait for current thread to complete the execution
-	If Class has Three synchronized Methods then all the 3 methods will be locked by Currently Executing Thread - Other Threads can't execute any of the synchronized methods of the Class
- Synchronization is Reentrant meaning that Thread can execute other synchronized methods or block as it already hold the lock on the object or instance
		
		
##### 2. Synchronizing a Block of Statements

-	Instead of making whole method Synchronized ... we can particular statements synchronized with synchronized blocks
	
	
		
	Code Snippet demonstrating Thread Race Conditions :
	
		package raceconditions;

		public class Countdown {

			private int i;// Instance variable will allocated memory in the Heap Area .. i will be shared
							// across the thread resulting in inconsistent results

			public void doCountdown() {
				String color = ThreadColor.ANSI_RED;

				switch (Thread.currentThread().getName()) {
				case "RED":
					color = ThreadColor.ANSI_RED;
					break;
				case "GREEN":
					color = ThreadColor.ANSI_GREEN;
					break;
				case "PURPLE":
					color = ThreadColor.ANSI_PURPLE;
					break;
				}

				//synchronized (color) {
				synchronized (this) {
					for (i = 10; i > 0; i--) {
						// for (int i = 10; i > 0; i--) { // Local variable i will allocated on the
						// Thread Stack Area .. Each Thread will have its own Stack Area ... Specific to
						// that ... resulting Consistent result
						System.out.println(color + Thread.currentThread().getName() + " : i =" + i);
					}
				}
			}
		}
		
		package raceconditions;

		public class CountdownThread extends Thread {

			private Countdown countdown;

			CountdownThread(Countdown countdown) {
				this.countdown = countdown;
			}

			public void run() {
				this.countdown.doCountdown();
			}
		}

		package raceconditions;

		public class RaceConditionTest {

			public static void main(String[] args) {
				Countdown cd = new Countdown();

				CountdownThread cdt1 = new CountdownThread(cd);
				CountdownThread cdt2 = new CountdownThread(cd);
				cdt1.setName("RED");
				cdt2.setName("PURPLE");
				
				cdt1.start();
				cdt2.start();

			}
		}
	
	
	
	Output :
	
			PURPLE : i =10
			PURPLE : i =9
			PURPLE : i =8
			RED : i =10
			RED : i =6
			RED : i =5
			RED : i =4
			RED : i =3
			RED : i =2
			RED : i =1
			PURPLE : i =7
			
		
		After adding synchronized and using object lock
		
			
			RED : i =10
			RED : i =9
			RED : i =8
			RED : i =7
			RED : i =6
			RED : i =5
			RED : i =4
			RED : i =3
			RED : i =2
			RED : i =1
			PURPLE : i =10
			PURPLE : i =9
			PURPLE : i =8
			PURPLE : i =7
			PURPLE : i =6
			PURPLE : i =5
			PURPLE : i =4
			PURPLE : i =3
			PURPLE : i =2
			PURPLE : i =1



		
----------------------------------------------------------------------------

## Thread Dead Lock, wait, notify and notifyAll


-	Deadlock is a situation where Threads holding resources is waiting for another Threads to release the hold on those resources
-	Deadlock can be avoidable my making proper use of wait, notify and notifyAll methods of Object Class


	1.	wait() - invoking Thread will go to waiting mode by release the lock .... will be waiting state until another Threads notify it explicitly
	2.	notify() - Once Thread finishes its task ... it notify other thread by release the lock
		-	There is no mechanism to notify a particular thread
	3.	notifyAll() - Since there no mechanism to notify a particular thread ... it's convention to use notifyAll() to notify all the waiting threads
	
		-	notifyAll may result in performance issue ... if lots of Threads are waiting for same resource or waiting to perform same task
			
		Code Snippet showing Thread Deadlock and overcome by using wait, notify and notifyAll :
	
			package producerconsumer;

			public class ProducerConsumerTest {

				public static void main(String[] args) throws InterruptedException {
					Message message = new Message();
					Writer writer = new Writer(message);
					writer.setName("WRITER");

					Reader reader = new Reader(message);
					reader.setName("READER");

					writer.start();
					reader.start();

					writer.join();
					reader.join();
				}

			}

			class Message {

				private String message;
				private boolean isEmpty = true;

				public synchronized String read() {
					if (isEmpty) {
						try {
							wait();
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
					}
					isEmpty = true;
					notifyAll();
					return this.message;
				}

				public synchronized void write(String message) {
					if (!isEmpty) {
						try {
							wait();
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
					}
					isEmpty = false;
					this.message = message;
					notifyAll();
				}
			}

			class Writer extends Thread {

				Message message;

				Writer(Message message) {
					this.message = message;
				}

				public synchronized void run() {
					String[] messages = new String[] { "aaa", "bbbb", "ccc", "dddd", "eeee" };

					for (int i = 0; i < messages.length; i++) {
						System.out.println(Thread.currentThread().getName() + " Thread is writing new message....");

						System.out.println(messages[i]);
						message.write(messages[i]);
						try {
							Thread.sleep(2000);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
					}
					message.write("Finished");
				}
			}

			class Reader extends Thread {

				Message message;

				Reader(Message message) {
					this.message = message;
				}

				public void run() {
					System.out.println(Thread.currentThread().getName() + " Thread is Consuming new message....");

					for (String latestMessage = message.read(); !latestMessage.equals("Finished"); latestMessage = message.read()) {
						System.out.println("Latest Message : " + latestMessage);
						try {
							Thread.sleep(100);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
					}
				}
			}
		
		Output :

			READER Thread is Consuming new message....
			WRITER Thread is writing new message....
			aaa
			Latest Message : aaa
			WRITER Thread is writing new message....
			bbbb
			Latest Message : bbbb
			WRITER Thread is writing new message....
			ccc
			Latest Message : ccc
			WRITER Thread is writing new message....
			dddd
			Latest Message : dddd
			WRITER Thread is writing new message....
			eeee
			Latest Message : eeee
			
### Threads Suspension

-	While executing a Synchronized code Threads can be suspended while executing any single line of code 
-	Thread can be suspended while performing before or after the operations	or while calling the methods

###	Atomic Operations 

-	Atomic Operations are the operations that happens all at once 
-	Some of the Atomic Operations are
	
	1.	Object Comparison --> object1.equals(object2)
	2.	Reading and writing primitive variables except of those type long and double 
	3.	Thread can't suspended while int i=10 but can be suspended while executing double d = 10.90
	
	
### Collection Classes 

-	Few Collection Classes are Thread Safe and few are not
-	ArrayList is not Thread Safe --> Multiple Threads can share or work on the single instance of ArrayList
-	While using ArrayList Developer needs to write a synchronized code
- 	Vector is Thread safe --> all the methods in Vector class is synchronized
-	Developer no need to needs to handle synchronization explicitly


-------------------------------------------------------------------

## Java Util Concurrent package and Thread Interference with ArrayList


-	ArrayList is not synchronized meaning when two or more threads working on same ArrayList Instance we may exceptions especially reading and writing from the ArrayList
-	Below is Producer-Consumer Program in which both Producer and Consumer Threads interfere with each while reading and writing Messages from same ArrayList Instance 
- 	Since ArrayList is not synchronized, Developer should provide a Custom Implementation of Synchronized code ... Threads may end-up with ArrayIndexOutOfBoundException
-	Another Solution is to Synchronized List Implementation like Vector ... where all methods are Synchronized
-	Producer-Consumer with Synchronized block
	
	Code Snippet :
	
		public class ArrayListProducerAndConsumer {

			public static final String EOF = "EOF";

			public static void main(String[] args) {

				List<String> buffer = new ArrayList<>();

				Producer producer = new Producer(buffer, ANSI_RED);
				Consumer consumer1 = new Consumer(buffer, ANSI_CYAN);
				Consumer consumer2 = new Consumer(buffer, ANSI_BLUE);

				producer.start();
				consumer1.start();
				consumer2.start();

			}

		}

		// Producer
		class Producer extends Thread {

			private List<String> buffer;
			private String color;

			Producer(List<String> buffer, String color) {
				this.buffer = buffer;
				this.color = color;
			}

			public void run() {
				String[] messages = { "a", "b", "c", "d" };
				for (String message : messages) {
					synchronized (this.buffer) { // Producer getting the Lock on ArrayList
						System.out.println(color + "Producer adding to Buffer: " + message);
						this.buffer.add(message);
					}
					try {
						System.out.println(color+ "Producer is going to sleep for 3 secs...");
						Thread.sleep(3000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
				synchronized (this.buffer) { // Producer getting the Lock on ArrayList
					this.buffer.add(EOF);
				}
				System.out.println(color + "Adding EOF and Exiting...");
			}
		}

		// Consumer
		class Consumer extends Thread {

			private List<String> buffer;
			private String color;

			public Consumer(List<String> buffer, String color) {
				this.buffer = buffer;
				this.color = color;
			}

			public void run() {
				while (true) {
					// Consumers getting the Lock on ArrayList
					// And only one Thread will used to get execute
					synchronized (this.buffer) {
						if (this.buffer.isEmpty()) {
							continue;
						}
						if (this.buffer.get(0).equals(EOF)) {
							System.out.println(color + "EOF Reached .... Exiting ...");
							break;
						} else {
							System.out.println(color + "Consumer: " + Thread.currentThread().getName()
									+ " Removing Element from Buffer " + this.buffer.remove(0));
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
					}

				}
			}
		}

		
		Output :
		
			Producer adding to Buffer: a
			Producer is going to sleep for 3 secs...
			Consumer: Thread-1 Removing Element from Buffer a
			Producer adding to Buffer: b
			Producer is going to sleep for 3 secs...
			Consumer: Thread-2 Removing Element from Buffer b
			Producer adding to Buffer: c
			Producer is going to sleep for 3 secs...
			Consumer: Thread-1 Removing Element from Buffer c
			Producer adding to Buffer: d
			Producer is going to sleep for 3 secs...
			Consumer: Thread-2 Removing Element from Buffer d
			Adding EOF and Exiting...
			EOF Reached .... Exiting ...
			EOF Reached .... Exiting ...




###	Drawbacks of using Synchronized Block

1.	Threads will get blocked until they get the Lock and currently executing Thread can't be interrupted
2.	Synchronized block must be within the same method .. can't start in one method and endup in another one
3.	Don't have info on the object's Intrinsic lock availability or any other information about the Lock
4.	Flow of execution may reach the top of synchronized block either Thread needs to get a Lock and continue or block at that point of line
5.	Threads will not be served in FIFO ... First Blocked Thread may execute at Last and vice versa


Sol : Thread Interference can be avoided ... Instead of using synchronization ... we can use Classes that implement java.util.concurrent.locks.Lock Interface
		
----------------------------------------------------------------------

##	Reentrant Lock and Unlock


-	Reentrant Lock in which developer needs to explicitly open the lock and close the lock
-	Reentrant Lock can open and close across the methods
-	Unlike INTRINSIC LOCK where JVM will OPEN and CLOSE the LOCK with synchronized methods and Blocks ... Developer needs to open and close the lock explicitly.
-	Advantage of using REETRANT LOCK is that Developer knows where exactly LOCK is opening and LOCK is closing and AVAILABILITY of LOCK




	Code Snippet :
	
		public class ReentrantLockDemo {

			public static void main(String[] args) {

				List<String> buffer = new ArrayList<>();
				
				// Create an Instance of ReentrantLock from Concurrent Lock Package
				// ReentrantLock instance must be shared with Threads that Competing for Same Lock
				ReentrantLock reentrantLock = new ReentrantLock();

				Producer producer = new Producer(buffer, ANSI_RED, reentrantLock);
				Consumer consumer1 = new Consumer(buffer, ANSI_CYAN, reentrantLock);
				Consumer consumer2 = new Consumer(buffer, ANSI_BLUE, reentrantLock);

				producer.start();
				consumer1.start();
				consumer2.start();

			}

		}

		class Producer extends Thread {

			private List<String> buffer;
			private String color;
			private ReentrantLock reentrantLock;

			Producer(List<String> buffer, String color, ReentrantLock reentrantLock) {
				this.buffer = buffer;
				this.color = color;
				this.reentrantLock = reentrantLock;
			}

			public void run() {
				String[] messages = { "a", "b", "c", "d" };
				for (String message : messages) {
					//synchronized (this.buffer) { // Producer getting the Lock on ArrayList
						reentrantLock.lock(); // Reentrant Lock Opening
						System.out.println(color + "Producer adding to Buffer: " + message);
						this.buffer.add(message);
						reentrantLock.unlock();// Reentrant Lock Closing
					//}
					try {
						System.out.println(color + "Producer is going to sleep for 3 secs...");
						Thread.sleep(3000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
				//synchronized (this.buffer) { // Producer getting the Lock on ArrayList
					reentrantLock.lock(); // Reentrant Lock Opening
					this.buffer.add(EOF);
					reentrantLock.unlock(); // Reentrant Lock Closing
				//}
				System.out.println(color + "Adding EOF and Exiting...");
			}
		}

		class Consumer extends Thread {

			private List<String> buffer;
			private String color;
			ReentrantLock reentrantLock;

			public Consumer(List<String> buffer, String color, ReentrantLock reentrantLock) {
				this.buffer = buffer;
				this.color = color;
				this.reentrantLock = reentrantLock;
			}

			public void run() {
				while (true) {
					// Consumers getting the Lock on ArrayList
					// And only one Thread will used to get execute
					//synchronized (this.buffer) {
						 Maximum Lock Count Exceeded Problem
						
						reentrantLock.lock(); // Reentrant Lock Opening
						
						if (this.buffer.isEmpty()) {
							continue;
						}
						if (this.buffer.get(0).equals(EOF)) {
							System.out.println(color + "EOF Reached .... Exiting ...");
							break;
						} else {
							System.out.println(color + "Consumer: " + Thread.currentThread().getName()
									+ " Removing Element from Buffer " + this.buffer.remove(0));
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
						}
						reentrantLock.unlock();// Reentrant Lock Closing
					//}

				}
			}
		}
				
		
	Output :

		Exception in thread "Thread-2" java.lang.Error: Maximum lock count exceeded
		at java.base/java.util.concurrent.locks.ReentrantLock$Sync.nonfairTryAcquire(ReentrantLock.java:138)
		at java.base/java.util.concurrent.locks.ReentrantLock$NonfairSync.tryAcquire(ReentrantLock.java:199)
		at java.base/java.util.concurrent.locks.AbstractQueuedSynchronizer.acquire(AbstractQueuedSynchronizer.java:1237)
		at java.base/java.util.concurrent.locks.ReentrantLock.lock(ReentrantLock.java:267)
		at reentrantlock.Consumer.run(ReentrantLockDemo.java:88)
		
		
### Note :

-	Above Program will error out due to maximum lock opening but not closing explicitly by Consumer Threads
-	If we are using Reentrant Lock then programmer should make sure that ... Reentrant Locks should be closed explicitly otherwise it will opened forever
	-	Thread will be in Blocked Status forever
-	Unlike in the Intrinsic Lock where the JVM will manage Opening and Closing the Locks


		
	Code Snippet After Closing the Reentrant Lock explicitly:

		public class ReentrantLockDemo {

			public static void main(String[] args) {

				List<String> buffer = new ArrayList<>();

				// Create an Instance of ReentrantLock from Concurrent Lock Package
				// ReentrantLock instance must be shared with Threads that Competing for Same
				// Lock
				ReentrantLock reentrantLock = new ReentrantLock();

				Producer producer = new Producer(buffer, ANSI_RED, reentrantLock);
				Consumer consumer1 = new Consumer(buffer, ANSI_CYAN, reentrantLock);
				Consumer consumer2 = new Consumer(buffer, ANSI_BLUE, reentrantLock);

				producer.start();
				consumer1.start();
				consumer2.start();

			}

		}

		class Producer extends Thread {

			private List<String> buffer;
			private String color;
			private ReentrantLock reentrantLock;

			Producer(List<String> buffer, String color, ReentrantLock reentrantLock) {
				this.buffer = buffer;
				this.color = color;
				this.reentrantLock = reentrantLock;
			}

			public void run() {
				String[] messages = { "a", "b", "c", "d" };
				for (String message : messages) {
					// synchronized (this.buffer) { // Producer getting the Lock on ArrayList
					reentrantLock.lock();
					System.out.println(color + "Producer adding to Buffer: " + message);
					this.buffer.add(message);
					reentrantLock.unlock();
					// }
					try {
						System.out.println(color + "Producer is going to sleep for 3 secs...");
						Thread.sleep(3000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
				// synchronized (this.buffer) { // Producer getting the Lock on ArrayList
				reentrantLock.lock();
				this.buffer.add(EOF);
				reentrantLock.unlock();
				// }
				System.out.println(color + "Adding EOF and Exiting...");
			}
		}

		class Consumer extends Thread {

			private List<String> buffer;
			private String color;
			ReentrantLock reentrantLock;

			public Consumer(List<String> buffer, String color, ReentrantLock reentrantLock) {
				this.buffer = buffer;
				this.color = color;
				this.reentrantLock = reentrantLock;
			}

			int lockCounter;

			public void run() {

				while (true) {
					// Consumers getting the Lock on ArrayList
					// And only one Thread will used to get execute
					// synchronized (this.buffer) {
					/*
					 * Maximum Lock Count Exceeded Problem Below code is opening the Lock explicitly
					 * but not able to reach Closing Statement Due to continue statement inside if
					 * buffer isEmpty
					 */
					reentrantLock.lock();
					if (this.buffer.isEmpty()) {
						reentrantLock.unlock();
						continue;
					}
					if (this.buffer.get(0).equals(EOF)) {
						System.out.println(color + "EOF Reached .... Exiting ...");
						reentrantLock.unlock();
						break;
					} else {
						System.out.println(color + "Consumer: " + Thread.currentThread().getName()
								+ " Removing Element from Buffer " + this.buffer.remove(0));
					}
					reentrantLock.unlock();
					// }

				}
			}
		}
		*
		
	Output after closing explicitly:

		Producer adding to Buffer: a
		Producer is going to sleep for 3 secs...
		Consumer: Thread-1 Removing Element from Buffer a
		Producer adding to Buffer: b
		Producer is going to sleep for 3 secs...
		Consumer: Thread-1 Removing Element from Buffer b
		Producer adding to Buffer: c
		Producer is going to sleep for 3 secs...
		Consumer: Thread-2 Removing Element from Buffer c
		Producer adding to Buffer: d
		Producer is going to sleep for 3 secs...
		Consumer: Thread-2 Removing Element from Buffer d
		Adding EOF and Exiting...
		EOF Reached .... Exiting ...
		EOF Reached .... Exiting ...

	
		
--------------------------------------------------------------------------------		
		
##	Using Try Finally with Threads

-	Try finally can be used to close the Reentrant Lock explicitly in finally Block
-	Instead of writing REENTRANT CLOSE reentrantLock.close() the code multiple times
-	We can put the ReentrantLock opening Statement in the Try Block and can put ReentrantLock Closing Statement in finally Block
-	Finally block will execute irrespective of exceptions or conditions in the try block


### Advantages of Reentrant Lock

-	Reentrant Lock Class provides various methods that helps to get information about lock explicitly
-	boolean tryLock() method returns true if lock is freely available and locks the instance 
-	int getHoldCount() method returns the number of holds on the lock
-	int getQueueLength() method returns an estimate number of Threads that are waiting for this lock
-   boolean hasQueuedThreads() methods boolean if any threads are waiting for lock on this object
-	boolean isFair() methods returns whether ReentrantLock is Fair ... Lock Serves in FIFO manner ... if Lock is fair then while releasing current lock it will look for longest waiting Thread-0
-	boolean isHeldByCurrentThread() method returns boolean if lock is currently held by current running thread
-	boolean isLocked() method queries whether Lock is held by any threads	

		
		
	Code Snippet :
	
		public class TryFinallyThreadsDemo {

			public static final String EOF = "EOF";

			public static void main(String[] args) {
				List<String> buffer = new ArrayList<>();
				ReentrantLock reentrantLock = new ReentrantLock();

				Producer producer = new Producer(buffer, ANSI_RED, reentrantLock, "Producer");
				Consumer consumer1 = new Consumer(buffer, ANSI_PURPLE, reentrantLock, "Consumer 1");
				Consumer consumer2 = new Consumer(buffer, ANSI_CYAN, reentrantLock, "Consumer 2");

				new Thread(producer).start();
				new Thread(consumer1).start();
				new Thread(consumer2).start();

			}

		}

		class Producer implements Runnable {

			private List<String> buffer;
			private String color;
			private ReentrantLock reentrantLock;
			private String threadName;

			public Producer(List<String> buffer, String color, ReentrantLock reentrantLock, String threadName) {
				super();
				this.buffer = buffer;
				this.color = color;
				this.reentrantLock = reentrantLock;
				this.threadName = threadName;
			}

			@Override
			public void run() {

				String[] messages = new String[] { "1", "2", "3", "4", "5", "6" };

				for (String message : messages) {
					System.out.println(color + threadName + " - has added message to buffer: " + message);
					try {
						this.reentrantLock.lock();
						System.out.println(color + threadName +" Get Hold Count: "+this.reentrantLock.getHoldCount());
						System.out.println(color + threadName +" Queue Length: "+this.reentrantLock.getQueueLength());
						System.out.println(color + threadName +" Has Queued Threads: "+this.reentrantLock.hasQueuedThreads());
						System.out.println(color + threadName +" Is Fair: "+this.reentrantLock.isFair());
						System.out.println(color + threadName +" IsHeldByCurrentThread: "+this.reentrantLock.isHeldByCurrentThread());
						System.out.println(color + threadName +" Is Locked: "+this.reentrantLock.isLocked());
						buffer.add(message);
						try {
							Thread.sleep(3000);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
					} finally {
						this.reentrantLock.unlock();
					}
				}
				try {
					this.reentrantLock.lock();
					buffer.add(EOF);
				} finally {
					this.reentrantLock.unlock();
				}

			}

		}

		class Consumer implements Runnable {

			private List<String> buffer;
			private String color;
			private ReentrantLock reentrantLock;
			private String threadName;

			public Consumer(List<String> buffer, String color, ReentrantLock reentrantLock, String threadName) {
				super();
				this.buffer = buffer;
				this.color = color;
				this.reentrantLock = reentrantLock;
				this.threadName = threadName;
			}

			@Override
			public void run() {
				long lockCounter = 0;
				while (true) {
					try {
						if (this.reentrantLock.tryLock(5,TimeUnit.SECONDS)) {
							System.out.println(color + threadName +" Get Hold Count: "+this.reentrantLock.getHoldCount());
							System.out.println(color + threadName +" Queue Length: "+this.reentrantLock.getQueueLength());
							System.out.println(color + threadName +" Has Queued Threads: "+this.reentrantLock.hasQueuedThreads());
							System.out.println(color + threadName +" Is Fair: "+this.reentrantLock.isFair());
							System.out.println(color + threadName +" IsHeldByCurrentThread: "+this.reentrantLock.isHeldByCurrentThread());
							System.out.println(color + threadName +" Is Locked: "+this.reentrantLock.isLocked());
							try {
								// this.reentrantLock.lock();
								if (buffer.isEmpty()) {
									continue;
								}
								System.out.println(color + threadName + " Lock Counter: " + lockCounter);
								lockCounter = 0;
								if (buffer.get(0).equals(EOF)) {
									System.out.println(color + "Reached EOF.... Exiting....");
									break;
								} else {
									System.out.println(
											color + threadName + " - is removing message from buffer: " + buffer.remove(0));
								}
							} finally {
								this.reentrantLock.unlock();
							}
						} else {
							lockCounter++;
						}
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}

			}
		}
		
		
		
----------------------------------------------------------------------

##	Thread Pools

-	Thread Pool is a managed set of Threads from JVM
-	Thread Pool managed by JVM offers Resource, Memory Optimization, reduces time consuming and manages life-cycle of Threads
-	JVM manages Thread scheduling and Thread life-cycle
-	Thread Pool is suitable for application with large set of threads
-	ExecutorService provides implementation for different Thread Pools in Java
-	ExecutorService is from java.util.concurrent package
-	ExecutorService offers different factory methods that returns implementation of Thread Pool
- 	ExecutorService helps to focus the code instead of Thread management


	Code Snippet :
	
		public class ExecutorServiceDemo {

			public static void main(String[] args) throws InterruptedException, ExecutionException {
				List<String> buffer = new ArrayList<>();
				ReentrantLock lock = new ReentrantLock();

				Producer producer1 = new Producer(buffer, ANSI_RED, "Producer ", lock);
				Consumer consumer1 = new Consumer(buffer, ANSI_PURPLE, "Consumer 1 ", lock);
				Consumer consumer2 = new Consumer(buffer, ANSI_CYAN, "Consumer 2 ", lock);

				ExecutorService es = Executors.newFixedThreadPool(4);

				es.submit(producer1);
				es.submit(consumer1);
				es.submit(consumer2);

				Callable<String> c = new Callable<String>() {
					public String call() {
						return "Bharath The Great";
					}
				};
				//// Get Method on Future is Blocking meaning ... it will not executed until the
				// result is not available in the Future Instance
				Future<String> future = es.submit(c);
				
				
				Future<String> submit = es.submit(() -> "Bharath");
				System.out.println(ANSI_GREEN + future.get());
				System.out.println(submit.get());

				es.shutdown();
			}

		}

		class Producer implements Runnable {

			private List<String> buffer;
			private String color;
			private String threadName;
			private ReentrantLock lock;

			public Producer(List<String> buffer, String color, String threadName, ReentrantLock lock) {
				super();
				this.buffer = buffer;
				this.color = color;
				this.threadName = threadName;
				this.lock = lock;
			}

			public void run() {
				String[] messages = { "1", "2", "3", "4", "5", "6", "7", "8" };

				for (String message : messages) {
					try {
						this.lock.lock();
						System.out.println(color + threadName + " has added a Message: " + message);
						buffer.add(message);
					} finally {
						this.lock.unlock();
					}
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
				}
				try {
					this.lock.lock();
					buffer.add("EOF");
				} finally {
					this.lock.unlock();
				}
			}
		}

		class Consumer implements Runnable {
			private List<String> buffer;
			private String color;
			private String threadName;
			private ReentrantLock lock;

			public Consumer(List<String> buffer, String color, String threadName, ReentrantLock lock) {
				super();
				this.buffer = buffer;
				this.color = color;
				this.threadName = threadName;
				this.lock = lock;
			}

			public void run() {
				long countLock = 0;
				while (true) {
					if (this.lock.tryLock()) {
						try {
							if (buffer.isEmpty()) {
								continue;
							}
							System.out.println(color + threadName + " Lock Count: " + countLock);
							countLock = 0;
							if (buffer.get(0).equals("EOF")) {
								System.out.println(color + threadName + " Reached EOF.... EXITING....");
								break;
							} else {
								System.out.println(
										color + threadName + "--> is removing message from Buffer: " + buffer.remove(0));
							}
						} finally {
							this.lock.unlock();
						}
					} else {
						countLock++;
					}
				}
			}
		}

	Output :

		Producer  has added a Message: 1
		Consumer 2  Lock Count: 6834
		Bharath The Great
		Consumer 2 --> is removing message from Buffer: 1
		Producer  has added a Message: 2
		Consumer 2  Lock Count: 43416272
		Consumer 2 --> is removing message from Buffer: 2
		Producer  has added a Message: 3
		Consumer 2  Lock Count: 35687034
		Consumer 2 --> is removing message from Buffer: 3
		Producer  has added a Message: 4
		Consumer 1  Lock Count: 131046307
		Consumer 1 --> is removing message from Buffer: 4
		Producer  has added a Message: 5
		Consumer 2  Lock Count: 101386327
		Consumer 2 --> is removing message from Buffer: 5
		Producer  has added a Message: 6
		Consumer 1  Lock Count: 95686684
		Consumer 1 --> is removing message from Buffer: 6
		Producer  has added a Message: 7
		Consumer 2  Lock Count: 92031560
		Consumer 2 --> is removing message from Buffer: 7
		Producer  has added a Message: 8
		Consumer 2  Lock Count: 36699126
		Consumer 2 --> is removing message from Buffer: 8
		Consumer 1  Lock Count: 131470594
		Consumer 1  Reached EOF.... EXITING....
		Consumer 2  Lock Count: 51520908
		Consumer 2  Reached EOF.... EXITING....
		
		
		
		
		
----------------------------------------------------------------------

##	ArrayBlockingQueue		

-	ArrayBlockingQueue is one of the ThreadSafe Queue Class form java.util.concurrent package
-	Instead of using ArrayList we can use ThreadSafe Classes like ArrayBlockingQueue to Reduce the Synchronization code
-	ArrayBlockingQueue methods are Thread Safe meaning that only Thread at a time can execute the method and other threads will wait for the lock
-	ArrayBlockingQueue is FIFO Data Structure which is best suitable for Producer and Consumer Problem
-	add() and remove() method throws NoSuchElementException if not able to perform immediately or items are present in buffer
-	put() and take() methods are synchronized and will be blocked,  so no need to add synchronized code explicitly
-	put() and take() needs to handle exception explicitly
-	poll() method will retrieve and remove head of queue ... if queue is empty then return null
-	Even if we use Thread Safe Classes like ArrayBlockingQueue it not sure that there will no Thread interference --> so need to add synchronization explicitly to consumers	
		
	Code Snippet :
	
		public class ArrayBlockingQueueDemo {

			public static void main(String[] args) {
				ArrayBlockingQueue<String> buffer = new ArrayBlockingQueue<>(100);

				Producer producer1 = new Producer(buffer, ANSI_RED, "Producer 1");
				Consumer consumer1 = new Consumer(buffer, ANSI_PURPLE, "Consumer 1 ");
				Consumer consumer2 = new Consumer(buffer, ANSI_CYAN, "Consumer 2 ");

				new Thread(producer1).start();
				new Thread(consumer2).start();
				new Thread(consumer1).start();
			}

		}

		class Producer implements Runnable {

			private ArrayBlockingQueue<String> buffer;
			private String color;
			private String name;

			public Producer(ArrayBlockingQueue<String> buffer, String color, String name) {
				super();
				this.buffer = buffer;
				this.color = color;
				this.name = name;
			}

			@Override
			public void run() {
				String[] messages = { "1", "2", "3", "4", "5", "6", "7", "8"};
				try {
					for (String message : messages) {
						System.out.println(color + name + " has added a Message: " + message);
						buffer.add(message);
						Thread.sleep(3000);
					}
					buffer.put("EOF");
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
		}

		class Consumer implements Runnable {
			private ArrayBlockingQueue<String> buffer;
			private String color;
			private String name;

			public Consumer(ArrayBlockingQueue<String> buffer, String color, String name) {
				super();
				this.buffer = buffer;
				this.color = color;
				this.name = name;
			}

			public void run() {

				while (true) {
					if (buffer.isEmpty()) {
						continue;
					}
					if (buffer.peek().equals("EOF")) {
						System.out.println(color + name + " EOF Reached and Exiting...");
						break;
					} else {
						System.out.println(color + name + " --> Removed Message from Buffer: " + buffer.poll());
					}
				}
			}
		}

		
	Output: 

		Producer 1 has added a Message: 1
		Consumer 1  --> Removed Message from Buffer: 1
		Consumer 2  --> Removed Message from Buffer: null
		Producer 1 has added a Message: 2
		Consumer 2  --> Removed Message from Buffer: 2
		Consumer 1  --> Removed Message from Buffer: null
		Producer 1 has added a Message: 3
		Consumer 2  --> Removed Message from Buffer: 3
		Consumer 1  --> Removed Message from Buffer: null
		Producer 1 has added a Message: 4
		Consumer 1  --> Removed Message from Buffer: 4
		Consumer 2  --> Removed Message from Buffer: null
		Producer 1 has added a Message: 5
		Consumer 2  --> Removed Message from Buffer: 5
		Consumer 1  --> Removed Message from Buffer: null
		Producer 1 has added a Message: 6
		Consumer 1  --> Removed Message from Buffer: 6
		Consumer 2  --> Removed Message from Buffer: null
		Producer 1 has added a Message: 7
		Consumer 1  --> Removed Message from Buffer: 7
		Producer 1 has added a Message: 8
		Consumer 2  --> Removed Message from Buffer: 8
		Consumer 1  --> Removed Message from Buffer: null
		Consumer 2  EOF Reached and Exiting...
		Consumer 1  EOF Reached and Exiting...

		
------------------------------------------------------------------------

## Deadlocks		

-	Deadlock is a situation where a Thread Holding lock trying to get a lock on another instance which in turn holding by another Thread
- 	Deadlock usually occurs due to improper coding structure
-	Deadlock occurs when from multiple class try to access the locks in opposition direction


Preventing Deadlocks 

1.	Obtain the Locks in same order 
2. 	Make Threads to work on single shared object or lock



	Code snippet of Showing Deadlocks] Situation: 
		
		
		public class DeadLock1Demo {
			public static Object lock1 = new Object();
			public static Object lock2 = new Object();

			public static void main(String[] args) {
				new Thread1().start();
				new Thread2().start();
			}

			static class Thread1 extends Thread {

				public void run() {
					System.out.println(Thread.currentThread().getName()+ " Started ...");
					synchronized (lock1) {
						System.out.println(Thread.currentThread().getName()+": Has Lock 1");
						try {
							Thread.sleep(1000);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
						System.out.println(Thread.currentThread().getName()+": Waiting for Lock 2");
						synchronized (lock2) {
							System.out.println(Thread.currentThread().getName()+": Has Lock 1 and Lock 2");
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
							System.out.println(Thread.currentThread().getName()+": Released Lock 2");
						}
						System.out.println(Thread.currentThread().getName()+": Released Lock 1");
					}
				}
			}

			static class Thread2 extends Thread {

				public void run() {
					System.out.println(Thread.currentThread().getName()+ " Started ...");
					synchronized (lock2) {
						System.out.println(Thread.currentThread().getName()+": Has Lock 2");
						try {
							Thread.sleep(1000);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
						System.out.println(Thread.currentThread().getName()+": Waiting for Lock 1");
						synchronized (lock1) {
							System.out.println(Thread.currentThread().getName()+": Has Lock 1 and Lock 2");
							try {
								Thread.sleep(1000);
							} catch (InterruptedException e) {
								e.printStackTrace();
							}
							System.out.println(Thread.currentThread().getName()+": Has Release Lock1");
						}
						System.out.println(Thread.currentThread().getName()+": Has Released Lock2");
					}
				}
			}
		}

	Output :

		Thread-0 Started ...
		Thread-0: Has Lock 1
		Thread-1 Started ...
		Thread-1: Has Lock 2
		Thread-0: Waiting for Lock 2
		Thread-1: Waiting for Lock 1
		
		
----------------------------------------------------------------

##	Deadlock Scenario 2 	


	Display display = new Display();
	Data data = new Data();
	
	display.setData(data);
	data.setDisplay(display);
	
-	In the below code deadlock is happening since two different threads will enter the sayHello by holding a lock on calling object(bharath and sharath)
-	Synchronized method will have intrinsic lock on "this" instance
-	Two Different threads will enter synchronized methods by getting hold of intrinsic lock on calling instance and waiting for each other resulting in DeadLock
-	Below program shows an example of Getting Locks in different order

		
	Code Snippet of DeadLock :
	
		
		Execution flow :
		
			1.	Thread1 acquires lock on Bharath object and enters sayHello() method
				It prints to console and then suspends
			2. Thread2 acquires lock on Sharath object and enters sayHello() method
				It prints to console and then suspends
			3.	Thread1 runs again and wants to sayHelloBack to Sharath Object. It then tries to call sayHelloBack() method with Sharath object ... but Sharath object has been already locked by Thread2, so Thread1 will be in BLOCKED state and get suspended.
			4.  Thread2 runs again and wants to sayHelloBack to Bharath Object. It then tries to call sayHelloBack() method with Bharath object ... but Bharath object has been already locked by Thread1, so Thread1 will be in BLOCKED state and get suspended.
			5.	Since Both Threads will end-up in Blocked Status ... it will result in Deadlock
		
		
		
		
		
		public class DeadLock2Demo {
			public static void main(String[] args) {
				PolitePerson bharath = new PolitePerson("Bharath");
				PolitePerson sharath = new PolitePerson("Sharath");
		//		bharath.sayHello(sharath);
		//		sharath.sayHello(bharath);
				
				// Java 8
				new Thread(()->bharath.sayHello(sharath)).start();
				new Thread(()->sharath.sayHello(bharath)).start();
			}
		}

		class PolitePerson {

			private String name;

			PolitePerson(String name) {
				this.name = name;
			}
			
			

			public synchronized  void sayHello(PolitePerson person) {
				System.out.println(Thread.currentThread().getName()+" Has Started sayHello");
				System.out.format("%s: %s has said hello to me%n" ,this.name, person.name);
				person.sayHelloBack(this);// Deadlock point
			}
			
			public synchronized  void sayHelloBack(PolitePerson person) {
				System.out.println(Thread.currentThread().getName()+" sayHelloBack");
				System.out.format("%s: %s has said hello back to me%n" , this.name, person.name);
			}
		}


	Output :

		Thread-0 Has Started sayHello
		Bharath: Sharath has said hello to me
		Thread-1 Has Started sayHello
		Sharath: Bharath has said hello to me

		
------------------------------------------------------------------------

## Thread Starvation

	
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
