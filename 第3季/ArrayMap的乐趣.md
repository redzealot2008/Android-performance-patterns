# Fun with ArrayMaps

程序内存的管理是否合理高效对应用的性能有着很大的影响，有的时候对容器的使用不当也会导致内存管理效率低下。Android为移动操作系统特意编写了一些更加高效的容器，例如SparseArray，今天要介绍的是一个新的容器，叫做[ArrayMap](https://android.googlesource.com/platform/frameworks/base.git/+/master/core/java/android/util/ArrayMap.java)。

我们经常会使用到HashMap这个容器，它非常好用，但是却很占用内存。下图演示了HashMap的简要工作原理：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_3_arraymap_key_value.png)

为了解决HashMap更占内存的弊端，Android提供了内存效率更高的ArrayMap。它内部使用两个数组进行工作，其中一个数组记录key hash过后的顺序列表，另外一个数组按key的顺序记录Key-Value值，如下图所示：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_3_arraymap_two_array.png)

当你想获取某个value的时候，ArrayMap会计算输入key转换过后的hash值，然后对hash数组使用二分查找法寻找到对应的index，然后我们可以通过这个index在另外一个数组中直接访问到需要的键值对。如果在第二个数组键值对中的key和前面输入的查询key不一致，那么就认为是发生了碰撞冲突。为了解决这个问题，我们会以该key为中心点，分别上下展开，逐个去对比查找，直到找到匹配的值。如下图所示：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_3_arraymap_binary_search.png)

随着数组中的对象越来越多，查找访问单个对象的花费也会跟着增长，这是在内存占用与访问时间之间做权衡交换。

既然ArrayMap中的内存占用是连续不间断的，那么它是如何处理插入与删除操作的呢？请看下图所示，演示了Array的特性：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_3_arraymap_del.png)

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_3_arraymap_add.png)

很明显，ArrayMap的插入与删除的效率是不够高的，但是如果数组的列表只是在一百这个数量级上，则完全不用担心这些插入与删除的效率问题。HashMap与ArrayMap之间的内存占用效率对比图如下：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_3_arraymap_memory_compare.png)

与HashMap相比，ArrayMap在循环遍历的时候也更加简单高效，如下图所示：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_3_arraymap_list.png)

前面演示了很多ArrayMap的优点，但并不是所有情况下都适合使用ArrayMap，我们应该在满足下面2个条件的时候才考虑使用ArrayMap：

- 对象个数的数量级最好是千以内
- 数据组织形式包含Map结构

我们需要学会在特定情形下选择相对更加高效的实现方式。