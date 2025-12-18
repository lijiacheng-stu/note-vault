 The `spring-boot-starter-parent` is a special starter that provides useful Maven defaults. It also provides a [`dependency-management`](https://docs.spring.io/spring-boot/reference/using/build-systems.html#using.build-systems.dependency-management) section so that you can omit `version` tags for “blessed” dependencies.

```
package com.example;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

@RestController
@SpringBootApplication
public class MyApplication {

	@RequestMapping("/")
	String home() {
		return "Hello World!";
	}

	public static void main(String[] args) {
		SpringApplication.run(MyApplication.class, args);
	}

}
```
The first annotation on our `MyApplication` class is [`@RestController`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/web/bind/annotation/RestController.html). This is known as a _stereotype_ annotation. It provides hints for people reading the code and for Spring that the class plays a specific role. In this case, our class is a web [`@Controller`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/stereotype/Controller.html), so Spring considers it when handling incoming web requests.

The [`@RequestMapping`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/web/bind/annotation/RequestMapping.html) annotation provides “routing” information. It tells Spring that any HTTP request with the `/` path should be mapped to the `home` method. The [`@RestController`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/web/bind/annotation/RestController.html) annotation tells Spring to render the resulting string directly back to the caller.

The second class-level annotation is [`@SpringBootApplication`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/autoconfigure/SpringBootApplication.html). This annotation is known as a _meta-annotation_, it combines [`@SpringBootConfiguration`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/SpringBootConfiguration.html), [`@EnableAutoConfiguration`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html) and [`@ComponentScan`](https://docs.spring.io/spring-framework/docs/6.2.x/javadoc-api/org/springframework/context/annotation/ComponentScan.html).
Of those, the annotation we’re most interested in here is [`@EnableAutoConfiguration`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html). [`@EnableAutoConfiguration`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/autoconfigure/EnableAutoConfiguration.html) tells Spring Boot to “guess” how you want to configure Spring, based on the jar dependencies that you have added. Since `spring-boot-starter-web` added Tomcat and Spring MVC, the auto-configuration assumes that you are developing a web application and sets up Spring accordingly.

Our main method delegates to Spring Boot’s [`SpringApplication`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/SpringApplication.html) class by calling `run`. [`SpringApplication`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/SpringApplication.html) bootstraps our application, starting Spring, which, in turn, starts the auto-configured Tomcat web server. We need to pass `MyApplication.class` as an argument to the `run` method to tell [`SpringApplication`](https://docs.spring.io/spring-boot/3.4.4/api/java/org/springframework/boot/SpringApplication.html) which is the primary Spring component. The `args` array is also passed through to expose any command-line arguments.

Type `mvn spring-boot:run` from the root project directory to start the application.