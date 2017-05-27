# Tool:Profile GPU Rendering

性能问题如此的麻烦，幸好我们可以有工具来进行调试。打开手机里面的开发者选项，选择Profile GPU Rendering，选中On screen as bars的选项。

![](http://onmer39jj.bkt.clouddn.com/image/54bdca8ab535a.jpg)

选择了这样以后，我们可以在手机画面上看到丰富的GPU绘制图形信息，分别关于StatusBar，NavBar，激活的程序Activity区域的GPU Rending信息。

![](http://onmer39jj.bkt.clouddn.com/image/54bdcaa3b06c3.jpg)

随着界面的刷新，界面上会滚动显示垂直的柱状图来表示每帧画面所需要渲染的时间，柱状图越高表示花费的渲染时间越长。

![](http://onmer39jj.bkt.clouddn.com/image/54bdcabb4ddb0.jpg)

中间有一根绿色的横线，代表16ms，我们需要确保每一帧花费的总时间都低于这条横线，这样才能够避免出现卡顿的问题。

![](http://onmer39jj.bkt.clouddn.com/image/54bdcad2c5a24.jpg)

每一条柱状线都包含三部分，蓝色代表测量绘制Display List的时间，红色代表OpenGL渲染Display List所需要的时间，黄色代表CPU等待GPU处理的时间。