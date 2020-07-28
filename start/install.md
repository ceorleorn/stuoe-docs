## 安装


##### 你需要一个安装了[Python3.8+](https://python.org/) , [nginx1.16.1](https://www.nginx.com/)的服务器

从[pypi](https://pypi.org/project/stuoe)安装（强烈不推荐）
``` bash
pip install -U stuoe
```
或者从[Github](https://github.com/)安装（实时细微版本同步）
``` bash
git clone https://github.com/stuoe/stuoe.git
cd stuoe
python setup.py install
```
新建项目
``` bash
stuoe startproject --name mysite
cd mysite
```
初始化数据库
``` bash
flask db init
flask db migrate
flask db update
```
运行在5000端口
``` bash
python app.py
```
打开[127.0.0.1:5000/install](127.0.0.1:5000/install)配置论坛信息，填写论坛名称，配置smtp邮箱，设置管理员用户等

