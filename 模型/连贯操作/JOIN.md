# JOIN

JOIN方法也是连贯操作方法之一，用于根据两个或多个表中的列之间的关系，从这些表中查询数据。

join通常有下面几种类型，不同类型的join操作会影响返回的数据结果。

* INNER JOIN: 等同于 JOIN（默认的JOIN类型）,如果表中有至少一个匹配，则返回行

* LEFT JOIN: 即使右表中没有匹配，也从左表返回所有的行

* RIGHT JOIN: 即使左表中没有匹配，也从右表返回所有的行

* FULL JOIN: 只要其中一个表中存在匹配，就返回行

join方法可以支持以上四种类型，例如：

```php
$Model = M('Artist');
$Model
->join('think_work ON think_artist.id = think_work.artist_id')
->join('think_card ON think_artist.card_id = think_card.id')
->select();
```

join方法支持多次调用，但指定的数据表必须是全称，但我们可以这样来定义：

```php
$Model
->join('__WORK__ ON __ARTIST__.id = __WORK__.artist_id')
->join('__CARD__ ON __ARTIST__.card_id = __CARD__.id')
->select();
```
    __WORK__和 __CARD__在最终解析的时候会转换为 think_work和 think_card。

默认采用INNER JOIN 方式，如果需要用其他的JOIN方式，可以改成

```php
$Model->join('RIGHT JOIN __WORK__ ON __ARTIST__.id = __WORK__.artist_id')->select();
```

或者使用：

```php
$Model->join('__WORK__ ON __ARTIST__.id = __WORK__.artist_id','RIGHT')->select();
```

join方法的第二个参数支持的类型包括：INNER LEFT RIGHT FULL。
如果join方法的参数用数组的话，只能使用一次join方法，并且不能和字符串方式混合使用。 例如：

```php
join(array(' __WORK__ ON __ARTIST__.id = __WORK__.artist_id','__CARD__ ON __ARTIST__.card_id = __CARD__.id'))
```

使用数组方式的情况下，第二个参数无效。因此必须在字符串中显式定义join类型，例如：

```php
join(array(' LEFT JOIN __WORK__ ON __ARTIST__.id = __WORK__.artist_id','RIGHT JOIN __CARD__ ON __ARTIST__.card_id = __CARD__.id'))
```
