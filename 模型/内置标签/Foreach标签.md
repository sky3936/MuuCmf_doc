# Foreach标签

foreach标签类似与volist标签，只是更加简单，没有太多额外的属性，例如：

```php
<foreach name="list" item="vo">
    {$vo.id}:{$vo.name}
</foreach>
```

name表示数据源 item表示循环变量。

可以输出索引，如下：

```php
<foreach name="list" item="vo" >
    {$key}|{$vo}
</foreach>
```

也可以定义索引的变量名

```php
<foreach name="list" item="vo" key="k" >
   {$k}|{$vo}
</foreach>
```
