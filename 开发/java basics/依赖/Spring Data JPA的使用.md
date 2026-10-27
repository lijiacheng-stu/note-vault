## annotating the domain as entities
1. @Entity，类，用以标注JPA实体
2. @Id，属性，用于指定主键，javax.persistence，而不是`org.springframework.data.annotation` package
3. `@NoArgsConstructor(access=AccessLevel.PRIVATE, force=true)`，类
	- access=AccessLevel.PRIVATE，表示private修饰
	- force=true，表示对final给一个默认值
4. @GeneratedValue(strategy = GenerationType.AUTO)，属性，Because you’re relying on the database to automatically generate the ID value, you also annotate the `id` property with `@GeneratedValue`, specifying a `strategy` of `AUTO`.
5. @OneToMany,  @ManyToMany()，属性，用以标注Collection属性，AToB，A表示ClassB的1个对应多少个ClassA，B表示ClassA的1个对应多少个ClassB。
```
@OneToMany(cascade = CascadeType.ALL)
private List<Taco> tacos = new ArrayList<>();

@ManyToMany()
private List<Ingredient> ingredients = new ArrayList<>();
```

## Declaring JPA repositories
```
public interface IngredientRepository 
         extends CrudRepository<Ingredient, String> {
  
}
```
- Ingredient是entity类型
- String是主键（ID）的数据类型。


