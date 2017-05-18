# mylibrary 
```
<dependencies>
<!--markdown-->
	<dependency>
		<groupId>org.commonjava.googlecode.markdown4j</groupId>
		<artifactId>markdown4j</artifactId>
		<version>2.2-cj-1.0</version>
	</dependency>
	<dependency>
		<groupId>org.commonjava.googlecode.markdown4j</groupId>
		<artifactId>markdown4j</artifactId>
		<version>2.2-cj-1.0</version>
		<classifier>sources</classifier>
		<scope>provided</scope>
	</dependency>
<!--markdown-->
<!--json-->
		<dependency>
			<groupId>org.json</groupId>
			<artifactId>json</artifactId>
			<version>20150729</version>
		</dependency>
		<dependency>  
			<groupId>com.google.code.gson</groupId>  
			<artifactId>gson</artifactId>  
		<version>2.3.1</version>  
	</dependency> 
<!--json-->
</dependencies>
```
# ssh
```
  <properties>
          <struts2.version>2.3.14</struts2.version>
          <spring.version>4.1.3.RELEASE</spring.version>
          <!-- 
          	<hibernate.version>4.3.11.Final</hibernate.version>
           -->
          <hibernate.version>4.2.21.Final</hibernate.version>
          <mysql.jdbc.version>5.1.8</mysql.jdbc.version>
  </properties>
  <dependencies>
  		<!-- ssh -->
  		<dependency>
			<groupId>org.apache.struts</groupId>
			<artifactId>struts2-core</artifactId>
			<version>${struts2.version}</version>
		</dependency>
		<dependency>  
	        <groupId>org.springframework</groupId>  
	        <artifactId>spring-core</artifactId>  
	        <version>${spring.version}</version>  
	    </dependency>
		<dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-web</artifactId>
            <version>${spring.version}</version>
        </dependency>
	  	<dependency>
		   <groupId>org.hibernate</groupId>
		   <artifactId>hibernate-core</artifactId>
		   <version>${hibernate.version}</version>
		</dependency>
		<!-- ssh -->
	  	<dependency>
		    <groupId>mysql</groupId>
		    <artifactId>mysql-connector-java</artifactId>
		    <version>${mysql.jdbc.version}</version>
		</dependency>
		<!--json-->
		<dependency>
			<groupId>org.json</groupId>
			<artifactId>json</artifactId>
			<version>20150729</version>
		</dependency>
		<dependency>  
			<groupId>com.google.code.gson</groupId>  
			<artifactId>gson</artifactId>  
		<version>2.3.1</version>  
	</dependency> 
  </dependencies>
```
# mvc
```
<properties>
          <struts2.version>2.3.14</struts2.version>
          <spring.version>4.1.3.RELEASE</spring.version>
          <!--
          	<hibernate.version>4.2.21.Final</hibernate.version>
          	<hibernate.version>4.3.11.Final</hibernate.version>
           -->
           <hibernate.version>4.2.21.Final</hibernate.version>
          <mysql.jdbc.version>5.1.8</mysql.jdbc.version>
          <c3p0.version>0.9.1.2</c3p0.version>
          
          <org.springframework.version>4.0.0.RELEASE</org.springframework.version>
  </properties>
  <dependencies>
  		<!-- ssh -->
  		<dependency>
			<groupId>org.apache.struts</groupId>
			<artifactId>struts2-core</artifactId>
			<version>${struts2.version}</version>
		</dependency>
		<dependency>  
	        <groupId>org.springframework</groupId>  
	        <artifactId>spring-core</artifactId>  
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
	        <artifactId>spring-orm</artifactId>
	        <version>4.0.0.RELEASE</version>
	    </dependency>
        <dependency>
            <groupId>org.springframework</groupId>
            <artifactId>spring-tx</artifactId>
            <version>${spring.version}</version>
        </dependency>
        <!-- hibernate -->
	  	<dependency>
		   <groupId>org.hibernate</groupId>
		   <artifactId>hibernate-core</artifactId>
		   <version>${hibernate.version}</version>
		</dependency>
		<dependency>  
            <groupId>org.hibernate</groupId>  
            <artifactId>hibernate-ehcache</artifactId>  
            <version>${hibernate.version}</version>  
        </dependency> 
        <dependency>  
            <groupId>org.hibernate</groupId>  
            <artifactId>hibernate-entitymanager</artifactId>  
            <version>${hibernate.version}</version>  
        </dependency>
        <dependency>
            <groupId>org.hibernate.javax.persistence</groupId>
            <artifactId>hibernate-jpa-2.0-api</artifactId>
            <version>1.0.1.Final</version>
        </dependency>
        <!-- Spring MVC框架 -->
         <dependency>
             <groupId>org.springframework</groupId>
             <artifactId>spring-core</artifactId>
             <version>${org.springframework.version}</version>
         </dependency>
         <dependency>
             <groupId>org.springframework</groupId>
             <artifactId>spring-expression</artifactId>
             <version>${org.springframework.version}</version>
         </dependency>
		<!-- ssh -->
	  	<dependency>
		    <groupId>mysql</groupId>
		    <artifactId>mysql-connector-java</artifactId>
		    <version>${mysql.jdbc.version}</version>
		</dependency>
		<!-- c3p0 -->
		<dependency>
            <groupId>c3p0</groupId>
            <artifactId>c3p0</artifactId>
            <version>${c3p0.version}</version>
        </dependency>
  </dependencies>
```