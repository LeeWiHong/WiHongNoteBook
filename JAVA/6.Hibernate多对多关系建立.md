多对多关系主要是应用在不同的用户具备多个不同的角色，比如王者荣耀中赵云既可以拿来打野又可以拿来打上单，李元芳既可以拿来打野也可以拿来打射手，因此这期间的多个用户具备多个角色属性用先前的一对多关系就不能解决了，需要多对多的映射关系
#### 1.创建数据库表
![](https://ws3.sinaimg.cn/large/006tKfTcgy1fp36rbgj91j315a0b0qbn.jpg)
sql语句如下

```
CREATE TABLE IF NOT EXISTS sys_user(
  user_id BIGINT NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '用户id',
  user_code VARCHAR(32) DEFAULT NULL COMMENT '用户code值',
  user_name VARCHAR(32) DEFAULT NULL COMMENT '用户名',
  user_password VARCHAR(32) DEFAULT NULL COMMENT '用户名密码',
  user_state VARCHAR(32) DEFAULT NULL COMMENT '用户职位'
);

CREATE TABLE IF NOT EXISTS sys_role(
  role_id BIGINT NOT NULL AUTO_INCREMENT PRIMARY KEY COMMENT '职位id',
  role_name VARCHAR(32) DEFAULT NULL COMMENT '职位名称',
  role_memo VARCHAR(32) DEFAULT NULL COMMENT '职位成员'
);

CREATE TABLE IF NOT EXISTS sys_user_role(
  user_id BIGINT NOT NULL ,
  FOREIGN KEY(user_id) REFERENCES sys_user(user_id) ON DELETE  NO ACTION ON UPDATE NO ACTION ,
  role_id BIGINT NOT NULL ,
  FOREIGN KEY (role_id) REFERENCES sys_role(role_id) ON DELETE NO ACTION ON UPDATE NO ACTION
);
```
#### 2.创建实体
创建Sys_user实体

```
package com.classes;

import java.util.HashSet;
import java.util.Set;

public class Sys_user {
	private Long user_id;
	private String user_code;
	private String user_name;
	private String user_password;
	private String user_state;
	
	private Set<Sys_role> roles  = new HashSet<Sys_role>();
	
	
	public Set<Sys_role> getRoles() {
		return roles;
	}
	public void setRoles(Set<Sys_role> roles) {
		this.roles = roles;
	}
	public Long getUser_id() {
		return user_id;
	}
	public void setUser_id(Long user_id) {
		this.user_id = user_id;
	}
	public String getUser_code() {
		return user_code;
	}
	public void setUser_code(String user_code) {
		this.user_code = user_code;
	}
	public String getUser_name() {
		return user_name;
	}
	public void setUser_name(String user_name) {
		this.user_name = user_name;
	}
	public String getUser_password() {
		return user_password;
	}
	public void setUser_password(String user_password) {
		this.user_password = user_password;
	}
	public String getUser_state() {
		return user_state;
	}
	public void setUser_state(String user_state) {
		this.user_state = user_state;
	}
}
```
创建Sys_role实体

```
package com.classes;

import java.util.HashSet;
import java.util.Set;

public class Sys_role {
	private Long role_id;
	private String role_name;
	private String role_memo;
	
	private Set<Sys_user>users = new HashSet<Sys_user>();
	
	public Set<Sys_user> getUsers() {
		return users;
	}
	public void setUsers(Set<Sys_user> users) {
		this.users = users;
	}
	public Long getRole_id() {
		return role_id;
	}
	public void setRole_id(Long role_id) {
		this.role_id = role_id;
	}
	public String getRole_name() {
		return role_name;
	}
	public void setRole_name(String role_name) {
		this.role_name = role_name;
	}
	public String getRole_memo() {
		return role_memo;
	}
	public void setRole_memo(String role_memo) {
		this.role_memo = role_memo;
	}
}
```
#### 3.创建映射文件
用工具创建Sys_user的映射表,创建完毕需要对原有多对多的地方进行修改

```
<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<!-- Generated Mar 6, 2018 4:29:51 PM by Hibernate Tools 3.5.0.Final -->
<hibernate-mapping>
    <class name="com.classes.Sys_user" table="SYS_USER">
        <id name="user_id" type="java.lang.Long">
            <column name="USER_ID" />
            <generator class="native" />
        </id>
        <property name="user_code" type="java.lang.String">
            <column name="USER_CODE" />
        </property>
        <property name="user_name" type="java.lang.String">
            <column name="USER_NAME" />
        </property>
        <property name="user_password" type="java.lang.String">
            <column name="USER_PASSWORD" />
        </property>
        <property name="user_state" type="java.lang.String">
            <column name="USER_STATE" />
        </property>
        <set name="roles" table="sys_user_role" inverse="false" lazy="true">
            <key>
                <column name="USER_ID" />
            </key>
            <!-- <one-to-many class="com.classes.Sys_role" /> -->
            <many-to-many class="com.classes.Sys_role" column="role_id"/>
        </set>
    </class>
</hibernate-mapping>
```
用工具创建Sys_role映射表，需要对多对多的地方进行修改成如下的代码

```
<?xml version="1.0"?>
<!DOCTYPE hibernate-mapping PUBLIC "-//Hibernate/Hibernate Mapping DTD 3.0//EN"
"http://hibernate.sourceforge.net/hibernate-mapping-3.0.dtd">
<!-- Generated Mar 6, 2018 4:29:51 PM by Hibernate Tools 3.5.0.Final -->
<hibernate-mapping>
    <class name="com.classes.Sys_role" table="SYS_ROLE">
        <id name="role_id" type="java.lang.Long">
            <column name="ROLE_ID" />
            <generator class="native" />
        </id>
        <property name="role_name" type="java.lang.String">
            <column name="ROLE_NAME" />
        </property>
        <property name="role_memo" type="java.lang.String">
            <column name="ROLE_MEMO" />
        </property>
        <set name="users" table="sys_user_role" inverse="false" lazy="true">
            <key>
                <column name="ROLE_ID" />
            </key>
           <!--  <one-to-many class="com.classes.Sys_user" /> -->
           <many-to-many class="com.classes.Sys_user" column="user_id"/>
        </set>
    </class>
</hibernate-mapping>
```
#### 4.在核心配置文件中添加入映射文件

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
        <mapping resource="com/classes/Sys_role.hbm.xml"/>
        <mapping resource="com/classes/Sys_user.hbm.xml"/>
    </session-factory>
</hibernate-configuration>
```
#### 5.引入封装的数据工具以及编写测试代码
##### 5.1数据工具
```
package com.HibernateUtils;

import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;

import com.classes.Sys_role;
import com.classes.Sys_user;

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
		
		// 1.创建用户
		Sys_user user1 = new Sys_user();
		user1.setUser_name("赵云");
		
		Sys_user user2 = new Sys_user();
		user2.setUser_name("马克");
		
		Sys_user user3 = new Sys_user();
		user3.setUser_name("干将莫邪");
		
		// 2.创建角色职位
		Sys_role role1 = new Sys_role();
		role1.setRole_name("ADC射手");
		
		Sys_role role2 = new Sys_role();
		role2.setRole_name("打野");
		
		Sys_role role3 = new Sys_role();
		role3.setRole_name("中单");
		
		Sys_role role4 = new Sys_role();
		role4.setRole_name("战士");
		
		user1.getRoles().add(role2);
		user1.getRoles().add(role4);
		
		user2.getRoles().add(role3);
		user2.getRoles().add(role2);
		
		user3.getRoles().add(role3);
		
		session.save(user1);
		session.save(user2);
		session.save(user3);
		session.save(role1);
		session.save(role2);
		session.save(role3);
		session.save(role4);
		
		transaction.commit();
		System.out.println("bbbbb----");
	}
}
```

##### 5.2测试类

```
package com.testHibernate;

import com.HibernateUtils.DButils;

public class testHib {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		DButils dButils = new DButils();
		dButils.SaveData();
	}

}
```
因为有前面出现的一些坑本篇也出线了一些坑但是按照先前的一些思路还是比较顺利的解决了，多对多的主要是在hbm配置时候需要column对应各个属性





