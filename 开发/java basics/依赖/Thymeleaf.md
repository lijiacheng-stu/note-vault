View libraries such as Thymeleaf are designed to be decoupled from any particular web framework. As such, they’re unaware of Spring’s model abstraction and are unable to work with the data that the controller places in `Model`. But they can work with servlet request attributes. Therefore, before Spring hands the request over to a view, it copies the model data into request attributes that Thymeleaf and other view-templating options have ready access to.


 if there were a request attribute whose key is `"message"`, and you wanted it to be rendered into an HTML `<p>` tag by Thymeleaf, you’d write the following in your Thymeleaf template:
 `<p th:text="${message}">placeholder message</p>`
 
 
 Thymeleaf namespace attribute
 - th:text, performs the replacement.
 - th:each, iterates over a collection of elements, rendering the HTML once for each item in the collection.
 - th:field, ultimately sets the `<input>` element’s `name` attribute
 - th:action，是form标签的属性，决定要不要注入 CSRF。Thymeleaf 的 Spring 集成里有个专门处理 action 的处理器，只要标签上写了 th:action，它就会调用 Spring 的 RequestDataValueProcessor 往表单里塞 _csrf 隐藏字段。和值的写法无关。

operator：
- ${}，use the value of a request attribute
- @{}, is used to produce a context-relative path to the static artifacts that these tags are referencing. As you learned in chapter 1, static content in a Spring Boot application is served from the /static directory at the root of the classpath.
- 