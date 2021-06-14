# RestFul风格

<br/>

方法名上加注解：

```java
@RequestMapper("/add/{a}/{b}")
public String test(@PathVariable int a,@PathVariable int b){
  String res = a+b;
  model.addAttribute("msg",a+b);
  return "test";
}
```

其他请求方式使用衍生注解：

- @GetMapping("")
- @PostMapping("")
- @PutMapperMapping("")
- @DeleteMapping("")
- @PatchMapping("")

注意：在方法参数中要声明传递到url中的参数，使用注解声明：

@PathVariable
