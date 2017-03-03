#AJAX返回

ThinkPHP可以很好的支持AJAX请求，系统的\Think\Controller类提供了ajaxReturn方法用于AJAX调用后返回数据给客户端。并且支持JSON、JSONP、XML和EVAL四种方式给客户端接受数据，并且支持配置其他方式的数据格式返回。

ajaxReturn方法调用示例：

```Php
$data = 'ok';
$this->ajaxReturn($data);
```

支持返回数组数据：

```Php
$data['status']  = 1;
$data['content'] = 'content';
$this->ajaxReturn($data);
```

默认配置采用JSON格式返回数据（通过配置DEFAULT_AJAX_RETURN进行设置），我们可以指定格式返回，例如：

```Php
// 指定XML格式返回数据
$data['status']  = 1;
$data['content'] = 'content';
$this->ajaxReturn($data,'xml');
```

返回数据data可以支持字符串、数字和数组、对象，返回客户端的时候根据不同的返回格式进行编码后传输。如果是JSON/JSONP格式，会自动编码成JSON字符串，如果是XML方式，会自动编码成XML字符串，如果是EVAL方式的话，只会输出字符串data数据。
JSON和JSONP虽然只有一个字母的差别，但其实他们根本不是一回事儿：JSON是一种数据交换格式，而JSONP是一种非官方跨域数据交互协议。一个是描述信息的格式，一个是信息传递的约定方法。

默认的JSONP格式返回的处理方法是jsonpReturn，如果你采用不同的方法，可以设置：

```Php
'DEFAULT_JSONP_HANDLER' =>  'myJsonpReturn', // 默认JSONP格式返回的处理方法
```

或者直接在页面中用callback参数来指定。

除了上面四种返回类型外，我们还可以通过行为扩展来增加其他类型的支持，只需要对ajax_return标签位进行行为绑定即可。

