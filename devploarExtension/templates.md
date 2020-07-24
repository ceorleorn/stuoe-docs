## 一个完整的示例

在extension文件夹中创建example文件夹，example作为扩展名称，里面固定有一个main.py文件
``` bash
├─extension
│ --snip--
│
│  └─example
│    └─main.py   
│      
├─migrations
│  --snip--
│
├─public
│  --snip--
│ 
├─storage
│  --snip
└─__pycache__
```


*这个目录是使用stuoe startproject创建的目录*




*main.py*

``` python
# Example - 示例插件

from flask import *
import os

# 插件头，标明插件的标题，图标，描述，README，
# 版本，作者等等信息


header = {
    "name": "example",
    "icon": "extension",
    "describe": "这个插件是为了方便介绍做如何制作插件的演示而制作的",
    "use": "some text",
    "author": "The Stuoe Project",
    "version": "0.0.1"
}


class Main():
    # 获取Flask对象和SQLAlchemy对象
    def __init__(self, forum):
        self.forum = forum
    # 绑定这些路由,然后再将新的Flask对象归还

    def init(self,forum):
        return self.forum


```

运行

``` bash
python app.py
```

输出

``` bash
=============================
导入模块: example
=============================

 * Serving Flask app "app" (lazy loading)
 * Environment: production
   WARNING: This is a development server. Do not use it in a production deployment.
   Use a production WSGI server instead.
 * Debug mode: off
 * Running on http://0.0.0.0:5000/ (Press CTRL+C to quit)

```

### 修改标识信息

标识header是一个字典

``` python
header = {
    "name": "example",
    "icon": "extension",
    "describe": "这个插件是为了方便介绍做如何制作插件的演示而制作的",
    "use": "some text",
    "author": "The Stuoe Project",
    "version": "0.0.1"
}
```


* name 插件名称,尽量用英文
* icon [Material Icon](https://www.mdui.org/docs/material_icon)
* describe 简短的描述
* use 介绍，例如README.md
* author 作者名字
* version 版本


 
### 添加路由

这已经是一个标准的扩展，但并未有任何作用。在加载扩展时，Forum对象的所有权归于扩展,只要及时归还，就可以做任何可以做的更改.让我们尝试添加路由


``` python
def init(self,forum):
    app = forum.app_get_app()

    @app.route("/SNBCK_is_a_boy")
    def snbck_is_a_boy():
        return "Yes, that's right 😎"

    @app.route("/Is_SNBCK_a_boy/<boll>")
    def is_snbck_a_boy(boll):
        if boll == "yes":
            return "Yes, that's right 😎"
        else:
            return "Your answer is too bad 😒"

    forum.app_replace_app(app)
    return self.forum
```



>通过app_get_app()来获取Flaskapp对象，添加route，然后调用app_replace_app()来更新最新的更改



>恭喜你，学会了如何制作一个最简单了插件。你可以阅读[函数库](/devploarExtension/api/serverconf)来使用函数读取/创建/修改论坛的配置文件，更改论坛界面的控件，将新增的路由使用模板界面发送等等

