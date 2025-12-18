一、读写文件
1. with的作用
```
filename = 'pi_digits.txt'
with open(filename) as file_object:
	//snips
```
系统根据snip中的运行情况，择机打开和关闭文件，释放相应的系统资源。

2. 在路径中`\`的作用
- 命名：backslash. 看上头，往后为backslash,往前为forward slash
- 作用：防止某些字符被解析为字符串。`\t` 防止t被解析成字符串，表示制表符。 `\` 如果是字符串，则得`\\` 
- `\` 与`/` :在Windows中，都行，注意反斜杠在作用中的特性。

3. 一些方法
- open(): 
```
//四种模式，默认只读。'r' 'w' 'a' 'r+' 
//a = append 
//r+ = read + write
//'w': 清除文件后再写，没有文件将创建文件
```

- 对文件以字符串形式的读写：
	- file_object.read()
	- file_object.readlines()
	- file_object.write()：
	```
	// The write() function doesn’t add any newlines to the text you write. 
	
	// 写方法都是往文件后面增内容，清除写或者非清除写的操作发生在open()的模式选择时
	```

- 对文件以json格式的读写：
```
import json
//写list型和dictionary型
ls = [1, 2, 3, 4]
json.dump(ls, f) //f 是文件对象，由open()生成

dic = {"name": 'lsx', age: 22, }
json.dump(dic, f)

//读
ls = json.load(f)
dic = json.load(f)
```

4. convention 规范：
```
//用f标识文件对象。the use of the variable f to represent the file object, which is a common convention
```

二、异常的处理
```
try:
	//snippets,仅仅包含可能出现异常的代码，一般属于外部错误
		//类型一：用户输入格式非法
		//类型二：文件不存在
		//类型三：网络连接失败
except <异常类型> [as <异常类型的具体对象>]:
	//异常处理操作
else:
	//snippets，try中未出现异常，执行该语句，要求对try中的东西有依赖关系。
```