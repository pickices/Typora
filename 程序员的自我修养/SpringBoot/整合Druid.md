# 整合Druid

1. 需要自己为DruidDataSource绑定全局配置文件中的参数，再添加到容器中，而不再使用Spring Boot的自动生成；我们需要自己添加DruidDataSource 组件到容器中，并绑定属性；
   ```java
   package com.kuang.config;
   
   import com.alibaba.druid.pool.DruidDataSource;
   import org.springframework.boot.context.properties.ConfigurationProperties;
   import org.springframework.context.annotation.Bean;
   import org.springframework.context.annotation.Configuration;
   
   import javax.sql.DataSource;
   
   @Configuration
   public class DruidConfig {
       /*
          将自定义的 Druid数据源添加到容器中，不再让 Spring Boot自动创建
          绑定全局配置文件中的 druid数据源属性到 com.alibaba.druid.pool.DruidDataSource从而让它们生效
          @ConfigurationProperties(prefix = "spring.datasource")：作用就是将 全局配置文件中
          前缀为 spring.datasource的属性值注入到 com.alibaba.druid.pool.DruidDataSource 的同名参数中
        */
       @ConfigurationProperties(prefix = "spring.datasource")
       @Bean
       public DataSource druidDataSource() {
           return new DruidDataSource();
       }
   }
   ```

2. Druid数据源具有监控的功能，并提供了一个web界面方便用户查看。所以需要设置 Druid 的后台管理页面，比如登录账号、密码 等；配置后台管理；

   ```java
   //配置 Druid 监控管理后台的Servlet；
   //内置 Servlet 容器时没有web.xml文件，所以使用 Spring Boot 的注册 Servlet 方式
   @Bean
   public ServletRegistrationBean statViewServlet() {
       ServletRegistrationBean bean = new ServletRegistrationBean(new StatViewServlet(), "/druid/*");
   
       // 这些参数可以在 com.alibaba.druid.support.http.StatViewServlet 
       // 的父类 com.alibaba.druid.support.http.ResourceServlet 中找到
       Map<String, String> initParams = new HashMap<>();
       initParams.put("loginUsername", "admin"); //后台管理界面的登录账号
       initParams.put("loginPassword", "123456"); //后台管理界面的登录密码
   
       //后台允许谁可以访问
       //initParams.put("allow", "localhost")：表示只有本机可以访问
       //initParams.put("allow", "")：为空或者为null时，表示允许所有访问
       initParams.put("allow", "");
       //deny：Druid 后台拒绝谁访问
       //initParams.put("kuangshen", "192.168.1.20");表示禁止此ip访问
   
       //设置初始化参数
       bean.setInitParameters(initParams);
       return bean;
   }
   ```

3. 配置完毕后，我们可以访问 ：http://localhost:8080/druid/login.html

4. 配置 Druid web 监控 filter 过滤器

   ```java
   //配置 Druid 监控 之  web 监控的 filter
   //WebStatFilter：用于配置Web和Druid数据源之间的管理关联监控统计
   @Bean
   public FilterRegistrationBean webStatFilter() {
       FilterRegistrationBean bean = new FilterRegistrationBean();
       bean.setFilter(new WebStatFilter());
   
       //exclusions：设置哪些请求进行过滤排除掉，从而不进行统计
       Map<String, String> initParams = new HashMap<>();
       initParams.put("exclusions", "*.js,*.css,/druid/*,/jdbc/*");
       bean.setInitParameters(initParams);
   
       //"/*" 表示过滤所有请求
       bean.setUrlPatterns(Arrays.asList("/*"));
       return bean;
   }
   平时在工作中，按需求进行配
   ```

   
