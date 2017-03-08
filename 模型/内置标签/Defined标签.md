# Defined标签

DEFINED标签用于判断某个常量是否有定义，用法如下：

```php
<defined name="NAME">
NAME常量已经定义
</defined>
```

name属性的值要注意严格大小写
如果判断没有被定义，可以使用：

```php
<notdefined name="NAME">
NAME常量未定义
</notdefined>
```

可以把上面两个标签合并成为：

```php
<defined name="NAME">
NAME常量已经定义
<else /> 
NAME常量未定义
</defined>
```