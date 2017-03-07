# DISTINCT

DISTINCT 方法用于返回唯一不同的值 。


例如：

```php
$Model->distinct(true)->field('name')->select();
```

生成的SQL语句是： SELECT DISTINCT name FROM think_user

distinct方法的参数是一个布尔值。
