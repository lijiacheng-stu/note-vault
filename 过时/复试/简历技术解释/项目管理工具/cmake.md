cmake是c++的项目管理工具。
通过编辑cmakelists.txt来管理项目。核心的两句话add_executable()和add_library()，分别用于生成可执行文件和库文件。target_include_directories()和target_link_diretories()，target_link_libraries()是服务于上面这两个函数的。分别用于指明头文件的位置，以及链接的时候链接哪儿写已经编译好的库。
cmake本质上是一个翻译层，真正在构件项目的是传统的构件工具如ninja和Make。以使用ninja为例，通过cmake将cmakelists.txt翻译成构建配置文件build.ninja,ninja按照build文件构建项目。构建项目工具在涉及编译等操作的使用也是使用底层的编译工具，比如MINGW里面的g++，gcc。这三层架构，下面两层都可以根据自己的环境进行配置。可以从指令的角度来理解，在bash中命令`cmake -G "MinGW Makefiles" ../Step1` 实现的是翻译，翻译成的makefile适合mingw32-make.exe来构建。`cmake --build .` 调用mingw32-make.exe对makefiles文件实现构建项目。
此外，使用cmake指定cmake的版本，项目的名称，使用c++的版本
