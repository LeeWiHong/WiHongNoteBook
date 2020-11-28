 No appenders could be found for logger(log4j)?
直接写我的解决办法：
在src下面新建file名为log4j.properties内容如下:

```
Configure logging for testing: optionally with log file
log4j.rootLogger=WARN, stdout
log4j.rootLogger=WARN, stdout, logfile

log4j.appender.stdout=org.apache.log4j.ConsoleAppender
log4j.appender.stdout.layout=org.apache.log4j.PatternLayout
log4j.appender.stdout.layout.ConversionPattern=%d %p [%c] - %m%n

log4j.appender.logfile=org.apache.log4j.FileAppender
log4j.appender.logfile.File=target/spring.log
log4j.appender.logfile.layout=org.apache.log4j.PatternLayout
log4j.appender.logfile.layout.ConversionPattern=%d %p [%c] - %m%n
```
===============================
重新发布，OK,没有提示了。加入了这个配置文件后，再次运行程序上面的警告就会消失。尤其在进行Web 层开发的时候，只有加入了这个文件后才能看到Spring 后台完整的出错信息。在开发Spring 整合应用
时，经常有人遇到出现404 错误但是却看不到任何出错信息的情况，这时你就需要检查一
下这个文件是不是存在。

在Eclipse中开发相关项目时,在控制台经常看到如下信息:
log4j:WARN No appenders could be found for logger
log4j:WARN Please initialize the log4j system properly.

此处输出信息并不是错误信息而仅只是警告信息,因为log4j无法输出日志,log4j是一个日志输入软件包。可以将Struts或Hibernate等压缩包解压，内有log4j.properties文件，将它复制到项目src文件夹或将log4j.properties放到 \WEB-INF\classes文件夹中即可。

＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝
WARN No appenders could be found for logger的解决办法

这几天做一个SSH项目，tomcat启动时出现以下问题：
log4j:WARN No appenders could be found for logger (org.springframework.web.context.ContextLoader).
log4j:WARN Please initialize the log4j system properly.

在网上查了一下，多是说把ContextLoaderListener改为SpringContextServlet，但我这样改了没用。后来在一个英文网站上看到一个遇到同样问题的帖子，他是这样改的：
```
<context-param>
   <param-name>log4jConfigLocation</param-name>
   <param-value>/WEB-INF/config/log4j.properties</param-value>
</context-param>
······
<!-- 定义LOG4J监听器 -->
<listener>
   <listener-class>
org.springframework.web.util.Log4jConfigListener
   </listener-class>
</listener>
```
这样改了问题就解决了，不用再修改ContextLoaderListener。

