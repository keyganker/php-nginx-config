 - request_terminate_timeout
 	- Default Value: 0  
 	- 在fpm模式下max_execution_time会不起作用,可以设置该参数确保最大执行时间  
The timeout for serving a single request after which the worker process will
be killed. This option should be used when the 'max_execution_time' ini option
does not stop script execution for some reason. A value of '0' means 'off'.
Available units: s(econds)(default), m(inutes), h(ours), or d(ays)
- 如果php-fpm worker超时（在request_terminate_timeout指定时间内没有返回），则会导致nginx 502错误，并且超时的php-fpm worker会退出，然后fpm重新起一个worker



