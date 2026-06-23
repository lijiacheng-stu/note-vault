@SpringBootApplication:
- @SpringBootConfiguration
- @EnableAutoConfiguration
- @ComponentScan


@SpringBootTest:
- it’s enough to think of this as the test class equivalent of calling `SpringApplication.run()` in a `main()` method.


@WebMvcTest(HomeController.class)