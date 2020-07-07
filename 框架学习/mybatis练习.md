# MyBatis练习

## 1. 前置
    先建立一个就Java项目，新建一个lib文件夹用于放置jar包，本次练习只需要导入mybatis包中的mybatis.jar+ojbc6.jar包，鼠标右键将两个包bulid path构建包相对路径。

## 2. db.properties的配置
    1. 在src文件夹下新建一个config包，用于放置配置文件
    2. 在config包下创建File文件，命名为db.properties,该文件用于配置jdbc，代码如下：
```
    #加载驱动
    db.driver=oracle.jdbc.driver.OracleDriver
    #加载数据库
    db.url=jdbc:oracle:thin:@127.0.0.1:1521:orcl
    #用户名
    db.username=scott
    #密码
    db.password=123
```

- 注：
    连接池配置文件db.properties是java中采用数据库连接池技术完成应用对数据库的操作的配置文件信息的文件。
    具体配置项目如下：
    
    ```
    drivers=com.microsoft.sqlserver.jdbc.SQLServerDriver  注册驱动，sqlsever,oracle，mysql都行
    logfile=d:\\log.txt     日志文件的位置
    customer_system.url=jdbc:sqlserver://192.168.2.252:2433; 
    DatabaseName=customer_system 数据库的url
    customer_system.user=sa     用户名
    customer_system.password=SA  密码
    customer_system.maxConns=5  最大连接数
    customer_system.minConns=1  最小连接数
    customer_system.logInterval=60000   监听时长 
    ```
## 3. 创建实体类entity
    1.在src文件夹下新建一个com.neu包，在该包下创建entity包，用于放置数据库中数据对应的Java类
    2.在com.neu.entity包下创建Perosn类，代码如下：

```java
package com.neu.entity;

import java.sql.Date;

public class Person {
	private int id;
	private String name;
	private int age;
	private String address;
	private int dept_id;
	private Date time;
	
	//生成有参、无参构造器、get、set方法的快捷键：alt+s
	//每写一个方法，记得保存：ctrl+s
	
	public Person() {
		super();
		// TODO Auto-generated constructor stub
	}
	
	
	public Person(int id, String name, int age, String address, int dept_id,
			Date time, String path) {
		super();
		this.id = id;
		this.name = name;
		this.age = age;
		this.address = address;
		this.dept_id = dept_id;
		this.time = time;
		this.path = path;
	}


	private String path;
	
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
	}
	public String getAddress() {
		return address;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	public int getDept_id() {
		return dept_id;
	}
	public void setDept_id(int dept_id) {
		this.dept_id = dept_id;
	}
	public Date getTime() {
		return time;
	}
	public void setTime(Date time) {
		this.time = time;
	}
	public String getPath() {
		return path;
	}
	public void setPath(String path) {
		this.path = path;
	}
}
```

## 4. 配置MyBatis的数据库映射配置
    1.在config包下创建mapsql包用于放置sql语句的映射文件
    2.在config.mapsql下创建mapsql.xml文件代码如下

* namespace 定位了命名空间
* select、delete等标签内的id属性定位了对应的sql语句
* resultType="Person" 定义了调用该sql语句 查找到的数据自动赋值给resultType：Person类中，这个Person即之前自定义的实体类，赋值按数据库中顺序赋值
* parameterType="int"为参数类型，SQL语句中的#{value}即为该参数的值，当参数类型为其他实体类时，可以用#{属性名}来访问对应实体类中的属性，如id、name等等
* 后面操作数据库时，Session类调用时需要这些


```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN" "mybatis-3-mapper.dtd" >
<mapper namespace="person">
	<!-- 查找到的数据自动赋值给resultType：Person类中，这个Person即后面自定义的实体类 
         赋值按数据库中顺序赋值 -->
  	<select id="findAll" resultType="Person">
  		select * from person
  	</select>
 
 	<select id="findById" resultType="Person" parameterType="int">
 		select * from person where id=#{value}
 	</select> 		
 	
  	<select id="findById2" resultType="Person" parameterType="Person">
 		select * from person where id=#{id}
 	</select> 	
  	
  	<select id="findByName" resultType="Person" parameterType="String">
		select * from person where name=#{value}
  	</select>
  	
  	<select id="findByMohu" resultType="Person" parameterType="String">
  		select * from person where name like '%' ||#{name} ||'%'
  	</select>
  	
  	<delete id="deleteById" parameterType="int">
  		delete from person where id=#{value}
  	</delete>
  	
  	<insert id="insertPerson" parameterType="Person">
  		insert into person (id,name,age,address) values(#{id},#{name},#{age},#{address})
  	</insert>
  	
  	<update id="updateById" parameterType="Person">
  		update person set name=#{name},age=#{age},address=#{address} where id=#{id}
  	</update>
  	 	
</mapper>

```

## 5.配置MyBatis.xml文件
    在config包下创建MyBatis.xml文件,代码如下：
```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "mybatis-3-config.dtd" >
<configuration>
	<!-- 加载db.properties文件 -->
	<properties resource="config/db.properties"></properties>
	<!-- 扫描实体包 -->
	<typeAliases>
		<package name="com.neu.entity"></package>
	</typeAliases>
	
	<!-- 全局数据库的相关配置 -->
		<environments default="development">
			<environment id="development">
			<!-- 配置事务管理 -->
			<transactionManager type="JDBC"></transactionManager>
			<!-- 配置数据库的连接 -->
			<dataSource type="POOLED">
				<!-- 加载数据库驱动 -->
				<property name="driver" value="${db.driver}"/>
				<!-- 加载数据库连接 -->
				<property name="url" value="${db.url}"/>
				<!-- 加载用户名和密码 -->
				<property name="username" value="${db.username}"/>
				<property name="password" value="${db.password}"/>
			</dataSource>
			</environment>
		</environments>
		
		<!-- 加载映射文件 -->
		<mappers>
			<mapper resource="config/mapsql/mapsql.xml"></mapper>
		</mappers>	
	
</configuration>

```

## 6. 定义测试类，即具体实现数据库功能的类
    在com.neu包下创建test包（或者叫controller包），新建一个类Test,代码如下：

```java
package com.neu.test;

import java.io.IOException;
import java.io.Reader;
import java.util.List;

import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;

import com.neu.entity.Person;

public class Test {

	/**
	 * @param args
	 */
	public static void main(String[] args) {
		// TODO Auto-generated method stub
		SqlSessionFactory sessionFactory=null;
		SqlSession session=null;
		//读取核心配置文件
		try{
			Reader reader=Resources.getResourceAsReader("config/MyBatis.xml");
			//通过xml文件构造SqlSessionFactory
			sessionFactory=new SqlSessionFactoryBuilder().build(reader);
			//通过工厂类实例化SqlSession
			session=sessionFactory.openSession();
			
/*			
			//查找所有用户
			List<Person> list=session.selectList("person.findAll");
			for(Person p:list){
			System.out.println(p.getAge());
		}
*/			
			
/*			//根据id查找用户方法1
			Person p1=session.selectOne("person.findById", 1);
			System.out.println(p1.getName());
*/			
			
/*			//根据id查找用户方法2
			Person p2=session.selectOne("person.findById2", p1);
			System.out.println(p2.getName());
*/			
			
/*			
			//根据名字name属性查找用户：
			Person p=session.selectOne("person.findByName","zzh");
			System.out.println(p.getId());			
*/
/*			
			//模糊查找
			String name="z";
			List<Person> list=session.selectList("person.findByMohu",name);
			for(Person p:list){
				System.out.println(p.getName());
			}
*/			
/*			//删除用户
			int count=session.delete("deleteById", 1);
			System.out.println(count);
			//提交用户
			session.commit();
			*/
			
/*			//添加用户
			Person p=new Person();
			p.setId(1);
			p.setName("ZZH");
			p.setAge(18);
			p.setAddress("shou401");
			int count=session.insert("insertPerson",p);
			System.out.println(count);
			//提交用户
			session.commit();*/
			
			//更新用户信息
			Person p=new Person();
			p.setId(1);
			p.setName("ZZH");
			p.setAge(18);
			p.setAddress("shou401");
			int count=session.update("updateById",p);
			System.out.println(count);
			//提交用户
			session.commit();
			
		} catch (IOException e){
			e.printStackTrace();
		}
	}

}

```