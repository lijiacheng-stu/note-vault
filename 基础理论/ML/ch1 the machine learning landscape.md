- OCR
- the spam filter

- 语音提示
- 自动翻译
- 产品推荐
- 图像搜素

- chatbot

观念：大数据，硬件的提升，算法，三个东西让机器学习的应用诞生。


### what is machine learning
什么是机器学习？
- 给计算机编程使计算机能够从数据中学习的课程的科学

怎么判断计算机从数据中学习了？
- 定义：如果计算机程序针对任务T的性能P，随着经验E而提高，那么我们就说这段程序经验E中学习了。



- 训练集，训练实例（样本），模型
- T, E, P(P需要定义，比如准确度)

模型：
The part of a machine learning system that learns and makes predictions is called a _model_.

训练集：
The examples that the system uses to learn are called the _training set_.

训练实例：
 Each training example is called a _training instance_ (or _sample_)

T：
 to flag spam for new emails
E:
 the _training data_
 P:
 _P_ needs to be defined; for example, you can use the ratio of correctly classified emails.


### Why use Machine learning

什么是数据挖掘？
Digging into large amounts of data to discover hidden patterns is called _data mining_, and machine learning excels at it.

什么是模式呢？
-  unsuspected correlations or new **trend**？



### Types of Machine Learning Systems

三种分类标准，这些标准相互独立，所以可以任意组合。就像是对人在年龄，性别，身高上的分类一样：
- How they are guided during training (supervised, unsupervised, semi-supervised, self-supervised, and others)
    
- Whether or not they can learn incrementally on the fly (online versus batch learning)
    
- Whether they work by simply comparing new data points to known data points, or instead by detecting patterns in the training data and building a predictive model, much like scientists do (instance-based versus model-based learning)

#### Training Supervison

Supervised learning
- 定义/特征:In _supervised learning_, the training set you feed to the algorithm includes the desired solutions, called _labels_
- 任务：
	- classification： it must learn how to classify new emails.
	- regression： predict a _target_ numeric value
- 注意：Note that some regression models can be used for classification as well, and vice versa. 例如：logistic regression

#### Unsupervised learning
- 特征：In _unsupervised learning_, as you might guess, the training data is unlabeled.
- 概念：
	-  _feature extraction_：merge several correlated features into one. 
	- _dimensionality reduction_： the goal is to simplify the data without losing too much information.
	- 注：特征提取是降维的一种方式
- 任务：
	- 聚类
	- 可视化
	- 降维
	- 异常检测
	-  _association rule learning_

Semi-supervised learning
- 特征：半监督算法是监督算法和无监督算法的结合。例如：通过聚类算法将相似的实例放在一个组里面，这样没有被标记的实例就可以被统一标记了，大大节省了标记的成本。标记好后，就可以用任何监督学习的算法了。

- 使用场景：少量数据被标记，大量数据没有被标记

自监督学习：
For example, suppose that what you really want is to have a pet classification model: given a picture of any pet, it will tell you what species it belongs to. If you have a large dataset of unlabeled photos of pets, you can start by training an image-repairing model using self-supervised learning. Once it’s performing well, it should be able to distinguish different pet species: when it repairs an image of a cat whose face is masked, it must know not to add a dog’s face. Assuming your model’s architecture allows it (and most neural network architectures do), it is then possible to tweak the model so that it predicts pet species instead of repairing images. The final step consists of fine-tuning the model on a labeled dataset: the model already knows what cats, dogs, and other pet species look like, so this step is only needed so the model can learn the mapping between the species it already knows and the labels we expect from it.
 这里的自监督学习，感觉像是给一个完整的没标签的训练集，然后挖掉每个训练实例的一部分，然后(挖掉部分)作为新的训练集，而完整部分作为label，进行监督学习。




Out-of-core learning is usually done offline (i.e., not on the live system), so online learning can be a confusing name. Think of it as incremental learning. Moreover, mini-batches are often just called “batches”, so batch learning is also a confusing name. Think of it as learning from scratch on the full dataset. 
这段话我可以这么理解吗？online learning的过程往往是在offline（不需要网络）状态下进行的，所以这个名字容易让人产生误解（误解的内容是把online learning理解成需要连接网络的学习，其实online learning中online强调的是模型能随新数据实时更新而非网路），用incremental learning来等价理解online learning。 因为在online learning中涉及mini-batchs（也即batchs），所以batch learning这个名字也容易被误解（误解成online learning中练习新batchs的一个步骤），所以用基于完全的数据集从零开始学习来理解batch learning

![[Pasted image 20251022154735.png]]

典型的机器学习项目的工作流：研究数据，选择模型，训练模型，使用模型

训练模型：寻找让损失函数最小的参数。
- 损失函数的选择
- 学习算法的选择