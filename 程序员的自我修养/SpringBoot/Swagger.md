# Swagger

1. 导入maven依赖

   ```xml
   <dependency>
       <groupId>io.springfox</groupId>
       <artifactId>springfox-swagger2</artifactId>
       <version>2.9.2</version>
   </dependency>
   <dependency>
       <groupId>io.springfox</groupId>
       <artifactId>springfox-swagger-ui</artifactId>
       <version>2.9.2</version>
   </dependency>
   ```

2. 编写配置类

   ```xml
   @Configuration
   @EnableSwagger2
   public class SwaggerConfig {
   
       @Bean
       public Docket docket(){
           return new Docket(DocumentationType.SWAGGER_2).
                   apiInfo(apiInfo()).
                   select().
                   //过滤接口
                   apis(RequestHandlerSelectors.basePackage("com.liuxinchi.springboot05swagger.controller")).
                   //过滤链接
                   paths(PathSelectors.any()).
                   build();
       }
   
       public ApiInfo apiInfo(){
           Contact contact = new Contact("柳鑫驰","http://localhost","pickices@qq.com");
           return new ApiInfo(
                   "Swagger Test",
                   "拾荒老冰棍学习swagger",
                   "v1.0",
                   "urn:tos",
                   contact,
                   "Apache 2.0",
                   "http://www.apache.org/licenses/LICENSE-2.0",
                   new ArrayList<VendorExtension>());
       }
   }
   ```

   
