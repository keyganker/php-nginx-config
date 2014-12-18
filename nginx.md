# fastcgi 和 nginx 通信时的buffer(如果太小会导致upstream sent too big header while reading response header from upstream)
- fastcgi_buffers 4 32k; 
- fastcgi_buffer_size 32k;
- fastcgi_busy_buffers_size 64k;


