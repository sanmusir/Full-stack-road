```
fastcgi_param SCRIPT_FILENAME $document_root$fastcgi_script_name;#脚本文件请求的路径,也就是说当访问127.0.0.1/index.php的时候，需要读取网站根目录下面的index.php文件，如果没有配置这一配置项时，nginx不回去网站根目录下访问.php文件，所以返回空白
fastcgi_param QUERY_STRING $query_string;                        #请求的参数;如?app=123
fastcgi_param REQUEST_METHOD $request_method;                    #请求的动作(GET,POST)
fastcgi_param CONTENT_TYPE $content_type;                        #请求头中的Content-Type字段
fastcgi_param CONTENT_LENGTH $content_length;                    #请求头中的Content-length字段。

fastcgi_param SCRIPT_NAME $fastcgi_script_name;                  #脚本名称 
fastcgi_param REQUEST_URI $request_uri;                          #请求的地址不带参数
fastcgi_param DOCUMENT_URI $document_uri;                        #与$uri相同。 
fastcgi_param DOCUMENT_ROOT $document_root;                      #网站的根目录。在server配置中root指令中指定的值 
fastcgi_param SERVER_PROTOCOL $server_protocol;                  #请求使用的协议，通常是HTTP/1.0或HTTP/1.1。

fastcgi_param GATEWAY_INTERFACE CGI/1.1;                         #cgi 版本
fastcgi_param SERVER_SOFTWARE nginx/$nginx_version;              #nginx 版本号，可修改、隐藏

fastcgi_param REMOTE_ADDR $remote_addr;                          #客户端IP
fastcgi_param REMOTE_PORT $remote_port;                          #客户端端口
fastcgi_param SERVER_ADDR $server_addr;                          #服务器IP地址
fastcgi_param SERVER_PORT $server_port;                          #服务器端口
fastcgi_param SERVER_NAME $server_name;                          #服务器名，域名在server配置中指定的server_name

fastcgi_param PATH_INFO $path_info;                             #可自定义变量
```
