# SQL 日志打印

## 内置方案

MyBatis-Flex 内置了 SQL 打印分析的功能，其是使用 SQL 审计模块进行完成的，开启 SQL 日志打印代码如下：

```java
//开启审计功能
AuditManager.setEnable(true);

//设置 SQL 审计收集器
MessageCollector collector = new ConsoleMessageCollector();
AuditManager.setMessageCollector(collector);
```

通过以上代码，配置 `AuditManager` 的 `MessageCollector` 为 `ConsoleMessageCollector` 后，
每次执行 sql 请求，控制台将输入内容如下：

```
Flex exec sql taked 2 ms >>>  SELECT * FROM `tb_account` WHERE `id` = 1
Flex exec sql taked 3 ms >>>  INSERT INTO `tb_account`(`user_name`, `age`, `birthday`)  VALUES ('lisi', 22, '2023-04-07 15:28:46')
```

控制台输出了完整的 SQL，以及 SQL 执行消耗时间，方便我们在开发的时候，对慢 SQL 进行排查和快速定位。

## p6spy 方案

我们可以把数据源配置为 p6spy 数据源，使用 p6spy 的 SQL 输出功能进行 SQL 打印。更多文档参考 p6spy 官方文档：
[https://p6spy.readthedocs.io/en/latest/index.html](https://p6spy.readthedocs.io/en/latest/index.html)

使用 SpringBoot 的情况下，参考文档 [https://github.com/gavlyukovskiy/spring-boot-data-source-decorator](https://github.com/gavlyukovskiy/spring-boot-data-source-decorator)