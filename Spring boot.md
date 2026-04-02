# Spring Boot :

## Singleton Design , Singleton Pattern  and Singleton class :
Singleton  pattern is a pattern in which we restrict a class to have  only  one object (instance) throughout the application  for this we 
have to provide the private constructor and factory  method .

->We use Singleton  pattern for better performance according to given condition , like in case of database connection.<br>
->In singleton pattern we have two types  of initialization Eager and Lazy.
  
### Lazy initialization 
    
     class Singleton
	{
	  static Singleton single;
	  
	  private Singleton()
	  {
	    
	  }
	  public static  Singleton getObject()
	  {
	    if(single==null)
		{
		 single = new Singleton();
		}
		return single;
	  }
	  
	}
	class demo
	{
	 public static void main(String ar[])
	 {
	   Singleton  single1= Singleton.getObject();
	   Singleton  single2= Singleton.getObject();
	   System.out.println(single1.hashCode());
	   System.out.println(single2.hashCode());
	   System.out.println(single1==single2);
	   
	 }
	}
	Output : 918221580
             918221580
             true
			 
			 
### Eager initialization
   
     class Singleton
	{
	  static Singleton single= new Singleton();
	  
	  private Singleton()
	  {
	    
	  }
	  public static  Singleton getObject()
	  {
	    
		return single;
	  }
	  
	}
	class demo
	{
	 public static void main(String ar[])
	 {
	   Singleton  single1= Singleton.getObject();
	   Singleton  single2= Singleton.getObject();
	   System.out.println(single1.hashCode());
	   System.out.println(single2.hashCode());
	   System.out.println(single1==single2);
	   
	 }
	}
	Output :: 918221580
			  918221580
			  true



#  Coupling ::
Coupling refers to how strongly one class or module depends on another. Loosely coupling is preferred because it improves flexibility, 
maintainability, and reusability.

## Loose coupling :
   Loose coupling means that classes or modules are minimally dependent on each other and interact through interfaces or abstractions,
   not through direct implementations.
   
## Tight coupling:
Tight coupling means that one class is strongly dependent on another class’s implementation, so changes in one class directly affect the
 other.
 
 
### Let's understand  Tight coupling with an example :

      Suppose your senior gives you a task to read data from datbase,se making a dummy example not actual database connectivity.
	  
            
		class DbReader
		{
		   public void show()
		   {
		   System.out.println("Database data..");
		   }
		   
		}
		
		class Reader
		{
		  DbReader db ;
		  public Reader(DbReader db)
		  {
		    this.db=db;
		  }
		  public void readData()
		  {
		  db.show();
		  }
		}
		
		class TightCoupling
		{
		  public static void main(String ar[])
		  {
		     Reader rd = new Reader(new DbReader());
			 rd.readData();
		  }
		}
		
		Output : Database data...
		
		Here in above example Reader class is directly dependent on DbReader.Now suppose your senior tell that you have to read data from 
		Excel then lots of change  we have to perform in code.
		
		         class DbReader
		{
		   public void show()
		   {
		   System.out.println("Database data..");
		   }
		   
		}
		
		class ExReader
		{
			public void show()
			{
				System.out.println("Excel data...");
			}
		}
		
		class Reader
		{
		  ExReader ex ;
		  public Reader(ExReader ex)
		  {
		    this.ex=ex;
		  }
		  public void readData()
		  {
		  ex.show();
		  }
		}
		
		class TightCoupling
		{
		  public static void main(String ar[])
		  {
		     Reader rd = new Reader(new ExReader());
			 rd.readData();
		  }
		}
		
		Output : Excel data...
		
	  
	  Here , in above example we see lots of problem because the classes are dependent on direct implementation.
	  So the solution is loose  coupling.
	  

### Let's see  the solution for above problem with the help of loose coupling :

         interface Reading 
		{
			void show();
		}
		class DbReader implements Reading
		{
		   public void show()
		   {
		   System.out.println("Database data..");
		   }
		   
		}
		
		class ExReader implements Reading 
		{
			public void show()
			{
				System.out.println("Excel data...");
			}
		}
		
		class Reader 
		{
			Reading  rd ;
			public Reader(Reading  rd)
			{
				this.rd=rd;
				
			}
			
			public void readData()
			{
				rd.show();
			}
		}
		
		
		
		
		class LooseCoupling
		{
		  public static void main(String ar[])
		  {
		     Reader rd1 =  new Reader(new DbReader());
			 rd1.readData();
			 
			 Reader  rd2 = new Reader( new ExReader());
			 rd2.readData();
		  }
		}
		
		Output : Database data..
                 Excel data...
				

# Why  Spring Boot exists and how it is differ from Spring Framework  ?

## What is Servlet ?
 
   A Servlet in Java is a server-side component used to handle HTTP requests and generate responses, most commonly for web applications.
   A Servlet is a Java class that runs on a web server and handles web requests using HTTP.

## 	What is Servlet Container (Manages Servlet)? 

A Servlet Container is a part of a web/application server that loads servlets, handles HTTP requests, and manages their lifecycle. Basically Servlet Container manages the servlets.
You write the Servlet.The container does everything else.

## **NOTE**

Apache is an server and inside Apache there is tomcat which is container that is responsible to handle servlet.



<img width="826" height="287" alt="servlet-container" src="https://github.com/user-attachments/assets/ad5ed1ab-3ef8-43c6-9a57-23e9892e56ad" />

## Headache in Servlets 

<img width="873" height="841" alt="Screenshot 2026-04-01 202902" src="https://github.com/user-attachments/assets/5de96e70-8f37-4da6-8892-48676c6bb692" />

 
If we are using Servlet then to map it in Servlet container  we have to provide information in web.xml that is used by Servlet container  it create
a lots of code like  servlet name, class and URL  lots of thing we have to  remember .

  localhost:8080/ProjectName folder name/endpoints
  
## Key point : 
 
  -> What is @WebServlet?<br>
   @WebServlet is a Java annotation used to declare and configure a Servlet directly in code, without using web.xml.
   
    It tells the Servlet Container :
    “This class is a Servlet, and this is the URL that should trigger it.”
	
## 	To solve the issue of Servlet,  Spring MVC comes into the picture  which is the part of Spring Framework .

<img width="872" height="615" alt="a1" src="https://github.com/user-attachments/assets/f81cf922-5e34-42a3-987c-d2825b72e72f" />

<img width="869" height="804" alt="a2" src="https://github.com/user-attachments/assets/fd3427da-3666-4e9e-89f7-8ec6bd9f09cd" />

<img width="744" height="765" alt="a3" src="https://github.com/user-attachments/assets/c820474b-4d87-4013-8518-7bf7e34aeb97" />

<img width="873" height="338" alt="a4" src="https://github.com/user-attachments/assets/db88718a-1675-4979-94cc-7008d6f39664" />

<img width="884" height="869" alt="a5" src="https://github.com/user-attachments/assets/0e109b45-7ff7-4fc6-b61d-3c89877f85ab" />

<img width="1379" height="775" alt="a6" src="https://github.com/user-attachments/assets/844022e3-f2f6-442d-b5c7-8e8810a95f9c" />


## Spring Boot Solves problems of Spring Framework

<img width="934" height="721" alt="p1" src="https://github.com/user-attachments/assets/ef8872f9-a4e8-48b1-8535-7c3553ecbcc1" />

<img width="851" height="372" alt="p2" src="https://github.com/user-attachments/assets/0bcf5844-cfa5-47fe-a524-0dc5bdca56fd" />

<img width="815" height="572" alt="p3" src="https://github.com/user-attachments/assets/cd91355c-0f33-4cd0-a41b-d062824501b1" />

<img width="854" height="718" alt="p4" src="https://github.com/user-attachments/assets/73044edb-be00-45b6-a68b-57a08a95b95e" />

<img width="1379" height="777" alt="p5" src="https://github.com/user-attachments/assets/298a3fb9-530f-431f-89b2-b792d97c0c15" />

Note :  If you are implementing Spring MVC and Spring REST with Spring boot then no need to worry about Dispatcher Servlet(Front Contoller) 
        spring boot will take care  of that.
		
		

##Spring Framework vs Spring boot
Spring Framework is the core framework that provides powerful features like IoC, DI, and AOP, but it requires a lot of manual configuration.
Spring Boot is built on top of the Spring Framework. It simplifies the development process using auto-configuration, starter dependencies, and an 
embedded server, which allows you to build and deploy applications quickly with less boilerplate code.”

		Spring :
		✅ Key Features:
		•	Provides core features like IoC, DI, AOP, transaction management.
		•	Uses XML or Java-based configuration.
		•	Requires manual setup (Tomcat, WAR deployment, DispatcherServlet, etc.).
		•	More control over configuration and components.
		•	Not opinionated → You decide the structure and dependencies.
		🧰 Example:
		•	You create applicationContext.xml or @Configuration classes manually.
		•	Configure DispatcherServlet manually in web.xml.
		•	Add required dependencies one by one.


		Spring Boot :
		✅ Key Features:
		•	Auto Configuration – Reduces boilerplate code.
		•	Starter Dependencies – No need to add each dependency manually.
		•	Embedded Server (like Tomcat/Jetty) → No need for external server setup.
		•	Production-ready (Actuator, metrics, health checks).
		•	Opinionated defaults → ready-to-use project structure.
		🧰 Example:
		•	You just create a @SpringBootApplication class and run it.
		•	No web.xml or manual XML configuration.
		•	Built-in Tomcat starts automatically


## Setting up Spring project :

			Go to spring initializer i.e. start.spring.io
			Project Metadata (Spring Boot)
			•	Group
			👉 Your company or organization name (used as base package)
			Example: com.example
			
			•	Artifact
			👉 The project name / jar name
			Example: demo → creates demo.jar
			
			•	Name
			👉 Display name of the project
			Usually same as artifact
			
			•	Description
			👉 Short explanation of what your project does
			
			•	Package Name
			👉 Java package where your code starts
			Example: com.example.demo

			Packaging
			•	Jar ✅
			👉 Standalone application (most common in Spring Boot)
			•	War
			👉 Used when deploying to external servers (Tomcat)
			
			
 
##    What are standalone Applications ?
A standalone application is an application that contains everything it needs to run and can be started directly.

			Standalone application in Java (Spring Boot) ☕
			In Spring Boot:
			•	You run the app using:
			•	java -jar demo.jar
			•	No need to install Tomcat separately
			•	The server is embedded inside the app
			👉 That’s why Spring Boot apps are called standalone
			
			
## What are  jar files ?
				JAR stands for Java ARchive.
				👉 A JAR file is a single file that contains:
				•	Java .class files
				•	Libraries
				•	Configuration files
				•	Resources (images, properties, etc.)
				All packed together like a ZIP file.
				A JAR file is used to package Java applications so they can be run easily as one file.
				

## JAR in Spring Boot 🚀
				Spring Boot creates a fat JAR (executable JAR):
				It contains:
				•	Your application code
				•	Embedded Tomcat
				•	All dependencies
				Run it like:
				java -jar demo.jar
				👉 No need to install Tomcat separately
				👉 This is called a standalone application
				

##  What  are  war files ?
    A WAR file is used to package and deploy Java web applications on an external web server.
	
      ->What does a WAR file contain?
			A WAR file includes:
			•	Servlets
			•	JSP files
			•	HTML / CSS / JS
			•	WEB-INF folder
			o	web.xml
			o	classes
			o	lib (JAR dependencies)
			📦 Everything needed for a web app, but NOT the server.
			
	 
	 -> Example 🧩
		Project structure (before WAR)
		myapp/
		 ├── src/
		 ├── WEB-INF/
		 │    ├── web.xml
		 │    └── lib/
		 └── index.jsp
		After building:
		myapp.war
		
		
     ->How to use WAR 🚀
		1.	Install Tomcat
		2.	Copy myapp.war into:
		3.	tomcat/webapps/
		4.	Start Tomcat
		5.	Open browser:
		6.	http://localhost:8080/myapp
		✅ App runs inside Tomcat

		Note : JAR is used for standalone applications, while WAR is used for web applications deployed on external servers.
	
	

##  Quick Comparison
| File Type | Application Type             | Server Needed |
|---------- |------------------------------|---------------|
| JAR       | Standalone / Microservices   | ❌ No         |
| WAR       | Web / Enterprise apps        | ✅ Yes        |


NOTE -> 
In modern Spring Boot applications, we often use JAR files with embedded servers, making deployment simpler. WAR is still used when deploying to 
external enterprise servers.”


# Layered Architecture

<img width="602" height="308" alt="a1" src="https://github.com/user-attachments/assets/c2ad36fe-8538-4f07-b42b-a0faf55f195e" />




## What is Maven ?
It is a project Management tool , help developers with :
•	Build generation.
•	Dependency resolution.
•	Documentation etc .
-Maven uses POM (Project Object Model) to achieve this.
-When  “maven” command is given , it looks for “pom.xml” in the current directory and get needed configuration.


##  Why maven ?
Maven is used because it automates builds, manages dependencies, enforces project standards, and integrates easily with CI/CD—making Java projects
reliable and scalable in teams.
 
		✅ 1. Automatic dependency management
		Instead of downloading JARs manually, you declare them once in pom.xml.
		Maven:
		•	downloads libraries for you
		•	pulls their dependencies (transitive deps)
		•	handles versions & conflicts
		👉 Result: consistent builds across every developer and CI server.
		
		✅ 2. One command builds everything
		Run:
		mvn clean install
		Maven automatically:
		•	cleans old output
		•	compiles code
		•	runs tests
		•	packages the app
		•	installs it locally
		No custom scripts needed.
		
		
		✅ 3. Standard project structure
		Every Maven project looks the same:
		src/main/java
		src/test/java
		pom.xml
		👉 New developers can jump in immediately.
	
	
		✅ 4. Huge plugin ecosystem
		Maven uses plugins to do real work:
		•	compile Java
		•	run unit tests
		•	generate coverage
		•	build fat JARs
		•	integrate with Docker
		•	publish artifacts
		You configure once—reuse everywhere.
		
		
		✅ 5. CI/CD friendly (enterprise favorite)
		Build servers simply run Maven commands.
		Typical flow:
		Developer → Git → CI → mvn package → artifact repo → deploy
		This repeatability is why enterprises love Maven.
		
		
		✅ 6. Single source of truth (pom.xml)
		Everything lives in one place:
		•	dependencies
		•	versions
		•	plugins
		•	build rules
		•	environment profiles
		No guessing. No hidden configs.
		

# Annotations in Spring Boot 

## What is Annotation ?

			In Java, an annotation is a special type of metadata (data about data) that provides additional information about code.
			                              OR
			Annotations in Java are metadata that provide information about code to the compiler or runtime without changing its logic.

			👉 It does not directly affect program execution, but it helps:

			Compiler (for checking errors)
			Tools (like frameworks)
			Developers (for understanding code)
			
			Examples of built-in annotations:
			•	@Override
			•	@Deprecated
			•	@SuppressWarnings
			
			

## Why Do We Need Custom Annotations?

		Custom annotations are used when built-in annotations are not enough and we want to:
		1.  Add application-specific metadata
		2.  Reduce boilerplate code
		3.  Improve readability
		4.  Support frameworks (validation, logging, security, mapping, etc.)
		5.  Implement cross-cutting concerns using AOP or reflection

## How to generate custome annotationa ?
 Custom annotation is a user-defined metadata used to add application-specific information to classes or methods. We create it using @interface 
 along with @Retention and @Target. It doesn’t change logic directly but is processed using reflection or frameworks like Spring. Custom annotations
 help reduce boilerplate, improve readability, and implement features like validation, logging, and security.
 

##  @ SpringBootApplication 

		@SpringBootApplication is a convenience annotation that combines three important Spring annotations:
		@SpringBootApplication= @SpringBootConfiguration advanced version of @Configuration
		+ @EnableAutoConfiguration
		+ @ComponentScan
		So basically, instead of writing these three annotations separately, you can just use one 
_
			🧠 What each part does:
			1.	@Configuration 🧱
				Tells Spring that this class contains bean definitions.
				Works like applicationContext.xml in traditional Spring.
			
			2.	@EnableAutoConfiguration ⚡
				Tells Spring Boot to automatically configure beans based on the dependencies in the classpath.
				Example: If spring-boot-starter-web is present → Spring Boot auto-configures Tomcat, DispatcherServlet, etc.
			
			3.	@ComponentScan 🔍
				Tells Spring to scan the current package and its subpackages for components (@Component, @Service, @Controller, etc.) and make them 
			   beans automatically.
			   

##  @Controller :
			@Controller is a Spring MVC annotation used to mark a class as a web controller — a component that:
			•	receives HTTP requests
			•	processes them
			•	returns a view name (HTML/JSP/Thymeleaf) or a Model
			
			
			
			Example :
			
					@Controller
		            public class HomeController 
					{
                      @GetMapping("/home")
					  
			          public String home(Model model) 
					  {
					  model.addAttribute("message", "Hello Spring!");
				       return "home"; // resolves to home.html / home.jsp
		               }
					}
					
			
		 
		 Note :  To send data directly here we have to use ResponseBody with Controller 
		 
		     
			  Example :
			  
			   @Controller
               public class MyController 
			   {

				@RequestMapping("/hello")
				@ResponseBody
                public String hello() {
                return "Hello Giriraj!";
                  }
               }
			   
		
		 🔍 How it works
			@Controller → tells Spring this is a web controller
			@ResponseBody → tells Spring:
			👉 “Don’t return a view (HTML/JSP), return data directly”
			

##  @RestController 
 
             
			Example :
			
			@RestController
			public class MyController {

				@GetMapping("/hello")
				public String sayHello() {
					return "Hello Giriraj!";
				}
			}
			
			
			🔍 What happens here?
			@RestController 👉 Combines:
			@Controller
			@ResponseBody

			👉 So no need to write @ResponseBody separately

			@GetMapping("/hello") 👉 Creates API endpoint
		

##  @RequestMapping

    @RequestMapping is used in Spring MVC / Spring Boot to map HTTP requests (URLs + methods) to specific controller methods.
     When a client hits a certain URL (like /users), @RequestMapping tells Spring which Java method should handle that request.
	 
	  -> Basic Example :
	    
		@RestController
       public class MyController 
	   {

          @RequestMapping("/hello")
        public String hello() 
		{
        return "Hello World!";
        }
       }
	   
	   
	  -> Example with HTTP Method
	  
	    @RestController
        public class UserController 
		{

         @RequestMapping(value = "/user", method = RequestMethod.GET)
			public String getUser() {
				return "GET User";
                }

			@RequestMapping(value = "/user", method = RequestMethod.POST)
			public String createUser() {
				return "POST User";
			}
        }
		
		
		-> Class-Level + Method-Level Mapping
		
		@RestController
        @RequestMapping("/api")
       public class MyController 
	   {

         @RequestMapping("/hello")
        public String hello()
	     {
        return "Hello API!";
         }
       }
	   http://localhost:8080/api/hello
	   
	   
	   @RequestMapping Default HTTP Methods
		When you use @RequestMapping without specifying a method, it maps to ALL HTTP methods by default.
		This means the endpoint will accept:

			GET
			POST
			PUT
			DELETE
			PATCH
			HEAD
			OPTIONS
			TRACE
			
			
		🔷 1. Class-Level @RequestMapping

       👉 Applied on the class
       👉 Defines a base URL (common prefix) for all methods inside the controller
	   
	   
	   🔷 2. Method-Level @RequestMapping

	   👉 Applied on individual methods
	   👉 Defines the specific endpoint
		
	   
	   
	   
	   
	   

			







			
			
			

				















   

  
  






