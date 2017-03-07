# ALIAS

alias用于设置当前数据表的别名，便于使用其他的连贯操作例如join方法等。

示例：

```php
$Model = M('User');
$Model->alias('a')->join('__DEPT__ b ON b.user_id= a.id')->select();
```

最终生成的SQL语句类似于：

```php
SELECT * FROM think_user a INNER JOIN think_dept b ON b.user_id= a.id
```

