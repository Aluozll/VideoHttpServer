# VideoHttpServer

在Windows平台上提供简单的视频web服务。

python实现视频资源页面，nginx实现视频流服务。

注：用python，是因为Windows平台上，nginx不支持中文路径，不支持中文路径，不支持中文路径。

## python

安装python，2.7或3.6以上，地址：https://www.python.org/downloads 。

代码是从python2 SimpleHTTPServer（python3 http.server）修改过来的，用于枚举目标目录下所有视频，并把视频的超链接指向nginx。


## nginx

下载nginx，最新版本，地址：https://nginx.org/en/download.html 。

配置nginx.conf（端口自定义）:
```
  # D:/Temp资源目录
  location /{
      #root   html;
      root D:/Temp;
      index  index.html index.htm;
      charset utf-8;
      autoindex on;
      #autoindex_exact_size on;
      #autoindex_localtime on;
  }
  
  # 反向代理到python http server
  location /home {
      proxy_pass   http://127.0.0.1:8089;
  }

```

注：Windows平台上的nginx的文件名是用utf-8编码的，因此，web页面中的超链接必须是utf-8编码，否则会出错。
