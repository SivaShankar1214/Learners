### what is Spring?
- It is a Java Framework which was developed to make enterprise Java Application easier.

### what is Inversion of Control(IOC)?
- Inversion of Control is a principle which transfers the control of objects of a 
- program to a Container/framework.
- we can achieve IOC through various design patterns like Strategy,Service Locator pattern,Factory and Dependency Injection Pattern(DI).
	
### what is Dependency Injection?
- Dependency Injection is a pattern used to implement IOC where the control is being inverted is setting an Object's dependencies.//where control is transfered to framework/container
- Eg:Spring achieves DI using BeanFactory,ApplicationContext interfaces where user need to provide meta data to beans in the form of XML or annotations.

### Spring IOC Container
- Spring IOC Container is responsible for instantiation,configuring and assembling the beans. the Container gets its information on what objects to instantiate, configure and manage by reading configuration meta data we define for the application.
- There are two main IOC Containers i.BeanFactory ii.ApplicationContext.
#### BeanFactory
- BeanFactory interface is a simplest yet configurable way to manage objects by Spring IOC Container which takes care of life cycle of a bean.
- But It does not support annotations.
#### ApplicationContext
- is a IOC Container which was used to manages objects which takes care of Life cycle of a bean.
Same as BeanFactory but Spring Recommends ApplicationContext as it was a superset of BeanFactory.

#### Difference b/w BeanFactory and ApplicationContext?
- Both supports Bean instantiation/wiring but does not support Convenient MessageSource access (for i18n) and Automatic BeanPostProcessor/BeanFactoryPostProcessor  registration(transactions and AOP will not take effect in BeanFactory because of above items) and ApplicationEvent publication(Supports custom Events).
- Bean Factory = Basic management of beans and wiring of beans. spring recommeds only for memory are resource less space like IOT Devices where memory and space is very less.
- Application Context = Bean Factory ++ Spring's AOP Features + I18n capabilities + WebApplicationContext for Web Applications

### Spring Dependency Injection Types
- Dependency Injection in Spring Can be done through Constructor,Setter and Field.

#### Constructor Injection
- The Container will invoke a constructor with arguments each representing a dependency we want to set.

#### Setter Injection
- The Container will call a setter methods of our class after invoking a no-argument
constructor or no argument static factory method to instintiate the bean.
- We can combine Constructor/Setter for a same bean. Spring recommends constructor-based injection for mandatory and setter for optional dependencies. 
	
#### Field Injection
- we can inject the dependency by marking them with an @Autowired Annotation.

- Drawbacks of Field Injection:::
	1. This Method uses Reflection to inject dependencies which was costlier than other two.
	2. It's Really easier to add multiple dependencies, having multiple arguments/dependencies makes us think that the class does more than one thing which violate the Single Responsibility Principle. 
	
### Auto wired modes/types in Spring
- NO         : default Type:No wiring is used for the bean and we have to explictly name the dependencies.
- byName     : auto wiring can be done based on the name of the property.
- byType     : auto wiring can be done based on the type of the property.
- constructor:auto wiring can be done based on the constructor arguments where spring will look for the same type of constructor arguments.
	
Lazy Initialized Beans
- By default, the container creates and configures all singleton beans during initialization, to avoid this we can use lazy-init with value "true".
- Faster initialization but Disadvantage is we cannot find any error until it was initialized.

### Dependency Injection Design Pattern?
The dependency injection technique is a popular alternative to the service locater pattern. 

### Bean Scopes in Spring:
- The Scope of a Bean Defines life cycle and visibility of that bean in it's context we use it.   
	There are 6 Bean Scopes as per latest Spring version. Last four are web aware related. 
- Singleton:The Container creates a single instance of that bean.all requests to the bean returns same object which was cached.Default Scope Singleton if no Scope is defined by user.
- prototype:The Container will create a different instance for all the requests to that bean.
Web Aware Scopes
- Request -> The Request Scope will create a bean instance for a single HTTP Request.
- Session -> The Session Scope will create a bean instance for a HTTP Session.
- Application -> Creates a bean instance for the lifecycle of a ServletContext.
- WebSocket -> Creates a bean for a particular WebSocket Session.

Bean Life Cycle
- when Container Starts, a Spring Bean needs to be instantiated based on java/xml bean definition. it may be required to perform some initialization to get it into a usable state. Similarly, when the bean is no longer required and is removed from the container, some cleanup may be required.
- Container is responsible for managing the life cycle of beans created through spring container.
- There are two types of life cycle callbacks,
	1. Post-initialization call back methods.
	2. pre-destruction call back methods.
- Four ways of Controlling Bean Life Cycle events:
	1.	initializingBean(afterPropertySet()) and disposableBean(destory()) Callback interfaces.
		- Not recommended way as it has tight Couple your bean class with spring container.
	2. *Aware interfaces for specific behaviour.
		- Spring Provides a set of *Aware interface which we need to provide implementation to them.
	3. custom init() and destroy() methods.
			this can be defined in 
        - BeanLocal Definition :::In XML to a single bean tag with init-method and destroy-method 
        - Global Definition :::In XML to a beans tag with init-method and destroy-method
	4. @PostConstruct and @PreDestroy Annotations:::
        Spring Call these methods only once and they are JSR-250 annotations.
         - PostConstruct::: will be called just after the created with default constructor and before it was returned to requested object.
         - PreDestory: is called just before the bean is about to destroyed inside the bean container.
         - These are part of JavaEE and JavaEE was deprecated in java 9 and removed in java 11. so, we need to add additional dependency :javax.annotation.

### Major Annotations in Spring

### @Bean
	@Bean will return an object that should be registered as a bean in the Spring application context.
	To declare a bean, simply annotate a method with the @Bean annotation. When JavaConfig encounters such a method, it will execute that method and register the return value as a bean within a BeanFactory. By default, the bean name will be the same as the method name. @Bean is a method-level annotation is same as XML <bean/> element. it supports autowired,lazy-init,scope,init-method etc attributes.
### @Configuration (@Component vs @Configuration)
	@Configuration indicates that the class can be used by the Spring IoC container as a source of bean definitions. it was similar to spring-beans.xml
### @Component
	You cannot autowire (@Autowired) any class if it is not marked with @Component. It means when you want to autowire any class using annotation that class should be annotated with @Component.
### @Primary
	we use @Primary to give higher preference to a bean when there are multiple beans of the same type.  It sets the bean preference 
### @Autowired
	It allows Spring to resolve and inject collaborating beans into our bean
	the default method of auto wiring for this is "byType"
### @Qualifier
	we can eliminate the issue of which bean needs to be injected with the help of @Qualifier
### @ComponentScan
	we use the @ComponentScan annotation along with the @Configuration annotation to specify the packages that we want to be scanned. @ComponentScan without arguments tells Spring to scan the current package and all of its sub-packages.
