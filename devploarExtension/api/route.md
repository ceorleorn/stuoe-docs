## 路由与上下文

>路由便是URL,定义请求方式，响应函数，获取上下文信息

### 获取app再同步

``` python
app = forum.app_get_app

@app.route("/atgoodtemplates")
def atgoodtemplates():
    return "atgoodtemplates"

forum.app_replace__app(app)
```

这种方法很好，可以直接添加原本的代码

### 直接修改forum.app

``` python
@forum.app("/atgoodtemplates")
def atgoodtemplates():
    return "atgoodtemplates"
```

### 使用上下文

在扩展代码中使用上下文与在Flask应用中一模一样，因为这再熟悉不过了

``` python
@forum.app("/giveform",methods=["POST"])
def giveform():
    return request.form["amwsome"]
```
*一个最简单的表单路由*

### 使用Session

Session也属于上下文，可以直接调用，但在标准的请求中，Stuoe通常不会直接使用Session

``` python
@forum.app("/clearmysession")
def clearmysession():
    session.clear()
    return "You Session is cleared"
```

[Flask官方上下文文档](https://flask.palletsprojects.com/en/1.1.x/quickstart/#sessions)

