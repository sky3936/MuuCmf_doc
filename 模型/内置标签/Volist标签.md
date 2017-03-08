# Volist标签

volist标签通常用于查询数据集（select方法）的结果输出，通常模型的select方法返回的结果是一个二维数组，可以直接使用volist标签进行输出。 在控制器中首先对模版赋值：

```php
$User = M('User');
$list = $User->limit(10)->select();
$this->assign('list',$list);
```

在模版定义如下，循环输出用户的编号和姓名：

```php
<volist name="list" id="vo">
{$vo.id}:{$vo.name}<br/>
</volist>
```

Volist标签的name属性表示模板赋值的变量名称，因此不可随意在模板文件中改变。id表示当前的循环变量，可以随意指定，但确保不要和name属性冲突，例如：

```php
<volist name="list" id="data">
{$data.id}:{$data.name}<br/>
</volist>
```

支持输出查询结果中的部分数据，例如输出其中的第5～15条记录

```php
<volist name="list" id="vo" offset="5" length='10'>
{$vo.name}
</volist>
```

输出偶数记录

```php
<volist name="list" id="vo" mod="2" >
<eq name="mod" value="1">{$vo.name}</eq>
</volist>
```

Mod属性还用于控制一定记录的换行，例如：

```php
<volist name="list" id="vo" mod="5" >
{$vo.name}
<eq name="mod" value="4"><br/></eq>
</volist>
```

为空的时候输出提示：

```php
<volist name="list" id="vo" empty="暂时没有数据" >
{$vo.id}|{$vo.name}
</volist>
```

empty属性不支持直接传入html语法，但可以支持变量输出，例如：

```php
$this->assign('empty','<span class="empty">没有数据</span>');
$this->assign('list',$list);
```

然后在模板中使用：

```php
<volist name="list" id="vo" empty="$empty" >
{$vo.id}|{$vo.name}
</volist>
```

输出循环变量

```php
<volist name="list" id="vo" key="k" >
{$k}.{$vo.name}
</volist>
```

如果没有指定key属性的话，默认使用循环变量i，例如：

```php
<volist name="list" id="vo"  >
{$i}.{$vo.name}
</volist>
```

如果要输出数组的索引，可以直接使用key变量，和循环变量不同的是，这个key是由数据本身决定，而不是循环控制的，例如：

```php
<volist name="list" id="vo"  >
{$key}.{$vo.name}
</volist>
```

模板中可以直接使用函数设定数据集，而不需要在控制器中给模板变量赋值传入数据集变量，如：

```php
<volist name=":fun('arg')" id="vo">
{$vo.name}
</volist>
```
