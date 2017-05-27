# Using LINT for Performance Tips

Lint是Android提供的一个静态扫描应用源码并找出其中的潜在问题的一个强大的工具。

![](http://onmer39jj.bkt.clouddn.com/image/android_perf_2_lint_overview.png)

例如，如果我们在onDraw方法里面执行了new对象的操作，Lint就会提示我们这里有性能问题，并提出对应的建议方案。Lint已经集成到Android Studio中了，我们可以手动去触发这个工具，点击工具栏的Analysis -> Inspect Code，触发之后，Lint会开始工作，并把结果输出到底部的工具栏，我们可以逐个查看原因并根据指示做相应的优化修改。

Lint的功能非常强大，他能够扫描各种问题。当然我们可以通过Android Studio设置找到Lint，对Lint做一些定制化扫描的设置，可以选择忽略掉那些不想Lint去扫描的选项，我们还可以针对部分扫描内容修改它的提示优先级。

建议把与内存有关的选项中的严重程度标记为红色的Error，对于Layout的性能问题标记为黄色Warning。