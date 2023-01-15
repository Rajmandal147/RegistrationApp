<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.cdac</groupId>
  <artifactId>expense-mng-system</artifactId>
  <version>0.0.1-SNAPSHOT</version>
  <packaging>war</packaging>
  <build>
    <sourceDirectory>src</sourceDirectory>
    <plugins>
      <plugin>
        <artifactId>maven-compiler-plugin</artifactId>
        <version>3.8.0</version>
        <configuration>
          <source>1.8</source>
          <target>1.8</target>
        </configuration>  
      </plugin>
      <plugin>
        <artifactId>maven-war-plugin</artifactId>
        <version>3.2.1</version>
        <configuration>
          <warSourceDirectory>WebContent</warSourceDirectory>
        </configuration>
      </plugin>
    </plugins>
  </build>
  
  
  <properties>
  	<spring.version>4.3.20.RELEASE</spring.version>
  	<aspectj.version>1.8.13</aspectj.version>
  	<mysql.connector.java.version>8.0.13</mysql.connector.java.version>
  	<hibernate.version>4.3.0.Final</hibernate.version>
  </properties>
  <dependencies>
  
  <dependency>
    	<groupId>org.springframework</groupId>
    	<artifactId>spring-core</artifactId>
    	<version>${spring.version}</version>
  </dependency>
  <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-beans</artifactId>
        <version>${spring.version}</version>
    </dependency>
	
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-context-support</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-jdbc</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-orm</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-web</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-webmvc</artifactId>
        <version>${spring.version}</version>
    </dependency>
	
	
	<dependency>
        <groupId>org.springframework</groupId>
        <artifactId>spring-aop</artifactId>
        <version>${spring.version}</version>
    </dependency>
    <dependency>
		<groupId>org.aspectj</groupId>
		<artifactId>aspectjrt</artifactId>
		<version>${aspectj.version}</version>
	</dependency>
		
	<dependency>
		<groupId>org.aspectj</groupId>
		<artifactId>aspectjweaver</artifactId>
		<version>${aspectj.version}</version>
	</dependency>
	
	<dependency>
		<groupId>mysql</groupId>
		<artifactId>mysql-connector-java</artifactId>
		<version>${mysql.connector.java.version}</version>
	</dependency>
	
	<dependency>
		<groupId>mysql</groupId>
		<artifactId>mysql-connector-java</artifactId>
		<version>${mysql.connector.java.version}</version>
	</dependency>
	
  	<dependency>
  		<groupId>org.hibernate</groupId>
  		<artifactId>hibernate-core</artifactId>
  		<version>${hibernate.version}</version>
  	</dependency>
  	<dependency>
    	<groupId>org.hibernate</groupId>
    	<artifactId>hibernate-entitymanager</artifactId>
    	<version>${hibernate.version}</version>
	</dependency>
	<dependency>
    	<groupId>org.hibernate</groupId>
    	<artifactId>hibernate-ehcache</artifactId>
    	<version>${hibernate.version}</version>
	</dependency>
	<dependency>
    <groupId>javax.servlet</groupId>
    <artifactId>javax.servlet-api</artifactId>
    <version>3.1.0</version>
    <scope>provided</scope>
</dependency>
	
  </dependencies>
  
</project>

----------------------------------------------------------------------web.xml----------------------------------------------------------------------


<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:p="http://www.springframework.org/schema/p"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd">

  
	<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource" >
		<property name="driverClassName" value="com.mysql.cj.jdbc.Driver" ></property>
		<property name="url" value="jdbc:mysql://localhost:3306/Rajmandal" ></property>
		<property name="username" value="Rajmandal" ></property>
		<property name="password" value="Riddhi@147" ></property>
	</bean>
	 
	<bean id="sessionFactory" class="org.springframework.orm.hibernate4.LocalSessionFactoryBean" autowire="byName" >
		<property name="hibernateProperties">
			<props>
				<prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
				<prop key="hibernate.show_sql">true</prop>
				<prop key="hibernate.hbm2ddl.auto">update</prop>
			</props>
		</property>
		<property name="annotatedClasses">
			<list>
				<value>com.task.dto.User</value>
				
			</list>
		</property>
	</bean>
	<bean id="hibernateTemplate" class="org.springframework.orm.hibernate4.HibernateTemplate" autowire="byType" ></bean>
	
	<context:component-scan base-package="com.task"></context:component-scan>
	
	<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver" >
		<property name="prefix" value="/" ></property>
		<property name="suffix" value=".jsp" ></property>
	</bean>

</beans>
--------------------------------------------------------dispatcher-servlet.xml--------------------------------------------
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xmlns:aop="http://www.springframework.org/schema/aop"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:p="http://www.springframework.org/schema/p"
	xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-4.3.xsd
		http://www.springframework.org/schema/aop http://www.springframework.org/schema/aop/spring-aop-4.3.xsd
		http://www.springframework.org/schema/context http://www.springframework.org/schema/context/spring-context-4.3.xsd
		http://www.springframework.org/schema/mvc http://www.springframework.org/schema/mvc/spring-mvc-4.3.xsd">

  
	<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource" >
		<property name="driverClassName" value="com.mysql.cj.jdbc.Driver" ></property>
		<property name="url" value="jdbc:mysql://localhost:3306/Rajmandal" ></property>
		<property name="username" value="Rajmandal" ></property>
		<property name="password" value="Riddhi@147" ></property>
	</bean>
	 
	<bean id="sessionFactory" class="org.springframework.orm.hibernate4.LocalSessionFactoryBean" autowire="byName" >
		<property name="hibernateProperties">
			<props>
				<prop key="hibernate.dialect">org.hibernate.dialect.MySQLDialect</prop>
				<prop key="hibernate.show_sql">true</prop>
				<prop key="hibernate.hbm2ddl.auto">update</prop>
			</props>
		</property>
		<property name="annotatedClasses">
			<list>
				<value>com.task.dto.User</value>
				
			</list>
		</property>
	</bean>
	<bean id="hibernateTemplate" class="org.springframework.orm.hibernate4.HibernateTemplate" autowire="byType" ></bean>
	
	<context:component-scan base-package="com.task"></context:component-scan>
	
	<bean id="viewResolver" class="org.springframework.web.servlet.view.InternalResourceViewResolver" >
		<property name="prefix" value="/" ></property>
		<property name="suffix" value=".jsp" ></property>
	</bean>

</beans>
--------------------------------------------------------------------User.java--------------------------------------------
package com.task.dto;

import javax.persistence.Column;
import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.Id;
import javax.persistence.Table;

@Entity
@Table(name = "user")
public class User {
	@Id
	@GeneratedValue
	@Column(name = "user_id")
	private int userId;
	@Column(name = "user_name")
	private String userName;
	@Column(name = "user_pass")
	private String userPass;
	
	@Column(name = "address")
	private String address;
	@Column(name = "city")
	private String city;
	@Column(name = "state")
	private String state;
	@Column(name = "dob")
	private String dob;
	@Column(name = "gender")
	private String gender;
	
	
	
	public User(int userId) {
		super();
		this.userId = userId;
	}
	public User() {
		super();
		
	}
	public int getUserId() {
		return userId;
	}
	public void setUserId(int userId) {
		this.userId = userId;
	}
	public String getUserName() {
		return userName;
	}
	public void setUserName(String userName) {
		this.userName = userName;
	}
	public String getUserPass() {
		return userPass;
	}
	public void setUserPass(String userPass) {
		this.userPass = userPass;
	}
	public String getAddress() {
		return address;
	}
	public void setAddress(String address) {
		this.address = address;
	}
	public String getCity() {
		return city;
	}
	public void setCity(String city) {
		this.city = city;
	}
	public String getState() {
		return state;
	}
	public void setState(String state) {
		this.state = state;
	}
	public String getDob() {
		return dob;
	}
	public void setDob(String dob) {
		this.dob = dob;
	}
	public String getGender() {
		return gender;
	}
	public void setGender(String gender) {
		this.gender = gender;
	}
	public User(int userId, String userName, String userPass, String address, String city, String state, String dob,
			String gender) {
		super();
		this.userId = userId;
		this.userName = userName;
		this.userPass = userPass;
		this.address = address;
		this.city = city;
		this.state = state;
		this.dob = dob;
		this.gender = gender;
	}
	
	
	
}
-----------------------------------------------------------UserDao------------------------------------
package com.task.dao;

import java.util.List;

import com.task.dto.User;

public interface UserDao {
	void insertUser(User user);
	boolean checkUser(User user);
	List<User> selectAll(int userId);
	
	
	
}
-----------------------------------------------------------UserDaoImple------------------------------
package com.task.dto;
import com.task.*;
import java.util.List;

import org.hibernate.HibernateException;
import org.hibernate.Query;
import org.hibernate.Session;
import org.hibernate.Transaction;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.orm.hibernate5.HibernateCallback;
import org.springframework.orm.hibernate5.HibernateTemplate;
import org.springframework.stereotype.Repository;

import com.task.dao.*;
@Repository
public class UserDaoImple implements UserDao {
	@Autowired
	private HibernateTemplate hibernateTemplate;

	@Override
	public void insertUser(User user) {
		hibernateTemplate.execute(new HibernateCallback<Void>() {

			@Override
			public Void doInHibernate(Session session) throws HibernateException {
				Transaction tr=session.beginTransaction();
				session.save(user);
				tr.commit();
				session.flush();
				session.close();
				return null ;
			}
		});}

	@Override
	public boolean checkUser(User user) {
		
	boolean b=	hibernateTemplate.execute(new HibernateCallback<Boolean>() {

			@Override
			public Boolean doInHibernate(Session session) throws HibernateException {
				Transaction tr=session.beginTransaction();
				Query q=session.createQuery("from User where userName=? and userPass=?");
				q.setString(0, user.getUserName());
				q.setString(1, user.getUserPass());
				List<User> li=q.list();
				boolean flag= !li.isEmpty();
				user.setUserId(li.get(0).getUserId());
				tr.commit();
				session.flush();
				session.close();
				return  flag;
			}
		});
		
		return b;
	}

	@Override
	public List<User> selectAll(int userId) {
		List<User> userList=hibernateTemplate.execute(new HibernateCallback<List<User>>() {

			@Override
			public List<User> doInHibernate(Session session) throws HibernateException {
				Transaction tr=session.beginTransaction();
				Query al=session.createQuery("from User");
				List<User> all=al.list();
				
				Query re=session.createQuery("from User where userId=?");
				re.setInteger(0, userId);
				
				all.remove(re);
				return all;
			}
		});
		return userList;
	}

}


---------------------------------------------------------------UserController------------------------------
package com.task.cntr;

import java.util.List;

import javax.servlet.http.HttpSession;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.ui.ModelMap;
import org.springframework.validation.BindingResult;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestMethod;

import com.task.dto.User;
import com.task.service.UserService;

@Controller
public class UserController {
	
	@Autowired
	private UserService userService;


	@RequestMapping(value = "/prep_reg_form.htm",method = RequestMethod.GET)
	public String prepRegForm(ModelMap map) {
		map.put("user", new User());
		return "reg_form";  
	}
	
	@RequestMapping(value = "/reg.htm",method = RequestMethod.POST)
	public String register(User user,ModelMap map) {
		userService.addUser(user);
		
		return "index";           
	}
	
	
	
	
	                         
	@RequestMapping(value = "/prep_log_form.htm",method = RequestMethod.GET)
	public String prepLogForm(ModelMap map) {
		map.put("user", new User());
		return "login_form";
	}
	
	
	                 
	@RequestMapping(value = "/login.htm",method = RequestMethod.POST)
	public String login(User user,BindingResult result,ModelMap map,HttpSession session) {
	
		boolean b = userService.findUser(user);
		if(b) {
			session.setAttribute("user", user); 
			return "home";
		}else {
			map.put("user", new User());
		return "login_form";
		}
}
	
	@RequestMapping(value = "/user_list.htm",method = RequestMethod.GET)
	public String allUser(ModelMap map,HttpSession session) {
		int userId = ((User)session.getAttribute("user")).getUserId();
		List<User> li = userService.listAll(userId);
		map.put("userList", li);
		return "user_list";
	}
	
	
}

---------------------------------------------------------UserService----------------------------------------
package com.task.service;

import java.util.List;

import com.task.dto.User;

public interface UserService {
	void addUser(User user);
	boolean findUser(User user);
	List<User> listAll(int userId);
}
--------------------------------------------------------UserServiceImple-----------------------------

package com.task.service;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.task.dao.UserDao;
import com.task.dto.User;

@Service
public class UserServiceImple implements UserService {
	
	@Autowired
	private UserDao userDao;

	@Override
	public void addUser(User user) {  //4) this method is call now
		userDao.insertUser(user);     //5)control is here and call (userDao.insertUser(user)) method  of (UserDaoImple.java)
	}

	@Override
	public boolean findUser(User user) {
		return userDao.checkUser(user);
	}

	@Override
	public List<User> listAll(int userId) {
		// TODO Auto-generated method stub
		return userDao.selectAll(userId);
	}
	

	
}



-----------------------------------------home.jsp--------------------------------
<%@page import="com.task.dto.User"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Home Page</title>
</head>
<body> 
	<table align="center" >
		<tr><td>&nbsp;&nbsp;</td></tr>
		<tr>
			<td> Welcome <%=(session.getAttribute("user")!=null) ? ((User)session.getAttribute("user")).getUserName() : "!!!!!!!!" %> </td>
		</tr>
		<tr>
			<td> <a href="user_list.htm" >Show User</a> </td>
		</tr>
		
		<tr>
			<td> <a href="index.jsp" >Logout</a> </td>
		</tr>
	</table>
</body>
</html>

-----------------------------------------index.jsp---------------------------------
<%@ page language="java" contentType="text/html; charset=UTF-8"
    pageEncoding="UTF-8"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="UTF-8">
<title>Welcome Page</title>
</head>
<body >
	<table align="center" >
		<tr>
			<td> <a  href="prep_reg_form.htm"><h2>Registration</h2> </a> </td>
		</tr>
		<tr>
			<td> <a href="prep_log_form.htm" ><h2>Sign In</h2></a> </td>
		</tr>
	</table>
</body>
</html>  

----------------------------------------------login_form----------------------------------------
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="spr" %>    
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Login Form</title>
</head>
<body>                <!-- 11) after submitting data and control goes to (login.htm) which is in (UserController.java) page -->
	<spr:form action="login.htm" method="post" commandName="user" >
	<table align="center" >
		<tr>
			<td>
				User Name:
			</td>
			<td>
				<spr:input path="userName"/>
				<font color="red" ><spr:errors path="userName" ></spr:errors></font>
			</td>
		</tr>
		<tr>
			<td> 
				Password:
			</td>
			<td>
				<spr:password path="userPass"/>
				<font color="red" ><spr:errors path="userPass" ></spr:errors></font>
			</td>
		</tr>
		<tr>
			<td>
				<a href="index.jsp" >Back</a>
			</td>
			<td>
				<input type="submit"  value="Login" >
			</td>
		</tr>
	</table>
	</spr:form>
</body>
</html>

---------------------------------------------------------------reg_form.jsp--------------------------
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<%@ taglib uri="http://www.springframework.org/tags/form" prefix="spr" %>    
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Registration Form</title>
</head>
<body>
	<spr:form action="reg.htm" method="post" commandName="user" > <!-- 2nd) after submiting control go back to 
	                                                                   (UserController.java) -->
	<table align="center" >
		<tr>
			<td>
				User Name:
			</td>
			<td>
				<spr:input path="userName"/>
			</td>
		</tr>
		<tr>
			<td>
				Password: 
			</td>
			<td>
				<spr:password path="userPass"/>
			</td>
		</tr>
		<tr>
			<td>
				Address :
			</td>
			<td>
				<spr:input path="address"/>
			</td>
		</tr>
		<tr>
			<td>
				City:
			</td>
			<td>
				<spr:input path="city"/>
			</td>
		</tr>
		<tr>
			<td>
				State :
			</td>
			<td>
				<spr:input path="state"/>
			</td>
		</tr>
		<tr>
			<td>
				DOB:
			</td>
			<td>
				<spr:input path="dob"/>
			</td>
		</tr>
		
		<tr>
			<td>
				Gender :
			</td>
			<td>
			<spr:radiobutton path="gender" value="male" />Male
				<spr:radiobutton path="gender" value="female" />Female<br>
			</td>
		</tr>
		
		<tr>
			<td>
				<a href="index.jsp" >Back</a>
			</td>
			<td>
				<input type="submit"  value="Register" >
			</td>
		</tr>
	</table>
	</spr:form>
</body>
</html>

-------------------------------------------------------------user_list--------------------------------------------
<%@page import="com.task.dto.User"%>
<%@page import="java.util.List"%>
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
	pageEncoding="ISO-8859-1"%>

<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Login Form</title>
</head>
<body>

	<table align="center">
  <tr>
    <th>Name</th>
    <th>Password</th>
    <th>Address</th>
    <th>City</th>
    <th>State</th>
    <th>Date of Birth</th>
    <th>Gender</th>
  </tr>
 
		<% 
		List<User> elist = (List<User>)request.getAttribute("userList");
		for(User exp : elist){
		%>
		
		<tr>
			<td><%=exp.getUserName()%></td>
			<td><%=exp.getUserPass()%></td>
			<td><%=exp.getAddress()%></td>
			<td><%=exp.getCity()%></td>
			<td><%=exp.getState()%></td>
			<td><%=exp.getDob()%></td>
			<td><%=exp.getGender()%></td>
		</tr>
		<% } %>
		<tr>
			<td><a href="home.jsp">Back</a></td>
			<td></td>
		</tr>
	</table>

</body>
</html>
