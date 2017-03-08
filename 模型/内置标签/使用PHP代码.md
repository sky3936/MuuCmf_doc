# 使用PHP代码

Php代码可以和标签在模板文件中混合使用，可以在模板文件里面书写任意的PHP语句代码 ，包括下面两种方式：

#### 使用php标签

例如：

```php
<php>echo 'Hello,world!';</php>
```

我们建议需要使用PHP代码的时候尽量采用php标签，因为原生的PHP语法可能会被配置禁用而导致解析错误。

#### 使用原生php代码

```php
<?php echo 'Hello,world!'; ?>
```

注意：php标签或者php代码里面就不能再使用标签（包括普通标签和XML标签）了，因此下面的几种方式都是无效的：

```php
<php><eq name='name'value='value'>value</eq></php>
```

Php标签里面使用了eq标签，因此无效

```php
<php>if( {$user} != 'ThinkPHP' ) echo  'ThinkPHP' ;</php>
```

Php标签里面使用了{$user}普通标签输出变量 ，因此无效。

```php
<php>if( $user.name != 'ThinkPHP' ) echo  'ThinkPHP' ;</php>
```

Php标签里面使用了$user.name 点语法变量输出 ，因此无效。

简而言之，在PHP标签里面不能再使用PHP本身不支持的代码。
如果设置了TMPL_DENY_PHP参数为true，就不能在模板中使用原生的PHP代码，但是仍然支持PHP标签输出。