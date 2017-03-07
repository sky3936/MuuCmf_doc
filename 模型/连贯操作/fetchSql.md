# fetchSql


fetchSql用于直接返回SQL而不是执行查询，适用于任何的CURD操作方法。 例如：

```php
$result = M('User')->fetchSql(true)->find(1);
```

输出result结果为：

```php
SELECT * FROM think_user where id = 1
```

