
上面的说明只做演示，如果你想在生产中使用，请阅读该部分（预览版不推荐）


实例使用Nginx转发Flask服务，一般来讲应该用[Gunicorn](https:/gunicorn.org/)等HTTP服务器来充当Nginx与Flask服务的中间人，这里为了方便演示，就不使用HTTP服务器

#### 运行Flask服务

``` bash
cd mysite
python app.py
```

#### 配置Nginx服务
``` conf
server {    
            listen 80;
            server_name localhost;
            

            location / {
                    proxy_pass http://127.0.0.1:5000/;
            }
}
```
