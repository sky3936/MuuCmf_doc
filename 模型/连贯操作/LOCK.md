# LOCK

Lock方法是用于数据库的锁机制，如果在查询或者执行操作的时候使用：

```php
lock(true);
```

就会自动在生成的SQL语句最后加上 FOR UPDATE或者FOR UPDATE NOWAIT（Oracle数据库）。