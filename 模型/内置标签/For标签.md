# For标签


用法：

```php
<for start="开始值" end="结束值" comparison="" step="步进值" name="循环变量名" >
</for>
```

开始值、结束值、步进值和循环变量都可以支持变量，开始值和结束值是必须，其他是可选。comparison 的默认值是lt；name的默认值是i，步进值的默认值是1，举例如下：

```php
<for start="1" end="100">
{$i}
</for>
```

解析后的代码是

```php
for ($i=1;$i<100;$i+=1){
    echo $i;
} 
```
