# 一对多表关系在hibernate中的配置
#### 1.数据库建表
创建用户表以及联系人表，其中一个用户对应多个联系人，联系人外键参照于用户表的主键
![](https://ws3.sinaimg.cn/large/006tNc79gy1fp1yeo3inxj31660guwoo.jpg)
创建cst_customer表

```
CREATE TABLE IF NOT EXISTS cst_customer(
  cst_id BIGINT NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '用户ID',
  cst_name VARCHAR(32) NOT NULL COMMENT '客户名称',
  cst_source VARCHAR(32) DEFAULT NULL COMMENT '客户信息来源',
  cst_industry VARCHAR(32) DEFAULT NULL COMMENT '客户所属行业',
  cst_level VARCHAR(32) DEFAULT NULL COMMENT '客户所属级别',
  cst_phone VARCHAR(64) DEFAULT NULL COMMENT '固定电话',
  cst_mobile VARCHAR(14) DEFAULT NULL COMMENT '移动电话'
);
```
创建cst_linkman表

```
CREATE TABLE IF NOT EXISTS cst_linkman(
  lkm_id BIGINT NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '联系人ID',
  lkm_name VARCHAR(32) DEFAULT NULL COMMENT '联系人名字',
  lkm_gender VARCHAR(32) DEFAULT NULL COMMENT '联系人关系',
  lkm_phone VARCHAR(64) DEFAULT NULL COMMENT '联系人固定电话',
  lkm_mobile VARCHAR(14) DEFAULT NULL COMMENT '联系人移动电话',
  lkm_email VARCHAR(64) DEFAULT NULL COMMENT '联系人邮箱',
  lkm_qq VARCHAR(32) DEFAULT NULL COMMENT '联系人qq',
  lkm_position VARCHAR(64) DEFAULT NULL COMMENT '联系人地址',
  lkm_memo VARCHAR(32) DEFAULT NULL COMMENT '联系人成员',
  lkm_cust_id BIGINT,
  FOREIGN KEY (lkm_cust_id) REFERENCES cst_customer(cst_id) ON UPDATE NO ACTION ON DELETE NO ACTION
);
```
建表成功后如下图所示
![](https://ws3.sinaimg.cn/large/006tNc79gy1fp1ydfuplxj30de0oedjr.jpg)
#### 2.创建实体
##### 2.1创建cst_customer实体

```
package com.classes;

import java.util.HashSet;
import java.util.Set;

import javax.persistence.Transient;

public class cst_customer {
	private long cst_id;
	private String cst_name;
	private String cst_source;
	private String cst_industry;
	private String cst_level;
	private String cst_phone;
	private String cst_mobile;
	
	private Set<cst_linkman> linkmans = new HashSet<cst_linkman>();

	public long getCst_id() {
		return cst_id;
	}
	public void setCst_id(long cst_id) {
		this.cst_id = cst_id;
	}
	public String getCst_name() {
		return cst_name;
	}
	public void setCst_name(String cst_name) {
		this.cst_name = cst_name;
	}
	public String getCst_source() {
		return cst_source;
	}
	public void setCst_source(String cst_source) {
		this.cst_source = cst_source;
	}
	public String getCst_industry() {
		return cst_industry;
	}
	public void setCst_industry(String cst_industry) {
		this.cst_industry = cst_industry;
	}
	public String getCst_level() {
		return cst_level;
	}
	public void setCst_level(String cst_level) {
		this.cst_level = cst_level;
	}
	public String getCst_phone() {
		return cst_phone;
	}
	public void setCst_phone(String cst_phone) {
		this.cst_phone = cst_phone;
	}
	public String getCst_mobile() {
		return cst_mobile;
	}
	public void setCst_mobile(String cst_mobile) {
		this.cst_mobile = cst_mobile;
	}
	public Set<cst_linkman> getLinkmans() {
		return linkmans;
	}
	public void setLinkmans(Set<cst_linkman> linkmans) {
		this.linkmans = linkmans;
	}
}
```
##### 2.2创建cst_linkman实体

```
package com.classes;

import javax.persistence.Transient;

public class cst_linkman {
	private long lkm_id;
	private String lkm_name;
	private String lkm_gender;
	private String lkm_phone;
	private String lkm_mobile;
	private String lkm_email;
	private String lkm_qq;
	private String lkm_position;
	private String lkm_memo;
	
	private cst_customer cst_customer;
	
	public cst_customer getCst_customer() {
		return cst_customer;
	}
	public void setCst_customer(cst_customer cst_customer) {
		this.cst_customer = cst_customer;
	}
	public long getLkm_id() {
		return lkm_id;
	}
	public void setLkm_id(long lkm_id) {
		this.lkm_id = lkm_id;
	}
	public String getLkm_name() {
		return lkm_name;
	}
	public void setLkm_name(String lkm_name) {
		this.lkm_name = lkm_name;
	}
	public String getLkm_gender() {
		return lkm_gender;
	}
	public void setLkm_gender(String lkm_gender) {
		this.lkm_gender = lkm_gender;
	}
	public String getLkm_phone() {
		return lkm_phone;
	}
	public void setLkm_phone(String lkm_phone) {
		this.lkm_phone = lkm_phone;
	}
	public String getLkm_mobile() {
		return lkm_mobile;
	}
	public void setLkm_mobile(String lkm_mobile) {
		this.lkm_mobile = lkm_mobile;
	}
	public String getLkm_email() {
		return lkm_email;
	}
	public void setLkm_email(String lkm_email) {
		this.lkm_email = lkm_email;
	}
	public String getLkm_qq() {
		return lkm_qq;
	}
	public void setLkm_qq(String lkm_qq) {
		this.lkm_qq = lkm_qq;
	}
	public String getLkm_position() {
		return lkm_position;
	}
	public void setLkm_position(String lkm_position) {
		this.lkm_position = lkm_position;
	}
	public String getLkm_memo() {
		return lkm_memo;
	}
	public void setLkm_memo(String lkm_memo) {
		this.lkm_memo = lkm_memo;
	}
	
}
```
#### 3.创建映射关系
在这里需要注意的是我使用的是eclipse中默认的那个工具所配置的，在这里是有一个大坑的，在后面会讲到，但是前面还是按照他默认的来进行配置
![](https://ws3.sinaimg.cn/large/006tNc79gy1fp1yjwl37lj31b20z0n4f.jpg)

cst_customer映射表对应生成的代码如下

```
<hibernate-mapping>
    <class name="com.classes.cst_customer" table="CST_CUSTOMER">
        <id name="cst_id" type="long">
            <column name="CST_ID" />
            <generator class="assigned" />
        </id>
        <property name="cst_name" type="java.lang.String">
            <column name="CST_NAME" />
        </property>
        <property name="cst_source" type="java.lang.String">
            <column name="CST_SOURCE" />
        </property>
        <property name="cst_industry" type="java.lang.String">
            <column name="CST_INDUSTRY" />
        </property>
        <property name="cst_level" type="java.lang.String">
            <column name="CST_LEVEL" />
        </property>
        <property name="cst_phone" type="java.lang.String">
            <column name="CST_PHONE" />
        </property>
        <property name="cst_mobile" type="java.lang.String">
            <column name="CST_MOBILE" />
        </property>
        <set name="linkmans" table="CST_LINKMAN" inverse="false" lazy="true">
            <key>
                <column name="CST_ID" />
            </key>
            <one-to-many class="com.classes.cst_linkman" />
        </set>
    </class>
</hibernate-mapping>
```

cst_linkman映射表对应生成的代码如下

```
<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<!-- Generated Mar 5, 2018 2:55:37 PM by Hibernate Tools 3.5.0.Final -->
<hibernate-mapping>
    <class name="com.classes.cst_linkman" table="CST_LINKMAN">
        <id name="lkm_id" type="long">
            <column name="LKM_ID" />
            <generator class="assigned" />
        </id>
        <property name="lkm_name" type="java.lang.String">
            <column name="LKM_NAME" />
        </property>
        <property name="lkm_gender" type="java.lang.String">
            <column name="LKM_GENDER" />
        </property>
        <property name="lkm_phone" type="java.lang.String">
            <column name="LKM_PHONE" />
        </property>
        <property name="lkm_mobile" type="java.lang.String">
            <column name="LKM_MOBILE" />
        </property>
        <property name="lkm_email" type="java.lang.String">
            <column name="LKM_EMAIL" />
        </property>
        <property name="lkm_qq" type="java.lang.String">
            <column name="LKM_QQ" />
        </property>
        <property name="lkm_position" type="java.lang.String">
            <column name="LKM_POSITION" />
        </property>
        <property name="lkm_memo" type="java.lang.String">
            <column name="LKM_MEMO" />
        </property>
        <many-to-one name="cst_customer" class="com.classes.cst_customer" fetch="join">
            <column name="CST_CUSTOMER" />
        </many-to-one>
    </class>
</hibernate-mapping>
```
#### 4.将映射文件添加到配置文件中，配置文件所对应的代码如下

```
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE hibernate-configuration PUBLIC
		"-//Hibernate/Hibernate Configuration DTD 3.0//EN"
		"http://www.hibernate.org/dtd/hibernate-configuration-3.0.dtd">
<hibernate-configuration>
    <session-factory>
        <property name="hibernate.connection.driver_class">com.mysql.jdbc.Driver</property>
        <property name="hibernate.connection.password">lwhong1017</property>
        <property name="hibernate.connection.url">jdbc:mysql://localhost:3306/myblog?useSSL=true</property>
        <property name="hibernate.connection.username">root</property>
        <mapping resource="com/classes/cst_customer.hbm.xml"/>
        <mapping resource="com/classes/cst_linkman.hbm.xml"/>
    </session-factory>
</hibernate-configuration>
```
#### 5.编写测试代码
DBuitls中代码如下

```
package com.HibernateUtils;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

import com.classes.cst_customer;
import com.classes.cst_linkman;

public class DButils {
	private static SessionFactory sessionFactory;
	private static Session session;
	public static Session getSession() {
		return session;
	}

	public static void setSession(Session session) {
		DButils.session = session;
	}

	static {
		Configuration configuration = new Configuration().configure();
		sessionFactory = configuration.buildSessionFactory();
	}
	static {
		session = sessionFactory.openSession();
	}
	
	public void SaveData() {
		System.out.println("aaaaa----");
		Session session = this.getSession();
		Transaction transaction = session.beginTransaction();
		// 创建一个客户
		cst_customer cst_customer = new cst_customer();
		cst_customer.setCst_name("赵云");
		// 创建两个联系人
		cst_linkman cst_linkman1 = new cst_linkman();
		cst_linkman1.setLkm_name("李秘书");
		cst_linkman cst_linkman2 = new cst_linkman();
		cst_linkman2.setLkm_name("王秘书");
		// 建立联系s
		cst_customer.getLinkmans().add(cst_linkman1);
		cst_customer.getLinkmans().add(cst_linkman2);
		cst_linkman1.setCst_customer(cst_customer);
		cst_linkman2.setCst_customer(cst_customer);
		session.save(cst_customer);
		session.save(cst_linkman1);
		session.save(cst_linkman2);
		transaction.commit();
		System.out.println("bbbbb----");
	}

}
```
在main方法中调用

```
DButils dButils = new DButils();
dButils.SaveData();
```
#### 6.错误
##### 6.1A different object with the same identifier value was already associated with the session

```
18/03/05 15:17:55 INFO orm.connections: HHH10001003: Autocommit mode: false
18/03/05 15:17:55 INFO internal.DriverManagerConnectionProviderImpl: HHH000115: Hibernate connection pool size: 20 (min=1)
18/03/05 15:17:55 INFO dialect.Dialect: HHH000400: Using dialect: org.hibernate.dialect.MySQL5Dialect
aaaaa----
Exception in thread "main" org.hibernate.NonUniqueObjectException: A different object with the same identifier value was already associated with the session : [com.classes.cst_linkman#0]
	at org.hibernate.event.internal.AbstractSaveEventListener.performSave(AbstractSaveEventListener.java:165)
	at org.hibernate.event.internal.AbstractSaveEventListener.saveWithGeneratedId(AbstractSaveEventListener.java:121)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.saveWithGeneratedOrRequestedId(DefaultSaveOrUpdateEventListener.java:192)
	at org.hibernate.event.internal.DefaultSaveEventListener.saveWithGeneratedOrRequestedId(DefaultSaveEventListener.java:38)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.entityIsTransient(DefaultSaveOrUpdateEventListener.java:177)
	at org.hibernate.event.internal.DefaultSaveEventListener.performSaveOrUpdate(DefaultSaveEventListener.java:32)
	at org.hibernate.event.internal.DefaultSaveOrUpdateEventListener.onSaveOrUpdate(DefaultSaveOrUpdateEventListener.java:73)
	at org.hibernate.internal.SessionImpl.fireSave(SessionImpl.java:679)
	at org.hibernate.internal.SessionImpl.save(SessionImpl.java:671)
	at org.hibernate.internal.SessionImpl.save(SessionImpl.java:666)
	at com.HibernateUtils.DButils.SaveData(DButils.java:49)
	at com.Test.TestHibMutiTabPro.main(TestHibMutiTabPro.java:10)
```
这行代码报错意思是在session中已经存在两个相同OID的对象在里面，因此而导致的错误，我在这里一开始也是去谷歌解决方法的，但是其实并没有什么好的解决方案，因此我在这里用排除法，在这里有相同的OID只能是我那里添加了两个联系人，所以我决定将cst_linkman2注销看看会出什么问题
![](https://ws1.sinaimg.cn/large/006tNc79gy1fp1z0t1rrgj313w0kwafh.jpg)

##### 6.2Unknown column in 'field list'

```
aaaaa----
18/03/05 15:26:28 WARN spi.SqlExceptionHelper: SQL Error: 1054, SQLState: 42S22
18/03/05 15:26:28 ERROR spi.SqlExceptionHelper: Unknown column 'CST_CUSTOMER' in 'field list'
18/03/05 15:26:28 INFO internal.AbstractBatchImpl: HHH000010: On release of batch it still contained JDBC statements
18/03/05 15:26:28 ERROR internal.SessionImpl: HHH000346: Error during managed flush [could not execute statement]
Exception in thread "main" org.hibernate.exception.SQLGrammarException: could not execute statement
	at org.hibernate.exception.internal.SQLExceptionTypeDelegate.convert(SQLExceptionTypeDelegate.java:63)
	at org.hibernate.exception.internal.StandardSQLExceptionConverter.convert(StandardSQLExceptionConverter.java:42)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:109)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:95)
	at org.hibernate.engine.jdbc.internal.ResultSetReturnImpl.executeUpdate(ResultSetReturnImpl.java:207)
	at org.hibernate.engine.jdbc.batch.internal.NonBatchingBatch.addToBatch(NonBatchingBatch.java:45)
	at org.hibernate.persister.entity.AbstractEntityPersister.insert(AbstractEntityPersister.java:2886)
	at org.hibernate.persister.entity.AbstractEntityPersister.insert(AbstractEntityPersister.java:3386)
	at org.hibernate.action.internal.EntityInsertAction.execute(EntityInsertAction.java:89)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:560)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:434)
	at org.hibernate.event.internal.AbstractFlushingEventListener.performExecutions(AbstractFlushingEventListener.java:337)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:39)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1282)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:465)
	at org.hibernate.internal.SessionImpl.flushBeforeTransactionCompletion(SessionImpl.java:2963)
	at org.hibernate.internal.SessionImpl.beforeTransactionCompletion(SessionImpl.java:2339)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.beforeTransactionCompletion(JdbcCoordinatorImpl.java:485)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl.beforeCompletionCallback(JdbcResourceLocalTransactionCoordinatorImpl.java:147)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl.access$100(JdbcResourceLocalTransactionCoordinatorImpl.java:38)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl$TransactionDriverControlImpl.commit(JdbcResourceLocalTransactionCoordinatorImpl.java:231)
	at org.hibernate.engine.transaction.internal.TransactionImpl.commit(TransactionImpl.java:65)
	at com.HibernateUtils.DButils.SaveData(DButils.java:50)
	at com.Test.TestHibMutiTabPro.main(TestHibMutiTabPro.java:10)
Caused by: com.mysql.jdbc.exceptions.jdbc4.MySQLSyntaxErrorException: Unknown column 'CST_CUSTOMER' in 'field list'
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:425)
	at com.mysql.jdbc.Util.getInstance(Util.java:408)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:943)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3973)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3909)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2527)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2680)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2494)
	at com.mysql.jdbc.PreparedStatement.executeInternal(PreparedStatement.java:1858)
	at com.mysql.jdbc.PreparedStatement.executeUpdateInternal(PreparedStatement.java:2079)
	at com.mysql.jdbc.PreparedStatement.executeUpdateInternal(PreparedStatement.java:2013)
	at com.mysql.jdbc.PreparedStatement.executeLargeUpdate(PreparedStatement.java:5104)
	at com.mysql.jdbc.PreparedStatement.executeUpdate(PreparedStatement.java:1998)
	at org.hibernate.engine.jdbc.internal.ResultSetReturnImpl.executeUpdate(ResultSetReturnImpl.java:204)
	... 19 more
```
果然第一个的相同OID的问题没有了，但是又出现了新的问题，通过查找资料这个地方意思是CST_CUSTOMER找不到没有存在这样的属性，首先来分析一下这个CST_CUSTOMER可是cst_linkman实体中的成员属性，cst_linkman所对应数据库中的表确实是没有这样的一个列属性，只有一个外键的，而数据库表与实体的对应关系是由hbm配置文件来决定的，所以可能出现的问题就在配置文件那个地方,因此我决定将原来的many-to-one这里将原来的cst_customer修改成lkm_cust_id，这个外键在表中可是实实在在存在的
原：

```
<many-to-one name="cst_customer" class="com.classes.cst_customer" fetch="join">
            <column name="CST_CUSTOMER" />
        </many-to-one>
```
现：

```
<many-to-one name="cst_customer" class="com.classes.cst_customer" fetch="join">
            <column name="lkm_cust_id" />
        </many-to-one>
```
再次运行报如下错误

#### 6.3Cannot add or update a child row: a foreign key constraint fails

```
18/03/05 15:39:30 INFO dialect.Dialect: HHH000400: Using dialect: org.hibernate.dialect.MySQL5Dialect
aaaaa----
18/03/05 15:39:31 WARN spi.SqlExceptionHelper: SQL Error: 1452, SQLState: 23000
18/03/05 15:39:31 ERROR spi.SqlExceptionHelper: Cannot add or update a child row: a foreign key constraint fails (`myblog`.`cst_linkman`, CONSTRAINT `cst_linkman_ibfk_1` FOREIGN KEY (`lkm_cust_id`) REFERENCES `cst_customer` (`cst_id`) ON DELETE NO ACTION ON UPDATE NO ACTION)
18/03/05 15:39:31 INFO internal.AbstractBatchImpl: HHH000010: On release of batch it still contained JDBC statements
18/03/05 15:39:31 ERROR internal.SessionImpl: HHH000346: Error during managed flush [could not execute statement]
Exception in thread "main" org.hibernate.exception.ConstraintViolationException: could not execute statement
	at org.hibernate.exception.internal.SQLExceptionTypeDelegate.convert(SQLExceptionTypeDelegate.java:59)
	at org.hibernate.exception.internal.StandardSQLExceptionConverter.convert(StandardSQLExceptionConverter.java:42)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:109)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:95)
	at org.hibernate.engine.jdbc.internal.ResultSetReturnImpl.executeUpdate(ResultSetReturnImpl.java:207)
	at org.hibernate.engine.jdbc.batch.internal.NonBatchingBatch.addToBatch(NonBatchingBatch.java:45)
	at org.hibernate.persister.entity.AbstractEntityPersister.insert(AbstractEntityPersister.java:2886)
	at org.hibernate.persister.entity.AbstractEntityPersister.insert(AbstractEntityPersister.java:3386)
	at org.hibernate.action.internal.EntityInsertAction.execute(EntityInsertAction.java:89)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:560)
	at org.hibernate.engine.spi.ActionQueue.executeActions(ActionQueue.java:434)
	at org.hibernate.event.internal.AbstractFlushingEventListener.performExecutions(AbstractFlushingEventListener.java:337)
	at org.hibernate.event.internal.DefaultFlushEventListener.onFlush(DefaultFlushEventListener.java:39)
	at org.hibernate.internal.SessionImpl.flush(SessionImpl.java:1282)
	at org.hibernate.internal.SessionImpl.managedFlush(SessionImpl.java:465)
	at org.hibernate.internal.SessionImpl.flushBeforeTransactionCompletion(SessionImpl.java:2963)
	at org.hibernate.internal.SessionImpl.beforeTransactionCompletion(SessionImpl.java:2339)
	at org.hibernate.engine.jdbc.internal.JdbcCoordinatorImpl.beforeTransactionCompletion(JdbcCoordinatorImpl.java:485)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl.beforeCompletionCallback(JdbcResourceLocalTransactionCoordinatorImpl.java:147)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl.access$100(JdbcResourceLocalTransactionCoordinatorImpl.java:38)
	at org.hibernate.resource.transaction.backend.jdbc.internal.JdbcResourceLocalTransactionCoordinatorImpl$TransactionDriverControlImpl.commit(JdbcResourceLocalTransactionCoordinatorImpl.java:231)
	at org.hibernate.engine.transaction.internal.TransactionImpl.commit(TransactionImpl.java:65)
	at com.HibernateUtils.DButils.SaveData(DButils.java:50)
	at com.Test.TestHibMutiTabPro.main(TestHibMutiTabPro.java:10)
Caused by: com.mysql.jdbc.exceptions.jdbc4.MySQLIntegrityConstraintViolationException: Cannot add or update a child row: a foreign key constraint fails (`myblog`.`cst_linkman`, CONSTRAINT `cst_linkman_ibfk_1` FOREIGN KEY (`lkm_cust_id`) REFERENCES `cst_customer` (`cst_id`) ON DELETE NO ACTION ON UPDATE NO ACTION)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance0(Native Method)
	at sun.reflect.NativeConstructorAccessorImpl.newInstance(NativeConstructorAccessorImpl.java:62)
	at sun.reflect.DelegatingConstructorAccessorImpl.newInstance(DelegatingConstructorAccessorImpl.java:45)
	at java.lang.reflect.Constructor.newInstance(Constructor.java:423)
	at com.mysql.jdbc.Util.handleNewInstance(Util.java:425)
	at com.mysql.jdbc.Util.getInstance(Util.java:408)
	at com.mysql.jdbc.SQLError.createSQLException(SQLError.java:935)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3973)
	at com.mysql.jdbc.MysqlIO.checkErrorPacket(MysqlIO.java:3909)
	at com.mysql.jdbc.MysqlIO.sendCommand(MysqlIO.java:2527)
	at com.mysql.jdbc.MysqlIO.sqlQueryDirect(MysqlIO.java:2680)
	at com.mysql.jdbc.ConnectionImpl.execSQL(ConnectionImpl.java:2494)
	at com.mysql.jdbc.PreparedStatement.executeInternal(PreparedStatement.java:1858)
	at com.mysql.jdbc.PreparedStatement.executeUpdateInternal(PreparedStatement.java:2079)
	at com.mysql.jdbc.PreparedStatement.executeUpdateInternal(PreparedStatement.java:2013)
	at com.mysql.jdbc.PreparedStatement.executeLargeUpdate(PreparedStatement.java:5104)
	at com.mysql.jdbc.PreparedStatement.executeUpdate(PreparedStatement.java:1998)
	at org.hibernate.engine.jdbc.internal.ResultSetReturnImpl.executeUpdate(ResultSetReturnImpl.java:204)
	... 19 more
```
这个问题似乎是因为其他问题导致的问题了，但是需要注意的是导致这个问题的原因是还有上面那个，不过先来排除导致这个问题的主要问题，从网上查找资料显示的问题就是

```
原因：
设置的外键和对应的另一个表的主键值不匹配。
解决方法：
找出不匹配的值修改。
或者清空两表数据。
```
这也的几句话对于新手来说真不懂是怎么回事，但是其实说的直白一点就是表与表之间值对不上啊，而两者之间有对应关系的就是那个外键了，在customer中id的主键属性是assign的，将其修改为native
![](https://ws4.sinaimg.cn/large/006tNc79gy1fp1znu7fbvj311g0v4kdw.jpg)
再次报错

```
aaaaa----
18/03/05 15:48:57 WARN spi.SqlExceptionHelper: SQL Error: 1054, SQLState: 42S22
18/03/05 15:48:57 ERROR spi.SqlExceptionHelper: Unknown column 'CST_ID' in 'field list'
18/03/05 15:48:57 INFO internal.AbstractBatchImpl: HHH000010: On release of batch it still contained JDBC statements
18/03/05 15:48:57 ERROR internal.SessionImpl: HHH000346: Error during managed flush [could not execute statement]
Exception in thread "main" org.hibernate.exception.SQLGrammarException: could not execute statement
	at org.hibernate.exception.internal.SQLExceptionTypeDelegate.convert(SQLExceptionTypeDelegate.java:63)
	at org.hibernate.exception.internal.StandardSQLExceptionConverter.convert(StandardSQLExceptionConverter.java:42)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:109)
	at org.hibernate.engine.jdbc.spi.SqlExceptionHelper.convert(SqlExceptionHelper.java:95)
```
有了上面6.2的解决方式其实就能明白是cst_customer映射表中column有问题
原:

```
<set name="linkmans" table="CST_LINKMAN" inverse="false" lazy="true">
            <key>
                <column name="CST_ID" />
            </key>
            <one-to-many class="com.classes.cst_linkman" />
        </set>
```
这里所对应的是cst_id去了，但实际上所对应的应该是外键lkm_cust_id，修改后成如下

```
<set name="linkmans" table="CST_LINKMAN" inverse="false" lazy="true">
            <key>
                <column name="lkm_cust_id" />
            </key>
            <one-to-many class="com.classes.cst_linkman" />
        </set>
```
再次运行没有报错误了，但是要知道这里所调试的是一个用户表customer中只添加了一个linkman记录的，要是一对多的话还需要将linkman2注释打开，再次打开注释运行是没有问题的，通过查询数据库表数据没有问题,因此出现6.1所示问题时需要检查其他配置是不是有问题，特别是主键生成策略










