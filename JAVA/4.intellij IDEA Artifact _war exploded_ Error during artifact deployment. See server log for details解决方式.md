#### 前沿
在整合ssh的时候一个web项目的时候发现了一个让我无法思议的问题，各个方面都配置好了，却因为出现一些bug而无法往下走去--`Artifact test1:war exploded: Error during artifact deployment. See server log for details.`我一直都不明白这个问题的症结在什么地方？难道是sdk的版本问题？tomcat版本的问题？(我项目中有tomcat7跟tomcat9两个版本),还是到底idea的问题？这个bug在开发中比较的常见，主要是像我这样的新手。
#### 分析思路
为了解决这个问题，我做了一些基础的排查，第一检查tomcat能不能正常工作，因此我用terminal启动tomcat，这个时候访问localhost是正常的，排除了web服务器的问题，因为我就用这个idea前不久在搭struts环境的时候是正常的能启动来的，所以也是需要排除idea的问题，为解决这个问题我谷歌了好久其实在网上也没有看到一些比较有效的解决方式，或者是对这个问题并没有做一些分析。
#### 解决方式
##### 新建工程
我为了解决这个问题新建一个struts工程只要能输出helloworld即可
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fpi72uqzzoj31gs14caic.jpg)
需要注意一下这里的画红圈的地方，因为这个地方是有坑的
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fpi73vwxgdj31gs14cgo3.jpg)
这个图也是需要注意这个红圈的地方的，注意项目的文件夹地址
##### 修改index.jsp的内容
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fpi76pnyjgj31kw0whqbg.jpg)
##### 配置tomcat
步骤一：
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fpi7abc2b3j31kw0vudob.jpg)
步骤二：
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fpi7bw1avzj31kw12i47d.jpg)
步骤三：
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fpi7dpah11j31kw12dtgb.jpg)
步骤四：
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fpi7eirmjbj31kw122tdj.jpg)
步骤五：
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fpi7eymb8tj31kw12idkn.jpg)
这里需要将根路径'/'修改成'/test1'因为你的tomcat以后不只一个项目的
因为idea自己帮我们做了很多事情的，似乎我们只要配上tomcat就OK了？那既然如此干脆跑一次会怎么样呢？

```
/Users/leewihong/tomcat7/bin/catalina.sh run
[2018-03-19 04:28:45,005] Artifact test1:war exploded: Server is not connected. Deploy is not available.
```
这就是报错信息
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fpi7jb8hfej31kw0vu7h8.jpg)
tomcat那样配置其实已经是没有问题的了，那么问题的症结就是在于项目的配置
##### 点击进入项目的设置界面
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fpi7kpssbqj31kw0vu14w.jpg)
一开始这个地方肯定是有问题的，直接点击fix修复就好了，如果没有的话不需要点击了
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fpi7npjli0j31kw0ywtcd.jpg)
因为我们的输出项目是到tomcat中去的，因此这个地方项目的文件位置就应该是定位到那里去
![](https://ws4.sinaimg.cn/large/006tKfTcgy1fpi7rh6ycuj31kw0ywwkb.jpg)
就是因为修改了这些文件的目录地址，所以才导致出现了那个问题
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fpi7t06jwwj31kw0ywgro.jpg)
就是因为修改了目录地址所以这个地方的东西要进行修改
![](https://ws2.sinaimg.cn/large/006tKfTcgy1fpi7t06jwwj31kw0ywgro.jpg)
对于1的问题因为默认没有添加metainfo那个文件的直接添加即可
而对于2这个问题我一开始完全没有注意到这个地方，而本问题的症结就是2这里，因为我一开始创建的是在idea那里的，后来model那里又改称了tomcat里面去，但是在facets这里又是在ideapro文件夹下面，所以这是自己挖的一个坑，把这个xml文件重新删除再创建一个即可
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fpi7wtnoxfj31kw0x5ahc.jpg)
修改Artifacts
![](https://ws1.sinaimg.cn/large/006tKfTcgy1fpi7xvph57j31kw0ywn2j.jpg)
这个地方都是需要进行修改的
这些步骤修改下来应该是可以看到正确结果的
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fpi7z61peej31kw0zbh0h.jpg)
所以这个问题的症结就是一个文件目录的问题

