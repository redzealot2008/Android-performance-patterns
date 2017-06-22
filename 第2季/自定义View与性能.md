# Custom Views and Performance

Android系统有提供超过70多种标准的View，例如TextView，ImageView，Button等等。在某些时候，这些标准的View无法满足我们的需要，那么就需要我们自己来实现一个View，这节会介绍如何优化自定义View的性能。

通常来说，针对自定义View，我们可能犯下面三个错误：

- **Useless calls to onDraw()：**我们知道调用View.invalidate()会触发View的重绘，有两个原则需要遵守，第1个是仅仅在View的内容发生改变的时候才去触发invalidate方法，第2个是尽量使用ClipRect等方法来提高绘制的性能。

- **Useless pixels：**减少绘制时不必要的绘制元素，对于那些不可见的元素，我们需要尽量避免重绘。

- **Wasted CPU cycles：**对于不在屏幕上的元素，可以使用Canvas.quickReject把他们给剔除，避免浪费CPU资源。另外尽量使用GPU来进行UI的渲染，这样能够极大的提高程序的整体表现性能。

最后请时刻牢记，尽量提高View的绘制性能，这样才能保证界面的刷新帧率尽量的高。更多关于这部分的内容，可以看[这里](http://hukai.me/android-performance-patterns/)