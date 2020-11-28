Hibernate入门指南笔记
#### 1. 首先下载Hibernate包 
[Hibernate5.0.7](https://sourceforge.net/projects/hibernate/files/hibernate-orm/5.0.7.Final/)
#### 2. 在MySQL中创建数据库和表

```
CREATE DATABASE myblog;
USE myblog;
CREATE TABLE IF NOT EXISTS cust_customer(
  cust_id BIGINT NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '用户id',
  cust_name VARCHAR(32) NOT NULL COMMENT '客户名称(公司名称)',
  cust_source VARCHAR(32) DEFAULT NULL COMMENT '客户信息来源',
  cust_industry VARCHAR(32) DEFAULT NULL COMMENT '客户所属行业',
  cust_level VARCHAR(32) DEFAULT NULL COMMENT '客户级别',
  cust_phone VARCHAR(64) DEFAULT NULL COMMENT '固定电话',
  cust_mobile VARCHAR(14) DEFAULT NULL COMMENT '移动电话'
);
```
#### 3. 导入数据库驱动包与Hibernate包以及日志记录包
##### 3.1 导入Hibernate包如下
![](https://ws3.sinaimg.cn/large/006tNc79gy1fow6qeis4lj30r30583zj.jpg)
##### 3.2 导入MySQL数据库连接驱动包
mysql-connector-java-5.1.43-bin.jar
##### 3.3 导入日志记录包
![](https://ws2.sinaimg.cn/large/006tNc79gy1fow6s6sv60j30bl03p0sy.jpg)

在工程目录下面新建一个lib目录将所需要的包拷贝到lib文件夹下
![](https://ws4.sinaimg.cn/large/006tNc79gy1fow72891w3j30ix0ax3zp.jpg)
选中所有文件将包添加到项目中
![](https://ws1.sinaimg.cn/large/006tNc79gy1fow73fpwbdj30fs0i7wgf.jpg)
如果添加成功，在项目文件目录下面会有一个Libraries包含所添加的外部库
![](https://ws2.sinaimg.cn/large/006tNc79gy1fow74vxnljj30l80xe0z0.jpg)

#### 4.在工程的src下创建一个实体，对应于数据库中的cust_customer表

```
package com.whong;
public class cust_customer {
	private long cust_id;
	private String cust_name;
	private String cust_source;
	private String cust_industry;
	private String cust_level;
	private String cust_phone;
	private String cust_mobile;
	
	public long getCust_id() {
		return cust_id;
	}
	public void setCust_id(long cust_id) {
		this.cust_id = cust_id;
	}
	public String getCust_name() {
		return cust_name;
	}
	public void setCust_name(String cust_name) {
		this.cust_name = cust_name;
	}
	public String getCust_source() {
		return cust_source;
	}
	public void setCust_source(String cust_source) {
		this.cust_source = cust_source;
	}
	public String getCust_industry() {
		return cust_industry;
	}
	public void setCust_industry(String cust_industry) {
		this.cust_industry = cust_industry;
	}
	public String getCust_level() {
		return cust_level;
	}
	public void setCust_level(String cust_level) {
		this.cust_level = cust_level;
	}
	public String getCust_phone() {
		return cust_phone;
	}
	public void setCust_phone(String cust_phone) {
		this.cust_phone = cust_phone;
	}
	public String getCust_mobile() {
		return cust_mobile;
	}
	public void setCust_mobile(String cust_mobile) {
		this.cust_mobile = cust_mobile;
	}
}
```

#### 5.创建映射文件
映射文件是将刚才的实体cust_customer映射到数据库中的
因为安装了hibernate的插件，所以在这里可以直接选择创建hbm文件，不需要手动去配置
![](https://ws3.sinaimg.cn/large/006tNc79gy1fow78dtlxyj30hp0h0jsr.jpg)
在这里有可能是这样一个包的，但是对应的不应该是这个包，需要对应于那个类cust_customer，因此需要点击Add class添加cust_customer类到这里来
![](https://ws1.sinaimg.cn/large/006tNc79gy1fow79gtjghj30hp0jawfi.jpg)
对应的hbm文件如下

```
<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<!-- Generated Feb 28, 2018 2:40:14 PM by Hibernate Tools 3.5.0.Final -->
<hibernate-mapping>
    <class name="com.whong.cust_customer" table="CUST_CUSTOMER">
        <id name="cust_id" type="long">
            <column name="CUST_ID" />
            <generator class="assigned" />
        </id>
        <property name="cust_name" type="java.lang.String">
            <column name="CUST_NAME" />
        </property>
        <property name="cust_source" type="java.lang.String">
            <column name="CUST_SOURCE" />
        </property>
        <property name="cust_industry" type="java.lang.String">
            <column name="CUST_INDUSTRY" />
        </property>
        <property name="cust_level" type="java.lang.String">
            <column name="CUST_LEVEL" />
        </property>
        <property name="cust_phone" type="java.lang.String">
            <column name="CUST_PHONE" />
        </property>
        <property name="cust_mobile" type="java.lang.String">
            <column name="CUST_MOBILE" />
        </property>
    </class>
</hibernate-mapping>
```

#### 6.创建Hibernate的核心配置文件
在第五步骤中的映射文件反应的是持久化类和数据库表的映射信息，而Hibernate的配置文件则主要是用来配置数据库连接以及Hibernate运行时所需要的各个属性的值，在src文件夹下创建cfg类型的文件
![](https://ws3.sinaimg.cn/large/006tNc79gy1fow7nlj4krj30hp0h075q.jpg)
![](https://ws2.sinaimg.cn/large/006tNc79gy1fow7o705rjj30hp0mkabf.jpg)
在cfg配置界面这里很关键需要注意
![](https://ws2.sinaimg.cn/large/006tNc79gy1fow7q39wxdj30hp0mkmyr.jpg)
点击Get values from Connection
![](https://ws4.sinaimg.cn/large/006tNc79gy1fow7rjgye5j31ai130q99.jpg)
新建一个连接配置文件
![](https://ws3.sinaimg.cn/large/006tNc79gy1fow7sewtfij30hp0iugn4.jpg)
选择mysql在name这里可以标注一下以示区分连接不同的数据库
在这里选择数据库的驱动
![](https://ws1.sinaimg.cn/large/006tNc79gy1fow7tyr1a3j30hp0jnmyq.jpg)
点击这个车轮
![](https://ws2.sinaimg.cn/large/006tNc79gy1fow7uttd3wj30t60x2q6w.jpg)
Name/Type选择5.1
![](https://ws1.sinaimg.cn/large/006tNc79gy1fow7vf9vv1j30xc0rsq6e.jpg)
Jar List需要移除这个驱动，点击Add JAR/Zip 选择刚才添加进去的sql数据库连接驱动
![](https://ws3.sinaimg.cn/large/006tNc79gy1fow7wtp2pkj30js0h00ts.jpg)
返回到Connection Profile这里，修改database为myblog所对应的数据库，同时需要注意的是，在url那里需要添加
`?usessl=true`
完整的url为`jdbc:mysql://localhost:3306/myblog?usessl=true`
![](https://ws4.sinaimg.cn/large/006tNc79gy1fow7yv9mscj30t60x2gpe.jpg)

#### 7.编写一个测试代码
测试代码如下所示

```
package com.testPackage;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
import com.whong.cust_customer;

public class testHibernate {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Configuration configuration = new Configuration().configure();
		SessionFactory sessionFactory = configuration.buildSessionFactory();
		Session session = sessionFactory.openSession();
		Transaction transaction = session.beginTransaction();
		cust_customer cust_customer = new cust_customer();
		cust_customer.setCust_name("伟鸿");
		cust_customer.setCust_phone("18*******969");
		session.save(cust_customer);
		transaction.commit();
		session.close();
	}
}
```

#### 8.试运行
如果这个时候试运行会报有如下的错误

```
log4j:WARN No appenders could be found for logger (org.jboss.logging).
log4j:WARN Please initialize the log4j system properly.
log4j:WARN See http://logging.apache.org/log4j/1.2/faq.html#noconfig for more info.
Exception in thread "main" org.hibernate.MappingException: Unknown entity: com.whong.cust_customer
	at org.hibernate.internal.SessionFactoryImpl.getEntityPersister(SessionFactoryImpl.java:781)
	at org.hibernate.internal.SessionImpl.getEntityPersister(SessionImpl.java:1520)
	at org.hibernate.event.internal.AbstractSaveEventListener.saveWithGeneratedId(AbstractSaveEventListener.java:100)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.saveWithGeneratedOrRequestedId(DefaultSaveOrUpdateEventListener.java:192)
	at org.hibernate.event.internal.DefaultSaveEventListener.saveWithGeneratedOrRequestedId(DefaultSaveEventListener.java:38)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.entityIsTransient(DefaultSaveOrUpdateEventListener.java:177)
	at org.hibernate.event.internal.DefaultSaveEventListener.performSaveOrUpdate(DefaultSaveEventListener.java:32)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.onSaveOrUpdate(DefaultSaveOrUpdateEventListener.java:73)
	at org.hibernate.internal.SessionImpl.fireSave(SessionImpl.java:679)
	at org.hibernate.internal.SessionImpl.save(SessionImpl.java:671)
	at org.hibernate.internal.SessionImpl.save(SessionImpl.java:666)
	at com.testPackage.testHibernate.main(testHibernate.java:21)
```

##### 8.1解决方案
这里最主要的问题就是log日志文件的问题
解决方式是需要添加一个有关日志的配置文件，具体可以看一下这个链接的文章[log4j WARN 和 SLF4J WARN 解决办法](http://blog.csdn.net/u013595419/article/details/77895262)
在src目录下添加log4j.properties配置文件

```
hadoop.root.logger=DEBUG, console
log4j.rootLogger=INFO, console
log4j.appender.console=org.apache.log4j.ConsoleAppender
log4j.appender.console.target=System.out
log4j.appender.console.layout=org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern=%d{yy/MM/dd HH:mm:ss} %p %c{2}: %m%n
```
##### 8.2实体映射错误解决方式
再次运行会报如下的错误

```
Exception in thread "main" org.hibernate.MappingException: Unknown entity: com.whong.cust_customer
	at org.hibernate.internal.SessionFactoryImpl.getEntityPersister(SessionFactoryImpl.java:781)
	at org.hibernate.internal.SessionImpl.getEntityPersister(SessionImpl.java:1520)
	at org.hibernate.event.internal.AbstractSaveEventListener.saveWithGeneratedId(AbstractSaveEventListener.java:100)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.saveWithGeneratedOrRequestedId(DefaultSaveOrUpdateEventListener.java:192)
	at org.hibernate.event.internal.DefaultSaveEventListener.saveWithGeneratedOrRequestedId(DefaultSaveEventListener.java:38)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.entityIsTransient(DefaultSaveOrUpdateEventListener.java:177)
	at org.hibernate.event.internal.DefaultSaveEventListener.performSaveOrUpdate(DefaultSaveEventListener.java:32)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.onSaveOrUpdate(DefaultSaveOrUpdateEventListener.java:73)
	at org.hibernate.internal.SessionImpl.fireSave(SessionImpl.java:679)
	at org.hibernate.internal.SessionImpl.save(SessionImpl.java:671)
	at org.hibernate.internal.SessionImpl.save(SessionImpl.java:666)
	at com.testPackage.testHibernate.main(testHibernate.java:21)
```
这个问题时因为核心配置文件cfg和实体映射文件hbm之间没有对应起来，所以找不到那个cust_customer实体
解决方式如下
拷贝hbm文件的路径
![](https://ws2.sinaimg.cn/large/006tNc79gy1fow8gvypltj30bb0jtgns.jpg)
在cfg配置文件下添加如下语句
`<mapping resource="/LearnHibernate/src/com/whong/cust_customer.hbm.xml"/>`
但是这个地方需要去掉src前面的路径
因此正确的路径是
`<mapping resource="com/whong/cust_customer.hbm.xml"/>`

再次运行的到正确的结果
并打印如下的一些日志记录

```
18/02/28 16:21:05 INFO hibernate.Version: HHH000412: Hibernate Core {5.0.7.Final}
18/02/28 16:21:05 INFO cfg.Environment: HHH000206: hibernate.properties not found
18/02/28 16:21:05 INFO cfg.Environment: HHH000021: Bytecode provider name : javassist
18/02/28 16:21:05 INFO common.Version: HCANN000001: Hibernate Commons Annotations {5.0.1.Final}
18/02/28 16:21:05 WARN orm.deprecation: HHH90000012: Recognized obsolete hibernate namespace http://hibernate.sourceforge.net/hibernate-mapping. Use namespace http://www.hibernate.org/dtd/hibernate-mapping instead.  Support for obsolete DTD/XSD namespaces may be removed at any time.
18/02/28 16:21:06 WARN orm.connections: HHH10001002: Using Hibernate built-in connection pool (not for production use!)
18/02/28 16:21:06 INFO orm.connections: HHH10001005: using driver [com.mysql.jdbc.Driver] at URL [jdbc:mysql://localhost:3306/myblog?useSSL=true]
18/02/28 16:21:06 INFO orm.connections: HHH10001001: Connection properties: {user=root, password=****}
18/02/28 16:21:06 INFO orm.connections: HHH10001003: Autocommit mode: false
18/02/28 16:21:06 INFO internal.DriverManagerConnectionProviderImpl: HHH000115: Hibernate connection pool size: 20 (min=1)
18/02/28 16:21:07 INFO dialect.Dialect: HHH000400: Using dialect: org.hibernate.dialect.MySQL5Dialect
```
再数据库中查询cust_customer表也是可以查询到这一条记录的
至此hibernate的入门配置笔记完毕









