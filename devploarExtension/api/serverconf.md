## 操作配置文件


>配置文件通常存放着整个论坛十分重要的配置，包括论坛名称，论坛简洁，主题色，SMTP配置等等

### 得到某个值
``` python
forum.severconf_get(key="js")
```

得到配置文件的某个值,得到空字符串则返回整个配置文件

### 得到某个值，不存在则创建
``` python
forum.serverconf_get_key_or_create(key="dark", value="True")
```

得到配置文件的某个值,得到空字符串则返回整个配置文件,如果值不存在则创建.一般用于扩展需要在配置文件中保存独立配置数据

### 修改/创建
``` python
forum.serverconf_chang(key="js, value="console.log("hello")")
```

修改/创建配置文件的某个值

