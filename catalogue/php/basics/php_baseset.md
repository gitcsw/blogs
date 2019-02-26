# PHP基础集合

### PHP语法规范
**命名规则**
- 常量名 类常量建议全大写，单词间用下划线分隔：MIN_WIDTH
- 变量名建议用下划线方式分隔：&nbsp;&nbsp;$var_name
- 函数名建议用驼峰命名法：&nbsp;&nbsp;varName
- 定界符建议全大写：&nbsp;&nbsp;<<<DING, <<<'DING'
- 文件名规范：
 - 普通文件名建议使用全小写和下划线、数字组成：&nbsp;&nbsp;func_name.php
 - C和M（控制器和模型）首字母必须大写，遵守驼峰格式，例如：UserBankController.php
- 私有属性名、方法名建议加下划线：&nbsp;&nbsp;private $_name _func
- 接口名建议加I_：&nbsp;&nbsp;interface I_Name
- 所有自行命名对象变量函数名等请避开php预留字符：如$_POST、function switch(){}等。

**大小写问题**
- 类名、方法名、属性名、函数名：不区分大小写；
- 变量名、常量名、元素下标：区分大小写。

**文件编码**
- 文件编码请使用UTF-8编码(不带BOM)。

**驼峰命名法**
- 骆驼式命名法就是当变量名或函数名是由一个或多个单词连结在一起，而构成的唯一识别字时，第一个单词以小写字母开始；从第二个单词开始以后的每个单词的首字母都采用大写字母，例如：myFirstName、myLastName，这样的变量名看上去就像骆驼峰一样此起彼伏，故得名。

小驼峰法
- 变量一般用小驼峰法标识。小驼峰法：除第一个单词之外，其他单词首字母大写。譬如：int myStudentCount;变量myStudentCount第一个单词是全部小写，后面的单词首字母大写。

大驼峰法
- 相比小驼峰法，大驼峰法（即帕斯卡命名法）把第一个单词的首字母也大写了。常用于类名，命名空间等。譬如：public class DataBaseUser;


### PHP基础集合

(参见[PHP手册](http://php.net/manual/zh/)或其它基础参考资料)

#### 大纲
##### 基本语法
- PHP标记、指令分隔符、注释；
##### 类型
- Boolean、Integer、Float、String、Array、Object、Resource、NULL、Callback / Callable等；
##### 变量
- 基础、预定义变量、变量范围、可变变量、来自 PHP 之外的变量；
##### 常量
- 语法、魔术常量；
##### 表达式
##### 运算符
- 运算符优先级、算术运算符、赋值运算符、位运算符等；
##### 流程控制
- if、else、elseif/else if、while、do-while、for、foreach、break、continue、switch、declare、return、require、include、require_once、include_once、goto等；
##### 函数
- 自定义函数、函数的参数、返回值、可变函数、内部（内置）函数、匿名函数；
##### 类与对象
- 属性、类常量、类的自动加载、构造函数和析构函数、访问控制等；
##### 命名空间
- namespace关键字和\_\_NAMESPACE\_\_常量、使用命名空间：别名/导入全局空间等；
##### 预定义变量
- 超全局变量、$GLOBALS、$_SERVER、$_GET、$_POST、$_FILES等；
##### 预定义异常
- Exception、ErrorException；
##### 预定义接口
- 遍历、迭代器、聚合式迭代器、数组式访问、序列化、Closure、生成器。

### 第一次作业

- 1、PHP中什么错误等级可以被捕获？
- 2、PHP的异常处理，exception和throwable有何区别？
- 3、什么是错误抑制符？
- 4、如何捕获php的致命错误？
- 5、spl_auto_load的原理或者执行过程是？
- 6、php的自动加载，带来的弊端是？如何针对该弊端对传统fpm进行加速？
- 7、传统的fpm模式，为什么导致了并发不高？
- 8、php手册中，规定的二进制安全文件操作，有哪些？
- 9、php手册中，类的魔术方法都是做什么用处的？
- 10、php手册中，什么是资源变量，他有什么特点？

要求：允许参考网络，请安照自行理解答题，可Word，建议使用Markdown。
