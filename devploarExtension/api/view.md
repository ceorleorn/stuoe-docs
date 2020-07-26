## 界面

>发送一个和stuoe一样的模板界面，配合数据库检查用户等

### 生成模板界面

``` python
@forum.app("sometextgiveyou")
def sometextgiveyou():
    return forum.view_templates(auth=False,userObj='',body="<h1>Hello</h1>",title="Hello Messages")
```

auth指的是登入状态，True为登入，False为访客。userObj则是登入状态为True时传入的用户数据库模型.如果状态为False,那么userObj则传None.auth+userObj用于渲染导航栏和用户栏.body则为实际的HTML正文,title则为界面标题，尾部会自动添加论坛标题

>MDUI已经自动添加到模板中，可以直接传入使用MDUI的HTML,[MDUI文档](https://mdui.org)

### 检查用户

扩展通常会有一些界面只允许登入用户访问，或者需要获取用户的信息

``` python
@forum.app.route("/getyournickname")
def getyournickname():
    user = forum.view_check_user(type='nickname')
    if user == False:
        return "你没有登入"
    return "你的昵称是:" + user
    
```
forum.view_check_user接受一个字符串参数，分别是nickname，id，obj，对应昵称，用户id，用户模型对象.如果用户未登入，则返回False,该函数只能在Flask上下文中调用

### 检查用户配合模板

``` python
@forum.app.route("/hello")
def hello():
    if forum.view_check_user('obj') == False:
        return forum.view_templates(auth=False,userObj='',body="<h1>Hello</h1>",title="Hello Messages")
    else:
        return forum.view_templates(auth=True,userObj=forum.view_check_user('obj'),body="<h1>Hello</h1>",title="Hello Messages")

```

一个标准的stuoe界面,无论是登入还是未登入

### 增添首页侧栏

``` python
forum.view_sidebar_add(name="test",url="/test",icon="ac_unit")
```
在首页侧栏上添加新的栏,name为名称，url为连接，icon为[Material Icon](https://www.mdui.org/docs/material_icon#mdui-dialog)