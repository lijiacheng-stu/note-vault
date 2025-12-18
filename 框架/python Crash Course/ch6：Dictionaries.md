1. 思想之字典的用法：
	- 用法一：字典可以用来存储一个对象的各种信息，这个时候字典的名字表明这个对象，键值对中的键表明这个对象的某个属性信息。
	```
	alien_0 = {'color': 'green', 'points': 5}
	```
	- 用法二：字典可以用来存储多个对象一个属性的信息，这个时候字典的名字表明这个属性，见hi对中的键表明这个对象
	```
	favorite_languages = {
		'jen': 'python',
		'sarah': 'c',
		'edward': 'ruby',
		'phil': 'python'
	}
	```
	- 底层逻辑：属性和对象是多对多的关系！
2. 规范：It’s good practice to include a comma after the last key value pair as well, so you’re ready to add a new key value pair on the next line.
![[Pasted image 20250529015710.png]]
3. 遍历字典时，键值对的访问顺序于插入字典的顺序相同
二、增删改查
4. 增
```
alien_0 = {'color': 'green', 'points': 5}
alien_0[x_coodinate] = 0;
```
3. 删
```
alien_0 = {'color': 'green', 'points': 5}
del alien_0['color']
```
4. 改
```
alien_0 = {'color': 'green', 'points': 5}
alien_0['color'] = 'yellow'
```
5. 查
```
alien_0 = {'color': 'green', 'points': 5}
print(alien_0['color'])

color_value = alien_0.get('color', 'No color value assigned')
print(color_value)
```
三、遍历
6. 遍历键值对
核心方法：将字典转化成能迭代的类型 dictionary.items();
![[Pasted image 20250529115640.png]]
```
user_0 = {
	'username': 'efermi',
	'first': 'enrico',
	'last': 'fermi'
}
for key,value in user_0.items():
	//snippits
```
7.  访问键
核心方法：dictionary.keys()
注意：通过键也可以访问到值。6和7本质上都可以。
![[Pasted image 20250529115814.png]]
8. 访问值
核心方法：dictionary.values()
注意：键值对中键一定是不重复的，但是值可能是重复的。dictionary.values()方法不提供对应的重复审查，直接放在列表中。
![[Pasted image 20250529120844.png]]
9. 通用（个人）：
	`.items() .keys() .values()` 返回值都是特殊的不可修改的列表，但可以使用`set() sorted()`等方法，不改变原来的列表，仅仅按照函数特点返回对应的要求的数据结构。
三、嵌套
10. A List of Dictionaries
11.  A List in Dictionary
12. A Dictionary in aD Dictionary