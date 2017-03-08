# IF标签

用法示例：

```php
<if condition="($name eq 1) OR ($name gt 100) "> value1
<elseif condition="$name eq 2"/>value2
<else /> value3
</if>
```

在condition属性中可以支持eq等判断表达式，同上面的比较标签，但是不支持带有”>”、”<”等符号的用法，因为会混淆模板解析，所以下面的用法是错误的：

```php
<if condition="$id < 5 ">value1
    <else /> value2
</if>
```

必须改成：

```php
<if condition="$id lt 5 ">value1
<else /> value2
</if>
```

除此之外，我们可以在condition属性里面使用php代码，例如：

```php
<if condition="strtoupper($user['name']) neq 'THINKPHP'">ThinkPHP
<else /> other Framework
</if>
```

condition属性可以支持点语法和对象语法，例如： 自动判断user变量是数组还是对象

```php
<if condition="$user.name neq 'ThinkPHP'">ThinkPHP
<else /> other Framework
</if>
```

或者知道user变量是对象

```php
<if condition="$user:name neq 'ThinkPHP'">ThinkPHP
<else /> other Framework
</if>
```

由于if标签的condition属性里面基本上使用的是php语法，尽可能使用判断标签和Switch标签会更加简洁，原则上来说，能够用switch和比较标签解决的尽量不用if标签完成。因为switch和比较标签可以使用变量调节器和系统变量。如果某些特殊的要求下面，IF标签仍然无法满足要求的话，可以使用原生php代码或者PHP标签来直接书写代码。