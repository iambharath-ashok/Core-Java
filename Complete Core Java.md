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
		








































			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
		
		

		

			
 
		
		
	
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
