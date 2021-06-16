# Swagger

```java
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
                paths(PathSelectors.ant("/root")).
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
