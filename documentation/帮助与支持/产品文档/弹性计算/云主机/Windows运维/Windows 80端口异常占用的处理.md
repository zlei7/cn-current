**Windows 80端口异常占用的处理**

**问题现象：**

服务器应用使用的端口被异常占用导致服务启动失败，例如：Windows上安装的Tomcat无法启动，TCP 80端口已经被其它应用占用。

**问题原因：**

应用程序需要使用的TCP/UDP端口被其它程序、或者病毒木马占用。

**解决办法：**

1. 使用命令
netstat -ano |find ":80"

看到占用端口的进程ID是4，注意：请根据实际情况修改端口。

![1.png](https://img1.jcloudcs.com/cms/5f5b4371-05ca-46fa-a677-f188dedf7fc820170908114515.png)

2.使用命令

tasklist /svc| find "4"

看到是系统进程。 注意：请根据实际情况修改进程ID

![2.png](https://img1.jcloudcs.com/cms/0ed4015a-571d-4515-ac2b-3cb0c929a32620170908114629.png)

3.尝试关闭iis服务，使用命令

iisreset /stop

![3.png](https://img1.jcloudcs.com/cms/7e57b062-d05b-4782-ad3b-5757ac016cfc20170908114742.png)

4.但是发现80端口仍然被占用。于是使用命令

curl -I 127.0.0.1

查看返回的server是 Microsoft-HTTPAPI/2.0 而不是Server: Microsoft-IIS/7.5。

![4.png](https://img1.jcloudcs.com/cms/aca72b5a-039a-4b4c-83e5-9b0d0f1bd3a020170908114919.png)

能够使用Microsoft-HTTPAPI/2.0的只能是微软的产品。检查是否有安装SQL SERVER ，如果有尝试关闭SQL Server Reporting Service这个服务。

![5.png](https://img1.jcloudcs.com/cms/6b0ed4dc-29ec-43b5-a790-41dcee84941d20170908120753.png)

5.关闭后再使用curl -I 127.0.0.1 就提示80端口无法连接，说明端口已经被释放。

![6.png](https://img1.jcloudcs.com/cms/390d3f52-0c59-46c4-acc1-9062a28675c220170908120906.png)

注意：如果没有安装curl还可以使用telnet 127.0.0.1 80 执行完，ctrl+c终止就会出现下面图片的样子，也可以看到server：Microsoft-HTTPAPI/2.0 ，当然仅靠这个是不能判断是哪个程序的。只能根据此判断是微软的应用占用了。具体还需要看ECS上实际安装了哪些微软的应用。

如无法解决您的问题，请向我们提工单。