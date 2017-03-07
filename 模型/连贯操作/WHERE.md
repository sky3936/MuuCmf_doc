# WHERE
where方法的用法是ThinkPHP查询语言的精髓，也是ThinkPHP ORM的重要组成部分和亮点所在，可以完成包括普通查询、表达式查询、快捷查询、区间查询、组合查询在内的查询操作。where方法的参数支持字符串和数组，虽然也可以使用对象但并不建议。

## 字符串条件

使用字符串条件直接查询和操作，例如：

```php
$User = M("User"); // 实例化User对象
$User->where('type=1 AND status=1')->select(); 
```
最后生成的SQL语句是
```php
SELECT * FROM think_user WHERE type=1 AND status=1
```
使用字符串条件的时候，建议配合预处理机制，确保更加安全，例如：

```php
$Model->where("id=%d and username='%s' and xx='%f'",array($id,$username,$xx))->select();
```
或者使用：
```php
$Model->where("id=%d and username='%s' and xx='%f'",$id,$username,$xx)->select();
```

如果$id变量来自用户提交或者URL地址的话，如果传入的是非数字类型，则会强制格式化为数字格式后进行查询操作。

字符串预处理格式类型支持指定数字、字符串等，具体可以参考vsprintf方法的参数说明。

## 数组条件

数组条件的where用法是ThinkPHP推荐的用法。

## 普通查询

最简单的数组查询方式如下：

```php
$User = M("User"); // 实例化User对象
$map['name'] = 'thinkphp';
$map['status'] = 1;
// 把查询条件传入查询方法
$User->where($map)->select(); 
```
最后生成的SQL语句是
```php
SELECT * FROM think_user WHERE `name`='thinkphp' AND status=1
```

## 表达式查询

上面的查询条件仅仅是一个简单的相等判断，可以使用查询表达式支持更多的SQL查询语法，查询表达式的使用格式：

>$map['字段1']  = array('表达式','查询条件1');

>$map['字段2']  = array('表达式','查询条件2');

>$Model->where($map)->select(); // 也支持

表达式不分大小写，支持的查询表达式有下面几种，分别表示的含义是：

|表达式	|含义|
|----|-----|
|EQ	|等于（=）|
|NEQ	|不等于（<>）|
|GT	|大于（>）|
|EGT	|大于等于（>=）|
|LT	|小于（<）|
|ELT	|小于等于（<=）|
|LIKE	|模糊查询|
|[NOT] BETWEEN	|（不在）区间查询|
|[NOT] IN	|（不在）IN 查询|
|EXP	|表达式查询，支持SQL语法|

## 多次调用

where方法支持多次调用，但字符串条件只能出现一次，例如：

```php
$map['a'] = array('gt',1);
$where['b'] = 1;
$Model->where($map)->where($where)->where('status=1')->select();
```
多次的数组条件表达式会最终合并，但字符串条件则只支持一次。

更多的查询用法，可以参考查询语言部分。
