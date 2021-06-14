# Mapper绑定方法

## resource方式绑定(推荐使用）

```xml
<mappers>
  <mapper resource="./UserMapper.xml"/>
</mappers>
```

## class方式绑定

```xml
<mappers>
  <mapper class="com.liuxinchi.dao.UserMapper"/> 
</mappers>
```

注意点：

- 接口和他的 Mappe配置文件必须同名
- 接口和他的 Mapper配置文件必须在同一个包下

## package方式绑定

```
<mappers>
  <package name="com.liuxinchi.dao" />
</mappers>
```

注意点：

- 接口和他的 Mappe配置文件必须同名
- 接口和他的 Mapper配置文件必须在同一个包下
