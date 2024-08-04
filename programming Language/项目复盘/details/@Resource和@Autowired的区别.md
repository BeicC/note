```java
 private StringRedisTemplate redisTemplate;
```
这行代码在项目中`@Resource`失败：
因为ioc容器中已经有了一个Bean，name为`redisTemplate`，但它的类型不是`StringRedisTemplate`，所以注入失败，报错

而使用`@Autowired`就可以成功，因为引入pom依赖时，ioc容器中就会有这样的一个bean