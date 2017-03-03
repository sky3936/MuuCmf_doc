# Url生成

为了配合所使用的URL模式，我们需要能够动态的根据当前的URL设置生成对应的URL地址，为此，ThinkPHP内置提供了U方法，用于URL的动态生成，可以确保项目在移植过程中不受环境的影响。

## 定义规则
U方法的定义规则如下（方括号内参数根据实际应用决定）：

> ### U('地址表达式',['参数'],['伪静态后缀'],['显示域名'])

## 地址表达式
地址表达式的格式定义如下：

> [模块/控制器/操作#锚点@域名]?参数1=值1&参数2=值2...

如果不定义模块的话 就表示当前模块名称，下面是一些简单的例子：


```Php
U('User/add') // 生成User控制器的add操作的URL地址

U('Blog/read?id=1') // 生成Blog控制器的read操作 并且id为1的URL地址

U('Admin/User/select') // 生成Admin模块的User控制器的select操作的URL地址
```

## 参数
U方法的第二个参数支持数组和字符串两种定义方式，如果只是字符串方式的参数可以在第一个参数中定义，例如：

```Php
U('Blog/cate',array('cate_id'=>1,'status'=>1))

U('Blog/cate','cate_id=1&status=1')

U('Blog/cate?cate_id=1&status=1')
```

三种方式是等效的，都是生成Blog控制器的cate操作 并且cate_id为1 status为1的URL地址。
但是不允许使用下面的定义方式来传参数

```Php
U('Blog/cate/cate_id/1/status/1');
```

## 伪静态后缀
U函数会自动识别当前配置的伪静态后缀，如果你需要指定后缀生成URL地址的话，可以显式传入，例如：

```Php
U('Blog/cate','cate_id=1&status=1','xml');
```

## 自动识别
根据项目的不同URL设置，同样的U方法调用可以智能地对应产生不同的URL地址效果，例如针对：

```Php
U('Blog/read?id=1');
```

这个定义为例。

如果当前URL设置为普通模式的话，最后生成的URL地址是：

> http://serverName/index.php?m=Blog&a=read&id=1

如果当前URL设置为PATHINFO模式的话，同样的方法最后生成的URL地址是：

> http://serverName/index.php/Home/Blog/read/id/1

如果当前URL设置为REWRITE模式的话，同样的方法最后生成的URL地址是：

> http://serverName/Home/Blog/read/id/1

如果当前URL设置为REWRITE模式，并且设置了伪静态后缀为.html的话，同样的方法最后生成的URL地址是：

> http://serverName/Home/Blog/read/id/1.html

如果开启了URL_CASE_INSENSITIVE，则会统一生成小写的URL地址。

## 生成路由地址

U方法还可以支持路由，如果我们定义了一个路由规则为：

```Php
'news/:id\d'=>'News/read'
```

那么可以使用

```Php
U('/news/1');
```

最终生成的URL地址是：

> http://serverName/index.php/Home/news/1

注意：如果你是在模板文件中直接使用U方法的话，需要采用 {:U('参数1', '参数2'…)} 的方式，具体参考模板的使用函数内容。

## 域名支持

如果你的应用涉及到多个子域名的操作地址，那么也可以在U方法里面指定需要生成地址的域名，例如：

```Php
U('Blog/read@blog.thinkphp.cn','id=1');
```

@后面传入需要指定的域名即可。

系统会自动判断当前是否SSL协议，生成https://。

此外，U方法的第4个参数如果设置为true，表示自动识别当前的域名，并且会自动根据子域名部署设置APP_SUB_DOMAIN_DEPLOY和APP_SUB_DOMAIN_RULES自动匹配生成当前地址的子域名。

## 锚点支持

U函数可以直接生成URL地址中的锚点，例如：

```Php
U('Blog/read#comment?id=1');
```

生成的URL地址可能是：

> http://serverName/index.php/Home/Blog/read/id/1#comment