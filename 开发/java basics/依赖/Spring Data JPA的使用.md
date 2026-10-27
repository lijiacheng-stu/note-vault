1. @Entity，类，用以标注JPA实体
2. @Id，属性，用于指定主键，javax.persistence，而不是`org.springframework.data.annotation` package
3. `@NoArgsConstructor(access=AccessLevel.PRIVATE, force=true)`，类
	- access=AccessLevel.PRIVATE，表示private修饰
	- force=true，表示对final给一个默认值
4. @GeneratedValue(strategy = GenerationType.AUTO)，属性，Because you’re relying on the database to automatically generate the ID value, you also annotate the `id` property with `@GeneratedValue`, specifying a `strategy` of `AUTO`.
5. @ManyToMany()，属性，用以标注Collection属性
```

```