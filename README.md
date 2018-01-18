# java-notes
notes from web

### mybatis-generator不用装插件就可以生成*实体类、DAO接口和Mapping映射文件*<br>
需要3个jar包和一个xml配置文件，文件都在同一目录，mybatis-3.x/mybatis-generator-core-1.3.2/mysql-connector-java-5.1.30<br>
配置文件generatorConfig.xml如下<br>
```<?xml version="1.0" encoding="UTF-8"?>    
<!DOCTYPE generatorConfiguration    
  PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"    
  "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">    
<generatorConfiguration>    
<!-- 数据库驱动-->    
    <classPathEntry  location="mysql-connector-java-5.1.30.jar"/>    
    <context id="DB2Tables"  targetRuntime="MyBatis3">    
        <commentGenerator>    
            <property name="suppressDate" value="true"/>    
            <!-- 是否去除自动生成的注释 true：是 ： false:否 -->    
            <property name="suppressAllComments" value="true"/>    
        </commentGenerator>    
        <!--数据库链接URL，用户名、密码 -->    
        <jdbcConnection driverClass="com.mysql.jdbc.Driver" connectionURL="jdbc:mysql://localhost/test_mybatis" userId="root" password="wangli222222">    
        </jdbcConnection>    
        <javaTypeResolver>    
            <property name="forceBigDecimals" value="false"/>    
        </javaTypeResolver>    
        <!-- 生成模型的包名和位置-->    
        <javaModelGenerator targetPackage="com.wangli.pojo" targetProject="web-front/src">    
            <property name="enableSubPackages" value="true"/>    
            <property name="trimStrings" value="true"/>    
        </javaModelGenerator>    
        <!-- 生成映射文件的包名和位置-->    
        <sqlMapGenerator targetPackage="com.wangli.mapper" targetProject="web-front/src">    
            <property name="enableSubPackages" value="true"/>    
        </sqlMapGenerator>    
        <!-- 生成DAO的包名和位置-->    
        <javaClientGenerator type="XMLMAPPER" targetPackage="com.wangli.dao" targetProject="web-front/src">    
            <property name="enableSubPackages" value="true"/>    
        </javaClientGenerator>    
        <!-- 要生成的表 tableName是数据库中的表名或视图名 domainObjectName是实体类名-->    
        <table tableName="user_info" domainObjectName="User" enableCountByExample="false" enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false" selectByExampleQueryId="false"></table>  
    </context>    
</generatorConfiguration>
```
##### cmd进入这些文件所在的目录，运行命令`java -jar mybatis-generator-core-1.3.2.jar -configfile generatorConfig.xml -overwrite`，最后将生成的文件复制到项目对应目录中

#### 注意：生成实体类之前，数据库中要创建好对应的表和字段
