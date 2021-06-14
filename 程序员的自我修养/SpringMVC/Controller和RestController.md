# Controller和RestController

<br/>

- Controller
  
  如果方法体上没有@ResponseBody，则方法返回的字符串为转发位置。
  
  如果方法体上有@ResponseBody，则方法返回的字符串就是字符串本身。
- RestController
  
  注解有RestController的所有方法的返回值都是字符串而非转发位置
