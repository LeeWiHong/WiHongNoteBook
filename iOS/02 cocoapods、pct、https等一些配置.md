# 02 cocoapods、pct、https等一些配置

## 第三方类库管理工具  —  CocoaPods

1. (打开终端) 删除默认ruby环境：sudo gem sources --remove https://rubygems.org/

2. 用淘宝的Ruby镜像: sudo gem sources -a https://ruby.taobao.org/

3. 查看当前Ruby环境： gem sources

4. 安装cocoaPod:   sudo gem install cocoapods

5. (安装完成后) cd 到工程目录文件夹中

6. 创建Podfile 配置文件： pod init

7. (工程目录文件夹下)  编辑Podfile文件
![](https://ww2.sinaimg.cn/large/006tNc79gy1fdhpb8btrzj30yg0c077w.jpg)
8. (回到终端) 开始导入： pod install 
9. 如需更新 或添加和删除先在podfile中修改内容，再更新： pod update
10. 完成后 会有  “工程名.xcworkspace" 文件，以后就打开它就是了。想要详细了解的：[CocoaPods安装和使用教程](http://code4app.com/article/cocoapods-install-usage)

***
## 预编译文件 —  PCH文件
pch 可以用来存储共享信息 如：全局的宏、整个项目中都能用到的头文件
1. 新建pch文件
![](https://ww2.sinaimg.cn/large/006tNc79gy1fdhpxcts4bj30yg0oa42z.jpg)
新建pch
2. 配置pch文件
![](https://ww3.sinaimg.cn/large/006tNc79gy1fdhpycgphsj30yg0ld45x.jpg)

修改配置
Precompile  Prefix Header改为YES ，预编译后的pch文件会被缓存起来，可以提高编译速度。Prefix Header 是pct文件的路径。在pch导入头文件格式

***
## 三、cocoapods 导入第三方库头文件自动补齐

想要引入CocoaPods的第三方框架时，发现没提示头文件，这就比较尴尬了，
![](https://ww3.sinaimg.cn/large/006tNc79gy1fdhq0rzh01j30yg0k044j.jpg)
这样就能完美提示了。

***
## 四、解决Http不能连接问题
苹果默认只允许https://协议能连接，而认为http://协议是不安全的。解决办法：
![](https://ww1.sinaimg.cn/large/006tNc79gy1fdhq1p70ykj30yg0htjyi.jpg)
设置为YES后，就能使用http://协议了





