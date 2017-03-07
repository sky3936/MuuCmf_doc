# INDEX


index方法用于数据集的强制索引操作，例如：

```php
$Model->index('user')->select();
```

对查询强制使用user索引，user必须是数据表实际创建的索引名称。
