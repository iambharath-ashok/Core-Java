Core Java



1.	JDK

	-	Install JDK - Java Developement Kit
	-	JDK comes with Compiler and JRE
		
		JRE - Java Runtime Environment
		
			-	JRE contains JVM and API 
			-	JVM uses JIT Compiler - Just In Time compiler to run the application efficiently 
			-	JRE provides runtime environment for compiled code or byte code to run
			-	JRE is like a duplicate OS or Virtual Machine
			-	JRE interprets the bytecode and converts it to the machine code for the underlying OS
			
			JVM - Java Virtual Machine

				-	In Java, Compiled code will be run on the JVM and directly on the OS
			
			
			API - Application Programming Interface
			
				-	Predefined and can use without knowing much background or how its been implemented
				-	Reading and writing files
					
					-	Java IO Library
				
		
		Compiler
		
			-	Compiler converts .java source file to .class byte code
			-	Byte code is a binary file and understood by JVM and will be run on the JVM
			
		
			
## 2.	Java Platform Independent

		-	We can't run c program compiled on Windows on Mac OS
		-	In java .java file will be coverted to .class file which is a intermediate file by compiler
		-	Bytecode is not a machine code for particular OS 
		-	Bytecode can be interpreted by Linux JVM for Linux OS .... Windows JVM will interpret the byte code to Windows OS
	 	
		
		-	Platform independent will comes from this additional step
		-	JVM uses JIT Compiler to translate the byte code to machine code
		
		
		#### Java is a platform independent language ... once compiled it can be run on any OS

		
## 3. Object Oriented Programming

	
		-	Each object has properties and behavior
		-	Properties are represented by fields 
		-	Behavior is represented by methods or functions
		
			-	Objects will communicate with each other through methods
			-	Information is exchanged through variables or fields and properties
			
		### Java is object oriented programming language

			-	Advantage -> Easy to map real world problems
			


##  4.	Principles of Object Oriented Programming

		1.	Encapsulation
		2.	Abstraction
		3.	Polymorphism
		4.	Inheritance
		
		
		### 1. Encapsulation
		
			-	Encapsulation is about protecting properties and functionalities from other objects
			-	Binding together properties and methods together
			-	In Java we achieve encapsulation using class
			
				Ex: Class
					{ 
						fields
						methods
					}
			
					
		### 2.	Inheritance 
			
			-	Inheritance is a process creating a new object using an existing object
			-	New object will inherit the properties and functionalities from existing object and can provide the new functionalities
			-	IS- A and Reusability is a terms used to represent inheritance
			
			Ex 
			
				Vehicle -> Car and Bus 
						Car -> Audi and BWM
						Bus -> Benz and Volvo
			
			##### -	In Java inheritance will done using extends keyword 
			##### - Advn of Inheritance is code reusability			
			
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
		
		
				
##  5.	Building blocks of Java

	
		-	Class
		-	Properties
		-	Methods
		-	Blocks
			
			
##	6.	Static Members and their Execution Control Flow

		
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
			
			
##	6.	Non-Static Members and their Execution Control Flow
			
			
	1.	Non-static Variables
	2.	Non-static Methods
	3.	Non-static blocks
	4.	Constructor
	
		- 	Instance blocks will get executed whenever a new instance will be created
		-	Instance block will get executed before the constructor
		
		
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

		
		#### this keyword


			-	this keyword is used to refer to the current object that is being invoking
			-	this keyword points to current object address
			-	When we invoke Constructor using new operator then Object address will be assigned to this keyword
			
				
				
				Code Snippet:
				
					ExperimentalClass() {
						System.out.println(Constructor: "+ this);
					}
					
					public static void main(String[] args) {
						ExperimentalClass experimentalClass = new ExperimentalClass();
						System.out.println("Main method : " + experimentalClass);
						experimentalClass.method1();
					}
			
			
				Output:
				
					Constructor: com.bharath.nonstatic.ExperimentalClass@71be98f5
					com.bharath.nonstatic.ExperimentalClass@71be98f5
					Main method : com.bharath.nonstatic.ExperimentalClass@71be98f5
					Method 1: com.bharath.nonstatic.ExperimentalClass@71be98f5
	
			
##	6.	Static vs Non-Static Members

	
		Static 
		
			-	Belongs to Classes
			-	Accessed using Class name
			-	Static blocks are executed at the time of Class loading
			-	Memory is allocated and initialized at the time of class loading
			
		Non-Static
			
			-	Belongs to Instances
			-	Accessed via Instance name
			-	Blocks are executed at the time of object creation
			-	Memory is allocated and initialized at the time of Object creation

##	7.	Data Type

	
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
	


##	8.	Wrapper Classes with  AutoBoxing and unboxing
	
	-	Wrapper Classes are used to convert primitive types to Object types
	-	Wrapper Classes are mainly required when we are working with Collection API	
	
		
		-	Each primitive type in Java has corresponding Wrapper class
		
		
		Primitive Type 						Wrapper Class
			byte								Byte
			short								Short
			int									Integer
			long								Long
			float								Float
			double								Double
			char								Character
			boolean								Boolean
			
			
	1.	Boxing 	-> Converting primitive type to Object type
	2.	Un-boxing ->	Converting Object type to primitive type
		
		Code Snippet : 	
			1.  Integer
			
				int i = 10;
				Integer integer = Integer.valueOf(i); //Boxing
				i = integer; //Un-Boxing
				i = integer.intValue(); //Un-Boxing
				
			2.	Short 
			
				short s = 200;
				Short sh1 = Short.valueOf(s); // Short short = Short.vauleOf(s); ---> Gives Compilation Error ... since short is a reserved keyword
				s = shortValue.shortValue();
			
			
	3.	String and Primitives

		long l = 20000000;
		String longString = Long.toString(l); // primitive to String
		l = longString.parseLong(longString); // String to Primitive
		
		
	4.	Wrapper Class Constructors

		-	Each Wrapper classes provided overloaded constructors
		-	One takes the primitive type and another as string as the argument to Wrapper class constructor
		
			Ex: 
				
				double d = 2999.553;
				Double dd = new Double(d);
				
				String s = "67584493.4232";
				Double dString = new Double(s);
			
			
			
##	9.	Operators and Assignments

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
		
	
##	9.	Flow Control Statement


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
			
			
				-	main() {
				
						l1 : {
						
							System.out.println("Block Begins");
							
							if(x == 20) {
								break l1; // Comes out of the l1 block 
								//	break can be used switch and looping blocks
							}
						}
					}



##	10. Access Modifiers

	-	Applicable for - Class, Methods, Constructors, Variables
	-	Private, Protected, Package, Public
	-	Access modifiers can't be used with blocks ... because blocks are executed by JVM 
	-	If no access specifier is specified then its by default will package level
	
	
		-	Classes
			
			-	Classes can only have Public and Package
			-	Classes can't mark with private ... because application or any other class can't access the private class
			-	Protected is used in inheritance ... used with methods and variables
		
		
			
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
		
	
	
	
##	10. Packages

	
	-	Packages are the folders used to place the related java files together
	-	Packages can have sub packages 
	
##	11. Event Management Use Case

	-	Entities
	
		-	Organizer
		-	Event
		-	Participants
		-	Venue
	
	
## 12. Inheritance

		
	1.	Single Inheritance
	2.	Multi-Level Inheritance
	3.	Hierarchical Inheritance
	4.	Method Overloading
	5.	Super Keyword
	6.	super() method
	7.	Constructor Chaining
	
		
		1.	Single Inheritance 
		
			-	Child Class Inheriting from Single Parent Class
			-	toString and hashCode methods are inherited from object class
			-	SingleInheritance Class inherits from java.lang.Object Class
			
			
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
			
		2.	Multi-Level Inheritance
			
			-	Inheritance by multiple level
			
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
			
		3.	Memory Allocation and Inheritance
			
			-	Two instances are created - one for parent and child 
			-	Both Child and Parent Instances share the same memory location
			
			#### Output for the above Program :
				*Parent Constructor* com.bharath.inheritance.*Child@71be98f5*
				*Child Constructor* com.bharath.inheritance.*Child@71be98f5*
				Parent Method
				Child Method

		4.	Hierarchical Inheritance
		
			
			-	Inheritance by Hierarchy and at several level
			
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
				
		5.	Method Overriding

			-	fuel method has been overridden in the above examples
			
		6.	super Keyword 

			-	super keyword is used to access the parent class members
			
			public class Child extends Parent {
				Child() {
					System.out.println("Child Constructor "+this);
				}
				void childMethod() {
					*super.parentMethod();*
					System.out.println("Child Method");
				}
			}

		
		7.	super() method
		
			-	super() is used in the constructor of child class to invoke the parent class constructor explicitly
			-	super() can also be used for constructor chaining
			
			
		8.	Constructor Chaining
		
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
		-	join() is a instance method	
		
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









			














































































			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
			
		
		

		

			
 
		
		
	
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
		
