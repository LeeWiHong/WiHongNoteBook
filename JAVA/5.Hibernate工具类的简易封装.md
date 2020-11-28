Hibernate用于持久化的一个框架，但是在实际项目中进行查询有很多的地方是需要进行一些封装的，比如他的configure以及session不可能有一个操作数据库调用dao层就创建一个，而且在获取数据的时候有很多是相同的操作，那么这些都需要进行一些封装，以下为自个进行的一个简易封装，在前面笔记[Hibernate入门笔记](https://github.com/LeeWiHong/WiHongNoteBook/blob/master/JAVA/Hibernate%E5%85%A5%E9%97%A8%E7%AC%94%E8%AE%B0.md)的基础上做的一个简易项目，创建HibernateUtils工具类，封装代码如下

```
package com.HibernateUtils;

import java.util.List;

import org.hibernate.Criteria;
import org.hibernate.Query;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
import org.hibernate.criterion.Restrictions;

import com.whong.cust_customer;

public class HibernateUtils {
	private static Session session;
	private static SessionFactory sessionFactory;
	private static Transaction transaction;
	static {
		Configuration configuration = new Configuration().configure();
		sessionFactory = configuration.buildSessionFactory();
	}
	static {
		session = sessionFactory.openSession();
	}
	static {
		transaction = session.beginTransaction();
	}
	// 插入数据
	public void insertData(String name,String phone) {
		cust_customer cust_customer = new cust_customer();
		cust_customer.setCust_name(name);
		cust_customer.setCust_phone(phone);
		session.save(cust_customer);
		transaction.commit();
		session.close();
	}
	// 查询所有的数据
	public void getAllData() {
		Configuration configuration = new Configuration().configure();
		SessionFactory sessionFactory = configuration.buildSessionFactory();
		Session session = sessionFactory.openSession();
		Query query = session.createQuery("from cust_customer");
		List<cust_customer>list = query.list();
		this.PrintListArray(list);
	}
	// 根据条件查询(通过序列号1 2 3 等数字来进行查询)
	public void getDatawithName(String name) {
		Query query = session.createQuery("from cust_customer where cust_name = ?");
		query.setString(0, name);
		List<cust_customer>list = query.list();
		this.PrintListArray(list);
	}
	
	// 条件查询(根据设定属性名称来进行查询)
	public void getDataWithNameAndPhone(String cust_name,String cust_phone) {
		Query query = session.createQuery("from cust_customer where cust_name = :cust_name and cust_phone = :cust_phone");
		query.setString("cust_name", cust_name);
		query.setString("cust_phone", cust_phone);
		List<cust_customer>list = query.list();
		this.PrintListArray(list);
	}
	
	// 分页查询
	public void getDataSeparater(Integer minipage,Integer maxpage	) {
		Query query = session.createQuery("from cust_customer");
		query.setFirstResult(minipage);
		query.setMaxResults(maxpage);
		List<cust_customer>list = query.list();
		this.PrintListArray(list);
	}
	
	// criterita查询所有数据
	public void getDataCriterita() {
		Criteria criteria = session.createCriteria(cust_customer.class);
		List<cust_customer>list = criteria.list();
		this.PrintListArray(list);
	}
	// criterita条件查询
	public void getDataCriteritaWithName(String cust_name) {
		Criteria criteria = session.createCriteria(cust_customer.class);
		criteria.add(Restrictions.eq("cust_name", cust_name));
		List<cust_customer>list = criteria.list();
		this.PrintListArray(list);
	}
	// criterita条件查询
	public void getDataCriteritaWithNameAndMobile(String name,String mobile) {
		Criteria criteria = session.createCriteria(cust_customer.class);
		criteria.add(Restrictions.eq("cust_name", name));
		criteria.add(Restrictions.eq("cust_mobile", mobile));
		List<cust_customer>list = criteria.list();
		this.PrintListArray(list);
	}
	// criterita分页查询
	public void getDataMinAndMax(Integer min,Integer max) {
		Criteria criteria = session.createCriteria(cust_customer.class);
		criteria.setFirstResult(min);
		criteria.setMaxResults(max);
		List<cust_customer>list	= criteria.list();
		this.PrintListArray(list);
	}
	
	// 打印所有的查询结果
	public void PrintListArray(List<cust_customer>list) {
		for (int i = 0; i < list.size(); i++) {
			cust_customer cust_customer = list.get(i);
			System.out.println(cust_customer.getCust_id()+cust_customer.getCust_name()+cust_customer.getCust_mobile());
		}
	}
}
```
在main中调用代码如下

```
package com.testPackage;

import org.hibernate.Query;
import org.hibernate.Session;
import org.hibernate.SessionFactory;
import org.hibernate.Transaction;
import org.hibernate.cfg.Configuration;
import org.hibernate.mapping.List;

import com.HibernateUtils.HibernateUtils;
import com.whong.cust_customer;

public class testHibernate {
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		HibernateUtils hibernateUtils = new HibernateUtils();
//		hibernateUtils.insertData("伟鸿", "185*******9");
//		hibernateUtils.getAllData();
//		hibernateUtils.getDatawithName("weihong");
//		hibernateUtils.getDataWithNameAndPhone("伟鸿", "185******69");
//		hibernateUtils.getDataSeparater(3, 10);
//		hibernateUtils.getDataCriterita();
//		hibernateUtils.getDataCriteritaWithName("weihong");
//		hibernateUtils.getDataCriteritaWithNameAndMobile("伟鸿", "18******69");
		hibernateUtils.getDataMinAndMax(3, 10);
	}
}
```



