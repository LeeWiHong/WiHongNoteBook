### DBCP数据源与应用服务器整合使用——  配置Tomcat数据源 

查看Tomcat文档（Tomcat-->TomcatDocument-->JNDI Resources-->定位到JDBC Data Sources），示例代码： 

`<Context> 
<Resource name="jdbc/datasource" auth="Container"  type="javax.sql.DataSource" username="root" password="root"  driverClassName="com.mysql.jdbc.Driver" 
url="jdbc:mysql://localhost:3306/jdbc"  maxActive="8" maxIdle="4"  /> 
<Resource name="jdbc/EmployeeDB " auth="Container" type="javax.sql.DataSource" 
username="root" password="root"  driverClassName="com.mysql.jdbc.Driver" 
url="jdbc:mysql://localhost:3306/jdbc"  maxActive="8" maxIdle="4"  /> 
</Context>`

放置位置：在MyEclipse中，在目录/META-INF/下创建文件context.xml，将上述内容粘贴其中（注：不要写XML文件的指令头句）。该文件将被发布到Tomcat服务器的conf\Catalina\localhost目录中，并以工程名称 命名该文件。

下面是调用JNDI，获取存储在JNDI容器中的资源的固定格式代码（有关JNDI的知识，参见下一章节）： 

Context initCtx = new InitialContext(); 
Context envCtx = (Context) initCtx.lookup("java:comp/env"); 
dataSource = (DataSource)envCtx.lookup("jdbc/datasource"); 
特别提醒：此种配置下，驱动jar文件需放置在tomcat的lib下 
可以创建工具类JDBCUtils,java来封装上面获取连接的代码。 
Demo样例： 封装JNDI调用DataSource 获取连接的代码。
复制代码
`public class JdbcUtils_Tomcat {
         private static DataSource ds;
         static {
             try {
                 Context initCtx = new InitialContext();
                 Context envCtx = (Context) initCtx.lookup("java:comp/env");
                 ds = (DataSource) envCtx.lookup("jdbc/EmployeeDB");
             } catch (Exception e) {
                 throw new RuntimeException(e);
             }
         }
         public static Connection getConnection() throws SQLException{
             return ds.getConnection();
         }
     }`

