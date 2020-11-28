#### Spring Configuration Check  Unmapped Spring configuration files found
![](https://ws1.sinaimg.cn/large/006tNc79gy1fpdbj2yt96j30st09v40o.jpg)
项目中有xml文件，但没有被用IntelliJ 导入现有工程时，如果原来的工程中有spring，每次打开工程就会提示：Spring Configuration Check
开始不知道怎么回事，但工程不影响。
![](https://ws1.sinaimg.cn/large/006tNc79gy1fpdbjlrlsxj30ka03w74r.jpg)
工程结构（Project Structure）有一个Facets 选项，可以设置各种框架。

Facets中则可以设置当前项目所用的框架，如Hibernate和Spring，如果是Web项目，也需要添加Web的Facets，这个界面中的显示和Modules中的很类似。如果想要通过idea做Hibernate的映射文件（.hbm）生成或jpa注解配置代码生成，则需要添加Hibernate配置，如果添加了Spring，则在Spring的xml中properties文件的占位符可以被自动替换为properties中已配置的值。

偶然发现这个提示是把spring的配置文件由IntelliJ来管理，打Project Structure－>Facets 配置。添加spring配置文件的模块。
![](https://ws1.sinaimg.cn/large/006tNc79gy1fpdbl3r87vj30gw11in04.jpg)
然后把sping的配置文件勾选上
![](https://ws4.sinaimg.cn/large/006tNc79gy1fpdblggeo8j31hi0w679t.jpg)

