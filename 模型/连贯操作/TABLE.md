# TABLE
table方法也属于模型类的连贯操作方法之一，主要用于指定操作的数据表。

## 用法

一般情况下，操作模型的时候系统能够自动识别当前对应的数据表，所以，使用table方法的情况通常是为了：

切换操作的数据表；
对多表进行操作；
例如：
```php
$Model->table('think_user')->where('status>1')->select();
```

也可以在table方法中指定数据库，例如：

```php
$Model->table('db_name.think_user')->where('status>1')->select();
```

table方法指定的数据表需要完整的表名，但可以采用下面的方式简化数据表前缀的传入，例如：

```php
$Model->table('__USER__')->where('status>1')->select();
```

会自动获取当前模型对应的数据表前缀来生成 think_user 数据表名称。

需要注意的是table方法不会改变数据库的连接，所以你要确保当前连接的用户有权限操作相应的数据库和数据表。 切换数据表后，系统会自动重新获取切换后的数据表的字段缓存信息。

如果需要对多表进行操作，可以这样使用：

```php
$Model->field('user.name,role.title')
->table('think_user user,think_role role')
->limit(10)->select();
```

为了尽量避免和mysql的关键字冲突，可以建议使用数组方式定义，例如：

```php
$Model->field('user.name,role.title')
->table(array('think_user'=>'user','think_role'=>'role'))
->limit(10)->select();
```

使用数组方式定义的优势是可以避免因为表名和关键字冲突而出错的情况。


>一般情况下，无需调用table方法，默认会自动获取当前模型对应或者定义的数据表。
