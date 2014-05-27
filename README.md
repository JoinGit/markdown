## Python文件类型

- 源代码
  - Python源代码的文件以`*.py`为扩展名，由`python`命令解释执行，不需要编译
   <pre>
    $ cat hello.py
    print 'hello world'
    $ python hello.py
    hello world
   </pre>
  - 在`linux`中文件头部分添加如下代码，并附加可执行权限，就能够直接执行
   <pre>
    $ cat hello.py
    #!/c/Python27/python
    print 'hello world'
    $ chmod +x hello.py
    $ hello.py
    hello world
   </pre>
- 字节代码
  - Python源文件经编译后生成的扩展名为`*.pyc`的文件，需要用`python`命令执行
  - 编译方法
   <pre>
    $ ls
    hello.py  world.py
    $ cat world.py
    import py_compile
    py_compile.compile("hello.py")
    $ python world.py
    $ ls
    hello.py  hello.pyc  world.py
    $ python hello.pyc
    hello world
   </pre>
- 优化代码
  - 经过优化后的源文件，扩展名为`*.pyo`，需要用`python`命令执行
  - 执行方法，注意参数是大写的`O`
   <pre>
    $ python -O -m py_compile hello.py
    $ ls
    hello.py  hello.pyo
    $ python hello.pyo
    hello world
   </pre>

## Python变量

**变量是计算机内存中的一块区域，变量可以存储规定范围内的值，而且值可以改变。**

- 变量的命名
  - 变量名由字母、数字、下划线组成
  - 不能以数字开头
  - 不可以使用关键字
- 变量的赋值
  - 变量声明和使用
   <pre>
    $ python
    >>> a=1
    >>> a
    1
    >>> print a
    1
    >>> b=10
    >>> a*b+3
    13
   </pre>
  - 查看变量内存空间地址`id(VarName)`，同一内存空间地址可以被多个变量所使用
   <pre>
    $ python
    >>> id(a)
    5090592
    >>> id(b)
    5090484
    >>> c=10
    >>> id(c)
    5090484
   </pre>

## Python运算符
- 算术运算符
  - 加法：`+`
   <pre>
    $ python
    >>> 2+3
    5
   </pre>
  - 减法：`-`
   <pre>
    $ python
    >>> 5-4
    1
   </pre>
  - 乘法：`*`
   <pre>
    $ python
    >>> 3*2
    6
   </pre>
  - 实数除法：`/`
   <pre>
    $ python
    >>> 3/2
    1
    >>> 3.0/2
    1.5
   </pre>
  - 整数除法：`//`
   <pre>
    $ python
    >>> 3//2
    1
    >>> 3.0//2
    1.0
    >>> 3.2//2
    1.0
   </pre>
  - 求余数：`%`
   <pre>
    $ python
    >>> 10%3
    1
   </pre>
  - 幂运算：`**`
   <pre>
    $ python
    >>> 2**3
    8
   </pre>
- 关系运算符，返回`True/False`
  - 小于：`1<2`
  - 大于：`3>2`
  - 小于等于：`1<=1`
  - 大于等于：`2>=2`
  - 不等于：`1!=2`
  - 等于：`2==2`
- 逻辑运算符，返回`True/False`
  - 逻辑与：`3>2 and 2<3`
  - 逻辑或：`1>2 or 3>2`
  - 逻辑非：`not 1>2`
- 赋值运算符，先用左边的变量和右边的表达式计算，再赋值给左边的变量
  - 等于：`=`
   <pre>
    $ python
    >>> a=22
    >>> b='xyz'
    >>> a
    22
    >>> b
    'xyz'
   </pre>
  - 加等于：`+=`
   <pre>
    $ python
    >>> a=22
    >>> a+=5
    >>> a
    27
   </pre>
  - 减等于：`-=`
   <pre>
    $ python
    >>> a=27
    >>> a-=4
    >>> a
    23
   </pre>
  - 乘等于：`*=`
   <pre>
    $ python
    >>> a=5
    >>> a*=4
    >>> a
    20
   </pre>
  - 除等于：`/=`
   <pre>
    $ python
    >>> a=20
    >>> a/=4
    >>> a
    5
   </pre>
  - 求余等于：`%=`
   <pre>
    $ python
    >>> a=5
    >>> a%=3
    >>> a
    2
   </pre>
  - 算术运算符优先级由低到高顺序
   <pre>
    Lambda
    逻辑或：or
    逻辑与：and
    逻辑非：not
    范围：in, not in
    同一性测试：is, is not
    比较：<, <=, >, >=, !=, ==
    按位或：|
    按位异或：^
    移位：<<, >>
    加法与减法：+, -
    乘法、除法与取余：`*, /, %`
    正负号：+X, -X
    按位翻转：~X
    幂运算：**
   </pre>

## Python数据类型

