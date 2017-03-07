# PAGE

page方法也是模型的连贯操作方法之一，是完全为分页查询而诞生的一个人性化操作方法。


我们在前面已经了解了关于limit方法用于分页查询的情况，而page方法则是更人性化的进行分页查询的方法，例如还是以文章列表分页为例来说，如果使用limit方法，我们要查询第一页和第二页（假设我们每页输出10条数据）写法如下：

```php
$Article = M('Article');
$Article->limit('0,10')->select(); // 查询第一页数据
$Article->limit('10,10')->select(); // 查询第二页数据
```

虽然利用扩展类库中的分页类Page可以自动计算出每个分页的limit参数，但是如果要自己写就比较费力了，如果用page方法来写则简单多了，例如：

```php
$Article = M('Article');
$Article->page('1,10')->select(); // 查询第一页数据
$Article->page('2,10')->select(); // 查询第二页数据
```

显而易见的是，使用page方法你不需要计算每个分页数据的起始位置，page方法内部会自动计算。

和limit方法一样，page方法也支持2个参数的写法，例如：

```php
$Article->page(1,10)->select();
// 和下面的用法等效
$Article->page('1,10')->select();
```

page方法还可以和limit方法配合使用，例如：

```php
$Article->limit(25)->page(3)->select();
```

当page方法只有一个值传入的时候，表示第几页，而limit方法则用于设置每页显示的数量，也就是说上面的写法等同于：

```php
$Article->page('3,25')->select(); 
```

