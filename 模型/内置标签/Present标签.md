# Present标签

present标签用于判断某个变量是否已经定义，用法：

```php
<present name="name">
name已经赋值
</present>
```

如果判断没有赋值，可以使用：

```php
<notpresent name="name">
name还没有赋值
</notpresent>
```

可以把上面两个标签合并成为：

```php
<present name="name">
name已经赋值
<else /> 
name还没有赋值
</present> 
```

present标签的name属性可以直接使用系统变量，例如：

```php
<present name="Think.get.name">
$_GET['name']已经赋值
</present>
```