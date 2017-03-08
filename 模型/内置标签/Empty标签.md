# Empty标签

empty标签用于判断某个变量是否为空，用法：

```php
<empty name="name">
name为空值
</empty>
```

如果判断没有赋值，可以使用：

```php
<notempty name="name">
name不为空
</notempty>
```

可以把上面两个标签合并成为：

```php
<empty name="name">
name为空
<else /> 
name不为空
</empty> 
```

name属性可以直接使用系统变量，例如：

```php
<empty name="Think.get.name">
$_GET['name']为空值
</empty>
```
