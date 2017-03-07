# SQL查询

ThinkPHP内置的ORM和ActiveRecord模式实现了方便的数据存取操作，而且新版增加的连贯操作功能更是让这个数据操作更加清晰，但是ThinkPHP仍然保留了原生的SQL查询和执行操作支持，为了满足复杂查询的需要和一些特殊的数据操作，SQL查询的返回值因为是直接返回的Db类的查询结果，没有做任何的处理。

主要包括下面两个方法：

### QUERY方法

query方法用于执行SQL查询操作，如果数据非法或者查询错误则返回false，否则返回查询结果数据集（同select方法）。

使用示例：

```php
$Model = new \Think\Model() // 实例化一个model对象 没有对应任何数据表
$Model->query("select * from think_user where status=1");
```

如果你当前采用了分布式数据库，并且设置了读写分离的话，query方法始终是在读服务器执行，因此query方法对应的都是读操作，而不管你的SQL语句是什么。
可以在query方法中使用表名的简化写法，便于动态更改表前缀，例如：

```php
$Model = new \Think\Model() // 实例化一个model对象 没有对应任何数据表
$Model->query("select * from __PREFIX__user where status=1");
// 3.2.2版本以上还可以直接使用
$Model->query("select * from __USER__ where status=1");
```

和上面的写法等效，会自动读取当前设置的表前缀。

### EXECUTE方法

execute用于更新和写入数据的sql操作，如果数据非法或者查询错误则返回false ，否则返回影响的记录数。

使用示例：

```php
$Model = new \Think\Model() // 实例化一个model对象 没有对应任何数据表
$Model->execute("update think_user set name='thinkPHP' where status=1");
```

>如果你当前采用了分布式数据库，并且设置了读写分离的话，execute方法始终是在写服务器执行，因此execute方法对应的都是写操作，而不管你的SQL语句是什么。
也可以在execute方法中使用表名的简化写法，便于动态更改表前缀，例如：

```php
$Model = new \Think\Model() // 实例化一个model对象 没有对应任何数据表
$Model->execute("update __PREFIX__user set name='thinkPHP' where status=1");
// 3.2.2版本以上还可以直接使用
$Model->execute("update __USER__ set name='thinkPHP' where status=1");
```

和上面的写法等效，会自动读取当前设置的表前缀。