## Notes

### What is Maven?

Maven is a software management and comprehension tool based on the concept of Project Object Model(POM). It can manage project build, reporting and documentation, from a central piece of information.

Maven is the most popular build and dependency resolution tool for Java, just like NPM is for JS. But it's not just the same tool for a different language. There are obviously huge differences between Java and JS builds, and these differences are directly visible in the way Maven operates.

When you use Maven, you describe your project using a well-defined project object model (the file pom.xml), similar to package.json. In both cases, the dependencies finally end up in the project directory (npm: /node_modules, Maven: /target).

### Packages

1. Packages are used to group related classes.
2. Packages are declared with the package keyword, and any Kotlin file with a package declaration at the beginning can contain declarations of classes, functions, or interfaces.

`
package org.example

fun printMessage() { /_..._/ }
class Message { /_..._/ }

`

3. All the contents (such as classes and functions) of the source file are contained by the package declared. So, in the example above, the full name of printMessage() is org.example.printMessage, and the full name of Message is org.example.Message.
4. If both classes are in same package, you don't have to import it.

### Annotations

https://springframework.guru/spring-framework-annotations/

Annotations are means of attaching metadata to code and do not change action of a compiled program However, annotations are not pure comments as they can change the way a program is treated by compiler.

For example,there are three built-in annotations available in Java (@Deprecated, @Override & @SuppressWarnings) that can be used for giving certain instructions to the compiler. For example the @override annotation is used for instructing compiler that the annotated method is overriding the method.

Secondly, annotations can provide compile-time instructions to the compiler that can be further used by sofware build tools for generating code, XML files etc.

Annotations can be applied to the classes, interfaces, methods and fields.

At the main of the app, we have, `@SpringBootApplication`.

What is it, its basically syntactic sugar for combining other annotations that we'll look at in just a moment. @SpringBootApplication is @Configuration, @EnableAutoConfiguration and @ComponentScan annotations combined, configured with their default attributes.
The trick with Spring Boot is that many things happen implicitly. We use the @SpringBootApplication annotation, but it's just a combination of three annotations:
@Configuration
@EnableAutoConfiguration
@ComponentScan

`@Configuration and @ComponentScan`

The @Configuration and @ComponentScan annotations that we described above make Spring create and configure the beans and components of your application. It's a great way to decouple the actual business logic code from wiring the app together.

Springboot will automatically return the instance of the class when it is required by you.

This annotation enables component-scanning so that the web controller classes and other components you create will be automatically discovered and registered as beans in Spring's Application Context. All the@Controller classes you write are discovered by this annotation

`@EnableAutoConfiguration`

Now the @EnableAutoConfiguration annotation is even better. It makes Spring guess the configuration based on the JAR files available on the classpath. It can figure out what libraries you use and preconfigure their components without you lifting a finger. It is how all the spring-boot-starter libraries work. Meaning it's a major lifesaver both when you're just starting to work with a library as well as when you know and trust the default config to be reasonable.

So what happens, is that, by having the annotation `@Component`, and then `@ComponentScan` it will automatically add these classes into the applicationContext of spring. Spring can auto scan all classes annotated with the stereotype annotations @Component, @Controller, @Service, and @Repository

`@AutoWired`

If we annotate a class with @Autowired, Spring will automatically resolve the instance and inject it into the class that declared it. So, we don’t need to obtain the singleton instance ourselves.

This annotation provide classes with a declarative way to resolve dependencies. For example:

@Autowired
ArbitraryClass arbObject;

as opposed to instantiating them directly (the imperative way), for example:

`ArbitraryClass arbObject = new ArbitraryClass();`

For example, we need an instance of BlogRepository in the BlogController class. Therefore, all we need to do is:

@Autowired
BlogRespository blogRespository;

By doing this, we can use blogRepository anywhere within the controller without having to instantiate it.

### Springboot Web Annotations

The following annotations make Spring configure your app to be a web application, capable of serving the HTTP response.

`@Controller`

@Controller marks the class as a web controller, capable of handling the HTTP requests. Spring will look at the methods of the class marked with the @Controller annotation and establish the routing table to know which methods serve which endpoints.

`@Service`
This annotation is used on a class. The @Service marks a Java class that performs some service, such as execute business logic, perform calculations and call external APIs. This annotation is a specialized form of the @Component annotation intended to be used in the service layer.

`@Repository`
This annotation is used on Java classes which directly access the database. The @Repository annotation works as marker for any class that fulfills the role of repository or Data Access Object.

`@ResponseBody`

The @ResponseBody is a utility annotation that makes Spring bind a method's return value to the HTTP response body. When building a JSON endpoint, this is an amazing way to magically convert your objects into JSON for easier consumption.

`@RestController`

Then there's the @RestController annotation -- a convenience syntax for @Controller and @ResponseBody together. This means that all the action methods in the marked class will return the JSON response.

`@RequestMapping`

The @RequestMapping(method = RequestMethod.GET, value = "/path") annotation specifies a method in the controller that should be responsible for serving the HTTP request to the given path. Spring will work the implementation details of how it's done. You simply specify the path value on the annotation and Spring will route the requests into the correct action methods.

Other variants of the @RequestMapping annotation are @GetMapping, @PostMapping, etc. for handling GET and POST requests, respectively.

Spring Boot annotations for handling different HTTP request types:

    @RequestMapping — For handling any request type.
    @GetMapping — For a GET request.
    @PostMapping — For a POST request.
    @PutMapping — For a PUT request.
    @PatchMapping — For a PATCH request.
    @DeleteMapping — For a DELETE request.

#### Path variables

`@GetMapping("/blog/{id}")`

Path variables are variables in the request URL and annotated with @PathVariable, e.g id.

public returnType methodName(@PathVariable String id)
{}

#### Request parameters e.g. blog/?param1=10&param2=20

Request parameters are key-value pairs in the request URL with the annotation @RequestParam, e.g. param1 and param2.

@GetMapping("/blog")
public returnType methodName(@RequestParam String param1, @RequestParam String param2)
{
......
}

#### Request Body

The POST, PUT, and DELETE requests can contain a payload known as “request body”. The payload contains the data that could be stored or updated. The payload is usually in JSON format.

They will usually be in the form of:

`"text":"blah blah blah`

The annotation for the request body is @RequestBody. As the request body is a key-value pair, it will be wise to declare it as a Map<String, String>.

@PostMapping("/blog")
public Blog create(@RequestBody Map<String, String> body){...}

To extract the respective keys and their values:

String id = body.get("text");
String title = body.get("title");
String content = body.get("content");

`@RequestParam(value="name", defaultValue="World")`

Naturally, the methods handling the requests might take parameters. To help you with binding the HTTP parameters into the action method arguments, you can use the @RequestParam(value="name", defaultValue="World") annotation. Spring will parse the request parameters and put the appropriate ones into your method arguments.

### How it works

The controller handles all incoming HTTP requests from the user and returns an appropriate response. This is done by using the `RestController` annotation.

1. @RestController annotation tells Spring that this class is a controller.
2. @RequestMapping(“/”) annotation means that any request (GET, POST, PUT, etc.) to the root URL(/) will be handled by the index() method. The response is of type String.

### Hiberate and JPA

JPA is Persistence Api which your code should use. JPA Api will pass on the call to actual peristence provider (ex:Hibernate/TopLink) to do the actual work.

1. JPA is just a specification, meaning there is no implementation. You can annotate your classes as much as you would like with JPA annotations, however without an implementation nothing will happen. Think of JPA as the guidelines that must be followed or an interface
2. while Hibernate's JPA implementation is code that meets the API as defined by the JPA specification and provides the under the hood functionality.
3. You can think JPA as a set of Rules which is implemented by Hibernate.

When you set up a new project to use JPA, you will need to configure the datastore and JPA provider. You'll configure a datastore connector to connect to your chosen database (SQL or NoSQL). You'll also include and configure the JPA provider, which is a framework such as Hibernate.

What hibernate does? It, the ORM layer converts Java classes and objects so that they can be stored and managed in a relational database. Application code --> JPA --> JDBC --> Sql

What is JDBC? One way to save an instance of the e.g Musician class to a relational database would be to use the JDBC library. JDBC is a layer of abstraction that lets an application issue SQL commands without thinking about the underlying database implementation. It basically is a structure to convert it into SQL query.

Currently, it is very verbose to use JDBC. However, with JPA, it can be as simple as

```
Musician georgeHarrison = new Musician(0, "George Harrison");
musicianManager.save(georgeHarrison);
```

How does it know?

The magic in which is created using JPA's annotations. Developers use annotations to inform JPA which objects should be persisted, and how they should be persisted.

You use `@Entity`as the object class. Persistent objects are sometimes called entities. Attaching @Entity to a class like Musician informs JPA that this class and its objects should be persisted.

### How to do mapping in jpa

In order to define an entity, you must create a class that is annotated with the @Entity annotation. The @Entity annotation is a marker annotation, which is used to discover persistent entities.

By default, it will map to the table name of the class's name. Else you can specify it specifically, by using the @Table annotation to do that.

Next, we have to map the attributes to the specific columns. Fields are defined as member variables in the class, with the name of each field being mapped to a column name in the table. You can override this default mapping by using the @Column annotation.

In JPA, we use the @Id annotation to designate a field to be the table's primary key. The primary key is required to be a Java primitive type, a primitive wrapper, such as Integer or Long, a String, a Date, a BigInteger, or a BigDecimal.

### Migration

Migration will be done automatically but in production you will usually use framework like flyAway.

## Putting it together

1. ENTITY MODEL - Create the data model class, this will involve creating a class with `@Entity`. This will perform the mapping to the table itself, as well as the various attributes to the column.

The @Entity annotation specifies that the class is an entity and is mapped to a database table. The @Table annotation specifies the name of the database table to be used for mapping.

@GeneratedValue

@GeneratedValue(strategy = GenerationType.AUTO) tells Spring that the field is auto-generated and will not be provided by the user, rather, it will be generated by the database.

2. REPOSITORY - Something to talk to the database itself, this is known as a repository. THis is nodeJS eqauvilent of writing the query itself. Create a JPA repo that will perform all CRUD with `@Repository`. This Repository is a Kotlin interface that inherits from JpaRepository. Under the hood, it uses Hibernate to map database queries to our database provider, PostgreSQL. This will help us to handle all the interactions with the database.

By extending from the Spring JPArepository which extends PagingAndSortingRepository and, in turn, the CrudRepository which gives us some functionality out of the box, such as fetching all records, a single record, saving, updating, deleting, etc.. This way, we do not have to write boilerplate codes such as findAll().

The reason by this repository has type JpaRepository<Task, Long>. Because the class you are extending, like CRUDRepository, has entity and ID (primary key) as its parameters.

`public interface CrudRepository<T, ID extends Serializable>extends Repository<T, ID>{ }`

3. SERVICE -

3.Create a controller with `@RestController`.

# Kotlin

Define variable using `var` which can be reassign or local read only using `val`.

`val name: String = "Herman`

You can put a question mark after the type to allow it to be of null value.

Type inference (Single expression function)

1. Remove curly braces and put a equals and the return type.
2. It will always return that type and thus don't have to define it.
   Such functions can use a shortened syntax that omits the braces and uses the = symbol before the expression rather than the return

### Constructor

`class Person(val firstName: String, val lastName:String)`

THis is your primary constructor and by adding val, you don't have to explicitly set it.
