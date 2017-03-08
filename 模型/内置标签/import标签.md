# import标签

传统方式的导入外部JS和CSS文件的方法是直接在模板文件使用：

```php
<script type='text/javascript' src='/Public/Js/Util/Array.js'>
<link rel="stylesheet" type="text/css" href="/App/Tpl/default/Public/css/style.css" />
```

系统提供了专门的标签来简化上面的导入：

第一个是import标签 ，导入方式采用类似ThinkPHP的import函数的命名空间方式，例如：

```php
<import type='js' file="Js.Util.Array" />
```

Type属性默认是js， 所以下面的效果是相同的：

```php
<import file="Js.Util.Array" />
```

还可以支持多个文件批量导入，例如：

```php
<import file="Js.Util.Array,Js.Util.Date" />
```

导入外部CSS文件必须指定type属性的值，例如：

```php
<import type='css' file="Css.common" />
```

上面的方式默认的import的起始路径是网站的Public目录，如果需要指定其他的目录，可以使用basepath属性，例如：

```php
<import file="Js.Util.Array"  basepath="./Common" />
```

第二个是load标签，通过文件方式导入当前项目的公共JS或者CSS

```php
<load href="/Public/Js/Common.js" />
<load href="/Public/Css/common.css" />
```

在href属性中可以使用特殊模板标签替换，例如：

```php
<load href="__PUBLIC__/Js/Common.js" />
```

Load标签可以无需指定type属性，系统会自动根据后缀自动判断。
系统还提供了两个标签别名js和css 用法和load一致，例如：

```php
<js href="/Public/Js/Common.js" />
<css href="/Public/Css/common.css" />
```