# Understanding Battery Drain on Android

电量消耗的计算与统计是一件麻烦而且矛盾的事情，记录电量消耗本身也是一个费电量的事情。唯一可行的方案是使用第三方监测电量的设备，这样才能够获取到真实的电量消耗。

当设备处于待机状态时消耗的电量是极少的，以N5为例，打开飞行模式，可以待机接近1个月。可是点亮屏幕，硬件各个模块就需要开始工作，这会需要消耗很多电量。

![](http://onmer39jj.bkt.clouddn.com/image/54bdf25b6044c_middle.jpg)

使用WakeLock或者[JobScheduler](在Android 5.0中使用JobScheduler.html)唤醒设备处理定时的任务之后，一定要及时让设备回到初始状态。每次唤醒无线信号进行数据传递，都会消耗很多电量，它比WiFi等操作更加的耗电。修复电量的消耗是另外一个很大的课题，这里就不展开继续了。