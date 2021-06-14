# SpringApplication



### 这个类主要做了以下四件事情

1. 推断应用的类型是普通的项目还是Web项目
2. 查找并加载所有可用初始化器，设置到initializers属性中
3. 找出所有的应用程序监听器，设置到 listeners属性中
4. 推断并设置main方法的定义类，找到运行的主类
