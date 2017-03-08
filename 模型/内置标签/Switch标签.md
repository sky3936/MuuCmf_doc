# Switch标签

用法：

```php
<switch name="变量" >
<case value="值1" break="0或1">输出内容1</case>
<case value="值2">输出内容2</case>
<default />默认情况
</switch>
```

使用方法如下：

```php
<switch name="User.level">
    <case value="1">value1</case>
    <case value="2">value2</case>
    <default />default
</switch>
```

其中name属性可以使用函数以及系统变量，例如：

```php
<switch name="Think.get.userId|abs">
    <case value="1">admin</case>
    <default />default
</switch>
```

对于case的value属性可以支持多个条件的判断，使用”|”进行分割，例如：

```php
<switch name="Think.get.type">
    <case value="gif|png|jpg">图像格式</case>
    <default />其他格式
</switch>
```

表示如果$_GET["type"] 是gif、png或者jpg的话，就判断为图像格式。

Case标签还有一个break属性，表示是否需要break，默认是会自动添加break，如果不要break，可以使用：

```php
<switch name="Think.get.userId|abs">
    <case value="1" break="0">admin</case>
    <case value="2">admin</case>
    <default />default
</switch>
```

也可以对case的value属性使用变量，例如：

```php
<switch name="User.userId">
    <case value="$adminId">admin</case>
    <case value="$memberId">member</case>
    <default />default
</switch>
```

使用变量方式的情况下，不再支持多个条件的同时判断。