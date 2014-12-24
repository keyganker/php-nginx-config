表单提交（POST）有两种主要的content-type：`multipart/form-data`和`application/x-www-form-urlencoded`

当content-type为`multipart/form-data`的时候，可以通过`$_POST`取数据，并且该数据是被`addslashes()`转义过的，无论是否开启了`magic_quotes_gpc`（这一点可以通过代码证明，并没有其他相关资料），
这个时候的参数是不能通过php://input来获取的.[php://input文档](http://php.net/manual/en/wrappers.php.php)

当content-type是`x-www-urlencode`的时候，既可以通过`$_POST`也可以通过`php://input`来取数据(即二者都会被填充)，但是`php://input`中的数据没有被`addslashes()`转义过(使用`parse_str`将`php://input`解析为数组)，而`$_POST`是被转义过的

php://input本质上是读取的http body体（request payload），即raw data。

content-type为multipart/form-data的时候raw data格式如下：

    ------WebKitFormBoundaryjgHkzZeXLSSezfJ8
    Content-Disposition: form-data; name="title"

    你个'#'空间和''
    ------WebKitFormBoundaryjgHkzZeXLSSezfJ8
    Content-Disposition: form-data; name="dsa"

    11
    ------WebKitFormBoundaryjgHkzZeXLSSezfJ8--

    通过 **------WebKitFormBoundaryjgHkzZeXLSSezfJ8** 来做分割符，该分割符在content-type中指定：

    multipart/form-data; boundary=----WebKitFormBoundaryjgHkzZeXLSSezfJ8


content-type为`x-www-urlencode`的时候raw data格式如下：

    title=%E4%BD%A0%E4%B8%AA'%23&dsa=11

与GET请求中的参数格式一样，但是该参数是放在body中的。


提交表单默认content-type是 `x-www-urlencode`


参考资料: http://stackoverflow.com/questions/4007969/application-x-www-form-urlencoded-or-multipart-form-data (至少要读第一个和第三个答案)