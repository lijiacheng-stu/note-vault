- Frame the Problem
	- 明确目标
	- 已有的解决方案
	- 设计系统：kind of training supervision,task, batch learning/ online learning 
- Select a Performance Measure
- Check the Assumptions


打开在集成开发环境中，打开`.ipynb`文件需要关心的一些点：
- 当前工作目录(cwd)：因为这关系到相对路径如何转化成绝对路径，继而影响指令执行的效果。
- 运行环境：运行python脚本所需的python解释器和依赖库。

集成开发环境：
- jupyter lab
- colab
- kaggle等

在jupyter lab中打开`.ipynb`文件的特点：
- 在普通的powershell中打开，cwd就是powershell的cwd，运行环境就是系统的运行环境。
- 在anaconda powershell中打开，cwd就是anaconda powershell的cwd，运行环境就是执行`jupyter lab`指令时括号里指明的环境。

在colab中`.ipynb`文件的特点：
- 运行在Linux上，且cwd是`/content`
- colab中的运行环境取决于什么呢？
	- 在`/usr/local/lib/pythonX.X/dist-packages` 可以查看到


对colab的认识：
- 怎样才能从github中导入ipynb
	- 3个主要途径：
		- github:通过仓库名搜索
		- 本地上传
		- Google Drive
	- 一个快捷方式：
		- Recent
- 下载的数据集，会放在什么位置？
	- 背景知识：在colab中，打开一个notebook，在google的云服务器提供一个notebook执行需要的运行环境runtime给自己，这个运行环境的特点是安装好了各种环境。这个runtime的当前工作目录是/content。 注意后面写的路径如果是相对路径，那就是相对工作目录而言的。
	- 在下载数据集时，会指定路径，就会安装在指定的路径中。安装也会安装在虚拟机中。
	- 可以通过将自己的Google Drive 挂载到指定的目录下面，然后再将数据集的安装路径指定到Google Drive中，那么就可以实现永久保存了。
- 怎么获得当前工作目录呢？
```
	import os
	os.getcwd()
```
- 在colab中打开`.ipynb` 文件并产生了修改，这样的修改是否会同步到数据来源？
	- 通过colab打开Google Drive中的，colab和google drive登录同一个账号时，是可以同步的。
	- 对来自github的notebook的修改时不会保存的


对rbf

![[Pasted image 20251028212519.png]]
不理解？




为什么不手动下载数据，而是写脚本用函数？
- 数据源可能会变化
- 多机器下载数据集，一套代码就能搞定

 & 


reg add "HKLM\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14\3895955085" /v EnabledState /t REG_DWORD /d 1 /f & reg add "HKLM\SYSTEM\ControlSet001\Control\FeatureManagement\Overrides\14\3895955085" /v EnabledStateOptions /t REG_DWORD /d 0 /f



"C:\Program Files\WindowsApps\28017CharlesMilette.TranslucentTB_2025.1.0.0_x64__v826wp6bftszj\TranslucentTB.exe"

我正在阅读Hands-On Machine Learning with Scikit-Learn and PyTorch的第二章。我产生了对

