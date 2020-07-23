## 学习命令


### 安装

在github下载命令行工具(版本更新快)
``` bash
git clone https://github.com/stuoe/stuoe.git
cd stuoe
python setup.py install
```
或者使用pip下载(版本同步较慢)
``` bash
pip install -U stuoe
```

### 初始化项目
``` bash
stuoe startproject --name mysite
flask db init
```

### 更新项目版本
``` bash
pip install -U stuoe
flask db migrate
flask db update
```
### 运行
```
python app.py
```
