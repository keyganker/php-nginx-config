## fastcgi 和 nginx 通信时的buffer(如果太小会导致upstream sent too big header while reading response header from upstream)
- fastcgi_buffers 4 32k; 
- fastcgi_buffer_size 32k;
- fastcgi_busy_buffers_size 64k;

## php-fpm + nginx模式下，如果请求超过了request_terminate_timeout设置的超时时间，则会报错502，fpm日志中会出现类似"execution timed out (3.377985 sec), terminating"的错误，nginx会报错 "recv() failed (104: Connection reset by peer) while reading response header from upstream"；当把request_terminate_timeout设置变大之后，还是有可能出现错误，这个时候如果错误是504，并且nginx中有错误日志"upstream timed out (110: Connection timed out) while reading response header from upstream"，而fpm日志中没有错误，则可能是fastcgi_read_timeout过小导致的;如果nginx是作为proxy来使用的，则可能是proxy_read_timeout过小导致的
- fastcgi_read_timeout 指nginx进程从fastcgi读取response的整个过程的超时时间
- fastcgi_send_timeout 是指nginx进程向fastcgi进程发送request的整个过程的超时时间
- 通常这两个参数和上面提到的proxy_read_timeout的值默认都足够大，不需要修改
