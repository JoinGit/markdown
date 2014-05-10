## 欢迎使用 MarkdownPad 2 ##

**MarkdownPad** 是 Windows 平台上一个功能完善的 Markdown 编辑器。
### 专为 Markdown 打造 ###

提供了语法高亮和方便的快捷键功能，给您最好的 Markdown 编写体验。
来试一下：

- **粗体** (`Ctrl+B`) and *斜体* (`Ctrl+I`)
- 引用 (`Ctrl+Q`)
- 代码块 (`Ctrl+K`)
- 标题 1, 2, 3 (`Ctrl+1`, `Ctrl+2`, `Ctrl+3`)
- 列表 (`Ctrl+U` and `Ctrl+Shift+O`)

### 实时预览，所见即所得 ###

无需猜测您的 [语法](http://markdownpad.com) 是否正确；每当您敲击键盘，实时预览功能都会立刻准确呈现出文档的显示效果。

### 自由定制 ###
 
100% 可自定义的字体、配色、布局和样式，让您可以将 MarkdownPad 配置的得心应手。

### 为高级用户而设计的稳定的 Markdown 编辑器 ###
 
 MarkdownPad 支持多种 Markdown 解析引擎，包括 标准 Markdown 、 Markdown 扩展 (包括表格支持) 以及 GitHub 风格 Markdown 。
 
 有了标签式多文档界面、PDF 导出、内置的图片上传工具、会话管理、拼写检查、自动保存、语法高亮以及内置的 CSS 管理器，您可以随心所欲地使用 MarkdownPad。


## MySQL Server Product

 * mysqld 是服务器进程
 * mysql 是客户端命令行工具

mysqld服务

    [root@localhost ~]# service mysqld start #启动服务
    [root@localhost ~]# service mysqld stop #关闭服务
    [root@localhost ~]# service mysqld restart #重启服务
    [root@localhost ~]# /etc/rc.d/init.d/mysqld --verbose #查看服务所支持的参数
    Usage: /etc/rc.d/init.d/mysqld {start|stop|status|condrestart|restart}
    [root@localhost ~]# netstat -tnlp #查看服务是否启动成功

mysql命令行所支持的参数

    [root@localhost ~]# mysql --verbose --help

mysql启动服务查找配置的顺序，并不是所有的版本都是一致，使用mysql --verbose --help可以找到当前版本查找的顺序

>- /etc/my.conf
>
>>     [mysqld]片段中添加以下配置
>>     default_storage_engine=InnoDB
>>     sql_mode=STRICT_ALL_TABLES
>
>- /etc/mysql/my.conf
>- $MYSQL\_HOME/my.conf $MYSQL_HOME环境变量设置的目录，如果没有设置，则找mysql数据目录，>即datadir=PATH
>- --default-extra-file=<PATH/FILE> 启动mysqld服务使用此参数
>- ~/.my.conf 用户家目录下




## MySQL Server Product

 * mysqld 是服务器进程
 * mysql 是客户端命令行工具

mysqld服务

    [root@localhost ~]# service mysqld start #启动服务
    [root@localhost ~]# service mysqld stop #关闭服务
    [root@localhost ~]# service mysqld restart #重启服务
    [root@localhost ~]# /etc/rc.d/init.d/mysqld --verbose #查看服务所支持的参数
    Usage: /etc/rc.d/init.d/mysqld {start|stop|status|condrestart|restart}
    [root@localhost ~]# netstat -tnlp #查看服务是否启动成功

mysql命令行所支持的参数

    [root@localhost ~]# mysql --verbose --help

mysql启动服务查找配置的顺序，并不是所有的版本都是一致，使用mysql --verbose --help可以找到当前版本查找的顺序

- **/etc/my.conf**
```
[mysqld]片段中添加以下配置
default_storage_engine=InnoDB
sql_mode=STRICT_ALL_TABLES
```
- /etc/mysql/my.conf
- $MYSQL\_HOME/my.conf `$MYSQL_HOME`环境变量设置的目录，如果没有设置，则找mysql数据目录，即`datadir=PATH`
- --default-extra-file=<PATH/FILE> 启动mysqld服务使用此参数
- ~/.my.conf 用户家目录下
