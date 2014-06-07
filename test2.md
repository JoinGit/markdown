## `<script>`注意事项

如果想输出一个`</script>`字符串，需要把字符串分成多个部分，通过连接符`+`来连接，否则浏览器会误解成`JavaScript`代码已经结束了。**注意在单独的`*.js`文件中不需要这样处理。**

```
<script type="text/javascript">
alert('</scr'+'ipt>');
</script>
```

使用`src`引用外部`*.js`文件的时候必须使用`</script>`，不能是`/>`结尾。在`script`之间添加的任何`JavaScript`代码都不会被执行。

```
<script type="text/javascript" src="xxx.js"></script> //正确用法
<script type="text/javascript" src="xxx.js"/> //错误用法
<script type="text/javascript" src="xxx.js">
alert('不会被执行！！！');
</script>
```

## 标识符

[[Back To Top]](#jump-to-section)

标识符用来对变量、函数、属性等进行命名。标识符命名规则如下：

 - 第一字符必须是字母、下划线`_`、美元符号`$`。
 - 其他字符可以是字母、下划线`_`、美元符号`$`或数字。
 - 不能把关键字、保留字作为标识符。

## 运算符

[[Back To Top]](#jump-to-section)

**typeof(*expression*)**

- 操作符返回一个字符串，括号是可有可无的

 | 操作数类型    | 返回值        |
 | ------------- |:-------------:|
 | undefined     | "undefined"   |
 | Null          | "object"      |
 | Boolean       | "boolean"     |
 | String        | "string"      |
 | Number        | "number"      |
 | Object        | "object"      |
 | Array         | "object"      |
 | Function      | "function"    |

- 用法

 ```javascript
 // Numbers
 typeof 37 === 'number';
 typeof 3.14 === 'number';
 typeof Math.LN2 === 'number';
 typeof Infinity === 'number';
 typeof NaN === 'number'; // 尽管NaN是"Not-A-Number"的缩写,意思是"不是一个数字"
 typeof Number(1) === 'number'; // 不要这样使用!

 // Strings
 typeof "" === 'string';
 typeof "bla" === 'string';
 typeof (typeof 1) === 'string'; // typeof返回的肯定是一个字符串
 typeof String("abc") === 'string'; // 不要这样使用!

 // Booleans
 typeof true === 'boolean';
 typeof false === 'boolean';
 typeof Boolean(true) === 'boolean'; // 不要这样使用!

 // Undefined
 typeof undefined === 'undefined';
 typeof blabla === 'undefined'; // 一个未定义的变量,或者一个定义了却未赋初值的变量

 // Objects
 typeof {a:1} === 'object';
 typeof [1, 2, 4] === 'object'; // 使用Array.isArray或者Object.prototype.toString.call方法可以分辨出一个数组和真实的对象
 typeof new Date() === 'object';

 typeof new Boolean(true) === 'object' // 令人困惑.不要这样使用
 typeof new Number(1) === 'object' // 令人困惑.不要这样使用
 typeof new String("abc") === 'object';  // 令人困惑.不要这样使用

 // Functions
 typeof function(){} === 'function';
 typeof Math.sin === 'function';

 // null
 typeof null === 'object'; // 从JavaScript诞生以来,一直是这样的.
 ```

## 数据类型

[[Back To Top]](#jump-to-section)
