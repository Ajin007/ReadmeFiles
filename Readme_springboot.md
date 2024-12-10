# Spring understanding

## structure of the spring project

1. src/main/java: Contains your Java source code
2. src/main/resources: Contains non-code resources (e.g., configurations, templates, static files).
3. resources/static:

    * Stores static assets like CSS, JavaScript, images, and other resources that do not need server-side processing.
    * These files are directly accessible via the / path in your web application.
        Example:
        * /resources/static/style.css → Accessed as /style.css.
4. resources/templates:

    * Stores server-side templates (e.g., Thymeleaf, Freemarker, Mustache) used for generating dynamic web pages.
    * Templates are processed by the server and served to the user as HTML.
        Example:
        * /resources/templates/index.html can be rendered by a controller returning a view name like return "index";.
5. resources/application.properties or application.yml:

    * Central configuration file for the application. Here you configure:
    * Database settings
    * Port numbers
    * Profiles (e.g., dev, prod).

6. mvnw and mvnw.cmd
    * These are Maven Wrapper scripts, which allow your project to use Maven without requiring the user to have Maven installed.
    * mvnw (Linux/Mac) and mvnw.cmd (Windows):
            - These scripts download and use a specific version of Maven specified in the project.
            - Useful for ensuring build consistency across teams and CI/CD systems.

## Dependecny Injection (IOC)

1. Dependency Injection concept for understanding

    ``` Java
                    @SpringBootApplication
            public class SpringappApplication {

                @Component
                class Service {
                    public String getMessage(){
                        return " This is from the service methods";
                    }
                }

                @Component
                class Consumer {

                    private final Service service;

                    @Autowired //constructor injection
                    public Consumer(Service service){
                        this.service=service;
                    }

                    public void printMessage(){
                        System.out.println(service.getMessage());
                    }
                }

                public static void main(String[] args) {
                    

                    ApplicationContext context= SpringApplication.run(SpringappApplication.class, args);

                    //to get the registered bean names
                    String[] beanNames=context.getBeanDefinitionNames();
                    System.out.println("Beans regsitered are");
                    for(String beanName:beanNames){
                        System.out.println(beanName);
                    }
                    Consumer consumer=context.getBean(Consumer.class);
                    consumer.printMessage();
                    
                }

            }

## Aspect oriented programming

1. Aspect-Oriented Programming (AOP) helps modularize cross-cutting concerns, which are concerns that affect multiple parts of an application. Examples include:

* Logging
* Performance monitoring
* Security checks
* Transactions
AOP allows you to define reusable logic (aspects) that can be applied to multiple parts of your application dynamically at runtime.

2. Key Components of AOP
    * Aspect:

A modular unit of cross-cutting concerns. In the code, the LoggingAspect class is an aspect.
Defined using the @Aspect annotation.
Advice:

     - The action taken by the aspect at a particular join point. Types of advice:
    @Before: Executes before the target method.
    @After: Executes after the target method.
    @Around: Wraps around the target method.
    @AfterReturning: Executes after the method returns a value.
    @AfterThrowing: Executes after the method throws an exception.
    In the code, logBefore() is a @Before advice.
Join Point:

    A point in the application where an aspect can be applied, such as method calls or exception handling.
    Example: The execution of performTask() in ExampleService.
Pointcut:

    A predicate that matches join points.
    Defined using expressions like "execution(* com.example.service.*.*(..))".
    In the code, it matches all methods in any class under the com.example.service package.
3. coding processed in the main class
    ```Java
            @Aspect
        @Component
        class LoggingAspect{
            @Before("execution(* com.example.service.*.*(..))")
            public void logBefore(JoinPoint jointpoint){
                System.out.println("Executing"+jointpoint.getSignature().getName());

            }

            
        }

        @Service

        class ExampleService{

            public void performTask(){
                System.out.println("performing task >>>>>");
            }

        }



            public static void main(String[] args) {
                ApplicationContext context=SpringApplication.run(SpringappApplication.class, args);

                ExampleService service=context.getBean(ExampleService.class);
                service.performTask();
            }

        }

## Spring Data Access

1. Jdbc connectivity

    ``` Java
                @Repository
        class UserRepository {
            @Autowired
            private JdbcTemplate jdbcTemplate;

            public void saveUser(String name, String email) {
                jdbcTemplate.update("INSERT INTO users (name, email) VALUES (?, ?)", name, email);
            }
        }

## Spring MVC

1. Spring using the RestController

    ```Java
                @RestController
        @RequestMapping("/api")
        class UserController {
            @GetMapping("/hello")
            public String sayHello() {
                return "Hello, Spring MVC!";
            }
        }

        @SpringBootApplication
        public class SpringMvcApplication {
            public static void main(String[] args) {
                SpringApplication.run(SpringMvcApplication.class, args);
            }
        }

## Spring Security

1. Connection for the basic authentication

    ```Java
         @Configuration
        @EnableWebSecurity
        class SecurityConfig extends WebSecurityConfigurerAdapter {
            @Override
            protected void configure(HttpSecurity http) throws Exception {
                http
                    .authorizeRequests()
                    .anyRequest().authenticated()
                    .and()
                    .httpBasic();
            }

            @Override
            protected void configure(AuthenticationManagerBuilder auth) throws Exception {
                auth.inMemoryAuthentication()
                    .withUser("user")
                    .password("{noop}password")
                    .roles("USER");
            }
        }

## Spring Transaction

1. To do the transaction changes for the same

    ```Java
                @Service
        class OrderService {
            @Autowired
            private OrderRepository orderRepository;

            @Transactional
            public void placeOrder(Order order) {
                orderRepository.save(order);
                // Other database operations
            }
        }

## Spring testing

1. Mocking with MockMvc

    ```java
                @WebMvcTest(UserController.class)
        class UserControllerTest {
            @Autowired
            private MockMvc mockMvc;

            @Test
            public void testSayHello() throws Exception {
                mockMvc.perform(get("/api/hello"))
                        .andExpect(status().isOk())
                        .andExpect(content().string("Hello, Spring MVC!"));
            }
        }

## Spring cloud

1. Working with the wdureka service

    ```java
            @EnableEurekaServer
    @SpringBootApplication
    public class EurekaServerApplication {
        public static void main(String[] args) {
            SpringApplication.run(EurekaServerApplication.class, args);
        }
    }


    // Edureka Client
        @EnableEurekaClient
    @SpringBootApplication
    public class EurekaClientApplication {
        public static void main(String[] args) {
            SpringApplication.run(EurekaClientApplication.class, args);
        }
    }



## Jackson library

1. Jackson is the default JSON serialization/deserialization library in Spring Boot,
     and it provides extensive capabilities for handling JSON data.
2. Core Packages:
        com.fasterxml.jackson.databind

        The central package in Jackson for handling data binding between Java objects and JSON.
        Contains key classes like ObjectMapper, JsonNode, and annotations like @JsonProperty.
        Important Classes/Interfaces:

        ObjectMapper: Converts JSON to Java objects and vice versa.
        JsonNode: Allows you to work with JSON dynamically as a tree structure.
        SerializationFeature and DeserializationFeature: Configure serialization/deserialization behavior.
        
     ```JSON
     //Example conceptvf y87-=-
                ObjectMapper mapper = new ObjectMapper();

        // Convert JSON string to Java object
        String jsonString = "{\"name\": \"John\", \"age\": 30}";
        Person person = mapper.readValue(jsonString, Person.class);

        // Convert Java object to JSON string
        String jsonOutput = mapper.writeValueAsString(person);
3. Annotations

    ```Java
        com.fasterxml.jackson.annotation

        Provides annotations to customize JSON serialization/deserialization.
        These annotations are critical for fine-tuning the JSON representation of your Java objects.
        Key Annotations:

        @JsonProperty: Customize property names in JSON.
        @JsonIgnore: Ignore certain fields during serialization/deserialization.
        @JsonInclude: Include/exclude fields based on conditions (e.g., non-null fields only,
            @JsonInclude(JsonInclude.Include.NON_NULL),ALWAYS,non_Empty).
        @JsonValue: Customize how an object is serialized into JSON.
        @JsonCreator: Specify constructors or factory methods for deserialization.
        @JsonFormat: Format date/time fields

4. Example including all

## SKCET Experiments

1. 1_Experiment one

    ```Java
             @RestController
            @RequestMapping("/")
            public class ApiController {

                @GetMapping("welcome")
                public String helloGetter(){

                    //this will return the value required by the Json body
                    return "Welcome Spring Boot!";
                }


                
                @GetMapping("welcomenew")
                public void helloGetterNew(){

                    //this will return the value in the console 
                    System.out.println("This is the new Spring boortmessage ");
                }



    }

2. 1_Experiment two :

    ```Java
        
        @RestController("/")
        public class ApiController {

        @GetMapping("studentName")
        public String getStudent(@RequestParam(name="studentName") String studentName){
            return "Welcome " + studentName + "!";
        }

        @ExceptionHandler(MissingServletRequestParameterException.class)
            public String handleMissingParams(MissingServletRequestParameterException ex){
                return "The parameter"+ex.getParameterName()+"is missing.please provide the same";

            }
        }

3. 1_Experiment three:
4. 1_Excercise four:

    ``` Java
            @RestController
        @RequestMapping("/")
        public class AddressController {


            @GetMapping("address")
        public Address getAddressDetails(){

            return new Address(
                "John",123,"Main St",56001,"inf","Bang","jatjnd","india"
            );
        }
        }

5. 1_Execercise five:

    ```Java
                @RestController
            @RequestMapping("/")
            public class StudentController {

                @GetMapping("/student")
                public List<Student> getStudents(){
                        List<Student> students=new ArrayList<Student>();

                        //general way
                        // students.add(new Student("Jphn", "welcome John!"));
                        // students.add(new Student("peter", "welcome peter!"));
                        // System.out.println(students);
                        // System.out.println(students.get(0).getStudentName());
                        // return students;

                        //to achieve the same using the loop 
                    String[] arrayofstudents={"John","Albert","Ashok"};
                    for (String student : arrayofstudents) {
                            students.add(new Student(student,"Welcome, "+student+"!"));

                    }
                            return students;

                }



            }
6. 1_Challenge yourself two

    ```Java
    @RestController
    @RequestMapping("/")
    public class CollegeController {

        @GetMapping("college")
        public College getCollege(){

        //     List<College> collegedetails=new ArrayList<College>();
        //     collegedetails.add(new College("ABC College","Computer Science",1));
        //     System.out.println(collegedetails);
        //     return collegedetails;
        // }

        return new College("ABC College", "Computer Science",1);

        
        }

7. 2_value_annotation

    ```Java

        //controller 
            
                    package com.examly.springapp.controller;

            import org.springframework.web.bind.annotation.GetMapping;
            import org.springframework.web.bind.annotation.RequestMapping;
            import org.springframework.web.bind.annotation.RestController;

            import com.examly.springapp.config.AppConfig;

            @RestController
            @RequestMapping("/")
            public class ApiController {

                private AppConfig appconfig;

                ApiController(AppConfig appConfig){
                    this.appconfig=appConfig;

                }

                // @GetMapping("info")
                // public String getConfigurationDetails(){
                //     String finalconcatedvalue="App Name:"+appconfig.getAppName()+
                //     ",Version:"+appconfig.getAppVersion();
                //     return finalconcatedvalue;
                // }


                @GetMapping("info")
                public String getConfigurationDetails(){
                    return String.format("App Name:%s,Version:%s",appconfig.getAppName(),appconfig.getAppVersion());
                }
            }

        //config
            package com.examly.springapp.config;

        import org.springframework.beans.factory.annotation.Value;
        import org.springframework.context.annotation.Configuration;

        @Configuration
        public class AppConfig {


            @Value("${app.name}")
            private String appName;

            @Value("${app.version}")
            private String appVersion;
            public AppConfig(String appName, String appVersion) {
                this.appName = appName;
                this.appVersion = appVersion;
            }

                    // private  String appName;
                    // private  String appVersion;

                    // public AppConfig(@Value("${app.name}")String appName,@Value("${app.version}")String appVersion){
                    //     this.appName = appName;
                    //     this.appVersion =appVersion;

                    // }


            public void setAppName(String appName) {
                this.appName = appName;
            }
            public void setAppVersion(String appVersion) {
                this.appVersion = appVersion;
            }
            public String getAppName() {
                return appName;
            }
            public String getAppVersion() {
                return appVersion;
            }

        }

8. 2_class Excercise

    ```Java
    //controller
            package com.examly.springapp.controller;

        import org.springframework.web.bind.annotation.PostMapping;
        import org.springframework.web.bind.annotation.RequestBody;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RestController;

        import com.examly.springapp.model.Student;

        @RestController
        @RequestMapping("/")
        public class StudentController {


            /*There is an annotation called @Valid which is from the jakarta library, 
            we shall use the same for the validation to avoid the null value
            */
            @PostMapping("students")
            public String createStudent( @RequestBody Student student){

                return String.format("Student created:%s,Age:%s",student.getName(),student.getAge());

            }

        }

    //model
    package com.examly.springapp.model;

        import com.fasterxml.jackson.annotation.JsonProperty;

        public class Student {


            @JsonProperty("student_name")
            private String name;

            @JsonProperty("student_age")
            private int age;
            public Student(String name, int age) {
                this.name = name;
                this.age = age;
            }
            public void setName(String name) {
                this.name = name;
            }
            public void setAge(int age) {
                this.age = age;
            }
            public String getName() {
                return name;
            }
            public int getAge() {
                return age;
            }

            



        }

9. 2_Class Excercise using the Json Ignore

    ```Java
    //controller
            package com.examly.springapp.controller;

        import org.springframework.web.bind.annotation.GetMapping;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RestController;

        import com.examly.springapp.model.Student;

        @RestController
        @RequestMapping("/")
        public class StudentController {

            private Student student;

            public StudentController(Student student){

                this.student=student;

            }

            @GetMapping("student")
            public Student getStudentDetail(){

            return student;
            
            }
        }
    //App Config
        package com.examly.springapp.model;

        import org.springframework.context.annotation.Bean;
        import org.springframework.context.annotation.Configuration;

        @Configuration
        public class AppConfig {


            // This @Bean annotation in the @configuration class tells Spring to manage 
            // the student object as a singleton bean
            // the student object is created once and it is reused throughout the application
            // wherever it is injected.

            @Bean
            public Student student(){
                return new Student(1L,"John Doe","This is a student description" );
            }


        }

    //Student java class
            package com.examly.springapp.model;

        import com.fasterxml.jackson.annotation.JsonIgnore;

        public class Student {
            private long id;
            private String name;
            
            //this will ignore the field that is connected
            
            @JsonIgnore
            private String description;


            public long getId() {
                return id;
            }
            public void setId(long id) {
                this.id = id;
            }
            public void setName(String name) {
                this.name = name;
            }
            public void setDescription(String description) {
                this.description = description;
            }
            public Student(long id, String name, String description) {
                this.id = id;
                this.name = name;
                this.description = description;
            }
            public String getName() {
                return name;
            }
            public String getDescription() {
                return description;
            }



        }

10. 2_practice@Home

    // same like the AppConfig excercise

11. 2_JSONFormat

    ```Java
    //controller
    package com.example.springapp.controller;

        import org.springframework.web.bind.annotation.GetMapping;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RestController;

        import com.example.springapp.model.Book;

        @RestController
        @RequestMapping("/")
        public class BookController {

            private Book book;

        BookController(Book book){
        this.book=book;
        }

            @GetMapping("book")
            public Book getBooks(){
                return book;
            }

        }
    //AppConfig
    package com.example.springapp.model;

        import java.util.Date;

        import org.springframework.context.annotation.Bean;
        import org.springframework.context.annotation.Configuration;

        @Configuration
        public class AppConfig {

            @Bean
            public Book book(){
                return new Book("The Great Soldier", "G. Gyan", new Date());
            }

        }
    //Book class
    package com.example.springapp.model;

        import java.util.Date;

        import com.fasterxml.jackson.annotation.JsonFormat;

        public class Book {

            private String title;
            private String author;

            @JsonFormat(shape =JsonFormat.Shape.STRING, pattern="YYY-MM-dd" )
            private Date publicationDate;

            public Book(String title, String author, Date publicationDate) {
                this.title = title;
                this.author = author;
                this.publicationDate = publicationDate;
            }
            public String getTitle() {
                return title;
            }
            public String getAuthor() {
                return author;
            }
            public void setTitle(String title) {
                this.title = title;
            }
            public void setAuthor(String author) {
                this.author = author;
            }
            public void setPublicationDate(Date publicationDate) {
                this.publicationDate = publicationDate;
            }
            public Date getPublicationDate() {
                return publicationDate;
            }

            

        }


12. 2_Daily_Assessment_JSONinclude

    ```Java
        //Appconfig
        package com.example.springapp.config;

        import org.springframework.context.annotation.Bean;
        import org.springframework.context.annotation.Configuration;

        import com.example.springapp.model.Book;

        @Configuration
        public class AppConfig {

            @Bean
            public Book book(){
                return new Book("The Great Gatsby","F. Scott Fitzgerald",null,"978-3-16-148410-0");
            }

        }

        //controller
        package com.example.springapp.controller;

            import org.springframework.web.bind.annotation.GetMapping;
            import org.springframework.web.bind.annotation.RequestMapping;
            import org.springframework.web.bind.annotation.RestController;

            import com.example.springapp.model.Book;

            @RestController
            @RequestMapping("/")
            public class BookController {

                private Book book;

            public BookController(Book book){
                    this.book=book;
                }

                @GetMapping("book")
                public Book getBooks(){
                    return book;
                }

            }

            //Book
            package com.example.springapp.model;

            import com.fasterxml.jackson.annotation.JsonInclude;

            @JsonInclude(JsonInclude.Include.NON_NULL)
            //only non null fields are included
            public class Book {

                private String title;
                private String author;
                private String genre;
                private String isbn;
                public Book(String title, String author, String genre, String isbn) {
                    this.title = title;
                    this.author = author;
                    this.genre = genre;
                    this.isbn = isbn;
                }
                public String getTitle() {
                    return title;
                }
                public void setTitle(String title) {
                    this.title = title;
                }
                public String getAuthor() {
                    return author;
                }
                public void setAuthor(String author) {
                    this.author = author;
                }
                public String getGenre() {
                    return genre;
                }
                public void setGenre(String genre) {
                    this.genre = genre;
                }
                public String getIsbn() {
                    return isbn;
                }
                public void setIsbn(String isbn) {
                    this.isbn = isbn;
                }
                

            }

14. 4_second_cE_Class_Exercise_2_Springboot_Post_Get_job
    ```Java
        //controller
            package com.example.springapp.controller;


        import java.util.List;

        import org.springframework.http.HttpStatus;
        import org.springframework.http.ResponseEntity;
        import org.springframework.web.bind.annotation.GetMapping;
        import org.springframework.web.bind.annotation.PathVariable;
        import org.springframework.web.bind.annotation.PostMapping;
        import org.springframework.web.bind.annotation.RequestBody;
        import org.springframework.web.bind.annotation.RequestMapping;
        import org.springframework.web.bind.annotation.RestController;

        import com.example.springapp.exception.ResourceNotFOundException;
        import com.example.springapp.model.Job;
        import com.example.springapp.service.JobService;

        @RestController
        @RequestMapping("/api")
        public class JobController {

            private JobService jobService;

            JobController(JobService jobService){
                this.jobService=jobService;
            }

            @PostMapping("/job")
            public ResponseEntity<Job> addJob(@RequestBody Job job){
                Job addedjob=  jobService.addJob(job);
                return ResponseEntity.status(HttpStatus.CREATED).body(addedjob); //creatded = status 201
            }

            @GetMapping("/job")
            public ResponseEntity<List<Job>> getAllJob(){
            List<Job> alljob=jobService.getAllJob();
            if(alljob.isEmpty()){
                throw new ResourceNotFOundException("No job Found.");
            }
            return ResponseEntity.ok(alljob); //return 200 status
            }

            @GetMapping("/job/{jobId}")
            public ResponseEntity<Job> getJobById(@PathVariable int jobId){

                // this is ok since i have used optional and easy way too
                Job jobbyid=jobService.getJobBYId(jobId).orElseThrow(()->new ResourceNotFOundException("Th job Id"+jobId+"is not avvailable"));
                return ResponseEntity.ok(jobbyid);

            }

        }
    
    //Exception/Errorresponse
    package com.example.springapp.exception;

        public class ErrorResponse {

            private int statuscode;
            private String message;
            public ErrorResponse(int statuscode, String message) {
                this.statuscode = statuscode;
                this.message = message;
                this.timestamp=System.currentTimeMillis();
            }
            private long timestamp;
            public int getStatuscode() {
                return statuscode;
            }
            public void setStatuscode(int statuscode) {
                this.statuscode = statuscode;
            }
            public String getMessage() {
                return message;
            }
            public void setMessage(String message) {
                this.message = message;
            }
            public long getTimestamp() {
                return timestamp;
            }
            public void setTimestamp(long timestamp) {
                this.timestamp = timestamp;
            }
            

        }

    //Exception/Global
                package com.example.springapp.exception;

        import org.springframework.http.HttpStatus;
        import org.springframework.http.ResponseEntity;
        import org.springframework.web.bind.annotation.ControllerAdvice;
        import org.springframework.web.bind.annotation.ExceptionHandler;

        @ControllerAdvice
        public class GlobalExceptionhandler {

            @ExceptionHandler(ResourceNotFOundException.class)
            public ResponseEntity<ErrorResponse> handleResourceNotFound(ResourceNotFOundException ex){
                ErrorResponse erroResponse=new ErrorResponse(HttpStatus.NOT_FOUND.value(),ex.getMessage());
                return ResponseEntity.status(HttpStatus.NOT_FOUND).body(erroResponse);

                

            }


        }
    //Resource
        package com.example.springapp.exception;

        public class ResourceNotFOundException extends RuntimeException {

            public ResourceNotFOundException(String message){
                super(message);
            }
        }
    //model
        package com.example.springapp.model;

            import javax.persistence.Entity;
            import javax.persistence.GeneratedValue;
            import javax.persistence.GenerationType;
            import javax.persistence.Id;

            @Entity
            public class Job {

                @Id
                @GeneratedValue(strategy = GenerationType.AUTO)

                int jobId;
                String jobTitle;
                int minSalary;
                String jobDescription;
                int maxSalary;
                public Job(int jobId, String jobTitle, int minSalary, String jobDescription, int maxSalary) {
                    this.jobId = jobId;
                    this.jobTitle = jobTitle;
                    this.minSalary = minSalary;
                    this.jobDescription = jobDescription;
                    this.maxSalary = maxSalary;
                }
                public Job(){

                }
                public int getJobId() {
                    return jobId;
                }
                public void setJobId(int jobId) {
                    this.jobId = jobId;
                }
                public String getJobTitle() {
                    return jobTitle;
                }
                public void setJobTitle(String jobTitle) {
                    this.jobTitle = jobTitle;
                }
                public int getMinSalary() {
                    return minSalary;
                }
                public void setMinSalary(int minSalary) {
                    this.minSalary = minSalary;
                }
                public String getJobDescription() {
                    return jobDescription;
                }
                public void setJobDescription(String jobDescription) {
                    this.jobDescription = jobDescription;
                }
                public int getMaxSalary() {
                    return maxSalary;
                }
                public void setMaxSalary(int maxSalary) {
                    this.maxSalary = maxSalary;
                }

            }

    //service
        package com.example.springapp.service;

        import java.util.List;
        import java.util.Optional;

        import org.springframework.stereotype.Service;

        import com.example.springapp.model.Job;
        import com.example.springapp.repository.JobRepo;

        @Service
        public class JobService {

            private JobRepo jobRepo;

            JobService(JobRepo jobRepo){
                this.jobRepo=jobRepo;
            }

            public Job addJob(Job job){
                return jobRepo.save(job);
            }

            public List<Job> getAllJob(){
                return jobRepo.findAll();
            }

            public Optional<Job> getJobBYId(int jobId){
                return jobRepo.findById(jobId);
            }

        }

15. 4_EXC_1_Medicine
    ```Java
    //controller
    package com.examly.springapp.controller;

      import java.util.List;
      import java.util.Optional;
      
      
      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.http.ResponseEntity;
      import org.springframework.web.bind.annotation.GetMapping;
      import org.springframework.web.bind.annotation.PathVariable;
      import org.springframework.web.bind.annotation.PostMapping;
      import org.springframework.web.bind.annotation.RequestBody;
      import org.springframework.web.bind.annotation.RequestMapping;
      import org.springframework.web.bind.annotation.RestController;
      
      // import com.examly.springapp.exception.MedicineNotFoundException;
      import com.examly.springapp.model.Medicine;
      import com.examly.springapp.service.MedicineService;
      
      @RestController
      @RequestMapping("/api")
      public class MedicineController {

    @Autowired
    private MedicineService medicineService;

    @PostMapping("/medicine")
    public ResponseEntity<Medicine> addMedicine(@RequestBody Medicine medicine){
       try {
        Medicine createMedicine=medicineService.addMedicine(medicine);
        return ResponseEntity.status(201).body(createMedicine);
       } catch (Exception e) {
            return ResponseEntity.status(500).build();
       }
        

    }


    // @GetMapping("medicines")
    // public ResponseEntity<List<Medicine>> getAllMedicines(){
    //    List<Medicine> allMedicines= medicineService.getMedicines();
    //    if(allMedicines.isEmpty()){
    //     throw new MedicineNotFoundException("no medicines found");
    //    }else{

    //        return ResponseEntity.ok(allMedicines);
    //    }
    // }

    //for test case
      
      @GetMapping("/medicines")
          public ResponseEntity<List<Medicine>> getAllMedicines(){
      try {
          List<Medicine> allMedicines= medicineService.getMedicines();
          return ResponseEntity.status(200).body(allMedicines);
      } catch (Exception e) {
          return ResponseEntity.status(404).build();
      }
    

    }

    // @GetMapping("medicine/{medicineId}")
    // public ResponseEntity<Medicine> getMedicineById(@PathVariable int medicineId){
    //     return medicineService.getMedicineById(medicineId).
    //     map(ResponseEntity::ok) //thisd is equivalent to ResponseEntity.ok(Medicine)
    //     .orElseThrow(()->new MedicineNotFoundException("Medicine with ID"+medicineId+"not found."));
    // }


    //for testcase
    
    @GetMapping("/medicine/{medicineId}")
     public ResponseEntity<Medicine> getMedicineById(@PathVariable int medicineId){
       try {
           
           Optional<Medicine> getMedicneId= medicineService.getMedicineById(medicineId);
           if(getMedicneId.isPresent()){
            return ResponseEntity.ok(getMedicneId.get());
           }else{
            return ResponseEntity.notFound().build();
           }
       } catch (Exception e) {
        // TODO: handle exception
        return ResponseEntity.status(500).build();
       }
       
        
        
     }



      }

    //ErroResponse.java
    package com.examly.springapp.exception;
      
      public class ErrorResponse {
      
        private  int statuscode;
        private  String message;
        private  long timestamp;
      public int getStatuscode() {
          return statuscode;
      }
      public ErrorResponse(int statuscode, String message) {
          this.statuscode = statuscode;
          this.message = message;
          this.timestamp=System.currentTimeMillis();
      }
      public void setStatuscode(int statuscode) {
          this.statuscode = statuscode;
      }
      public String getMessage() {
          return message;
      }
      public void setMessage(String message) {
          this.message = message;
      }
      public long getTimestamp() {
          return timestamp;
      }
      public void setTimestamp(long timestamp) {
          this.timestamp = timestamp;
      }
      
        
      
      }

    //globalExceptionHandler
          // package com.examly.springapp.exception;
      
      // import org.springframework.http.HttpStatus;
      // import org.springframework.http.ResponseEntity;
      // import org.springframework.web.bind.annotation.ControllerAdvice;
      // import org.springframework.web.bind.annotation.ExceptionHandler;
      
      // // @controllerAdvice is the global exception handler for all controllers
      // // Custom ErroResponse also shall be added if required
      
      // @ControllerAdvice
      // public class GlobalExceptionHandler {
      //     @ExceptionHandler(MedicineNotFoundException.class)
      //     public ResponseEntity<ErrorResponse> handleMedicineNotFound(MedicineNotFoundException ex){
      //         ErrorResponse errorResponse=new ErrorResponse(404,ex.getMessage());
      //         return ResponseEntity.status(HttpStatus.NOT_FOUND).body(errorResponse);
      //     }
      
      //     @ExceptionHandler(Exception.class)
      //     public ResponseEntity<String> handleGenericException(Exception ex){
      // return ResponseEntity.status(HttpStatus.INTERNAL_SERVER_ERROR).body("An unexpected error occured.");
      //     }
      
      
      
      // }

    //medicineNotFounfdException
             // package com.examly.springapp.exception;

         
         // public class MedicineNotFoundException extends RuntimeException {
         
         //     public MedicineNotFoundException(String message){
         //        super(message);
         //     }
         
         // }

       //Medicine
       package com.examly.springapp.model;
      
      import javax.persistence.Entity;
      import javax.persistence.GeneratedValue;
      import javax.persistence.GenerationType;
      import javax.persistence.Id;
      
      @Entity
      public class Medicine {
      
          @Id
    @GeneratedValue(strategy = GenerationType.AUTO)
    int medicineId;
    String medicineName;
    String medicineFor;
    String medicineBrand;
    String manufacturedIn;
    Double medicinePrice;
    String expiryDate;
    public Medicine(int medicineId, String medicineName, String medicineFor, String medicineBrand,
            String manufacturedIn, Double medicinePrice, String expiryDate) {
        this.medicineId = medicineId;
        this.medicineName = medicineName;
        this.medicineFor = medicineFor;
        this.medicineBrand = medicineBrand;
        this.manufacturedIn = manufacturedIn;
        this.medicinePrice = medicinePrice;
        this.expiryDate = expiryDate;
    }
    public int getMedicineId() {
        return medicineId;
    }
    public void setMedicineId(int medicineId) {
        this.medicineId = medicineId;
    }
    public String getMedicineName() {
        return medicineName;
    }
    public void setMedicineName(String medicineName) {
        this.medicineName = medicineName;
    }
    public String getMedicineFor() {
        return medicineFor;
    }
    public void setMedicineFor(String medicineFor) {
        this.medicineFor = medicineFor;
    }
    public String getMedicineBrand() {
        return medicineBrand;
    }
    public void setMedicineBrand(String medicineBrand) {
        this.medicineBrand = medicineBrand;
    }
    public String getManufacturedIn() {
        return manufacturedIn;
    }
    public void setManufacturedIn(String manufacturedIn) {
        this.manufacturedIn = manufacturedIn;
    }
    public Double getMedicinePrice() {
        return medicinePrice;
    }
    public void setMedicinePrice(Double medicinePrice) {
        this.medicinePrice = medicinePrice;
    }
    public String getExpiryDate() {
        return expiryDate;
    }
    public void setExpiryDate(String expiryDate) {
        this.expiryDate = expiryDate;
    }   

      }
    //service
    package com.examly.springapp.service;

      import java.util.List;
      import java.util.Optional;
      
      import org.springframework.beans.factory.annotation.Autowired;
      import org.springframework.stereotype.Service;
      
      import com.examly.springapp.model.Medicine;
      import com.examly.springapp.repository.MedicineRepo;
      
      @Service
      public class MedicineService {


    @Autowired
    private MedicineRepo medicinerepo;

    public Medicine addMedicine(Medicine medicine){
        return medicinerepo.save(medicine);
    }

    public List<Medicine> getMedicines(){
        return medicinerepo.findAll();
		
	}

    // /*
    //  * Here i shall use without the optional also like this 
    //  * */
    //    public Medicine getMedicineById(int id){
    //     return medicinerepo.findById(id).orElse(null);
    // }

     

     
    public Optional<Medicine> getMedicineById(int id){
        return medicinerepo.findById(id); // since i use optional map shall be accessed in the contyroller class
    }
      }
    










## Others

1. JSON is an text format

    ```JSON
                {
        "name": "John Doe",
        "age": 30,
        "isStudent": false,
        "hobbies": ["reading", "gaming", "traveling"]
        }

    // Addon
    1. JSON does not support the comment
    2. JSON5 shall be sued for the external documentation
    3. **Date** is not a datatype of the JSON
    4. In Java JSON.parse() is acxhieved by the 
        In Java, the equivalent of JSON.parse() depends on the library used:

        Jackson: ObjectMapper.readValue()
        Gson: Gson.fromJson()
        org.json: JSONObject constructor
    5. JSON is used for serializing and transmitting structured data over the network connection.

2. **Why parsing is done in the JSOn:**\
        JSON parsing is done to convert JSON-formatted data into a usable format for the application or system, such as objects, arrays, or primitives in a programming language.
    1. Example

        ```JSON
        JSON.parse(text, [rev-iver])
        // valid JSON string to parsed into a javascript object
        const jsonString = '{"name":"John", "age":30}';
        const obj = JSON.parse(jsonString);
        console.log(obj); // { name: "John", age: 30 }

        // Here we shall change the data that is recived which means we shall  modify or else we shall filter the same
                const jsonString = '{"name":"Bob", "age":40}';
        const obj = JSON.parse(jsonString, (key, value) => {
        if (key === "age") {
            return value + 5; // Add 5 to the age
        }
        return value; // Keep other values unchanged
        });
        console.log(obj); // { name: "Bob", age: 45 }

3. Controller is also called as the **Presentation layer**
    controller is also a **Concrete class**
4. Which directives in the Http response cache control can be used to specify the cacheing time limit ?
    **max-age**
5. Which header should be configured to tell the server XML is preferred over JSON?
    Accept
6. Foundation layer
    In Spring Boot, the Foundation Layer refers to the core infrastructure and functionality that supports the other layers of the application (e.g., Web Layer, Service Layer, and Data Access Layer). This layer provides common features and services that are used across the application, such as:

7. JAX-RS
    * JAX--> Java API for Restful web service
8. Key Features of JAX-RS--->(Jakarta EE to be included)
    *
    **Annotation-Based API**:

    Use annotations like @Path, @GET, @POST, @Produces, and @Consumes to define resources and HTTP methods.
    **HTTP Method Mapping**:

    Map HTTP methods (GET, POST, PUT, DELETE) to Java methods using annotations like @GET and @POST.
    **Content Negotiation**:

    Supports producing and consuming multiple formats like JSON, XML, and plain text using @Produces and @Consumes.
    **Parameter Binding**:

    Binds query parameters, path parameters, and headers to method arguments using annotations like @QueryParam, @PathParam, and @HeaderParam.
9. why ot use the JSON Schema ?
    [(https://json-schema.org/overview/what-is-jsonschema)]
10. How the @valid is used over here.
        How @Valid Works
        When an object annotated with @Valid is passed into a method, Spring triggers validation of the object’s fields based on the constraints applied (e.g., @NotNull, @Size).
        If validation fails:
        For web applications, a MethodArgumentNotValidException is thrown.
        This exception can be handled to return user-friendly error messages.
11. what error will occur if we are going to use the empty application.properties file
while using the @value anotation:
    * It will throw error like
    * Caused by: java.lang.IllegalArgumentException: Could not resolve placeholder 'spring.application.name' in value "${spring.application.name}"
12. why ResponseEntity is added in the controller what is the usage of the same?

        ResponseEntity is a Spring framework class that represents the entire HTTP response, including:

        HTTP Status Code: Specifies the status of the response (e.g., 200 OK, 404 Not Found).
        Response Headers: Metadata like content type, caching, etc.
        Response Body: The actual data sent back to the client (e.g., JSON, plain text).

     ```Java
    //Fine grained response control is achieved by using the response entity
                    @GetMapping("/example")
            public ResponseEntity<String> example() {
                return ResponseEntity.status(HttpStatus.OK)
                                    .header("Custom-Header", "ExampleValue")
                                    .body("Hello, World!");
            }

13. whay @pathVariable is used ?
    @GetMapping: Maps GET requests to /medicine/{medicineId}.
    @PathVariable: Extracts the medicineId from the URL.

## Mysql

1. To get the **Database** name in the portal use:
    SELECT DATABASE();
2. To get the **Version** in the portal use:
    SELECT VERSION();
3. Key parameters to remeber
    CHAR_LENGTH, AUTO_INCREMENT,COUNT,AVG,GROUP_CONCAT,UPPER,DATE_FORMAT
4. To get the Current_date is
    current_date;
5. How to show the tables ?
    use database_name;
    show tables;
6. How to uniquely identify the key
    Superkey: A superkey is any set of columns that can uniquely identify a row in a table. It may include extra attributes (columns) that are not necessary for unique identification.

    Candidate Key: A candidate key is a minimal superkey, meaning it is a superkey with no unnecessary attributes. It is a subset of a superkey that uniquely identifies rows, and there is no smaller subset that can also uniquely identify rows.
7. what is cross join ?
    Cross Join: A CROSS JOIN returns the Cartesian product of the two tables involved. This means that for each row in the first table, it combines with all rows in the second table.

        If table A has m rows and table B has n rows, the result of a CROSS JOIN will have m * n rows.
8. To undo a GRANT in MySQL, you should use the REVOKE statement.
9. How to use the substring the mysql.
    SELECT INSTR('I have an apple and an orange', 'apple');
    // answer = 12 (12th position of the above given value is the apple)
10. what is the use of the def in the query we used to create .
    // used with the trigger , see online for more information
11. **How to check the relationship with the tables in the mysql database**
    SHOW CREATE TABLE account;
