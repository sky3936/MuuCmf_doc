# CACHE

cache方法用于查询缓存操作，也是连贯操作方法之一。

cache可以用于select、find和getField方法，以及其衍生方法，使用cache方法后，在缓存有效期之内不会再次进行数据库查询操作，而是直接获取缓存中的数据，关于数据缓存的类型和设置可以参考缓存部分。

下面举例说明，例如，我们对find方法使用cache方法如下：

```php
$Model = M('User');
$Model->where('id=5')->cache(true)->find();
```

第一次查询结果会被缓存，第二次查询相同的数据的时候就会直接返回缓存中的内容，而不需要再次进行数据库查询操作。

默认情况下， 缓存有效期和缓存类型是由DATA_CACHE_TIME和DATA_CACHE_TYPE配置参数决定的，但cache方法可以单独指定，例如：

```php
$Model = M('User');
$Model->cache(true,60,'xcache')->find();
```

表示对查询结果使用xcache缓存，缓存有效期60秒。

cache方法可以指定缓存标识：

```php
$Model = M('User');
$Model->cache('key',60)->find();
```

指定查询缓存的标识可以使得查询缓存更有效率。
这样，在外部就可以通过S方法直接获取查询缓存的数据，例如：

```php
$Model = M('User');
$result = $Model->cache('key',60)->find();
$data = S('key');
```
