# Mongo模型

Mongo模型是专门为Mongo数据库驱动而支持的Model扩展，如果需要操作Mongo数据库的话，自定义的模型类必须继承Think\Model\MongoModel。

Mongo模型为操作Mongo数据库提供了更方便的实用功能和查询用法，包括：

* 对MongoId对象和非对象主键的全面支持；
* 保持了动态追加字段的特性；
* 数字自增字段的支持；
* 执行SQL日志的支持；
* 字段自动检测的支持；
* 查询语言的支持；
* MongoCode执行的支持；

### 主键

系统很好的支持Mongo的主键类型，Mongo默认的主键名是 _id，也可以通过设置pk属性改变主键名称（也许你需要用其他字段作为数据表的主键），例如：

```php
namespace Home\Model;
use Think\Model\MongoModel;
Class UserModel extends MongoModel {
    Protected $pk = 'id';
}
```

主键支持三种类型（通过_idType属性设置），分别是：

|类型	|描述|
|----|-----|
|self::TYPE_OBJECT或者1|（默认类型） 采用MongoId对象，写入或者查询的时候传入数字或者字符会自动转换，获取的时候会自动转换成字符串。|
|self::TYPE_INT或者2|整形，支持自动增长，通过设置_autoInc 属性|
|self::TYPE_STRING或者3|字符串hash|


设置主键类型示例：

```php
namespace Home\Model;
use Think\Model\MongoModel;
Class UserModel extends MongoModel {
     Protected $_idType = self::TYPE_INT;
     protected $_autoinc =  true;
}
```

### 字段检测

MongoModel默认关闭字段检测，是为了保持Mongo的动态追加字段的特性，如果你的应用不需要使用Mongo动态追加字段的特性，可以设置autoCheckFields为true即可开启字段检测功能，提高安全性。一旦开启字段检测功能后，系统会自动查找当前数据表的第一条记录来获取字段列表。

如果你关闭字段检测功能的话，将不能使用查询的字段排除功能。

### 连贯操作

MongoModel中有部分连贯操作暂时不支持，包括：group、union、join、having、lock和distinct操作。其他连贯操作都可以很好的支持，例如：

```php
$Model = new Think\Model\MongoModel("User");
$Model->field("name,email,age")->order("status desc")->limit("10,8")->select();
```

### 查询支持

Mongo数据库的查询条件和其他数据库有所区别。

首先，支持所有的普通查询和快捷查询；
表达式查询增加了一些针对MongoDb的查询用法；
统计查询目前只能支持count操作，其他的可能要自己通过MongoCode来实现了；

### MongoModel的组合查询支持

_string 采用MongoCode查询
_query 和其他数据库的请求字符串查询相同
_complex MongoDb暂不支持
MongoModel提供了MongoCode方法，可以支持MongoCode方式的查询或者操作。

### 表达式查询

表达式查询采用下面的方式：

```php
$map['字段名'] = array('表达式','查询条件');
```

因为MongoDb的特性，MongoModel的表达式查询和其他的数据库有所区别，增加了一些新的用法。

表达式不分大小写，支持的查询表达式和Mongo原生的查询语法对照如下：

|查询表达式	|含义	|Mongo原生查询条件|
|----|-----|
|neq 或者ne|不等于	|$ne|
|lt|小于	|$lt|
|lte 或者elt|小于等于	|$lte|
|gt|大于	|$gt|
|gte 或者egt|大于等于	|$gte|
|like|模糊查询 用MongoRegex正则模拟	|无|
|mod|取模运算	|$mod|
|in	|in查询|$in|
|nin或者not in not|in查询	|$nin|
|all|满足所有条件	|$all|
|between|在某个的区间	|无|
|not between|不在某个区间	|无|
|exists|字段是否存在	|$exists|
|size|限制属性大小|	$size|
|type|限制字段类型	|$type|
|regex|MongoRegex正则查询|	MongoRegex实现|
|exp|使用MongoCode查询	|无|

注意，在使用like查询表达式的时候，和mysql的方式略有区别，对应关系如下：

|Mysql模糊查询	|Mongo模糊查询|
|----|----|
|array('like','%thinkphp%');|array('like','thinkphp');|
|array('like','thinkphp%');	|array('like','^thinkphp');|
|array('like','%thinkphp');	|array('like','thinkphp$');|


LIKE： 同sql的LIKE 例如：

```php
$map['name'] = array('like','^thinkphp');
```

查询条件就变成name like 'thinkphp%'

设置支持 Mongo的数据更新设置用于数据保存和写入操作，可以支持：


|表达式	|含义	|Mongo原生用法|
|----|-----|
|inc|数字字段增长或减少	|$inc|
|set|字段赋值	|$set|
|unset|删除字段值	|$unset|
|push|追加一个值到字段（必须是数组类型）里面去	|$push|
|pushall|追加多个值到字段（必须是数组类型）里面去	|$pushall|
|addtoset|增加一个值到字段（必须是数组类型）内，而且只有当这个值不在数组内才增加	|$addtoset|
|pop|根据索引删除字段（必须是数组字段）中的一个值	|$pop|
|pull|根据值删除字段（必须是数组字段）中的一个值	|$pull|
|pullall|一次删除字段（必须是数组字段）中的多个值	|$pullall|

例如:

```php
$data['id'] = 5;
$data['score'] = array('inc',2);
$Model->save($data);
```

### 其他

 MongoModel增加了几个方法

- mongoCode 执行MongoCode

- getMongoNextId ([字段名]) 获取自增字段的下一个ID，可用于数字主键或者其他需要自增的字段，参数为空的时候表示或者主键的。

- Clear 清空当前数据表方法

