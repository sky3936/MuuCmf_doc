# ORDER
order方法属于模型的连贯操作方法之一，用于对操作的结果排序。

用法如下：
```php
$Model->where('status=1')->order('id desc')->limit(5)->select();
```
注意：连贯操作方法没有顺序，可以在select方法调用之前随便改变调用顺序。

支持对多个字段的排序，例如：

```php
$Model->where('status=1')->order('id desc,status')->limit(5)->select();
```

如果没有指定desc或者asc排序规则的话，默认为asc。
如果你的字段和mysql关键字有冲突，那么建议采用数组方式调用，例如：

```php
$Model->where('status=1')->order(array('order','id'=>'desc'))->limit(5)->select(); 
```
