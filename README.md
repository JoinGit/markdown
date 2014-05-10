## MySQL Server Product

 * mysqld 是服务器进程
 * mysql 是客户端命令行工具

### 1. mysqld服务

    [root@localhost ~]# service mysqld start #启动服务
    [root@localhost ~]# service mysqld stop #关闭服务
    [root@localhost ~]# service mysqld restart #重启服务
    [root@localhost ~]# /etc/rc.d/init.d/mysqld --verbose #查看服务所支持的参数
    Usage: /etc/rc.d/init.d/mysqld {start|stop|status|condrestart|restart}
    [root@localhost ~]# netstat -tnlp #查看服务是否启动成功

mysql启动服务查找配置的顺序，并不是所有的版本都是一致，使用mysql --verbose --help可以找到当前版本查找的顺序

1. /etc/my.conf

   [mysqld]片段中添加以下配置
   default_storage_engine=InnoDB
   sql_mode=STRICT_ALL_TABLES

2. /etc/mysql/my.conf
3. $MYSQL\_HOME/my.conf `$MYSQL_HOME`环境变量设置的目录，如果没有设置，则找mysql数据目录，即`datadir=PATH`
4. --default-extra-file=<PATH/FILE> 启动mysqld服务使用此参数
5. ~/.my.conf 用户家目录下

插件式存储引擎(表类型，表级别)
  MyISAM
  CSV
  MEMORY
  MyISAMMRG
  InnoDB
    innodb_file_per_table=ON 每张表使用单独的表空间文件
  Federated
  Archive
  Blcakhole

### 2. mysql命令行

    [root@localhost ~]# mysql --verbose --help #显示mysql所支持的参数

mysql命令的工作模式

1. 交互式模式
```
mysql [options] db_name
  --user=user_name, -u user_name 默认为root
  --password[=password], -p[password] 默认为使用空密码登录。可以不输入密码直接进入交互模式下输入密码
  --host=host_name, -h host_name 默认是localhost
    -h localhost --> mysql.sock，基于进程间通信
    -h 127.0.0.1 --> 3306/tcp，基于TCP/IP协议通信
  --protocol={TCP|SOCKET|PIPE|MEMORY} 除了TCP协议，其余都是进程间通信，也就是说mysql和mysqld必须运行在同一台主机上
    SOCKET: Linux/Unix --> mysql.sock
    PIPE,MEMORY: Windows, IPC
  --port=port_num, -P port_num 连接服务器TCP/IP端口
  -e "COMMAND" 在shell命令执行mysql命令，并将结果返回到shell窗口里
    [root@localhost init.d]# mysql -e"show databases"
```
2. 批处理模式













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
