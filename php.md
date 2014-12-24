php默认表单参数个数(不能改的太大，否则会有哈希攻击漏洞;攻击者可以通过恶意构造的表单参数key，导致$_POST或者$_GET数组退化成为链表)
- max_input_vars 1000;

Sets the magic_quotes state for GPC (Get/Post/Cookie) operations. When magic_quotes are on, all ' (single-quote), " (double quote), \ (backslash) and NUL's are escaped with a backslash automatically.
为表单输入添加转义符"\", 该功能是默认打开的, 使用get_magic_quotes_gpc()可以查看是否打开了; 5.4和5.4之后该功能被移除,永远返回0
- magic_quotes_gpc : on/off
