**Windows任务管理器数据暂停的原因**

**问题现象：**

在查看任务管理时，“进程”选项卡的 CPU、内存数据没有刷新，或发现性能选项卡的数据没有变动或一直处于0但实际上服务器是有网络传输的。

![1.png](https://img1.jcloudcs.com/cms/e143d8e9-ef73-4ef1-837b-1822ac241fcc20170817113023.png)

**问题原因：**

任务管理器更新速度已暂停导致的。

**解决办法：**

点击“查看”->更新速度，检查是否被配置为“已暂停”，可以将它改为“普通或正常”，然后观察一下任务管理器中的数据是否正常刷新了。

![2.png](https://img1.jcloudcs.com/cms/687aa0fa-01fd-49b0-99f7-b4c34095233420170817113242.png)

如无法解决您的问题，请向我们提工单。