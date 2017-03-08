# Assign标签

ASSIGN标签用于在模板文件中赋值变量，用法如下：

```php
<assign name="var" value="123" />
```

在运行模板的时候，赋值了一个var的变量，值是123。

name属性支持系统变量，例如：

```php
<assign name="Think.get.id" value="123" />
```

表示在模板中给$_GET['id'] 赋值了 123

value属性也支持变量，例如：

```php
<assign name="var" value="$val" />
```

或者直接把系统变量赋值给var变量，例如：

```php
<assign name="var" value="$Think.get.name" />
```

相当于，执行了：$var = $_GET['name'];