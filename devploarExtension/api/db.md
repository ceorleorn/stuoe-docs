## 操作数据库

>数据库存放着论坛的各种数据。用户，帖子，标签等等.


### 得到Sqlalchemy对象
``` python
forum.database_get_db()
```

得到整个db对象，则是flask-sqlalchemy的Sqlalchemy对象.用于创建表等等重要业务

### 替换Sqlalchemy对象
``` python
forum.database_replace_database(db=db)
```

用修改后的db对象替换掉之前的db对象，如注册了新的表，更改了session等

### 获取注册的表的immutabledict格式
``` python
forum.database_get_all_table_immutabledict()
```

获得当前db对象中所有注册的表的immutabledict格式,immutabledict是整个数据库中所有表的表结构

### 获取表

``` python
forum.database_get_table(table="Tags")
```
获取数据库表，并非从db中获取绑定，而是从forum.databaseTable中获取.不存在则为None,返回为数据库对象，可以直接进行Query,Create等业务


### 业务示例
``` python
Tags = forum.database_get_table("Tags")
for i in Tags.query.filter_by().all():
    print(i.name)
```
这个示例教会你如何使用database_get_table_or_all()来获取表，以来进行业务

### 添加新的模型
``` python
Tags = forum.database_get_table("Tags")
newTags = Tags(name="Tags",lock=False,icon="tags")
forum.database_add_to_session(newTags)
```
将模型添加到forum.db.session,相比直接在本地使用db.session.add()，减少了同步的麻烦。

### 删除模型
``` python
forum.database_delete_to_session(newTags)
```
将模型直接从forum.db.session删除,相比直接在本地使用db.session.delete()，减少了同步的麻烦。

### 添加新的模型并保存
``` python
Tags = forum.database_get_table("Tags")
newTags = Tags(name="Tags",lock=False,icon="tags")
forum.database_add_to_session_and_commit(newTags)
```
将模型添加到forum.db.session,相比直接在本地使用db.session.add()，减少了同步的麻烦.并直接进行flush+commit保存

### 删除模型并保存
``` python
forum.database_delete_to_session(newTags)
```
将模型直接从forum.db.session删除,相比直接在本地使用db.session.delete()，减少了同步的麻烦.并直接进行flush+commit保存

### 直接提交
``` python
forum.database_commit()
```
直接提交，调用db.session.flush()+db.session.commit()