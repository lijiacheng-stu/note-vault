cmake管理的项目的文件夹
- 项目
	- src
	- build
src是PROJECT_SOURCE_DIR的值
build是PROJECT_BINARY_DIR的值

- 在Step1_build目录下，使用命令：
`cmake -G "MinGW Makefiles" ../Step1`
该指令的效果是对指定的的文件夹以其中含有cmakelists.txt为蓝本，翻译成指定的makefile文件。有多种类型，通过-G来指定。在环境变量中，使用的是MinGW开发工具集，而cmake默认的不是，所以得指定为MinGW的。
使用该指令的文件夹下会生成对应的makefile文件，并且该文件夹称为PROJECT_BINARY_DIR指定的文件夹
- 在Step1_build文件夹中使用如下命令：
`cmake --build .`
按照当前目录的makefile，cmake使用mingw提供的工具构建项目
对target_include_directories()命令中public interface private的理解：
![[Pasted image 20250302222905.png]]

