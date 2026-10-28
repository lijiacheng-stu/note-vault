Lombok 的作用：通过注解自动生成 Java 中重复、繁琐的样板代码（Boilerplate Code），让代码更简洁。

常见的注解：
- 构造器
	- `@NoArgsConstructor` 自动生成无参构造方法
	- `@AllArgsConstructor` 自动生成包含所有字段的构造方法
	- `@RequiredArgsConstructor` 为 `final` 字段和标记了 `@NonNull` 的字段生成构造方法
- `@Data`
	-  The `@Data` annotation implicitly adds a required arguments constructor, but when a `@NoArgsConstructor` is used, that constructor is removed. An explicit `@RequiredArgsConstructor` ensures that you’ll still have a required arguments constructor, in addition to the `private` no-arguments constructor.
	- 综合提供 getter、setter、`toString()`、`equals()`、`hashCode()` 等功能
- @Slf4j

