# DATA

data方法也是模型类的连贯操作方法之一，用于设置当前要操作的数据对象的值。

## 写操作

通常情况下我们都是通过create方法或者赋值的方式生成数据对象，然后写入数据库，例如： 

```php
$Model = D('User');
$Model->create();
// 这里略过具体的自动生成和验证判断
$Model->add();
```

又或者直接对数据对象赋值，例如：

```php
$Model = M('User');
$Model->name = '流年';
$Model->email = 'thinkphp@qq.com';
$Model->add();
```

那么data方法则是直接生成要操作的数据对象，例如：

```php
$Model = M('User');
$data['name'] = '流年';
$data['email'] = 'thinkphp@qq.com';
$Model->data($data)->add();
```

注意：如果我们同时使用create方法和data创建数据对象的话，则最后调用的方法有效。
data方法支持数组、对象和字符串，对象方式如下：

```php
$Model = M('User');
$obj = new \stdClass;
$obj->name = '流年';
$obj->email = 'thinkphp@qq.com';
$Model->data($obj)->add();
```

字符串方式用法如下：

```php
$Model = M('User');
$data = 'name=流年&email=thinkphp@qq.com';
$Model->data($data)->add();
```

也可以直接在add方法中传入数据对象来新增数据，例如：

```php
$Model = M('User');
$data['name'] = '流年';
$data['email'] = 'thinkphp@qq.com';
$Model->add($data);
```

但是这种方式data参数只能使用数组。

当然data方法也可以用于更新数据，例如：

```php
$Model = M('User');
$data['id'] = 8;
$data['name'] = '流年';
$data['email'] = 'thinkphp@qq.com';
$Model->data($data)->save();
```

当然我们也可以直接这样用：

```php
$Model = M('User');
$data['id'] = 8;
$data['name'] = '流年';
$data['email'] = 'thinkphp@qq.com';
$Model->save($data);
```

同样，此时data参数只能传入数组。

在调用save方法更新数据的时候 会自动判断当前的数据对象里面是否有主键值存在，如果有的话会自动作为更新条件。也就是说，下面的用法和上面等效：

```php
$Model = M('User');
$data['name'] = '流年';
$data['email'] = 'thinkphp@qq.com';
$Model->data($data)->where('id=8')->save();
```

## 读操作

除了写操作外，data方法还可以用于读取当前的数据对象，例如：

```php
$User = M('User');
$map['name'] = '流年';
$User->where($map)->find();
// 读取当前数据对象
$data = $User->data(); 
```


