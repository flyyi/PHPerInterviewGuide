PHP 篇收集了一些常见的基础、进阶面试题。

### 基础篇

- Get 和 POST 的区别
    GET在浏览器回退时是无害的，而POST会再次提交请求。
    GET产生的URL地址可以被Bookmark，而POST不可以。
    GET请求会被浏览器主动cache，而POST不会，除非手动设置。
    GET请求只能进行url编码，而POST支持多种编码方式。
    GET请求参数会被完整保留在浏览器历史记录里，而POST中的参数不会被保留。
    GET请求在URL中传送的参数是有长度限制的，而POST没有。
    对参数的数据类型，GET只接受ASCII字符，而POST没有限制。
    GET比POST更不安全，因为参数直接暴露在URL上，所以不能用来传递敏感信息。
    GET参数通过URL传递，POST放在Request body中。
    GET产生一个TCP数据包，POST产生两个TCP数据包。

- 单引号和双引号的区别
    单引号包含的内容会被认为是普通字符串
    双引号中允许包含字符串变量，PHP会帮我们解析。
- isset 和 empty  array_key_exists的区别
    empty： 参数为0或为NULL时（如上面列子），empty均返回TRUE，详细情况可以参见empty官方手册
    isset： 参数为NULL时，返回FALSE，0与NULL在PHP中是有区别的，isset(0)返回TRUE
    array_key_exists： 纯粹的判断数组键值对是否存在，无论值是多少
- echo、print_r、print、var_dump 之间的区别
    1.echo 和 print 都是语言结构，只能输出简单类型的值(int,string)，它们在输出数组时提示Notice错误，输出对象时提示Catchable fatal error。两者唯一的不同是echo支持输出多参数，print只能输出一个参数。
    2.print_r和var_dump是函数，可用于打印数组和对象，print_r显示关于变量易于理解的信息，只支持一个参数。var_dump显示的是表达式的结构信息，包含表达式的类型和值。
    但是print_r输出布尔值会转换为0、1，null则没有输出，而var_dump输出的信息更加丰富，所以var_dump更适合调试,print_r一般在调试api接口时代替var_dump。
    3.var_export()输出的是一个变量的字符串表示，第二个参数为true则返回变量的表示。
    注意：var_export()的变量是资源类型时返回null。
    var_export()可以将变量例如$_POST,$_GET,$_SESSION 作为字符串形式存储，方便查看。
- 什么是 MVC？
    MVC全名是Model View Controller，是模型(model)-视图(view)-控制器(controller)的缩写，是一种设计模式，使程序的数据，视图和业务逻辑处理互相分      离。功能:模型层负责数据的流转，存入流出，控制器负责数据的业务逻辑处理，即响应视图输入的数据，给模型层，同时将模型层输出的数据处理后，交给视图层呈现。
- 传值和传引用的区别？
传值，
   是把实参的值赋值给行参
   那么对行参的修改，不会影响实参的值

   传地址
   是传值的一种特殊方式，只是他传递的是地址，不是普通的如int
   那么传地址以后，实参和行参都指向同一个对象

   传引用
   真正的以地址的方式传递参数
   传递以后，行参和实参都是同一个对象，只是他们名字不同而已
   对行参的修改将影响实参的值　　

　　$a = "123";
　　$b = &$a;
　　echo $a."-".$b; // 输出：123-123
　　echo "<br/>";
　　$b = "456465"; // 输出：456465-456465
　　echo $a."-".$b;

　　// 结论 ：
　　// PHP 传引用时 形参 发声改变的时候 实参也发生改变；
仅讨论一下值传递和引用：
   所谓值传递，就是说仅将对象的值传递给目标对象，就相当于copy；系统将为目标对象重新开辟一个完全相同的内存空间。
   所谓引用，就是说将对象在内存中的地址传递给目标对象，就相当于使目标对象和原始对象对应同一个内存存储空间。此时，如果对目标对象进行修改，内存中的数据也会改变。
- Cookie 和 Session 的区别和关系

> 1. Cookie 在客户端（浏览器），Session 在服务器端
> 2. Session 比 Cookie 安全性更高
> 3. 单个 Cookie 保存的数据不能超过 4K
> 4. Session 是基于 Cookie，如果浏览器禁用了 Cookie，Session 也会失效（但是可以通过其它方式实现，比如在 url 中传递 Session ID）

### 进阶篇

- 简述 S.O.L.I.D 设计原则

\- | - | -
--- | --- | ---
SRP	| 单一职责原则	| 一个类有且只有一个更改的原因
OCP	| 开闭原则	| 能够不更改类而扩展类的行为
LSP	| 里氏替换原则	| 派生类可以替换基类使用
ISP	| 接口隔离原则	| 使用客户端特定的细粒度接口
DIP	| 依赖反转原则	| 依赖抽象而不是具体实现

- PHP7 和 PHP5 的区别，具体多了哪些新特性？

> 1. 性能提升了两倍
> 2. 增加了结合比较运算符 (<=>)
> 3. 增加了标量类型声明、返回类型声明
> 4. `try...catch` 增加多条件判断，更多 Error 错误可以进行异常处理
> 5. 增加了匿名类，现在支持通过new class 来实例化一个匿名类，这可以用来替代一些“用后即焚”的完整类定义

- 为什么 PHP7 比 PHP5 性能提升了？

> 1. 变量存储字节减小，减少内存占用，提升变量操作速度
> 2. 改善数组结构，数组元素和 hash 映射表被分配在同一块内存里，降低了内存占用、提升了 cpu 缓存命中率
> 3. 改进了函数的调用机制，通过优化参数传递的环节，减少了一些指令，提高执行效率

- 简述一下 PHP 垃圾回收机制（GC）

> PHP 5.3 版本之前都是采用引用计数的方式管理内存，PHP 所有的变量存在一个叫 `zval` 的变量容器中，当变量被引用的时候，引用计数会+1，变量引用计数变为0时，PHP 将在内存中销毁这个变量。
>
> 但是引用计数中的循环引用，引用计数不会消减为 0，就会导致内存泄露。
>
> 在 5.3 版本之后，做了这些优化：
>
> 1. 并不是每次引用计数减少时都进入回收周期，只有根缓冲区满额后在开始垃圾回收；
> 2. 可以解决循环引用问题；
> 3. 可以总将内存泄露保持在一个阈值以下。

了解更多可以查看 PHP 手册，[垃圾回收机制](http://docs.php.net/manual/zh/features.gc.performance-considerations.php)。

- 如何解决 PHP 内存溢出问题

> 1. 增大 PHP 脚本的内存分配
> 2. 变量引用之后及时销毁
> 3. 将数据分批处理

- Redis、Memecached 这两者有什么区别？

> 1. Redis 支持更加丰富的数据存储类型，String、Hash、List、Set 和 Sorted Set。Memcached 仅支持简单的 key-value 结构。
> 2. Memcached key-value存储比 Redis 采用 hash 结构来做 key-value 存储的内存利用率更高。
> 3. Redis 提供了事务的功能，可以保证一系列命令的原子性
> 4. Redis 支持数据的持久化，可以将内存中的数据保持在磁盘中
> 5. Redis 只使用单核，而 Memcached 可以使用多核，所以平均每一个核上 Redis 在存储小数据时比 Memcached 性能更高。

- Redis 如何实现持久化？

> 1. RDB 持久化，将 Redis 在内存中的的状态保存到硬盘中，相当于备份数据库状态。
> 2. AOF 持久化（Append-Only-File），AOF 持久化是通过保存 Redis 服务器锁执行的写状态来记录数据库的。相当于备份数据库接收到的命令，所有被写入 AOF 的命令都是以 Redis 的协议格式来保存的。

### Web 安全防范

- CSRF 是什么？如何防范？

> CSRF（Cross-site request forgery）通常被叫做「跨站请求伪造」，可以这么理解：攻击者盗用用户身份，从而欺骗服务器，来完成攻击请求。

防范措施：

1. 使用验证码
2. 给每一个请求添加令牌 token 并验证

- XSS 是什么？如何防范？

> XSS(Cross Site Scripting)，跨站脚本攻击，攻击者往 Web 页面里插入恶意 Script 代码，当用户浏览该页之时，嵌入其中 Web 里面的 Script 代码会被执行，从而达到恶意攻击用户的目的。

防止 XSS 攻击的方式有很多，其核心的本质是：永远不要相信用户的输入数据，始终保持对用户数据的过滤。

- 什么是 SQL 注入？如何防范？

> SQL 注入就是攻击者通过一些方式欺骗服务器，结果执行了一些不该被执行的 SQL。

SQL 注入的常见场景

1. 数据库里被注入了大量的垃圾数据，导致服务器运行缓慢、崩溃。
2. 利用 SQL 注入暴露了应用程序的隐私数据

防范措施：

1. 保持对用户数据的过滤
2. 不要使用动态拼装 SQL
3. 增加输入验证，比如验证码
4. 对隐私数据加密，禁止明文存储

### 扩展阅读

- [3年PHPer的面试总结](http://coffeephp.com/articles/4?utm_source=laravel-china.org)
- [垃圾回收机制](http://docs.php.net/manual/zh/features.gc.performance-considerations.php)
- [S.O.L.I.D 面向对象设计](https://laravel-china.org/articles/4160/solid-object-oriented-design-and-programming-oodoop-notes?order_by=created_at&)
- [浅谈IOC--说清楚IOC是什么](http://www.cnblogs.com/DebugLZQ/archive/2013/06/05/3107957.html)
- [Redis和Memcached的区别](https://www.biaodianfu.com/redis-vs-memcached.html)
- [CSRF攻击与防御](https://www.cnblogs.com/phpstudy2015-6/p/6771239.html)
- [XSS跨站脚本攻击](https://www.cnblogs.com/phpstudy2015-6/p/6767032.html#_label9)
