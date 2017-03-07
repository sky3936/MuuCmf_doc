# LIMIT

limit方法也是模型类的连贯操作方法之一，主要用于指定查询和操作的数量，特别在分页查询的时候使用较多。ThinkPHP的limit方法可以兼容所有的数据库驱动类的。

### 限制结果数量

例如获取满足要求的10个用户，如下调用即可：

```php
$User = M('User');
$User->where('status=1')->field('id,name')->limit(10)->select();
```

limit方法也可以用于写操作，例如更新满足要求的3条数据：

```php
$User = M('User');
$User->where('score=100')->limit(3)->save(array('level'=>'A'));
```

### 分页查询

用于文章分页查询是limit方法比较常用的场合，例如：

```php
$Article = M('Article');
$Article->limit('10,25')->select();
```

表示查询文章数据，从第10行开始的25条数据（可能还取决于where条件和order排序的影响 这个暂且不提）。


你也可以这样使用，作用是一样的：

```php
$Article = M('Article');
$Article->limit(10,25)->select();
```

对于大数据表，尽量使用limit限制查询结果，否则会导致很大的内存开销和性能问题。
