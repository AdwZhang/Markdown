### SSM项目中导入一个模块在com包下的配置修改

#### 例子：我在com文件夹下导入一个customer会员模块

1. 修改mybatis.xml配置
    修改后如下：

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration PUBLIC "-//mybatis.org//DTD Config 3.0//EN" "mybatis-3-config.dtd" >

<configuration>
	<typeAliases>
		<package name="com.user.entity"/>
		<package name="com.roomType.entity"/>
		<package name="com.floor.entity"/>
        <package name="com.customer.entity"/>
	</typeAliases>
	
	
	
	<mappers>
		<mapper resource="com/user/mapper/UserMapper.xml"></mapper>
		<mapper resource="com/roomType/mapper/RoomTypeMapper.xml"></mapper>
		<mapper resource="com/floor/mapper/FloorMapper.xml"></mapper>
		<mapper resource="com/customer/mapper/CustomerMapper.xml"></mapper>
	</mappers>	
	
</configuration>

```

### 之后修改诸如此类，效果为找到Mapper.xml中使用的实体类所在的包路径。

例如：
 ```xml   
	<select id="findAll" resultType="Customer">
		select * from customer
	</select>
```
    在resultType对应的属性中使用了Customer类，在mybatis.xml的<typeAliases>路径下，扫描到了com.customer.entity找到了该类，然后默认根据select选到的各列名（不分大小写）注入到Customer类的同名属性中。
    



2. 修改applicationContext.xml文件，在property name的value中增加com.customer.mapper

```sql
	<!-- 扫描接口包 -->
	<bean class="org.mybatis.spring.mapper.MapperScannerConfigurer">
		<property name="basePackage" value="com.user.mapper,com.roomType.mapper,com.floor.mapper,com.customer.mapper"></property>
		<property name="sqlSessionFactoryBeanName" value="sqlSessionFactory"></property>
	</bean>
```
