   
# IDEA配置   
   
>####	导入配置   
```shell
File => Mange IDEA Settings => Import Settings
```

>####	 IDEA 插件
```shell
GenerateSerialVersionUID_plugin_V3.0.3   
MybatisCodeHelper   
Alibaba Java Coding Guidelines   
generate all setter   
Translation   
vue   
JRebel   
pojo to json   
```

>####	通用快捷键   
   
`快捷键基于 eclipse`<br>
   
|  按键   | 操作  |
|  ----  | ----  |
|<kbd>ctrl</kbd> + <kbd>y</kbd>				    |撤销回滚|
|<kbd>ctrl</kbd> + <kbd>d</kbd>				    |删除行|
|<kbd>ctrl</kbd> + <kbd>f</kbd>				    |查找|
|<kbd>alt</kbd> + <kbd>up</kbd> / <kbd>dn</kbd>			    |内容向 上/下 移动|
|<kbd>ctrl</kbd> + <kbd>alt</kbd> + <kbd>dn</kbd>			    |内容向下复制|
|<kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>r</kbd> / <kbd>l</kbd>		    |左/右 选中单词|
|<kbd>ctel</kbd> + <kbd>r</kbd> / <kbd>l</kbd>			    |左/右 跳过单词|
|<kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>y</kbd>		    |大小写转换||
>####	idea 快捷键   
   
|   按键  |   操作 |
| ---- | ---- |
|<kbd>ctrl</kbd> + <kbd>h</kbd> 				    |全局查找|
|<kbd>ctrl</kbd> + <kbd>o</kbd> 				    |选择可重写的方法|
|<kbd>shift</kbd>+ <kbd>alt</kbd> + <kbd>u</kbd>			    |下划线转驼峰转大写   |插件CamelCase|
|<kbd>alt</kbd> + <kbd>r</kbd> / <kbd>l</kbd>			    	|上/下 个光标位置|
|<kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>alt</kbd> + <kbd>up</kbd> / <kbd>dn</kbd>    |上/下 编辑位置|
|<kbd>shift</kbd> + <kbd>alt</kbd> + <kbd>s</kbd>			    |自动代码|
|<kbd>ctrl</kbd> + <kbd>alt</kbd> + <kbd>t</kbd>			    |抽取代码块|
|<kbd>ctrl</kbd> + <kbd>alt</kbd> + <kbd>v</kbd>			    |抽取为变量  .var|
|<kbd>ctrl</kbd> + <kbd>+</kbd> / <kbd>-</kbd> 		    	|代码收缩|
|<kbd>ctrl</kbd> + <kbd>alt</kbd> + <kbd>l</kbd>              |js代码格式化|
|<kbd>ctrl</kbd> + <kbd>shift</kbd> + <kbd>x</kbd>              |在文件管理器中打开|

# Node 安装环境(Windows)   

>#### 第一步:安装 nodeJs   
```shell
http://nodejs.cn/download/
```
>#### 第二步:安装 cnpm 和淘宝源   
```shell
npm install -g cnpm --registry=https://registry.npm.taobao.org
``` 
```shell 
npm config set registry https://registry.npm.taobao.org
```   
>#### 第三步:安装vue-cli
```shell
npm install -g @vue/cli
# 卸载包
npm install cropperjs -S
npm uninstall cropperjs -S
```
>#### 第四步:检查
```shell
vue --version
```

# Node 卸载环境
>#### 第一步

```shell
npm cache clean --force
```

>#### 第二步

```shell
选择腾讯管家或其自身的卸载工具，卸载 node
```

>#### 第三步

```shell
#找到类似下面文件夹，手动进行删除。如果不存在就不管它
C:\Program Files\nodejs
C:\Users\你的用户名\AppData\Roaming\npm
C:\Users\你的用户名\AppData\Roaming\npm-cache
C:\Users\你的用户名\.npmrc
C:\Users\你的用户名\AppData\Local\Temp\npm-*
```

>#### 第四步

```shell
删除掉 node 相关环境变量
删除环境变量 PATH 中 node 值
```

