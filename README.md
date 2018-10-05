# cart
app-servlet.xml
<beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
	xmlns:mvc="http://www.springframework.org/schema/mvc"
	xmlns:tx="http://www.springframework.org/schema/tx"
	xsi:schemaLocation="
        http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/mvc 
        http://www.springframework.org/schema/mvc/spring-mvc.xsd
        http://www.springframework.org/schema/tx
        http://www.springframework.org/schema/tx/spring-tx.xsd
        http://www.springframework.org/schema/context 
        http://www.springframework.org/schema/context/spring-context.xsd">

	<context:component-scan base-package="com.heb"/>

	<mvc:resources mapping="/resources/**" location="/resources/"/>
	
	<mvc:annotation-driven />
	
    <bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
        <property name="prefix" value="/WEB-INF/views/"/>
        <property name="suffix" value=".jsp"/>
    </bean>
    
    <bean class="org.springframework.web.servlet.handler.SimpleUrlHandlerMapping">
		<property name="interceptors">
			<list>
				<ref bean="sessionCheckInterceptor" />
			</list>
		</property>
	</bean>
	
	<bean id="sessionCheckInterceptor" class="com.heb.payroll.controller.SessionCheckInterceptor"/>
    
	<bean id="dataSource" class="org.springframework.jdbc.datasource.DriverManagerDataSource">
		<property name="driverClassName" value="oracle.jdbc.driver.OracleDriver" />
		<property name="url" value="jdbc:oracle:thin:@localhost:1521:xe" />
		<property name="username" value="payroll" />
		<property name="password" value="password" />
	</bean>
</beans>
