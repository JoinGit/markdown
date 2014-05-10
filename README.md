## MySQL Server Product

 - mysqld 是服务器进程
 - mysql 是客户端命令行工具

### 1. mysqld服务

    [root@localhost ~]# service mysqld start #启动服务
    [root@localhost ~]# service mysqld stop #关闭服务
    [root@localhost ~]# service mysqld restart #重启服务
    [root@localhost ~]# /etc/rc.d/init.d/mysqld --verbose #查看服务所支持的参数
    Usage: /etc/rc.d/init.d/mysqld {start|stop|status|condrestart|restart}
    [root@localhost ~]# netstat -tnlp #查看服务是否启动成功

**mysql启动服务查找配置的顺序，并不是所有的版本都是一致，使用mysql --verbose --help可以找到当前版本查找的顺序**

1. /etc/my.conf
<pre>
[mysqld]片段中添加以下配置
default_storage_engine=InnoDB
sql_mode=STRICT_ALL_TABLES
</pre>
2. /etc/mysql/my.conf
3. $MYSQL\_HOME/my.conf `$MYSQL_HOME`环境变量设置的目录，如果没有设置，则找mysql数据目录，即`datadir=PATH`
4. --default-extra-file=<PATH/FILE> 启动mysqld服务使用此参数
5. ~/.my.conf 用户家目录下

**插件式存储引擎(表类型，表级别)**
  - MyISAM
  - CSV
  - MEMORY
  - MyISAMMRG
  - InnoDB
        innodb_file_per_table=ON 每张表使用单独的表空间文件
  - Federated
  - Archive
  - Blcakhole

### 2. mysql命令行

    [root@localhost ~]# mysql --verbose --help #显示mysql所支持的参数

**mysql命令的工作模式**

1.  交互式模式
<pre>
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
</pre>
2. 批处理模式

**mysql命令**
  1. 客户端命令：都不用使用命令结束符
  <pre>
    ?, help 显示帮助信息
    \c, clear 相当于Linux中的Ctrl + c取消执行当前的命令
    \d, delimiter 设置命令结束符
    \g, go 忽视命令结束符，将命令发送到服务器执行
    \G, ego 忽视命令结束符，将命令发送到服务器执行，并将结果以竖排方式显示
    \s, status 显示服务器状态信息
    \., source script_file 执行sql script
    \u, use db_name 切换数据库
    \!, system shell_command 执行系统shell命令
    \W, warnings 打开警告信息
    \w, nowarning 关闭警告信息
  </pre>
  2. 服务端命令：都必须使用命令结束符
  <pre>
    show global variables; 显示所有的配置参数
      动态参数：
        在服务运行时可直接改变的参数，在重启MySQL服务后动态设置的参数值会失效
      静态参数：
        在服务启动前设定好
    show global variables like '%sql_mode%'; 搜索某个配置参数
    show global status; 显示服务器状态
    show local variables;
    show local status;
    show session variables;
    show session status;
    set global|session|local sql_mode='STRICT_ALL_TABLES'; 设置配置参数的值。
      session立即生效
      global改变后的值只有新建立的回话才生效，用户必须有super权限才能修改
    show binary logs; 显示二进制日志
    show master status; 显示当前正在使用的二进制日志
    show processlist; 显示所有的服务器线程信息
    flush logs; 手动滚动二进制日志
    flush privileges; 重新加载授权信息
    show character set; 显示当前支持的字符集
    show collation; 显示当前支持的排序规则集
    show databases; 显示所有的数据库
    show tables; 显示当前数据中所有的表
    show table status; 显示当前数据库中所有表的相关信息
    show table status like'%TABLE_NAME%' [\G]; 在当前数据库中搜索某个表的信息
    show indexes from TABLE_NAME; 显示表中的索引信息
  </pre>

**mysqladmin命令，shell命令**
<pre>
mysqladmin [OPTIONS] command[arg] command[arg]....
  create new_db_name 创建数据库
  drop db_name 删除数据库
  password 'PASSWORD' 设置密码
  processlist 显示所有的服务器线程信息
  shutdown 停止mysql服务，会立即停止
  status 显示简要的服务器全局状态信息
    --sleep=2 每隔2秒显示一次
    --count=5 只显示5次
  extended-status 显示扩展的服务器全局状态信息
  variables 显示全局变量值信息
  version 显示mysqld的版本信息
  flush-hosts 清除缓存的host/dns等信息
  flush-logs 手动滚动二进制日志(mysql-bin.000001)
  flush-privileges 重新加载授权信息
  flush-status 重置大部分变量计数器
  flush-tables 关闭当前所有打开的表
  flush-threads 重置线程缓存
  refresh 相当于执行flush-hosts和flush-logs两个命令
</pre>

**修改用户密码** select user,host,password from user;
1. 使用mysqladmin命令
`mysqladmin -u<USER> password <'PASSWORD'> [-p]`
`mysqladmin -u<USER> -h<HOST_NAME> password <'PASSWORD'> [-p]`
  `-p 修改用户密码，需要验证旧密码`
2. 在mysql命令中
  1) set password for 'USER'@'HOST_NAME'=password('PASSWORD');
  2) update mysql.user set password=password('PASSWORD') where user='USER' and host='HOST_NAME';
  最后都需要执行flush privileges;











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
