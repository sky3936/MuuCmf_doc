# Action参数绑定

Action参数绑定是通过直接绑定URL地址中的变量作为操作方法的参数，可以简化方法的定义甚至路由的解析。

Action参数绑定功能默认是开启的，其原理是把URL中的参数（不包括模块、控制器和操作名）和操作方法中的参数进行绑定。

要启用参数绑定功能，首先确保你开启了URL_PARAMS_BIND设置：

```Php
'URL_PARAMS_BIND'       =>  true, // URL变量绑定到操作方法作为参数
```

参数绑定有两种方式：按照变量名绑定和按照变量顺序绑定。

按变量名绑定

默认的参数绑定方式是按照变量名进行绑定，例如，我们给Blog控制器定义了两个操作方法read和archive方法，由于read操作需要指定一个id参数，archive方法需要指定年份（year）和月份（month）两个参数，那么我们可以如下定义：

```Php
namespace Home\Controller;
use Think\Controller;
class BlogController extends Controller{
    public function read($id){
        echo 'id='.$id;
    }

    public function archive($year='2013',$month='01'){
        echo 'year='.$year.'&month='.$month;
    }
}
```

注意这里的操作方法并没有具体的业务逻辑，只是简单的示范。
URL的访问地址分别是：


>http://serverName/index.php/Home/Blog/read/id/5
>http://serverName/index.php/Home/Blog/archive/year/2013/month/11

两个URL地址中的id参数和year和month参数会自动和read操作方法以及archive操作方法的同名参数绑定。

变量名绑定不一定由访问URL决定，路由地址也能起到相同的作用
输出的结果依次是：

```Php
id=5
year=2013&month=11
```

按照变量名进行参数绑定的参数必须和URL中传入的变量名称一致，但是参数顺序不需要一致。也就是说


>http://serverName/index.php/Home/Blog/archive/month/11/year/2013


和上面的访问结果是一致的，URL中的参数顺序和操作方法中的参数顺序都可以随意调整，关键是确保参数名称一致即可。

如果使用下面的URL地址进行访问，参数绑定仍然有效：

>http://serverName/index.php?s=/Home/Blog/read/id/5
>http://serverName/index.php?s=/Home/Blog/archive/year/2013/month/11
>http://serverName/index.php?c=Blog&a=read&id=5
>http://serverName/index.php?c=Blog&a=archive&year=2013&month=11

如果用户访问的URL地址是（至于为什么会这么访问暂且不提）：

>http://serverName/index.php/Home/Blog/read/

那么会抛出下面的异常提示： 参数错误:id

报错的原因很简单，因为在执行read操作方法的时候，id参数是必须传入参数的，但是方法无法从URL地址中获取正确的id参数信息。由于我们不能相信用户的任何输入，因此建议你给read方法的id参数添加默认值，例如：

```Php
    public function read($id=0){
        echo 'id='.$id;
    }
```

这样，当我们访问 http://serverName/index.php/Home/Blog/read/ 的时候 就会输出

```Php
id=0
```

当我们访问 http://serverName/index.php/Home/Blog/archive/ 的时候，输出：

```Php
year=2013&month=01
```

始终给操作方法的参数定义默认值是一个避免报错的好办法
按变量顺序绑定

第二种方式是按照变量的顺序绑定，这种情况下URL地址中的参数顺序非常重要，不能随意调整。要按照变量顺序进行绑定，必须先设置URL_PARAMS_BIND_TYPE为1：

```Php
'URL_PARAMS_BIND_TYPE'  =>  1, // 设置参数绑定按照变量顺序绑定
```

操作方法的定义不需要改变，URL的访问地址分别改成：


>http://serverName/index.php/Home/Blog/read/5
>http://serverName/index.php/Home/Blog/archive/2013/11

输出的结果依次是：

```Php
id=5
year=2013&month=11
```Php

这个时候如果改成

>http://serverName/index.php/Home/Blog/archive/11/2013

输出的结果就变成了：

```Php
year=11&month=2013
```Php
显然就有问题了，所以不能随意调整参数在URL中的传递顺序，要确保和你的操作方法定义顺序一致。

可以看到，这种参数绑定的效果有点类似于简单的规则路由。
按变量顺序绑定的方式目前仅对PATHINFO地址有效，所以下面的URL访问参数绑定会失效：


>http://serverName/index.php?c=Blog&a=read&id=5
>http://serverName/index.php?c=Blog&a=archive&year=2013&month=11

但是，兼容模式URL地址访问依然有效：

>http://serverName/index.php?s=/Home/Blog/read/5
>http://serverName/index.php?s=/Home/Blog/archive/2013/11

如果你的操作方法定义都不带任何参数或者不希望使用该功能的话，可以关闭参数绑定功能：

```Php
'URL_PARAMS_BIND'       =>  false
```