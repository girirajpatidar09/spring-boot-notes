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


## @RequestParam 

   @RequestParam is used to get data from query parameters (URL) and bind it to method arguments.
   
      @RestController
        public class MyController 
		{

			@GetMapping("/greet")
			public String greet(@RequestParam String name)
			{
				return "Hello " + name;
			}
       }
	   
	   
	   The framework automatically performs type conversion from the request parameter’s string representation to the specific type.

			1 Primitive types : such as int ,long , float,  double etc .
			2 Wrapper classes : Such as Integer , Long , float ,Double, Boolean etc .
			3 String : Request parameters are inherently treated as string only.
			4 Enums : you can bind request parameters to enum types.
			5 Custom Object types : We can do it using a registered PropertyEditor.
			
		
		How to used PropertyEditor ?
		<img width="602" height="466" alt="b1" src="https://github.com/user-attachments/assets/521a1177-3005-4d61-8a0a-e0152db33634" />
		


## @PathVariable

@PathVariable is used in Spring MVC / Spring Boot to extract values from the URL path and bind them to method parameters.

    Example :
	
	    @RestController
        @RequestMapping("/users")
         public class UserController 
		 {

          @GetMapping("/{id}")
           public String getUser(@PathVariable int id) 
		   {
             return "User ID: " + id;
           }
         }
		 
		 
		 http://localhost:8080/users/101
		 
		 
##  @RequestBody

@RequestBody is used to read data from the HTTP request body (usually JSON) and convert it into a Java object.

			✅ 📌 Simple Explanation

			When client sends data inside request body (POST/PUT), we use @RequestBody.

			👉 Example request (JSON):

			{
			  "name": "Giriraj",
			  "age": 22
			}
			
			
			 
			@RestController
            @RequestMapping("/users")
            public class UserController 
			{

              @PostMapping
             public String createUser(@RequestBody User user)
			 {
              return "User created: " + user.getName();
              }
               }
			   
			   
			   
			   public class User {
				private String name;
				private int age;

				// getters and setters
               }
			   
			   

## ResponseBody 

			ResponseEntity in Spring Boot

			ResponseEntity is used to control the full HTTP response:
			✔ Status code
			✔ Response body
			✔ Headers
			
			
			✅ 📌 Basic Example
			@RestController
			@RequestMapping("/users")
			public class UserController 
			{

				@GetMapping("/{id}")
				public ResponseEntity<String> getUser(@PathVariable int id)
				{
					return ResponseEntity.ok("User ID: " + id);
				}
			}
			
			
			
			✅ 📌 Custom Status Example
			@GetMapping("/{id}")
			public ResponseEntity<String> getUser(@PathVariable int id) {

				if (id <= 0) {
					return ResponseEntity.badRequest().body("Invalid ID");
				}

				return ResponseEntity.ok("User ID: " + id);
			}
			
			
			✅ 📌 Returning Object
			@PostMapping
			public ResponseEntity<User> createUser(@RequestBody User user) {
				return ResponseEntity.status(201).body(user);
			}
			
			
			✅ 📌 With Headers
			@PostMapping
			public ResponseEntity<String> createUser() {
				return ResponseEntity
						.status(201)
						.header("Custom-Header", "Value")
						.body("User Created");
			}


		 



		
## What is Inversion of control   ?
“IoC (Inversion of Control) is a design principle where the responsibility of object creation and dependency management is shifted from the
 developer to a framework or container
In Spring, this container is called the IoC Container, which creates, configures, and manages beans.
The main IoC containers in Spring are BeanFactory and ApplicationContext, wApplicationContext being the most commonly used.”

## What is Dependency Injection ?
 Dependency Injection (DI) is a design pattern in which an object’s dependencies (Beans )are provided (injected) by an external source such as an 
 IoC container 
Constructor based  and setter based dependency Injection or field based.

## Tips……………….
•	Spring IoC Container can be configured either via XML or Java annotations/configuration.
•	DI works the same in both; only configuration style differs.
•	Java configuration is preferred in Spring Boot.
•	Example: @Bean methods or @Component with @Autowired.
•	<spring.version>6.1.10</spring.version>(used in property tags )
Wherever required in pom.xml use <version>${spring.version}</version>



##   What is Auto Scanning ?
Auto scanning (or component scanning) is a feature in Spring where the Spring container automatically detects classes annotated with stereotypes like @Component, @Service, @Repository, or @Controller and registers them as beans in the IoC container.
 Goal: Avoid manually declaring every bean in XML or Java configuration.


## @ComponentScan
@ComponentScan is a Spring annotation that tells the IoC container to scan specific packages for classes annotated with stereotypes like:
@Component, @Service, @Repository, or @Controller
and automatically register them as beans.

@Component is a basic and general sterotype annotation.
@Repository – Used for tagging Repository classes(classes which contain logic to interact with database).
@Service- Used for tagging  Service classes(which contain business logic).
@Controller – Used for tagging Controller classes(classes which contains API’s)


-> @RestController and @Controller are aliases  of @Component   but their additional feature is they handle HTTP requests.

-> @Repositoy is alias of @Component but additional is that it converts checked persistence exceptions into unchecked DataAccessException.

-> @Service has no extra feature as alias of @Component  is is just for the readability purpose



#  Bean and its Lifecycle :

	@Configuration :
 “@Configuration tells Spring this class contains bean definitions that should be managed by the IoC container.”

	@Bean:
“@Bean creates and registers a Spring-managed object from a method inside a @Configuration class.”

<img width="602" height="332" alt="b2" src="https://github.com/user-attachments/assets/b0a10b8c-aae0-4c05-83d3-baa629e0e8cc" />

<img width="602" height="481" alt="b3" src="https://github.com/user-attachments/assets/8d858ed6-151a-48e1-8e2f-731434bd8083" />


      
			@Component
			public class User {
				
				String name;
				int id;
				public String getName() {
					return name;
				}
				public void setName(String name) {
					this.name = name;
				}
				public int getId() {
					return id;
				}
				public void setId(int id) {
					this.id = id;
				}
				
				}
				
		   -> This above example works fine .
		   
		   When Spring tries to create a bean using @Component, it needs to instantiate the class using reflection — and by default, it looks for 
		   a no-argument constructor.
		   
		   
		   
		  


					@Component
					public  class User {
						
						int id;
						String name;
						public User(int id, String name) {
							super();
							this.id = id;
							this.name = name;
						}
						public int getId() {
							return id;
						}
						public void setId(int id) {
							this.id = id;
						}
						public String getName() {
							return name;
						}
						public void setName(String name) {
							this.name = name;
						}
						}
						
						***************************
                        APPLICATION FAILED TO START
						***************************
						
					If a class has exactly ONE constructor, Spring will automatically use it for injection — BUT only if the parameters can be
					satisfied from the Spring context (i.e., they are Spring beans).
					
					int id → primitive, not a Spring bean ❌
                  String name → not a Spring-managed bean ❌

               Spring cannot find values to inject for these parameters from the Application Context, so it fails to instantiate the bean entirely.


        -> How to fix this above problem :
   
      
		✔️ Option 1: Add Default Constructor (Easiest)
		public User() {
		}
		
		✔️ Option 2: Use @Value (for fixed values)
		@Component
		public class User {

			int id;
			String name;

			public User(@Value("1") int id, @Value("Giriraj") String name) {
				this.id = id;
				this.name = name;
			}
		}

		
		
		 @Bean can also solve that problem of application started failde, because  spring boot does not know what to these
		 constructor
		 
		 So @Bean comes in the picture ,where we provide the configuratin details and tells Spring boot to use
		 it while creating a Bean .
		 
		 
		 @Configuration
         public class Config {

			@Bean
			User createUserBean()
			{
				
				 String name = "ram";
				 return new User(101,name);
				
	         }
			 }
			 
			 
			 
			 
			
			public  class User {
	
				int id;
				String name;
				
				
				public User(int id,String name)
				{
					this.id = id;
					this.name = name;
					System.out.println("Giriraj Patidar");
				}
				public int getId() {
					return id;
				}
				public void setId(int id) {
					this.id = id;
				}
				public String getName() {
					return name;
				}
				public void setName(String name) {
					this.name = name;
				}
				}

                -------------------------------------------------------------------------------------------------------------
				
			Configuration
				public class Config {

					@Bean
					User createUserBean()
					{
						
						 String name = "ram";
						 return new User(101,name);
						
					}
					
					
					@Bean
					
					User createAnotherUserBean()
					{
						
						 String name = "sita";
						 return new User(102,name);
						
					}
					
		   Here two objects are created 
		   
		   ---------------------------------------------------------------------------------------------------------------------
		   

## 🕒 At what time these beans get created

### Eagerness

-> Some Beans get created, When we start up an application.

-> For ex: Beans with Singleton Scope are Eagerly initialized.


### Lazy

-> Some Beans get created Lazily, means when they actually needed.

-> For ex: Beans with Scope like Prototype etc. are Lazily initialized.
   Or
   Beans with @Lazy annotation.
   
        Example :
		
		@Lazy
		@Component
		public class Order {

			public Order() {
				System.out.println("initializing Order");
			}
		}
		

## lifecycle of Bean

        -Application Start 
		
        → IOC Container Started 
            (Configuration Loaded)
			
        → Construct Bean 
		
        → Inject Dependency Into Constructed Bean 
		
        → @PostConstruct 
		
        → Use the Bean 
		
        → @PreDestroy 
		
        → Bean Destroyed
		

### Step 1: IOC Container Initialization

-> During Application Startup, Spring Boot invokes IOC Container
   (ApplicationContext provides the implementation of IOC container)

-> IOC Container makes use of Configuration and @ComponentScan
   to look out for the classes for which beans need to be created
   
   
🖥️ Console Output (IOC Container Invoked)
main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat initialized with port 8080 (http)
main] o.apache.catalina.core.StandardService  : Starting service [Tomcat]
main] o.apache.catalina.core.StandardEngine   : Starting Servlet engine: [Apache Tomcat/10.1.19]
main] o.a.c.c.C.[Tomcat].[localhost].[/]      : Initializing Spring embedded WebApplicationContext
main] o.s.c.ServletWebServerApplicationContext : Root WebApplicationContext: initialization completed in 419 ms
main] o.s.b.w.embedded.tomcat.TomcatWebServer  : Tomcat started on port 8080 (http) with context path ''
main] c.c.i.SpringbootApplication             : Started SpringbootApplication in 0.771 seconds (pro


###  Step 2: Construct the Beans

📦 Bean Class Example
@Component
public class User {

    public User() {
        System.out.println("initializing user");
    }
}


Cosole output 


2026-04-03T16:22:42.413+05:30  INFO 29308 --- [Demo2] [           main] com.giriraj.Demo2Application             : Starting Demo2Application using Java 17.0.12 with PID 29308 (C:\Pratice STS\Demo2\target\classes started by girir in C:\Pratice STS\Demo2)<br>
2026-04-03T16:22:42.417+05:30  INFO 29308 --- [Demo2] [           main] com.giriraj.Demo2Application             : No active profile set, falling back to 1 default profile: "default".<br>
initializing user<br>
2026-04-03T16:22:42.905+05:30  INFO 29308 --- [Demo2] [           main] com.giriraj.Demo2Application             : Started Demo2Application in 0.886 seconds (process running for 1.387)<br>



### Step 3: Dependency Injection

-> Inject the Dependency into the Constructed Bean

-> @Autowired first looks for a bean of the required type

-> If bean is found, Spring will inject it.
   Different ways of Injection:
     □ Constructor Injection
     □ Setter Injection
     □ Field Injection

****** We will see each injection and which one to use in next part ******

-> If bean is not found, Spring will create one and then inject it




📦 Example Code
👤 User Class
@Component
public class User {

    @Autowired
    Order order;

    public User() {
        System.out.println("initializing user");
    }
}



📦 Order Class (Lazy Initialization)
@Lazy
@Component
public class Order {

    public Order() {
        System.out.println("Lazy: initializing Order");
    }
}


Here Constructor is called then beasn is injected

		
		

Output at startup of application :
initializing user
Lazy: initializing Order


###  Step 4: Perform tasks before Bean is used

 Perform any task before Bean to be used in application.
 
 
@Component
public class User {

    @Autowired
    Order order;

    @PostConstruct
    public void initialize() {
        System.out.println("Bean has been constructed and dependencies have been injected");
    }

    public User() {
        System.out.println("initializing user");
    }
}




@Lazy
@Component
public class Order {

    public Order() {
        System.out.println("Lazy: initializing Order");
    }
}



Output ::
initializing user
Lazy: initializing Order
Bean has been constructed and dependencies have been injected
		  
		 
		   
					

		   
		   
		   
	








	   

	
		

	   

	   
	   

		
	   
	   
	   
	   
	   

			







			
			
			

				















   

  
  






