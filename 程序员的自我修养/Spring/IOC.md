# IOC

## 1、bean头文件

```xml
<?xml version="1.0" encoding="UTF-8"?>
<beans xmlns="http://www.springframework.org/schema/beans"
    xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
    xmlns:context="http://www.springframework.org/schema/context"
    xsi:schemaLocation="http://www.springframework.org/schema/beans
        http://www.springframework.org/schema/beans/spring-beans.xsd
        http://www.springframework.org/schema/context
        http://www.springframework.org/schema/context/spring-context.xsd">
<context:annotation-config/>
</beans>
```

## 2、Spring注解

- @Autowired
自动注入成员变量，先以bytype方式，若不能匹配，则用@Qualifier(value = "")
- @Resource 
自动注入成员变量，先以byname方式，若不能匹配，则用bytype方法，在jdk1.8后失效。
- @Component
自动注册类，放在类上，说明这个类已经被Spring管理
- @value
- 放在属性或者set方法上，可以直接给属性赋值@value(")

**Component会按照mvc三层架构生成几种衍生注解功能和Component完全一样！！！，都是将某个类注册到Spring中，装配Bean**

- Dao层：@Repository
- Service层：@Service
- Controller层：@Controller
- @Scope
设置作用域，@Scope("singleton")或@Scope("prototype")

## 3、**java注解进行配置**

- @Configuration
本身就自带了@Component，是一个配置类，和beans.xml等价
- @ComponentScan
扫描其他@Component,@ComponentScan("xxx.xxx.xxx")
- @Bean
- 相当于XML里的bean标签，方法名想当与bean标签的id，方法的返回值相当于bean标签的class
@Import
引入另一个配置类，@Import(另一个配置类.class)
