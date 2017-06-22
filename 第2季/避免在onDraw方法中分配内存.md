# Avoiding Allocations in onDraw()

我们都知道应该避免在onDraw()方法里面执行导致内存分配的操作，下面讲解下为何需要这样做。

首先onDraw()方法是执行在UI线程的，在UI线程尽量避免做任何可能影响到性能的操作。虽然分配内存的操作并不需要花费太多系统资源，但是这并不意味着是免费无代价的。设备有一定的刷新频率，导致View的onDraw方法会被频繁的调用，如果onDraw方法效率低下，在频繁刷新累积的效应下，效率低的问题会被扩大，然后会对性能有严重的影响。

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_ondraw_gc.png)

如果在onDraw里面执行内存分配的操作，会容易导致内存抖动，GC频繁被触发，虽然GC后来被改进为执行在另外一个后台线程(GC操作在2.3以前是同步的，之后是并发)，可是频繁的GC的操作还是会影响到CPU，影响到电量的消耗。

那么简单解决频繁分配内存的方法就是把分配操作移动到onDraw()方法外面，通常情况下，我们会把onDraw()里面new Paint的操作移动到外面，如下面所示：

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_ondraw_paint.png)