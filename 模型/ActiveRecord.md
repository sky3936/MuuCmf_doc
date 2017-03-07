# ActiveRecord

ThinkPHP实现了ActiveRecords模式的ORM模型，采用了非标准的ORM模型：表映射到类，记录映射到对象。最大的特点就是使用方便和便于理解（因为采用了对象化），提供了开发的最佳体验，从而达到敏捷开发的目的。

下面我们用AR模式来换一种方式重新完成CURD操作。

### 创建数据

```php
$User = M("User"); // 实例化User对象
// 然后直接给数据对象赋值
$User->name = 'ThinkPHP';
$User->email = 'ThinkPHP@gmail.com';
// 把数据对象添加到数据库
$User->add();
```

如果使用了create方法创建数据对象的话，仍然可以在创建完成后进行赋值

```php
$User = D("User");
$User->create(); // 创建User数据对象，默认通过表单提交的数据进行创建
// 增加或者更改其中的属性
$User->status = 1;
$User->create_time = time();
// 把数据对象添加到数据库
$User->add(); 
```

### 查询记录

AR模式的数据查询比较简单，因为更多情况下面查询条件都是以主键或者某个关键的字段。这种类型的查询，ThinkPHP有着很好的支持。 先举个最简单的例子，假如我们要查询主键为8的某个用户记录，如果按照之前的方式，我们可能会使用下面的方法：

```php
$User = M("User"); // 实例化User对象
// 查找id为8的用户数据
$User->where('id=8')->find();
```

用AR模式的话可以直接写成：

```php
$User->find(8);
```

如果要根据某个字段查询，例如查询姓名为ThinkPHP的可以用：

```php
$User = M("User"); // 实例化User对象
$User->getByName("ThinkPHP");
```

这个作为查询语言来说是最为直观的，如果查询成功，查询的结果直接保存在当前的数据对象中，在进行下一次查询操作之前，我们都可以提取，例如获取查询的结果数据：

```php
echo $User->name;
echo $User->email;
```

如果要查询数据集，可以直接使用：

```php
// 查找主键为1、3、8的多个数据
$userList = $User->select('1,3,8'); 
```

### 更新记录

在完成查询后，可以直接修改数据对象然后保存到数据库。

```php
$User->find(1); // 查找主键为1的数据
$User->name = 'TOPThink'; // 修改数据对象
$User->save(); // 保存当前数据对象
```

上面这种方式仅仅是示例，不代表保存操作之前一定要先查询。因为下面的方式其实是等效的：

```php
$User->id = 1;
$User->name = 'TOPThink'; // 修改数据对象
$User->save(); // 保存当前数据对象
```

### 删除记录

可以删除当前查询的数据对象

```php
$User->find(2);
$User->delete(); // 删除当前的数据对象
```

或者直接根据主键进行删除

```php
$User->delete(8); // 删除主键为8的数据
$User->delete('5,6'); // 删除主键为5、6的多个数据
```
