# URL大小写

系统默认的规范是根据URL里面的模块名、控制器名来定位到具体的控制器类的，从而执行控制器类的操作方法。

以URL访问 http://serverName/index.php/Home/Index/index 为例，其实访问的控制器类文件是：

Application/Home/Controller/IndexController.class.php 
如果是Windows环境，无论大小写如何都能定位到IndexController.class.php文件，所以下面的访问都是有效的：

>http://serverName/index.php/Home/Index/index
>http://serverName/index.php/Home/index/index
>http://serverName/index.php/home/index/index

如果在Linux环境下面，一旦大小写不一致，就会发生URL里面使用小写模块名不能找到模块类的情况。例如在Linux环境下面，我们访问 http://serverName/index.php/home/index/index 其实请求的控制器文件是

>Application/home/Controller/indexController.class.php

因为，我们定义的控制器类是IndexController而不是indexController（参考ThinkPHP的命名规范），由于Linux的文件特性，其实是不存在indexController控制器文件的，就会出现Index控制器不存在的错误，这样的问题会造成用户体验的下降。

但是系统本身提供了一个不区分URL大小写的解决方案，可以通过配置简单实现。

只要在项目配置中，增加：

```Php
'URL_CASE_INSENSITIVE' =>true
```

配置好后，即使是在Linux环境下面，也可以实现URL访问不再区分大小写了。


>http://serverName/index.php/Home/Index/index
>// 将等效于
>http://serverName/index.php/home/index/index

这里需要注意一个地方，一旦开启了不区分URL大小写后，如果我们要访问类似UserTypeController的控制器，那么正确的URL访问应该是：


>// 正确的访问地址
>http://serverName/index.php/home/user_type/index
>// 错误的访问地址（linux环境下）
>http://serverName/index.php/home/usertype/index

利用系统提供的U方法（后面一章URL生成会告诉你如何生成）可以为你自动生成相关的URL地址。

如果设置

```Php
'URL_CASE_INSENSITIVE' =>false
```

的话，URL就又变成： http://serverName/index.php/Home/UserType/add

注意：URL不区分大小写并不会改变系统的命名规范，并且只有按照系统的命名规范后才能正确的实现URL不区分大小写。