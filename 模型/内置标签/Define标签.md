# Define标签

DEFINE标签用于中模板中定义常量，用法如下：

```php
<define name="MY_DEFINE_NAME" value="3" />
```

在运行模板的时候，就会定义一个MY_DEFINE_NAME的常量。

value属性可以支持变量（包括系统变量），例如：

```php
<define name="MY_DEFINE_NAME" value="$name" />
```

或者

```php
<define name="MY_DEFINE_NAME" value="$Think.get.name" />
```