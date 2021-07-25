# SpringCloud生态

![image-20210714131936908](https://raw.githubusercontent.com/pickices/Typora/master/image/20210714131936.png)

SpringCloud是一种生态，他包含以下组件：

- API网关
- 服务注册中心
- 服务提供者
- 服务消费者
- 服务配置中心

## spring Cloud NetFlix（一站式解决方案）

- Api网关：zuul组件
- Feign：Httpclinet（Http通信方式，同步，阻塞）
- 服务注册发现：Eureka
- 熔断机制：HystriX



## Apache Dubbo Zookeeper（半自动，需要整合第三方组件）

- API网关：第三方组件，如zuul
- Feign：Dubbo
- 服务注册发现：Zookeeper
- 熔断机制：第三方组件，如HystriX



## Spring Cloud Alibaba（一站式解决方案）

