# The Magic of LRU Cache

这小节我们要讨论的是缓存算法，在Android上面最常用的一个缓存算法是LRU(Least Recently Use)，关于LRU算法，不展开述说，用下面一张图演示下含义：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_lru_mode.png)

LRU Cache的基础构建用法如下：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_lru_key_value.png)

为了给LRU Cache设置一个比较合理的缓存大小值，我们通常是用下面的方法来做界定的：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_lru_size.png)

使用LRU Cache时为了能够让Cache知道每个加入的Item的具体大小，我们需要Override下面的方法：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_lru_sizeof.png)

使用LRU Cache能够显著提升应用的性能，可是也需要注意LRU Cache中被淘汰对象的回收，否者会引起严重的内存泄露。