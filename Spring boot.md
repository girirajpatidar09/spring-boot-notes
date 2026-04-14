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


## 📌 Bean Creation with Constructors (Important Concept)

---

## ✅ Case 1: Default Constructor (Works Fine ✔️)

```java
@Component
public class User {

    private String name;
    private int id;

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
```

### 💡 Why this works?

- Spring uses **reflection** to create objects  
- It looks for a **no-argument constructor**  
- Since default constructor is available → Bean is created successfully ✅

---

## ❌ Case 2: Parameterized Constructor (Fails ❌)

```java
@Component
public class User {

    private int id;
    private String name;

    public User(int id, String name) {
        this.id = id;
        this.name = name;
    }
}
```

---

### 💥 Error

```
APPLICATION FAILED TO START
```

---

### ❓ Why it fails?

- Spring tries to use the **only constructor**
- But parameters must be **Spring beans**

```
int id     → ❌ Not a bean
String name → ❌ Not a Spring-managed bean
```

👉 Spring cannot resolve these dependencies → **Bean creation fails**

---

## 🧠 Important Rule

> If a class has **only one constructor**, Spring will use it automatically  
> BUT only if all parameters can be resolved from the Spring container

---

## ✅ How to Fix This?

---

### ✔️ Option 1: Add Default Constructor (Easiest)

```java
public User() {
}
```

👉 Now Spring can use default constructor

---

### ✔️ Option 2: Use `@Value`

```java
@Component
public class User {

    private int id;
    private String name;

    public User(@Value("1") int id, @Value("Giriraj") String name) {
        this.id = id;
        this.name = name;
    }
}
```

👉 Injects fixed values from configuration

---

### ✔️ Option 3: Use `@Bean` (Best for Custom Object Creation 🔥)

```java
@Configuration
public class Config {

    @Bean
    public User createUserBean() {
        String name = "Ram";
        return new User(101, name);
    }
}
```

---

### 📦 User Class

```java
public class User {

    private int id;
    private String name;

    public User(int id, String name) {
        this.id = id;
        this.name = name;
        System.out.println("User created");
    }

    // getters & setters
}
```

---

## 🔥 Multiple Beans Example

```java
@Configuration
public class Config {

    @Bean
    public User createUserBean() {
        return new User(101, "Ram");
    }

    @Bean
    public User createAnotherUserBean() {
        return new User(102, "Sita");
    }
}
```

---

### 💡 Result

- Two `User` beans are created:
  - `createUserBean`
  - `createAnotherUserBean`

---

## 🎯 Final Summary

- Default constructor → ✅ works automatically  
- Parameterized constructor → ❌ fails if params are not beans  
- Use:
  - `@Value` → for fixed values  
  - `@Bean` → for manual object creation  
- Multiple `@Bean` → multiple objects created  

---
		   

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

 Bean Class Example

```java
@Component
public class User {

    public User() {
        System.out.println("initializing user");
    }
}
```


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




## 📦 Example Code

 User Class

```java
@Component
public class User {

    @Autowired
    private Order order;

    public User() {
        System.out.println("initializing user");
    }
}
```

---

 Order Class (Lazy Initialization)

```java
@Lazy
@Component
public class Order {

    public Order() {
        System.out.println("Lazy: initializing Order");
    }
}
```



Here Constructor is called then beasn is injected

		
		
```text
Output at startup of application :
initializing user
Lazy: initializing Order
```


###  Step 4: Perform tasks before Bean is used

 

Perform any task before the Bean is used in the application.

---

### Code Example

```java
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
```

```java
@Lazy
@Component
public class Order {

    public Order() {
        System.out.println("Lazy: initializing Order");
    }
}
```

---

 Output

```text
initializing user
Lazy: initializing Order
Bean has been constructed and dependencies have been injected
```



##  Step 6: Perform tasks before Bean is getting destroyed

---

### 🚀 Main Class (Closing IOC Container)

```java
@SpringBootApplication
public class SpringbootApplication {

    public static void main(String[] args) {
        ConfigurableApplicationContext context =
                SpringApplication.run(SpringbootApplication.class, args);

        context.close(); // triggers bean destruction
    }
}
```

---

### 📦 Bean Class Example

```java
@Component
public class User {

    @PostConstruct
    public void initialize() {
        System.out.println("Post Construct initialized");
    }

    @PreDestroy
    public void preDestroy() {
        System.out.println("Bean is about to destroy, in PreDestroyMethod");
    }

    public User() {
        System.out.println("initializing user");
    }
}
```

---

### 🖥️ Output

```text
initializing user
Post Construct initialized
Bean is about to destroy, in PreDestroyMethod
```

---

### 💡 Key Notes

- `@PostConstruct` → runs after dependency injection  
- `@PreDestroy` → runs before bean destruction  
- `context.close()` → triggers destruction lifecycle  
- Used for cleanup tasks (closing DB, releasing resources, etc.)

---


## 📌 More About Dependency Injection

---

###  What is Dependency Injection?

**Dependency Injection (DI)** is a design pattern in which an object's dependencies (beans) are provided (injected) by an external source, such as the **IoC Container**.

---

###  Types of Dependency Injection

- **Constructor Injection**
- **Setter Injection**
- **Field Injection**

---

### Advantages of Dependency Injection

- Makes classes **independent of their dependencies**
- Promotes **loose coupling**
- Helps remove dependency on **concrete implementations**
- Dependencies are injected from an **external source (IoC Container)**
- Improves **testability and maintainability**

---

### Key Idea

> Instead of creating dependencies inside the class, Spring injects them from outside.



## 📌 Field Injection

Field Injection is a way of injecting dependencies directly into class fields using `@Autowired`.

---

### Advantage

- Easy to use (less boilerplate code)

---

###  Disadvantages

1. ❗ `@Autowired` cannot be used with **immutable (`final`) fields**  
   because field injection happens **after object creation**

---

### 💥 Problem Example (Incorrect ❌)

```java
@Component
public class User {

    @Autowired
    private final Order order; // ❌ Not allowed

}
```

👉 This will cause an error because:
- `final` fields must be initialized during constructor execution
- But field injection happens after object creation

---

### ✅ Correct Approach (Constructor Injection ✔️)

```java
@Component
public class User {

    private final Order order;

    public User(Order order) {
        this.order = order;
    }
}
```

---

### 💡 Key Point

> Field Injection does not support immutability.  
> Use **Constructor Injection** when working with `final` fields.



## 📌 Setter Injection

Setter Injection is a way of injecting dependencies using setter methods.

---

### ❌ Disadvantages

- Cannot make fields `final` (i.e., cannot make them immutable)
- Object remains **mutable** (dependency can be changed later)
- Not recommended for required dependencies

---

### 💥 Example

```java
@Component
public class User {

    private Order order;

    @Autowired
    public void setOrder(Order order) {
        this.order = order;
    }
}
```

---

###  Why not immutable?

```java
private final Order order; // ❌ Not allowed with setter injection
```

👉 Because:
- `final` fields must be initialized in the constructor
- Setter runs **after object creation**

---

###  Key Point

> Setter Injection allows flexibility but does not support immutability.  
> Use it only for **optional dependencies**.



## 📌 Issues with Tight Coupling

### ❌ Problem

- Both `User` and `Order` classes are **tightly coupled**

- If the object creation logic of `Order` changes  
  (e.g., it becomes an interface with multiple implementations),  
  then the `User` class also needs to be modified ❌

---

### 💥 Example (Tight Coupling ❌)

```java
public class User {

    Order order = new OnlineOrder(); // tightly coupled

    public User() {
        System.out.println("initializing user");
    }
}
```

---

### ✅ Better Design (Using Abstraction)

```java
public interface Order {
}
```

```java
public class OnlineOrder implements Order {
}
```

```java
public class OfflineOrder implements Order {
}
```

---

## 📌 Dependency Inversion Principle (DIP)

### ❌ Violates DIP

```java
public class User {

    Order order = new OnlineOrder(); // depends on concrete class ❌

    public User() {
        System.out.println("initializing user");
    }
}
```

---

### ✅ Follows DIP

```java
public class User {

    Order order;

    public User(Order orderObj) {
        this.order = orderObj;
    }
}
```

---

### 💡 Key Rule of DIP

> ❗ Do NOT depend on concrete implementations  
> ✅ Depend on abstractions (interfaces)

---

## 📌 How Spring Boot Achieves DIP?

### 🚀 Through Dependency Injection

- Using Dependency Injection, we can make our class **independent of its dependencies**
- It removes dependency on **concrete implementation**
- Dependencies are injected from an **external source (IoC Container)**

---

### ✅ Example with Spring

```java
@Component
public class User {

    @Autowired
    private Order order;
}
```

```java
@Component
public class Order {
}
```

---

### 🔄 How @Autowired Works

- Spring looks for a bean of the required type  
- If found → Spring injects it automatically  

---

## 🎯 Final Summary

- Tight coupling → ❌ bad design  
- DIP → depend on abstraction  
- Spring solves this using → **Dependency Injection**




## 📌 Constructor Injection

---

### 💡 Key Points

- Dependency gets resolved at the time of **object initialization**
- **Recommended** way of Dependency Injection ✅
- Supports **immutability (final fields)**

---

## ✅ Example (Using @Autowired)

```java
@Component
public class User {

    private Order order;

    @Autowired
    public User(Order order) {
        this.order = order;
        System.out.println("User initialized");
    }
}
```

```java
@Component
@Lazy
public class Order {

    public Order() {
        System.out.println("order initialized");
    }
}
```

---

### 🖥️ Output

```text
order initialized
User initialized
```

---

## 🚀 Important Note

> When only **one constructor** is present,  
> using `@Autowired` is **not mandatory** (from Spring 4.3)

---

## ✅ Example (Without @Autowired)

```java
@Component
public class User {

    private Order order;

    public User(Order order) {
        this.order = order;
        System.out.println("User initialized");
    }
}
```

```java
@Component
@Lazy
public class Order {

    public Order() {
        System.out.println("order initialized");
    }
}
```

---

## 🎯 Key Advantages

- Supports **immutable objects (final fields)**
- Ensures all required dependencies are available at creation time
- Promotes **clean and testable code**
- Recommended by Spring and industry best practices 🔥

---


## 📌 Constructor Injection (Multiple Constructors Case)

---

### ⚠️ Important Rule

> When **more than one constructor** is present,  
> using `@Autowired` on the constructor is **mandatory**

---

## ❌ Problem Example (Without @Autowired)

```java
@Component
public class User {

    private Order order;
    private Invoice invoice;

    public User(Order order) {
        this.order = order;
        System.out.println("User initialized with only Order");
    }

    public User(Invoice invoice) {
        this.invoice = invoice;
        System.out.println("User initialized with only Invoice");
    }
}
```

---

### 💥 Error

```text
BeanCreationException: Error creating bean with name 'user' defined : No default constructor found
```

👉 Spring gets confused ❌  
👉 It doesn’t know **which constructor to use**

---

## ✅ Correct Example (Using @Autowired)

```java
@Component
public class User {

    private Order order;
    private Invoice invoice;

    public User(Order order) {
        this.order = order;
        System.out.println("User initialized with only Order");
    }

    @Autowired
    public User(Invoice invoice) {
        this.invoice = invoice;
        System.out.println("User initialized with only Invoice");
    }
}
```

---

## 📦 Supporting Classes

```java
@Component
@Lazy
public class Invoice {

    public Invoice() {
        System.out.println("invoice initialized");
    }
}
```

```java
@Component
@Lazy
public class Order {

    public Order() {
        System.out.println("order initialized");
    }
}
```

---

### 🖥️ Output

```text
invoice initialized
User initialized with only Invoice
```

---

## 💡 Key Points

- If multiple constructors exist → `@Autowired` is required  
- Spring uses the constructor marked with `@Autowired`  
- Avoid ambiguity in dependency injection  
- Best practice: Prefer **single constructor** when possible  

---
		


## 📌 Why Constructor Injection is Recommended (Advantages)

---

### ✅ 1. Mandatory Dependencies Initialized at Creation

- All required dependencies are created at the time of **object initialization**
- Ensures object is **fully initialized (100%)**

#### ✔ Benefits:

- Avoids **NullPointerException (NPE)** during runtime  
- No need for unnecessary **null checks**

---

### ✅ 2. Supports Immutability

- We can create **immutable objects** using constructor injection
- Dependencies can be marked as `final`

---

## ✅ Correct Example (Recommended ✔️)

```java
@Component
public class User {

    private final Order order;

    public User(Order order) {
        this.order = order;
        System.out.println("User initialized");
    }
}
```

---

## ❌ Incorrect Example (Not Recommended)

```java
@Component
public class User {

    @Autowired
    private final Order order; // ❌ Not allowed

    public User() {
        System.out.println("User initialized");
    }
}
```

---

### 💡 Key Point

> Constructor Injection ensures all dependencies are available at creation time  
> and allows creation of **safe, immutable objects**

---




## 📌 Constructor Injection Advantage: Fail Fast

---

### ✅ 3. Fail Fast Behavior

- If any required dependency is missing, the application **fails immediately**
- Failure happens at **startup (initialization time)** instead of runtime

---

## ❌ Problem with Field Injection

```java
@Component
public class User {

    public Order order;

    public User() {
        System.out.println("User initialized");
    }

    @PostConstruct
    public void init() {
        System.out.println(order == null); // true → dependency missing
    }
}
```

```java
@Component
public class Order {

    public Order() {
        System.out.println("order initialized");
    }
}
```

---

### ⚠️ Issue

- Application starts successfully ❌  
- But dependency is `null`  
- Can cause **NullPointerException at runtime**

---

## ✅ Constructor Injection (Fail Fast ✔️)

```java
@Component
public class User {

    private Order order;

    public User(Order order) {
        this.order = order;
        System.out.println("User initialized");
    }

    @PostConstruct
    public void init() {
        System.out.println(order == null); // always false
    }
}
```

---

### 💥 If Dependency is Missing

```text
APPLICATION FAILED TO START

Description:
Parameter 0 of constructor in User required a bean of type 'Order' that could not be found
```

---

## 💡 Key Point

> Constructor Injection ensures that if a dependency is missing,  
> the application fails immediately (Fail Fast) instead of failing later at runtime.

---

## 🎯 Summary

- Field Injection → ❌ Runtime failure (late detection)  
- Constructor Injection → ✅ Startup failure (early detection)  
- Early failure = **easier debugging + safer application**

---






## 📌 Constructor Injection Advantage: Unit Testing is Easy

---

### ✅ 4. Unit Testing Becomes Easy

- Constructor Injection allows us to **inject dependencies manually**
- No need to start the Spring container for testing
- Easy to use **mock objects**

---

## 📦 Example (Production Code)

```java
@Component
public class User {

    private Order order;

    public User(Order order) {
        this.order = order;
        System.out.println("User initialized");
    }

    public void process() {
        order.process();
    }
}
```

---

## 🧪 Example (Unit Test using Mockito)

```java
class UserTest {

    private Order orderMockObj;
    private User user;

    @BeforeEach
    public void setup() {
        this.orderMockObj = Mockito.mock(Order.class);
        this.user = new User(orderMockObj);
    }
}
```

---

## 💡 Why this is Easy?

- We can directly pass **mock dependencies**  
- No need for `@Autowired` or Spring context  
- Faster and simpler testing  

---

## 🎯 Key Point

> Constructor Injection makes unit testing easy because dependencies can be manually injected using mocks.

---	




## 📌 Common Issues in Dependency Injection

---

## ❌ 1. Circular Dependency

A circular dependency occurs when two or more beans depend on each other.

---

### 💥 Example

```java
@Component
public class Order {

    @Autowired
    private Invoice invoice;

    public Order() {
        System.out.println("order initialized");
    }
}
```

```java
@Component
public class Invoice {

    @Autowired
    private Order order;

    public Invoice() {
        System.out.println("invoice initialized");
    }
}
```

---

### 🔁 Dependency Flow

```text
Order → Invoice → Order → Invoice (cycle)
```

---

### 💥 Error

```text
APPLICATION FAILED TO START

Description:

The dependencies of some of the beans in the application context form a cycle:

┌─────┐
| invoice
↑     ↓
| order
└─────┘
```

---

## ❓ Why this happens?

- Spring tries to create `Order`
- `Order` needs `Invoice`
- `Invoice` needs `Order`
- Infinite loop → ❌ Application fails

---


## 📌 Solutions for Circular Dependency

---

### ✅ 1. Refactor the Code (Best Practice 🔥)

- Identify the **common logic** between dependent classes
- Move that logic into a **separate class/service**
- This helps **break the circular dependency**

#### 💡 Idea:

```text
Before:
Order ↔ Invoice (circular ❌)

After:
        CommonService
         ↑       ↑
     Order     Invoice
```

👉 Both classes depend on a **third class**, not on each other

---

### ✅ 2. Use `@Lazy` Annotation

```java
@Component
public class Order {

    @Autowired
    @Lazy
    private Invoice invoice;
}
```

---

### 💡 How it works?

- Spring creates a **proxy object** instead of the actual bean
- Actual bean is created **only when needed (lazy initialization)**
- This breaks the circular dependency at startup

---

### ⚠️ Note

- `@Lazy` is a **temporary fix**, not a design solution  
- Best approach is always **refactoring**

---

## 🎯 Final Recommendation

- ✔ Prefer **refactoring (clean design)**  
- ✔ Use `@Lazy` only when necessary  
- ❌ Avoid tight coupling between classes  

---




## 📌 @Lazy with Field Injection

---

### 🧠 Concept


---

## ✅ Example

```java
@Component
@Lazy
public class Order {

    public Order() {
        System.out.println("Order initialized");
    }
}
```

```java
@Component
public class Invoice {

    @Autowired
    private Order order;

    public Invoice() {
        System.out.println("Invoice initialized");
    }
}
```

---

## 🖥️ Output

```text
Invoice initialized
Order initialized
```

---



## 📌 @Lazy on Field Injection (Understanding Behavior)

---

## ✅ Code Example

```java
@Component
public class Invoice {

    @Lazy
    @Autowired
    private Order order;

    public Invoice() {
        System.out.println("invoice initialized");
    }
}
```

```java
@Component
public class Order {

    public Order() {
        System.out.println("order initialized");
    }
}
```

---

## 🖥️ Output

```text
invoice initialized
order initialized
```

---



## 📌 @Lazy on Class vs Field Injection

---

## ✅ Example

```java
@Component
@Lazy
public class Order {

    public Order() {
        System.out.println("Order initialized");
    }
}
```

```java
@Component
public class Invoice {

    @Lazy
    @Autowired
    private Order order;

    public Invoice() {
        System.out.println("Invoice initialized");
    }
}
```

---

## 🖥️ Output

```text
Invoice initialized
```

---



## 📌 Resolving Circular Dependency using @Lazy

---

## ✅ Example

```java
@Component
public class Order {

    @Autowired
    private Invoice invoice;

    public Order() {
        System.out.println("order initialized");
    }
}
```

```java
@Component
public class Invoice {

    @Lazy
    @Autowired
    private Order order;

    public Invoice() {
        System.out.println("Invoice initialized");
    }
}
```

---

## 🖥️ Output

```text
Invoice initialized
Order initialized
```

---

## 📌 Resolving Circular Dependency using @PostConstruct

---

## ✅ Example

```java
@Component
public class Order {

    @Autowired
    private Invoice invoice;

    public Order() {
        System.out.println("Order initialized");
    }

    @PostConstruct
    public void initialize() {
        invoice.setOrder(this);
    }
}
```

```java
@Component
public class Invoice {

    private Order order;

    public Invoice() {
        System.out.println("Invoice initialized");
    }

    public void setOrder(Order order) {
        this.order = order;
    }
}
```

---

## 🖥️ Output

```text
Invoice initialized
Order initialized
```

---



## 📌 Unsatisfied Dependency

---

## ❌ Problem

```java
@Component
public class User {

    @Autowired
    private Order order;

    public User() {
        System.out.println("User initialized");
    }
}
```

---

## 📦 Order Interface & Implementations

```java
public interface Order {
}
```

```java
@Component
public class OnlineOrder implements Order {

    public OnlineOrder() {
        System.out.println("Online order initialized");
    }
}
```

```java
@Component
public class OfflineOrder implements Order {

    public OfflineOrder() {
        System.out.println("Offline order initialized");
    }
}
```

---

## 💥 Error

```text
APPLICATION FAILED TO START

UnsatisfiedDependencyException:
Error creating bean with name 'user'
```

---

## ❓ Why this happens?

- Spring finds **multiple beans** of type `Order`:
  - `OnlineOrder`
  - `OfflineOrder`

👉 It gets confused ❌  
👉 It doesn’t know which one to inject

---



## 📌 Solution: Using @Primary Annotation

---

## 📦 Interface

```java
public interface Order {
}
```

---

## ❌ Problem Recap

- Multiple implementations of `Order`:
  - `OnlineOrder`
  - `OfflineOrder`
- Spring gets confused → ❌ Unsatisfied Dependency

---

## ✅ Solution: Use `@Primary`

---

### 📦 OnlineOrder (Primary Bean)

```java
@Component
@Primary
public class OnlineOrder implements Order {

    public OnlineOrder() {
        System.out.println("Online order initialized");
    }
}
```

---

### 📦 OfflineOrder

```java
@Component
public class OfflineOrder implements Order {

    public OfflineOrder() {
        System.out.println("Offline order initialized");
    }
}
```

---

### 👤 User Class

```java
@Component
public class User {

    @Autowired
    private Order order;

    public User() {
        System.out.println("User initialized");
    }
}
```

---

## 🖥️ Output

```text
Offline order initialized
Online order initialized
User initialized
```

---

## 💡 How it works?

- `@Primary` tells Spring:
  👉 “If multiple beans exist, use this one by default”

---

## 🎯 Key Point

> `@Primary` resolves ambiguity when multiple beans of the same type exist.

---




## 📌 Solution: Using @Qualifier Annotation

---

## 📦 Interface

```java
public interface Order {
}
```

---

## ❌ Problem Recap

- Multiple implementations of `Order`:
  - `OnlineOrder`
  - `OfflineOrder`
- Spring gets confused → ❌ which bean to inject?

---

## ✅ Solution: Use `@Qualifier`

---

### 👤 User Class

```java
@Component
public class User {

    @Autowired
    @Qualifier("offlineOrderName")
    private Order order;

    public User() {
        System.out.println("User initialized");
    }
}
```

---

### 📦 OnlineOrder

```java
@Component
@Qualifier("onlineOrderName")
public class OnlineOrder implements Order {

    public OnlineOrder() {
        System.out.println("Online order initialized");
    }
}
```

---

### 📦 OfflineOrder

```java
@Component
@Qualifier("offlineOrderName")
public class OfflineOrder implements Order {

    public OfflineOrder() {
        System.out.println("Offline order initialized");
    }
}
```

---

## 🖥️ Output

```text
Offline order initialized
Online order initialized
User initialized
```

---

## 💡 How it works?

- `@Qualifier` tells Spring:
  👉 “Inject THIS specific bean”

- Matches bean name with qualifier value

---

## 🔥 Key Difference

| Annotation     | Purpose |
|----------------|--------|
| `@Primary`     | Default bean selection |
| `@Qualifier`   | Specific bean selection |

---

## 🎯 Key Point

> Use `@Qualifier` when multiple beans exist and you want to inject a specific one.

---



## 📌 @Value Annotation

`@Value` is a Spring annotation used to inject **simple values** or **property values** into fields, methods, or constructors.  
It helps make code more flexible and avoids hardcoding values.

---

## ✅ Example 1: Inject Hardcoded Values

```java
@Component
public class User {

    @Value("Giriraj")
    private String name;

    @Value("101")
    private int id;

    public void display() {
        System.out.println(name + " " + id);
    }
}
```

---

## ✅ Example 2: Inject Values from `application.properties`

### 📄 application.properties

```properties
user.name=Giriraj
user.id=101
```

---

### 📦 User Class

```java
@Component
public class User {

    @Value("${user.name}")
    private String name;

    @Value("${user.id}")
    private int id;

    public void display() {
        System.out.println(name + " " + id);
    }
}
```

---

## ✅ Example 3: Constructor Injection with @Value

```java
@Component
public class User {

    private final String name;
    private final int id;

    public User(@Value("${user.name}") String name,
                @Value("${user.id}") int id) {
        this.name = name;
        this.id = id;
    }
}
```

---

## 💡 Key Points

- Used for injecting:
  - Primitive values (`int`, `double`)
  - Strings
  - Values from `application.properties` / `application.yml`
- Supports **SpEL (Spring Expression Language)**  
- Helps in making applications **configurable**

---

## 🎯 Example Output

```text
Giriraj 101
```

---

## ⚠️ Note

> Prefer using `@Value` with external configuration (`application.properties`) instead of hardcoding values.

---


# 📌 @Scope Annotation

`@Scope` is used to define the **lifecycle and visibility** of a Spring bean.

---


## 📌 Bean Scope

```
           Scope
             │
   ┌─────────┼─────────┬─────────┐
   │         │         │         │
Singleton  Prototype  Request   Session
```

---

## 💡 Explanation

- **Singleton** → One instance per container (default)  
- **Prototype** → New instance every time requested  
- **Request** → One instance per HTTP request  
- **Session** → One instance per HTTP session  

---






## 📌 Singleton Scope (Detailed)

---

### ✅ Key Points

- Default scope in Spring ✔️  
- Only **one instance** is created per IOC container  
- Bean is **eagerly initialized**  
  (created at application startup)

---

## 📦 Bean Example

```java
@Component
@Scope("singleton") // optional (default)
public class User {

    public User() {
        System.out.println("User initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("User object hashCode: " + this.hashCode());
    }
}
```

---

## 🌐 Controller Example 1

```java
@RestController
@RequestMapping("/api")
public class TestController1 {

    @Autowired
    private User user;

    public TestController1() {
        System.out.println("TestController1 instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("TestController1 object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode());
    }

    @GetMapping("/fetchUser")
    public ResponseEntity<String> getUserDetails() {
        System.out.println("fetchUser api invoked");
        return ResponseEntity.ok("User fetched");
    }
}
```

---

## 🌐 Controller Example 2

```java
@RestController
@RequestMapping("/api")
@Scope(ConfigurableBeanFactory.SCOPE_SINGLETON)
public class TestController2 {

    @Autowired
    private User user;

    public TestController2() {
        System.out.println("TestController2 instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("TestController2 object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode());
    }

    @GetMapping("/fetchUser2")
    public ResponseEntity<String> getUserDetails() {
        System.out.println("fetchUser2 api invoked");
        return ResponseEntity.ok("User fetched");
    }
}
```

---

## 🖥️ Output Observation

```text
TestController instance initailization
User initailzation 
User Object hashCode : 1140202235
TestController1 object hashCode : 1046302571  User object hashCode : 1140202235
TestController2 instance initiazation 
TestController2 object hashCode : 1525241607 User Object hashCode : 1140202235
After hittin api
fetch User api invoked
```


---

## 💡 Key Observation

- `User` bean hashCode is **same everywhere** ✅  
- Only **one instance** of `User` is created  
- Shared across all controllers  

---

## 🎯 Final Understanding

> Singleton scope means **one shared instance per Spring container**

---

## ⚠️ Important Notes

- Be careful with **mutable data**  
- Not thread-safe by default  
- Avoid storing request-specific data in singleton beans  

---





## 📌 Prototype Scope

---

### ✅ Key Points

- A **new object is created every time** the bean is requested  
- Bean is **lazily initialized** (created only when needed)  
- Not shared like singleton  

---

## 📦 User Bean (Prototype)

```java
@Component
@Scope("prototype")
public class User {

    public User() {
        System.out.println("User initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("User object hashCode: " + this.hashCode());
    }
}
```

---

## 📦 Student Bean

```java
@Component
public class Student {

    @Autowired
    private User user;

    public Student() {
        System.out.println("Student instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("Student object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode());
    }
}
```

---

## 🌐 Controller Example

```java
@RestController
@RequestMapping("/api")
@Scope(ConfigurableBeanFactory.SCOPE_PROTOTYPE)
public class TestController1 {

    @Autowired
    private User user;

    @Autowired
    private Student student;

    public TestController1() {
        System.out.println("TestController1 instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("TestController1 object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode()
                + " | Student object hashCode: " + student.hashCode());
    }

    @GetMapping("/fetchUser")
    public ResponseEntity<String> getUserDetails() {
        System.out.println("fetchUser api invoked");
        return ResponseEntity.ok("User fetched");
    }
}
```

---

## 🖥️ Output Observation

```text
Student instance initialization
User initialization
User object hashCode: 1510009630

Student object hashCode: 2092450685 | User object hashCode: 1510009630

--- After hitting API ---



TestController1 instance initialization
User initialization
User object hashCode : 1984730322
TestController1 Object hashCode : 1786739287  User Object hashCode :1984730322 Student object hashCode :2092450685
fetchUser api invoked
```

---

## 💡 Key Observations

- `User` bean is **prototype** → new object each time ✅  
- Different `hashCode` = different instances  
- `Student` is singleton → created only once  
- Controller is prototype → new instance per request  

---

## ⚠️ Important Concept

> When a **prototype bean is injected into a singleton**,  
> it is created only once at injection time (NOT every use)

---

## 🎯 Final Understanding

| Bean Type  | Behavior |
|-----------|--------|
| Singleton | One instance |
| Prototype | New instance every time |

---

## 🚀 Summary

- Prototype = multiple objects  
- Lazy creation  
- Useful for **stateful objects**  
- Be careful when injecting into singleton  

---



## 📌 Request Scope

---

### ✅ Key Points

- A **new object is created for each HTTP request**  
- Bean is **lazily initialized**  
- Exists only for the duration of a single request  

---


## Scope Request

### 📦 User Bean (Request Scope)

```java
@Component
@Scope("request")
public class User {

    public User() {
        System.out.println("User initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("User object hashCode: " + this.hashCode());
    }
}
```

---

### 📦 Student Bean (Prototype Scope)

```java
@Component
@Scope("prototype")
public class Student {

    @Autowired
    private User user;

    public Student() {
        System.out.println("Student instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("Student object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode());
    }
}
```

---

### 🌐 Controller Example

```java
@RestController
@Scope("request")
@RequestMapping("/api")
public class TestController1 {

    @Autowired
    private User user;

    @Autowired
    private Student student;

    public TestController1() {
        System.out.println("TestController1 instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("TestController1 object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode()
                + " | Student object hashCode: " + student.hashCode());
    }

    @GetMapping("/fetchUser")
    public ResponseEntity<String> getUserDetails() {
        System.out.println("fetchUser api invoked");
        return ResponseEntity.ok("User fetched");
    }
}
```

---


## 🖥️ Output Behavior

```text

At Application startup no object is created
--- Request 1 ---
TestController1 instance initialization
User initialization
User object hashCode: 1111
Student instance initialization
Student Object hashCode :12345  User object hashCode :1111
TestController1 object hashCode: 67890 User Object hashCode : 1111 Student Object hashCode :12345
fetchuser api invoked
```

---



## 📌 Scope Mismatch Problem (Singleton + Request)

---

## ❌ Scenario

```java
@RestController
@Scope("singleton")
@RequestMapping("/api")
public class TestController1 {

    @Autowired
    private User user;

    public TestController1() {
        System.out.println("TestController1 instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("TestController1 object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode());
    }

    @GetMapping("/fetchUser")
    public ResponseEntity<String> getUserDetails() {
        System.out.println("fetchUser api invoked");
        return ResponseEntity.ok("response");
    }
}
```

---

## 📦 User Bean (Request Scope)

```java
@Component
@Scope("request")
public class User {

    public User() {
        System.out.println("User initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("User object hashCode: " + this.hashCode());
    }
}
```

---

## 💥 Error

```text
APPLICATION FAILED TO START

UnsatisfiedDependencyException:
Error creating bean with name 'testController1'
```

---

## ❓ Why this happens?

- `TestController1` → **Singleton** (created at startup)
- `User` → **Request scope** (created per HTTP request)

👉 Problem:

```text
Singleton bean is trying to inject Request bean ❌
```

👉 At startup:
- No HTTP request exists ❌  
- So Spring **cannot create User bean**

---


## 📌 Resolving Scope Mismatch using Scoped Proxy

---

## ❌ Problem Recap

- `Singleton` bean is created at application startup  
- `Request` bean is created only when an HTTP request is available  

👉 So:

```text
No active HTTP request at startup ❌
→ Request bean cannot be created
→ Application fails
```

---

## 💥 Problem Example

```java
@RestController
@Scope("singleton")
@RequestMapping("/api")
public class TestController1 {

    @Autowired
    private User user;

    public TestController1() {
        System.out.println("TestController1 instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("TestController1 object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode());
    }

    @GetMapping("/fetchUser")
    public ResponseEntity<String> getUserDetails() {
        System.out.println("fetchUser api invoked");
        return ResponseEntity.ok("response");
    }
}
```

---

## ✅ Solution: Use Scoped Proxy

```java
@Component
@Scope(value = "request", proxyMode = ScopedProxyMode.TARGET_CLASS)
public class User {

    public User() {
        System.out.println("User initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("User object hashCode: " + this.hashCode());
    }

    public void dummyMethod() {
        // some logic
    }
}
```

---

## 💡 How it works?

- Spring **does NOT inject real User object**
- Instead, it injects a **proxy object**

👉 During HTTP request:
- Proxy creates real `User` object  
- Delegates method calls to it  

---

## 🔄 Flow

```text
1. Application starts
2. Singleton bean is created
3. Proxy of User is injected (not real object)
4. HTTP request comes
5. Real User object is created
6. Proxy forwards call to real object
```

---

## 🖥️ Output Behavior

```text
TestController1 instance initialization
TestController1 object hashCode: 153952444 | User object hashCode: 0 (proxy)

--- HTTP Request ---

User initialization
User object hashCode: 987654321
fetchUser api invoked
```

---





## 📌 Session Scope

---

### ✅ Key Points

- A **new object is created for each HTTP session**  
- Bean is **lazily initialized**  
- Session is created when user hits any endpoint  
- Bean remains active **until session expires or is invalidated**  

---

## 📦 User Bean

```java
@Component
public class User {

    public User() {
        System.out.println("User initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("User object hashCode: " + this.hashCode());
    }

    public void dummyMethod() {
        // some logic
    }
}
```

---

## 🌐 Controller Example

```java
@RestController
@Scope("session")
@RequestMapping("/api")
public class TestController1 {

    @Autowired
    private User user;

    public TestController1() {
        System.out.println("TestController1 instance initialization");
    }

    @PostConstruct
    public void init() {
        System.out.println("TestController1 object hashCode: " + this.hashCode()
                + " | User object hashCode: " + user.hashCode());
    }

    @GetMapping("/fetchUser")
    public ResponseEntity<String> getUserDetails() {
        System.out.println("fetchUser api invoked");
        return ResponseEntity.ok("response");
    }

    @GetMapping("/logout")
    public ResponseEntity<String> logout(HttpServletRequest request) {
        System.out.println("End the session");
        HttpSession session = request.getSession();
        session.invalidate();
        return ResponseEntity.ok("Session ended");
    }
}
```

---


---

## 🖥️ Output Behavior

```text

User initialization 
User Object hashCode : 12345

after hitting api 
TestController1 instance initialization
TestController1 object hashCode : 67890   User object hashCode: : 12345
fetchUser api Invoked

Again hitting API
fetchUser api invoked

Again hitting api
end of the session

Again hitting api means new session

TestController1 instance initialization
TestController1 object hashCode : 896745s   User object hashCode: : 12345
fetchUser api Invoked
``` 


 ---



#  CommandLineRunner in Spring Boot

---

## 💡 Definition

👉 `CommandLineRunner` is an interface in Spring Boot that allows execution of code **after the application context is fully loaded**.

---

## 📦 Code

### 🔹 Main Class

```java
@SpringBootApplication
public class Demo {

    public static void main(String[] args) {

        SpringApplication.run(Demo.class, args);

        System.out.println("Main Method Ends");
    }
}
```

---

### 🔹 Runner Class

```java
@Component
public class MyRunner implements CommandLineRunner {

    @Override
    public void run(String... args) throws Exception {

        System.out.println("This run method is executed after configuration load");
    }
}
```

---

## 🖥️ Output

```text
This run method is executed after configuration load
Main Method Ends
```

---

## 🔄 Execution Flow (Important 🔥)

```text
1. main() starts
2. SpringApplication.run() called
3. Spring Boot initializes context
4. All beans are created
5. CommandLineRunner.run() executes
6. Control returns to main()
7. "Main Method Ends" prints
```

---



# 📘 Logging in Spring Boot

## 🔹 What is Logging?
Logging in Spring Boot is the process of recording information about what your application is doing while it runs.

It includes:
- Application flow messages  
- Errors and exceptions  
- Warning messages  
- Debugging details  

---

## 🔹 Why Logging is Important

Logging helps you to:

- Track application behavior  
- Debug issues and errors  
- Monitor performance  
- Audit system activity  

---

## 🔹 Default Logging in Spring Boot


Spring Boot uses SLF4J (Simple Logging Facade for Java) with Logback as the default logging framework.


## 🔹 Logging Levels

Spring Boot supports standard logging levels:

| Level  | Description                     |
|--------|---------------------------------|
| TRACE  | Very detailed information       |
| DEBUG  | Debugging information           |
| INFO   | General application events      |
| WARN   | Warning messages                |
| ERROR  | Error events                    |


## 🔹 Log File Configuration

You can specify a directory where log files will be stored using:

```properties
logging.file.path=logs
```
---



### 📌 Explanation

- `logging.file.path` → Defines the folder where log files will be created  
- `logs` → Log files will be stored inside a folder named `logs` in your project root  
- By default name of file is spring.log



## 🔹 Log File Name Configuration

You can specify the name of the log file using:

```properties
logging.file.name=Demo.log
```
---

### 📌 Explanation

- `logging.file.name` → Defines the name of the log file  
- `Demo.log` → Logs will be written into a file named `Demo.log` 




## 🔹 Log File Configuration (Path + Name)

```properties
logging.file.path=logs
logging.file.name=logs/Demo.log

```

``` text
Here insids logs folder Demo.log is created

--- 

