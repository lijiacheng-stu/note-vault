## The curse of Dimensionality
讲的是降维的必要性：
 high-dimensional datasets are often very sparse：
- -->most training instances are likely to be far away from each other, so training methods based on distance or similarity (such as _k_-nearest neighbors) will be much less effective.
- --> some types of models will not be usable at all because they scale poorly with the dataset’s dimensionality (e.g., SVMs or dense neural networks).
- -->new instances will likely be far away from any training instance, making predictions much less reliable
-  -->patterns in the data will become harder to identify, models will tend to fit the noise more frequently than in lower dimensions;
- -->models will become even harder to interpret.
解决方案：
增加训练集的数量，但是：With just 100 features—significantly fewer than in the MNIST problem—all ranging from 0 to 1, you would need more training instances than atoms in the observable universe in order for training instances to be within 0.1 of each other on average, assuming they were spread out uniformly across all dimensions.
