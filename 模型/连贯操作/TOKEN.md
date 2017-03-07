# TOKEN

token方法可用于临时关闭令牌验证，例如：

```php
$model->token(false)->create();
```

即可在提交表单的时候临时关闭令牌验证（即使开启了TOKEN_ON参数）。
