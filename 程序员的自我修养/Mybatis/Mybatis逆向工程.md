# Mybatis逆向工程



1. 引入maven插件

   ```xml
   <plugin>
       <groupId>org.mybatis.generator</groupId>
       <artifactId>mybatis-generator-maven-plugin</artifactId>
       <version>1.4.0</version>
       <!--插件设置-->
       <configuration>
           <!--允许移动生成的文件-->
           <verbose>true</verbose>
           <!--启用覆盖-->
           <overwrite>true</overwrite>
           <!--自动生成配置 如果名字是generatorConfig.xml可以省略配置-->
           <!--<configurationFile>src/main/resources/generatorConfig.xml</configurationFile>-->
       </configuration>
   </plugin>
   ```

   

2. 编写generatorConfig.xml

   ```xml
   <?xml version="1.0" encoding="UTF-8"?>
   <!DOCTYPE generatorConfiguration
     PUBLIC "-//mybatis.org//DTD MyBatis Generator Configuration 1.0//EN"
     "http://mybatis.org/dtd/mybatis-generator-config_1_0.dtd">
   <generatorConfiguration>
     <!-- 配置文件，放在resource目录下即可 -->
     <!--数据库驱动个人配置-->
     <classPathEntry
       location="C:\Users\拾荒老冰棍\.m2\repository\mysql\mysql-connector-java\5.1.49\mysql-connector-java-5.1.49.jar"/>
     <context id="MysqlTables" targetRuntime="MyBatis3">
       <property name="autoDelimitKeywords" value="true"/>
       <!--可以使用包括字段名，避免字段名与sql保留字冲突报错-->
       <property name="beginningDelimiter" value="`"/>
       <property name="endingDelimiter" value="`"/>
       <!-- optional，旨在创建class时，对注释进行控制 -->
       <commentGenerator>
         <property name="suppressDate" value="true"/>
         <property name="suppressAllComments" value="true"/>
       </commentGenerator>
       <!--数据库链接地址账号密码-->
       <jdbcConnection driverClass="com.mysql.jdbc.Driver"
         connectionURL="jdbc:mysql://10.16.68.188:3306/mumu_mall?useUnicode=true&amp;characterEncoding=UTF-8"
         userId="root"
         password="592295lxc">
         <property name="nullCatalogMeansCurrent" value="true"/>
       </jdbcConnection>
       <!-- 非必需，类型处理器，在数据库类型和java类型之间的转换控制-->
       <javaTypeResolver>
         <property name="forceBigDecimals" value="false"/>
       </javaTypeResolver>
       <!--生成Model类存放位置-->
       <javaModelGenerator targetPackage="com.liuxinchi.mumu_mall.model.pojo"
         targetProject="src/main/java">
         <!-- 是否允许子包，即targetPackage.schemaName.tableName -->
         <property name="enableSubPackages" value="true"/>
         <!-- 是否对类CHAR类型的列的数据进行trim操作 -->
         <property name="trimStrings" value="true"/>
         <!-- 建立的Model对象是否 不可改变  即生成的Model对象不会有 setter方法，只有构造方法 -->
         <property name="immutable" value="false"/>
       </javaModelGenerator>
       <!--生成mapper映射文件存放位置-->
       <sqlMapGenerator targetPackage="mappers" targetProject="src/main/resources">
         <property name="enableSubPackages" value="true"/>
       </sqlMapGenerator>
       <!--生成Dao类存放位置-->
       <javaClientGenerator type="XMLMAPPER" targetPackage="com.liuxinchi.mumu_mall.model.dao"
         targetProject="src/main/java">
         <property name="enableSubPackages" value="true"/>
       </javaClientGenerator>
       <!--生成对应表及类名-->
       <table schema="root" tableName="mumu_mall_cart" domainObjectName="Cart"
         enableCountByExample="false"
         enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false"
         selectByExampleQueryId="false">
       </table>
       <table tableName="mumu_mall_category" domainObjectName="Category" enableCountByExample="false"
         enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false"
         selectByExampleQueryId="false">
       </table>
       <table tableName="mumu_mall_order" domainObjectName="Order" enableCountByExample="false"
         enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false"
         selectByExampleQueryId="false">
       </table>
       <table tableName="mumu_mall_order_item" domainObjectName="OrderItem"
         enableCountByExample="false"
         enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false"
         selectByExampleQueryId="false">
       </table>
       <table tableName="mumu_mall_product" domainObjectName="Product" enableCountByExample="false"
         enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false"
         selectByExampleQueryId="false">
       </table>
       <table tableName="mumu_mall_user" domainObjectName="User" enableCountByExample="false"
         enableUpdateByExample="false" enableDeleteByExample="false" enableSelectByExample="false"
         selectByExampleQueryId="false">
       </table>
   
     </context>
   </generatorConfiguration>
   ```

   

3.使用maven插件

