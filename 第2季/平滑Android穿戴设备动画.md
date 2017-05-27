# Smooth Android Wear Animation

Android Material Design风格的应用采用了大量的动画来进行UI切换，优化动画的性能不仅能够提升用户体验还可以减少电量的消耗，下面会介绍一些简单易行的方法。

在Android里面一个相对操作比较繁重的事情是对Bitmap进行旋转，缩放，裁剪等等。例如在一个圆形的钟表图上，我们把时钟的指针抠出来当做单独的图片进行旋转会比旋转一张完整的圆形图的所形成的帧率要高56%。

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_waer_animation.png)

另外尽量减少每次重绘的元素可以极大的提升性能，假如某个钟表界面上有很多需要显示的复杂组件，我们可以把这些组件做拆分处理，例如把背景图片单独拎出来设置为一个独立的View，通过setLayerType()方法使得这个View强制用Hardware来进行渲染。至于界面上哪些元素需要做拆分，他们各自的更新频率是多少，需要有针对性的单独讨论。

如何使用Systrace等工具来查看某些View的渲染性能，在前面的章节里面有提到过，感兴趣的可以点击[这里](Android性能优化之渲染篇.html)

对于大多数应用中的动画，我们会使用PropertyAnimation或者ViewAnimation来操作实现，Android系统会自动对这些Animation做一定的优化处理，在Android上面学习到的大多数性能优化的知识同样也适用于Android Wear。

想要获取更多关于Android Wear中动画效果的优化，请点击[WatchFace](http://developer.android.com/samples/WatchFace/index.html)这个范例。