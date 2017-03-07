# FIELD
field方法属于模型的连贯操作方法之一，主要目的是标识要返回或者操作的字段，可以用于查询和写入操作。

## 用于查询

### 指定字段

在查询操作中field方法是使用最频繁的。
```php
$Model->field('id,title,content')->select();
```
这里使用field方法指定了查询的结果集中包含id,title,content三个字段的值。执行的SQL相当于：

```php
SELECT id,title,content FROM table
```
可以给某个字段设置别名，例如：

```php
$Model->field('id,nickname as name')->select();
```
执行的SQL语句相当于：

```php
SELECT id,nickname as name FROM table
```
使用SQL函数

可以在field方法中直接使用函数，例如：

```php
$Model->field('id,SUM(score)')->select();
```
执行的SQL相当于：

```php
SELECT id,SUM(score) FROM table
```
除了select方法之外，所有的查询方法，包括find等都可以使用field方法。
使用数组参数

field方法的参数可以支持数组，例如：

```php
$Model->field(array('id','title','content'))->select();
```
最终执行的SQL和前面用字符串方式是等效的。

数组方式的定义可以为某些字段定义别名，例如：

```php
$Model->field(array('id','nickname'=>'name'))->select();
```
执行的SQL相当于：

```php
SELECT id,nickname as name FROM table
```

对于一些更复杂的字段要求，数组的优势则更加明显，例如：

```php
$Model->field(array('id','concat(name,'-',id)'=>'truename','LEFT(title,7)'=>'sub_title'))->select();
```

执行的SQL相当于：

```php
SELECT id,concat(name,'-',id) as truename,LEFT(title,7) as sub_title FROM table
```

### 获取所有字段

如果有一个表有非常多的字段，需要获取所有的字段（这个也许很简单，因为不调用field方法或者直接使用空的field方法都能做到）：

```php
$Model->select();
$Model->field()->select();
$Model->field('*')->select();
```

上面三个用法是等效的，都相当于执行SQL：

```php
SELECT * FROM table
```
但是这并不是我说的获取所有字段，我希望显式的调用所有字段（对于对性能要求比较高的系统，这个要求并不过分，起码是一个比较好的习惯），那么OK，仍然很简单，下面的用法可以完成预期的作用：

```php
$Model->field(true)->select();
```
field(true)的用法会显式的获取数据表的所有字段列表，哪怕你的数据表有100个字段。

## 字段排除

如果我希望获取排除数据表中的content字段（文本字段的值非常耗内存）之外的所有字段值，我们就可以使用field方法的排除功能，例如下面的方式就可以实现所说的功能：

```php
$Model->field('content',true)->select();
```

则表示获取除了content之外的所有字段，要排除更多的字段也可以：

```php
$Model->field('user_id,content',true)->select();
//或者用
$Model->field(array('user_id','content'),true)->select();
```

### 用于写入

除了查询操作之外，field方法还有一个非常重要的安全功能--字段合法性检测。field方法结合create方法使用就可以完成表单提交的字段合法性检测，如果我们在表单提交的处理方法中使用了：

```php
$Model->field('title,email,content')->create();

即表示表单中的合法字段只有title,email和content字段，无论用户通过什么手段更改或者添加了浏览器的提交字段，都会直接屏蔽。因为，其他是所有字段我们都不希望由用户提交来决定，你可以通过自动完成功能定义额外的字段写入。

同样的，field也可以结合add和save方法，进行字段过滤，例如：

```php
$Model->field('title,email,content')->save($data);
```

如果data数据中包含有title,email,content之外的字段数据的话，也会过滤掉。
