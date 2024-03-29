
# 1-Operating Systems

## 1.1-进程和线程

1. 进程：系统进行资源分配的基本单位；
2. 线程：CPU调度的基本单位：
   1. 共享进程的全部资源；
   2. 独有程序计数器、寄存器和栈。

## 1.2-进程通信

低级通信：用信号量进行的进程间的互斥和同步；

高级通信：利用操作系统所提供的一组通信命令传送大量数据的通信方式：

1. 共享存储器系统：例：剪贴板；
2. 消息传递系统：例：邮槽；
3. 管道通信系统；

通信方式：

1. 管道：
   1. 有名管道：单向通信，有固定的读端和写端，半双工通信方式，允许无亲缘关系进程间的通信；
   2. 无名管道：数据单向流动，只能在具有亲缘关系的进程间使用；
2. 信号量：是一个计数器，控制多进程对共享资源的访问，作为一种锁机制；
3. 消息队列：消息的链表；
4. 信号；
5. 共享内存：最快的IPC，常与信号量配合，实现进程间的同步和通信；
6. 套接字。

## 1.3-线程通信

1. 互斥量；
2. 信号量；
3. 信号。

## 1.4-死锁

概念：在多个并发进程中，某个进程持有某种资源而又等待别的进程释放他们保持的资源，在为改变状态之前不能向前推进，从而在这一组进程中产生了死锁，多个进程被无限期地阻塞、相互等待的状态；

必要条件：

1. 互斥：一个资源每次只能被一个进程使用；
2. 不可抢占：进程已获得的资源，在未使用完之前，不能前行剥夺；
3. 占有并等待：一个进程因请求资源而阻塞时，对已获得的资源保持不放；
4. 环形等待：若干进程之间形成一种首尾相接的循环等待资源关系；

死锁的解除与预防：

1. 破坏互斥：
   * 允许系统资源都能共享；
   * 缺点：有些资源不能同时访问，如打印机，且在某些场合应保护互斥性；
2. 破坏占有并等待：
   * 预先静态分配，在进程运行前一次申请完它所需要的全部资源，在它的资源未满足前，不投入运行，一旦投入运行资源全部归他所有；
   * 缺点：系统资源浪费，个别资源长期被占用，导致一些进程不能运行；
3. 破坏不可抢占：
   * 当一个进程保持了某些资源，请求新资源而不能被满足时，必须释放所保持的资源，以后重新申请；
   * 缺点：实现复杂，释放资源可能会造成前一阶段工作失效，常用于易于保存和回恢复的资源；
4. 破坏循环等待：
   * 给系统资源编号，规定进程必须按照编号递增的顺序请求资源；
   * 缺点：实现复杂，编号不一定与实际使用顺序相同；

避免死锁的方式：

1. 判断系统状态：在分配前，先计算分配的安全性；
2. 银行家算法：
   1. 申请的贷款额度不能超过银行西安有资金总额；
   2. 分批次向银行提款，但是贷款额度不能超过一开始最大需求量的总额；
   3. 暂时不能满足客户申请的资金额度时，在有限时间内给予贷款；
   4. 客户要在规定时间内还款。

## 1.5-分段与分页内存管理的区别

1. 分段：符合用户视角，将地址空间分为若干段：代码段、数据段、堆、栈；
2. 分页：方便系统管理，将逻辑地址划分为固定大小的页，物理内存划分为同样大小的帧，方便程序加载。

## 1.6-虚拟内存

1. 让每个进程拥有独立的地址空间，且这些空间被分为大小相等的页，被映射到物理内存中，对进程而言，逻辑上有很大的内存空间，但其中一部分对应于物理内存，还有一些在硬盘上；
2. 页面置换算法：FIFO、LRU、LFU、OPT；
3. 优点：
   1. 物理内存可为多个进程共享；
   2. 通过共享页允许进程间共享内存
4. 虚拟内存大小：
   1. 对于32位：0-2^32 ~= 0-4G；
   2. 对于64位：0-2^64；

# 2-Computer Network

## 2.1-Https加密过程

1. 客户端发起握手请求；
2. 服务端返回已有的`证书公钥`（服务端通过CA认证后，拥有`证书公钥`和`证书私钥`）；
3. 客户端验证证书是否有效；
4. 若证书有效，则生成一个`随机数`；
5. 用`证书公钥`加密生成的随机数；
6. 将加密后的`密钥`发送给服务端；
7. 服务端用`证书私钥`解密密钥；
8. 服务端使用解密出的密钥加密要发送的内容并发送给客户端；
9. 客户端使用秘钥解密信息。

## 2.2-对称加密与非对称加密

对称加密：加密和解密使用同一个密钥；

非对称加密：使用公钥和私钥进行加解密。

## 2.3-CLOSE_WAIT和TIME_WAIT

在四次挥手中，

CLOSE_WAIT：服务端收到FIN后，发送ACK给客户端，之后进入CLOSE_WAIT状态；

TIME_WAIT：客户端收到FIN后，发送ACK给服务端，之后进入TIME_WAIT状态。

## 2.4-TCP如何保证传输可靠性

1. 数据包校验；
2. 重排序：TCP将失序数据进行重新排序后才交给应用层；
3. 应答机制：回复ACK；
4. 超时重传；
5. 流量控制：TCP连接的每一方都有固定大小缓冲空间，通过可变大小的滑窗协议完成。

## 2.5-如何预防TCP的DDos攻击

1. 限制同时打开SYN半链接的数目；

   方法：在注册表中对TCPMaxHalfOpen相关参数进行调整；

   TCPMaxHalfOpen相关参数：

   1. SynAttackProtect：决定了系统受到SYN攻击时采取的保护措施，包括减少系统SYN+ACK的重试次数等；
   2. TcpMaxHalfOpen：系统允许同时打开的半链接值；
   3. TcpMaxHalfOpenRetried：决定在什么情况下系统打开SYN攻击保护；

2. 缩短SYN半链接的Time out时间。

## 2.6-TCP如何实现拥塞控制

1. 慢启动：以指数方式，由小到大逐渐增加拥塞窗口(cwnd)的大小，慢启动达到ssthresh阈值则进入拥塞避免；
2. 拥塞避免：每经过一个往返时间RTT就把发送方拥塞窗口增加1，按照线性增长，发生拥塞，cwnd降为1，重新慢启动；
3. 快重传：接收方收到失序报文后，立即发出重复确认，发送方收到三个连续重复确认则立即重传；
4. 快恢复：发送方收到重复确认后，执行`乘法减小` ，把ssthresh减半，但不执行慢开始，因为如果发生阻塞，不会收到多个重复确认，而是将cwnd设置为ssthresh大小进行拥塞避免。

## 2.7-从输入网址到获得页面的过程

1. 浏览器通过DNS查询对应IP地址：
   1. 浏览器搜索自身DNS缓存；
   2. 搜索操作系统DNS缓存；
   3. 向本地DNS服务器进行查询；
   4. 若不在本地域名服务器，则递归或迭代查询：
      1. 递归查询：服务器作为DNS客户向根服务器查询；
      2. 迭代查询：根服务器告知服务器需要查询的IP，服务器自己进行查询；
2. 获取IP地址后，浏览器向服务器请求建立连接，发起三次握手；
3. TCP连接建立后，浏览器向服务器发送HTTP请求；
4. 浏览器对请求进行处理，并将处理结果返回给浏览器；
5. 浏览器进行渲染，呈现页面给用户。

## 2.8-Session 与 Cookie

**Session**： 

1. 用户访问服务器时，服务器首先检查请求中是否包含sessionId，若包含，说明session已创建，若不包含，则为用户建立一个session并分配sessionId（依赖Cookie）；

2. 用户提交表单时，浏览器将用户的SessionId附在HTTP头信息中，服务器处理完表单将结果返回sessionId对应的用户；

3. 若Cookie被禁用：
   1. URL重写：直接将sessionId附在URL后；
      2. 表单隐藏字段：修改表单，添加一个隐藏字段，以便提交时能够回传sessionId
4. session共享：修改cookie的域名为父域名；
5. 使用场景：购物车；

**Cookie**：

1. 若服务器需要记录用户状态，则使用response向客户端颁发一个cookie，再次请求时，浏览器将请求网址连同cookie一起提交给服务器；
2. 会话Cookie和持久Cookie：
   1. 会话cookie：不设置过期时间，关闭浏览器窗口，cookie就消失，一般保存在内存里而不是硬盘上；
   2. 持久cookie：设置了过期时间，cookie有效指导超过了设定的过期时间，一般存储在硬盘上；
3. 使用场景：登录网站。

## 2.9-七层网络体系结构

1. 物理层：实现相邻计算机节点之间比特流透明传送；
2. 数据链路层：接手物理层的位流行驶数据，封装成帧，传送到上一层，同样，也将上一层的数据帧，拆装成位流转发到物理层；
3. 网络层：将网络地址翻译为对应的物理地址，并通过路由算法选择最佳路径；
4. 传输层：为不同主机上运行的进程提供逻辑通信；
   1. 区别于网络层：网络层完成主机间的逻辑通信，传输层完成应用进程间的逻辑通信；
5. 会话层：应用程序与网络之间的接口，负责在网络中的两节点之间建立、维持和终止通信；
6. 表示层：对来自应用层的命令和数据进行解释；
7. 应用层：为用户的应用进程提供网络通信服务。

## 2.10-TCP和UDP对应的常见应用层协议

1. TCP：
   1. FTP：文件传输协议；
   2. Telnet：用于远程登录的端口：
      1. 和ssh的区别：
         1. telnet为明文传送，ssh为加密传送；
         2. ssh使用公钥对服务器的用户进行身份验证，telnet没有使用公钥；
   3. SMTP：邮件传送协议，用于发送邮件；
   4. POP3：用于接收邮件；
   5. HTTP；
2. UDP：
   1. DNS：域名解析服务；
   2. SNMP：网络管理协议，用于管理网络设备；
   3. TFTP：简单文件传输协议。

## 2.11-ARP

1. 将IP地址转换为MAC地址；
2. 网络通过帧进行传输，帧里面需要目标主机的MAC地址。

## 2.12-常见状态码

1XX：请求已被接受，正在处理；

2XX：请求成功被处理；

3XX：重定向：

​	301：永久性转移；

​	302：暂时性转移；

​	304：已缓存；

4XX：客户端请求不合法：

​	400：请求语法有问题；

​	403：拒绝请求；

​	404：客户端所访问的页面不存在；

5XX：服务器不能处理合法请求：

​	500：服务器内部错误；

​	503：服务暂时不可用。

# 3-C++

## 3.1-虚函数和纯虚函数

1. 虚函数：为了动态绑定，允许被子类重新定义的成员函数， virtual returnType func(parameter); 
2. 纯虚函数：为了派生接口，virtual returnType func(parameter) = 0;
3. 基类需要虚析构函数的原因：防止内存泄漏，假如没有虚析构函数，释放一个由基类指向派生类的对象是，不触发动态绑定，则只会调用基类析构函数，而不会调用派生类的，从而导致派生类内存空间的不到释放。 

## 3.2-static和const关键字

static：存储在静态存储区，未初始化时自动初始化为0：

1. 局部变量：
   1. 变为静态局部变量；
   2. 作用域仍为局部作用域；
   3. 离开作用域仍驻留在内存中，但不可访问；
2. 全局变量：
   1. 变为全局静态变量；
   2. 在声明的文件之外不可见；
3. 成员变量：
   1. 变为类的全局变量，被类的对象共享，包括派生类的对象；
   2. 必须在类外进行初始化，如int base::var = 10;，但可以用const修饰static数据成员，从而在类内初始化；
4. 成员函数：
   1. 使得成员函数为所有对象共享，不含this指针；
   2. 可以独立访问，不需要创建实例，如base::func(3, 5);
   3. 不可直接引用类的非静态成员，但是可以引用静态成员；
   4. 不可同时用const和static修饰成员函数（const含this指针，static不含，冲突）；

const：

1. 表明变量不可修改；
2. 限定成员函数不可修改任何数据成员；
3. const与指针：
   1. const char *p：指向的内容不能改变；
   2. char * const p：将p声明为常指针，地址不能变，但是内容可变。

## 3.3-C++的内存分区

1. 栈区（stack）：主要存放函数参数以及局部变量，由系统自动分配释放；
2. 堆区（heap）：用户通过malloc/new手动申请释放，分配类似链表；
3. 全局/静态区：存放全局变量、静态变量；
4. 字符串常量区：字符串常量；
5. 代码区：程序的二进制代码。

## 3.4-STL容器

底层数据结构：

1. vector：数组；
2. map、multimap：红黑树；
3. unordered_map、unordered_nultimap：哈希表。

## 3.5-内存泄漏

1. 一般为堆内存泄漏，即程序在运行中动态申请的内存空间不使用后，未及时释放；
2. 解决：
   1. 良好编程习惯；
   2. 重载new和delete，以链表形式自动管理分配的内存；
   3. 使用智能指针。

## 3.6-32位、64位系统中，常用内置数据类型所占字节数

1. 32位：
   1. char：1字节；
   2. 指针变量：4字节；
   3. short int：2字节；
   4. int：4字节；
   5. unsigned int：4字节；
   6. float：4字节；
   7. double：8字节；
   8. long：4字节；
   9. unsigned long：4字节；
   10. long long：8字节；
2. 64位：
   1. char：1字节；
   2. 指针变量：8字节；
   3. short int：2字节；
   4. int：4字节；
   5. unsigned int：4字节；
   6. float：4字节；
   7. double：8字节；
   8. long：8字节；
   9. unsigned long：8字节；
   10. long long：8字节。

## 3.7-inline、volatile关键字

1. inline：解决频繁调用小函数大量消耗栈空间的问题；
2. volatile：表明类型变量可被更改，不再优化，需要从如内存中重新读取。

## 3.8-深拷贝与浅拷贝

拷贝函数使用场景：

1. 一个对象以值的方式传入函数体；
2. 一个对象以值的方式从函数返回；
3. 一个对象需通过另一个对象进行初始化；

区别：

1. 浅拷贝：只是增加一个指针指向已存在的内存地址；
2. 深拷贝：增加一个指针，并且申请一个新的内存用于存放复制的对象。

## 3.9-派生类构造/析构函数调用顺序

1. 构造函数：先基后派；
2. 析构函数：先派后基。

## 3.10-数据成员初始化顺序

顺序：

1. 基类的静态变量或全局变量；
2. 派生类的静态变量或全局变量；
3. 基类的成员变量；
4. 派生类的成员变量。

## 3.11-static_cast, dynamic_cast, const_cast, reinpreter_cast区别

static_cast与dynamic_cast：

1. 发生时间不同，一个是static编译时，一个是runtime运行时；
2. static_cast为强制类型转换，不提供运行时的检查；
3. dynamic_cast用于转换指针和引用，不可用于转换对象，主要用于类层次间的上行和下行转换：
   1. 上行转换：B继承自A，由B转换为A；
   2. 下行转换：B继承自A，A转换为B；
4. 上行转换时，static_cast和dynamic_cast效果相同，下行转换时，dynamic_cast具有类型检查，更安全。

## 3.12-定义一个空类 编译器会做什么

1. 当用到相关函数时，编译器会去自动生成：默认构造函数、默认拷贝构造函数、默认拷贝赋值操作符、默认析构函数；
2. 所有自动生成的函数都是inline和public的。

## 3.13-哪些函数不能成为虚函数

1. 构造函数：假如子类继承基类构造函数，则子类对象将使用基类构造函数构造，而基类的构造函数并不知道自类的成员，不符合语义，且，多态是通过基类指针指向子类对象实现多态的，在对象构造之前，并没有对象产生，因此无法使用多态特性，是矛盾的；
2. 内联成员函数：内联函数在编译时展开，而虚函数是在运行时绑定的，两者相违背；
3. 静态成员函数：在编译时确定，无法动态绑定，不支持多态。

## 3.14-内联函数与宏定义的区别

1. 宏定义在于处理时把所有宏名用宏体替换，内联函数在编译时进行代码插入、展开、省去调用的开销；
2. 宏定义没有类型检查，内联函数满足函数的性质，如有返回值、参数列表等。

## 3.15-左值引用和右值引用

1. 左值引用要求右边的值必须能够取地址，如果不能取地址，可以使用常引用；

   1. 例：`const int &var = 10;`等价于

      1. ```c++
         const int temp = 10;
         const int &var = temp;
         ```

   2. 但常引用修饰后，不可以通过引用进行修改，只能进行读取；

2. 右值引用用来绑定到右值；

   1. 左值：可以取地址的，有名字的，非临时的值；
   2. 右值：不能取地址的，没有名字的，临时的值；
   3. 定义格式`类型 && 引用名 = 右值表达式;`
   4. 例：`int &&var = 10;`

## 3.16-substr用法

1. 目的：构建一个string；

2. 用法：s.substr(pos, n)：

   1. ```c++
      string s("testString");
      string newStr = s.substr(0, 6);
      ```

3. 注意：返回一个从pos开始，包含pos的n个字符，pos默认值为0，n默认值为s.size()-pos。

# 4-Database

## 4.1-数据库范式

第一范式：列不可分；

第二范式：有主键，保证完全依赖于主键；

第三范式：无传递依赖。    

## 4.2-索引

索引：对数据库表中一个或多个列的值进行排序的数据结构，从而达到快速查询、更新数据库表数据的目的；

实现：通常使用B树或B+树，如用B树可以实现O(logn)的时间复杂度检索：

1. B树特点（m叉树）：
   1. 树中每个节点最多有m个子节点；
   2. 所有叶子节点都在同一层；
2. B+树特点（InnoDB的索引实现）：
   1. 所有叶子节点中包含了所有关键码信息，及指向关键码记录的指针；
   2. 叶子节点本身根据关键码大小自小而大顺序链接；
   3. 含有两个指针，一个指向根节点，一个指向关键字最小的叶子节点；
3. B+树更适合文件和数据库索引的原因：
   1. B+树内部节点相对B树更小，磁盘读写代价更低；
   2. 每次查找都需要从根节点到叶子节点，查询效率更稳定；

索引的优点：

1. 加快数据检索速度；
2. 加快表与表之间的连接；
3. 减少分组和排序语句的时间；
4. 通过创建唯一性索引，保证数据库中每一行数据的唯一性；

设置了索引但是无法使用的情况：

1. 模糊查询，以“%”开头的Like语句；
2. OR语句前后没有同时使用索引；
3. 数据类型出现隐式转化，如varchar不加单引号自动转为int；
4. 对于多列索引，必须满足最左匹配原则：
   1. 如对于索引(a, b, c)，生效情况为a、(a, b)、(a, b, c)；
   2. 因为针对联合索引构建的B+树优先保证最左元素有序；

什么字段适合创建索引：

1. 经常作为查询选择的字段；
2. 经常作为表连接的字段；
3. 经常出现在order by、group by、distinct后面的字段；

创建索引时需要注意：

1. 非空字段：需要使用0或特殊值代替NULL，否则会使索引运算更加复杂；
2. 索引字段越小越好：数据库存储以页为单位，一页存储的数据越多，一次IO获取数据的效率越高；

索引缺点：

1. 时间：创建、维护索引需要耗费时间，对表中数据进行增加、删除、修改时，索引也要动态修改，降低了数据的维护速度；
2. 空间：索引需要额外的存储空间；

索引的分类：

1. 普通索引和唯一性索引：索引列值的唯一性；
2. 单个索引和复合索引：索引列包含的列数；
3. 聚簇索引和非聚簇索引：
   1. 聚簇索引：按照每张表的主键构建一个B+树，InnoDB中表数据文件本身就是按照B+树组织的索引结构；
   2. 非聚簇索引：按照value进行检索，最后获得想要数据的主键，再通过主索引进行检索；

唯一索引与主键索引：

1. 主键索引：为主键创建的唯一索引；
2. 唯一索引：索引列的值必须唯一，但允许有空值。

## 4.3-数据库事务

事务的特性：

1. 原子性（Atomicity）：事务所包含的一系列语句，要么全部成功执行，要么全部回滚；
2. 一致性（Consistency）：事务的执行结果必须使数据库从一个一致性状态到领一个一致性状态；
3. 隔离性（Isolation）：并发执行的并发之间不能相互影响；
4. 持久性（Durability）：事务一旦提交，对数库中的数据改变是永久性的；

事务并发带来的问题：

1. 脏读：一个事务读取了另一个事务未提交的数据；
2. 不可重复读：同样条件下，两次读取结果不同，即，被读取的数据可以被其他事务修改；
3. 幻读：同样条件下，两次读出的记录数不一样，即，被读取的数据可以被其他事务新增或删除；

隔离级别：

1. 读未提交（Read Uncommitted）：允许一个事务读取另一个事务还没提交的数据，可能会提高性能，但是会导致脏读；
2. 读已提交（Read Committed）：只允许读到其他事物已经提交的数据，不能避免不可重复读；
3. 可重复读（Repeatable Read）：一个事务开启后，其他事务对于数据库的修改在本事务中不可见，直到本事务提交或回滚，但是，其他事物的删除新增可见，不能避免幻读的问题；
4. 串行化（Serializable）：只允许事务串行执行；
5. MySQL默认隔离级别是Repeatable Read。

## 4.4-MySQL的优化

SQL语句及索引的优化：

1. SQL语句的优化：
   1. 通过慢查询日志，找出IO大的SQL、未命中索引的SQL，从而进行优化；
   2. 通过explain了解MySQL对于语句的处理，若扩展列extra出现Using filesort和Using temporay表示SQL需要优化；
   3. 其他tips：
      1. 优化insert语句：一次插入多值；
      2. 避免在where子句中使用!=或<>，以及避免在where子句中对字段进行null值判断，否则引擎会放弃使用索引而进行全表扫描；
      3. 优化嵌套查询：使用join代替子查询；
      4. 考虑用exists代替in；
2. 索引优化：
   1. 在经常做查询选择的字段、表连接的字段、经常出现在order by/group by/distincy后的字段中建立索引；
   2. 避免索引失效；
3. 表结构的优化：
   1. 选择合适的数据类型：
      1. 尽量选择较小的数据类型；
      2. 尽量使用简单的数据类型，int比varchar容易处理；
      3. 尽可能使用非空定义字段；
      4. 尽量避免使用text类型，非用不可需考虑分表；
   2. 表的范式优化；
   3. 垂直拆分和水平拆分：
      1. 垂直拆分：将表按照业务分类，分不到不同的数据库上，将数据压力分担到不同库上面；
      2. 水平拆分：将同一张表中的数据拆分到不同数据库中进行存储，或者把一张表拆分成多张小表；

## 4.5-drop、delete和truncate区别

1. delete：
   1. 用来删除表的全部或一部分数据行；
   2. 需要提交或回滚来执行或撤销删除操作；
2. truncate：
   1. 删除表中所有数据；
   2. 不可回滚；
   3. 比delete更快，占用空间更小；
3. drop：
   1. 删除表、所有数据行、索引等；
   2. 不可回滚；
4. 总结：不需要一张表的时候，用drop；想删除部分数据行时，用delete；保留表结构但删除所有数据时，用truncate。

## 4.6-悲观锁与乐观锁

1. 悲观锁：
   1. 先获取锁在进行业务操作；
   2. 通过select ... for update来实现，在当前事务结束时自动释放；
   3. MySQL中使用2.时所有扫描过的行都会上锁，需要确认使用了索引而不是全表扫描；
2. 乐观锁：
   1. 先进行业务操作，最后更新时检查是否被更新，若未被更新，则更新成功，否则失败重试；
   2. 依靠逻辑实现；
   3. 在业务操作前获取需要锁的数据的版本号，更新时进行对比；
3. 应用场景：
   1. 读多写少适合乐观锁；
   2. 读少写多适合悲观锁。

## 4.7-MySQL中MyISAM和InnoDB的差异

1. 存储结构：
   1. MyISAM存储为：.frm文件存储表定义、.MYD数据文件、.MYI索引文件；
   2. InnoDB都保存在同一个数据文件中；
2. 存储空间：
   1. MyISAM可被压缩，占据的存储空间较小；
   2. InnoDB需要更多内存和存储，会在主内存中建立专用的缓冲池，用于高速缓冲数据和索引；
3. 事务支持：
   1. MyISAM每次查询具有原子性，执行速度比InnoDB更快，但是不支持事务；
   2. InnoDB支持事务、外键，具有事务提交、回滚等能力；
4. 表锁差异：
   1. MyISAM只支持表级锁，CRUD时会自动给表加锁；
   2. InnoDB支持行级锁，在where主键时生效，非主键锁全表。

# 5-Linux

## 5.1-find命令

1. 查找指定文件名文件（不区分大小写）：

```shell
find -iname "ProgramToFind.java"
```

2. 对找到的文件执行某命令

```shell
find -iname "ProgramToOperate.java" -exec md5sum {} \;
```

3. 查找home目录下所有空文件

```shell
find ~ -empty
```

4. 在/home下找到大小超过3MB的文件

```shell
find /home -type f -size +3072k
```

## 5.2-static和const关键字

static：存储在静态存储区，未初始化时自动初始化为0：

1. 局部变量：
   1. 变为静态局部变量；
   2. 作用域仍为局部作用域；
   3. 离开作用域仍驻留在内存中，但不可访问；
2. 全局变量：
   1. 变为全局静态变量；
   2. 在声明的文件之外不可见；
3. 成员变量：
   1. 变为类的全局变量，被类的对象共享，包括派生类的对象；
   2. 必须在类外进行初始化，如int base::var = 10;，但可以用const修饰static数据成员，从而在类内初始化；
4. 成员函数：
   1. 使得成员函数为所有对象共享，不含this指针；
   2. 可以独立访问，不需要创建实例，如base::func(3, 5);
   3. 不可直接引用类的非静态成员，但是可以引用静态成员；
   4. 不可同时用const和static修饰成员函数（const含this指针，static不含，冲突）；

const：

1. 表明变量不可修改；
2. 限定成员函数不可修改任何数据成员；
3. const与指针：
   1. const char *p：指向的内容不能改变；
   2. char * const p：将p声明为常指针，地址不能变，但是内容可变。

## 5.3-C++的内存分区

1. 栈区（stack）：主要存放函数参数以及局部变量，由系统自动分配释放；
2. 堆区（heap）：用户通过malloc/new手动申请释放，分配类似链表；
3. 全局/静态区：存放全局变量、静态变量；
4. 字符串常量区：字符串常量；
5. 代码区：程序的二进制代码。

## 5.4-STL容器

底层数据结构：

1. vector：数组；
2. map、multimap：红黑树；
3. unordered_map、unordered_nultimap：哈希表。

## 5.5-内存泄漏

1. 一般为堆内存泄漏，即程序在运行中动态申请的内存空间不使用后，未及时释放；
2. 解决：
   1. 良好编程习惯；
   2. 重载new和delete，以链表形式自动管理分配的内存；
   3. 使用智能指针。

## 5.6-32位、64位系统中，常用内置数据类型所占字节数

1. 32位：
   1. char：1字节；
   2. 指针变量：4字节；
   3. short int：2字节；
   4. int：4字节；
   5. unsigned int：4字节；
   6. float：4字节；
   7. double：8字节；
   8. long：4字节；
   9. unsigned long：4字节；
   10. long long：8字节；
2. 64位：
   1. char：1字节；
   2. 指针变量：8字节；
   3. short int：2字节；
   4. int：4字节；
   5. unsigned int：4字节；
   6. float：4字节；
   7. double：8字节；
   8. long：8字节；
   9. unsigned long：8字节；
   10. long long：8字节。

## 5.7-inline、volatile关键字

1. inline：解决频繁调用小函数大量消耗栈空间的问题；
2. volatile：表明类型变量可悲更改，不再优化，需要从如内存中重新读取。

## 5.8-深拷贝与浅拷贝

拷贝函数使用场景：

1. 一个对象以值的方式传入函数体；
2. 一个对象以值的方式从函数返回；
3. 一个对象需通过另一个对象进行初始化；

区别：

1. 浅拷贝：只是增加一个指针指向已存在的内存地址；
2. 深拷贝：增加一个指针，并且申请一个新的内存用于存放复制的对象。

## 5.9-派生类构造/析构函数调用顺序

1. 构造函数：先基后派；
2. 析构函数：先派后基。

## 5.10-数据成员初始化顺序

顺序：

1. 基类的静态变量或全局变量；
2. 派生类的静态变量或全局变量；
3. 基类的成员变量；
4. 派生类的成员变量。

## 5.11-static_cast, dynamic_cast, const_cast, reinpreter_cast区别

static_cast与dynamic_cast：

1. 发生时间不同，一个是static编译时，一个是runtime运行时；
2. static_cast为强制类型转换，不提供运行时的检查；
3. dynamic_cast用于转换指针和引用，不可用于转换对象，主要用于类层次间的上行和下行转换：
   1. 上行转换：B继承自A，由B转换为A；
   2. 下行转换：B继承自A，A转换为B；
4. 上行转换时，static_cast和dynamic_cast效果相同，下行转换时，dynamic_cast具有类型检查，更安全。

## 5.12-定义一个空类 编译器会做什么

1. 当用到相关函数时，编译器会去自动生成：默认构造函数、默认拷贝构造函数、默认拷贝赋值操作符、默认析构函数；
2. 所有自动生成的函数都是inline和public的。

## 5.13-哪些函数不能成为虚函数

1. 构造函数：假如子类继承基类构造函数，则子类对象将使用基类构造函数构造，而积累的构造函数并不知道自类的成员，不符合语义，且，多态是通过基类指针指向子类对象实现多态的，在对象构造之前，并没有对象产生，因此无法使用多态特性，是矛盾的；
2. 内联成员函数：内联函数在编译时展开，而虚函数是在运行时绑定的，两者相违背；
3. 静态成员函数：在编译时确定，无法动态绑定，不支持多态。

## 5.14-内联函数与宏定义的区别

1. 宏定义在于处理时把所有宏名用宏体替换，内联函数在编译时进行代码插入、展开、省去调用的开销；
2. 宏定义没有类型检查，内联函数满足函数的性质，如有返回值、参数列表等。

## 5.15-左值引用和右值引用

1. 左值引用要求右边的值必须能够取地址，如果不能取地址，可以使用常引用；

   1. 例：`const int &var = 10;`等价于

      1. ```c++
         const int temp = 10;
         const int &var = temp;
         ```

   2. 但常引用修饰后，不可以通过引用进行修改，只能进行读取；

2. 右值引用用来绑定到右值；

   1. 左值：可以取地址的，有名字的，非临时的值；
   2. 右值：不能取地址的，没有名字的，临时的值；
   3. 定义格式`类型 && 引用名 = 右值表达式;`
   4. 例：`int &&var = 10;`

## 5.16-substr用法

1. 目的：构建一个string；

2. 用法：s.substr(pos, n)：

   1. ```c++
      string s("testString");
      string newStr = s.substr(0, 6);
      ```

3. 注意：返回一个从pos开始，包含pos的n个字符，pos默认值为0，n默认值为s.size()-pos。

## 5.17-Switch to end of line in vi:

```shell
shift+G
```

## 5.18-Switch to end of line in normal command line:

```
ctrl+E
```

## 5.19-Switch to specific line in target file:

```
vi <file directory> +<n>
```

## 5.20-Look up for filesystems of disk:

```
df -h
```

## 5.21-Look up for files in disk:

```
du
```

## 5.22-Look up with letter case ignored:

```
grep -i
```

## 5.23-Look up for CPU info:

```
htop
```

## 5.24-Switch to start of line in normal command line:

```
ctrl+A
```

## 5.25-Delete one fragment in normal command line:

```
ctrl+W
```

## 5.26-Delete one line in vi:

double click D

## 5.27-Redo in vi:

double click U

## 5.28-or loop for batch processing 

```shell
for i in `docker image ls`; do echo "$i"; done
```

## 5.29-/dev/null and 2&>1

### 5.29.1-Notice
1.1 `/dev/null` is the null file. Anything written to it is discarded.
1.2 `2>` means "redirect standard-error" to the given file.
1.3 `2>/dev/null` means "throw away any error messages".
1.4 `1` is stdout. `2` is stderr.
1.5 `2>&1` means redirecting stderr to stdout.

### 5.29.2-Example(s)
``` bash
wget -O /dev/null baidu.com 2>&1 
```

### 5.29.3-Reference(s)
Sepehr SaminiSepehr Samini 95544 gold badges1111 silver badges1515 bronze badges, et al. “What Does "/Dev/Null’ Mean at the End of Shell Commands.” Stack Overflow, 1 Feb. 1960, https://stackoverflow.com/questions/13408619/what-does-dev-null-mean-at-the-end-of-shell-commands. 

# 6-Algorithms

## 6.1-Sorting algorithm

### 6.1.1-Quick Sort

#### How to do it...

Divide and conquer.

In each division, seperate the data into two parts. 

All elements in the first part should be all less than the elements in the second part.

Loop until the array is sorted.

#### How to code it...

```c++
int partition(int array[], int left, int right) {
  int pivot;
  if (left < right) {
    int low = left;
    int high = right;
    int key = array[left];
    
    while (low < high) {
      while (array[high] >= ket && low < high) {
				high--;
      }
      array[low] = array[high];
      while (array[low] <= array[high] && low < high) {
        low++;
      }
      array[high] = array[low];
    }
    pivot = low;
    array[pivot] = key;
  }
  return pivot;
} 
```

```c++
void QuickSort(int array[], int left, int right) {
	if (left < right) {
    int pivot = partition(array, left, right);
    QuickSort(array, left, pivot - 1);
    QuickSort(array, pivot + 1, right);
  }
}
```

#### How to improve it...

```c++
void QuickSortRandom(int array[], int left, int right) {
	if (left < right) {
    srand(unsigned(time(NULL)));
    int Tem = rand()%(right - left + 1) + left;
    swap(array[left], array[Tem]);
    int pivot = partition(array, left, right);
    QuickSortRandom(array, left, pivot - 1);
    QuickSortRandom(array, pivot + 1, right);
  }
}
```

### 6.1.2-Bubble sort

#### How to do it...

Compare the adjacent elements.

If the first element is greater than the second element, swap them.

Loop until reaching the last pair of elements.

Repeat until all the array is sorted.

#### How to code it...

```c++
void BubbleSort(int array[]) {
  for (int i = 0; i < array.length(); i++) {
  	for (int j = 0; i < array.length() - i; j++) {
			if (array[j] > array[j+1]) {
      	swap(array[j], array[j+1]);
    	}
  	}
	}
}
```

#### How to improve it...

We can make a judgement before we do the algorithm.

Check whether the array is already sorted or not.

```c++
void BubbleSortwithCheck(int array[]) {
	for (int i = 0; i < array.length(); i++) {
  	bool sorted = true;
  	for (int j = 0; j < length() - i; j++) {
			if (array[j] > array[j+1]) {
      	swap(array[j], array[j+1]);
      	sorted = false;
    	}
  	}
  	if (sorted) {
			break;
  	}
	}
}
```

# 7-K8s and docker

## 7.1-Management tools for clusters, pods, deployments, etc. : 

k9s

## 7.2-When not able to delete resources in k8s:

First edit resource:

```
kubectl edit <resource name>
```

then delete the `finalizer` part and try again.

## 7.3-filtering docker images

```shell
docker image "name*"
```

## 7.4-save and load docker images

```shell
docker image save > smartcity_images
docker image load < smartcity_images
```

## 7.5-getting k8s events

```
kubectl get events
```

# 8-VM related


## 8.1-List all VMs:

```shell
virsh list
```

## 8.2-List network setting xml:

```shell
virsh net-dumpxml <network>
```

## 8.3-list and revert vm from snapshots:
```shell
virsh snapshot-list 476
virsh snapshot-revert --domain freebsd --snapshotname 5Sep2016_S1 --running
```


# 1. C++的内存管理分哪些区，分别有什么作用

C++的内存主要分为五大区：堆区、栈区、自由存储区、全局/静态存储区、常量存储区。

**堆区**：程序员分配释放，使用new分配内存块，使用delete归还内存空间。

**栈区**：编译器自动分配释放，用于存放局部变量、函数参数等。

**自由存储区**：程序员分配释放，使用malloc分配内存块，使用free归还内存空间。

**全局区/静态区**：全局变量和静态变量分配在同一块内存中。

**常量存储区**：存放不可修改的常量值。

# 2. C++源文本到可执行文件需要经历哪些阶段

**预处理**：将源代码和相关头文件处理成一个.i文件。

**编译**：将预处理的文件进行词法分析、语义分析，优化后产生相应的汇编代码。

**汇编**：将汇编语言代码翻译成目标机器码。

**链接**：把每个机器码文件按照要求连接起来，解决代码间的相互依赖问题。

# 3. 析构函数为什么必须是虚函数

为了保证整个派生类的对象完全被释放。

当析构函数不为虚函数时，在删除基类指针时，只会调用基类析构函数，而不调用派生类的析构函数，这样会导致基类指针指向的派生类对象析构不完全。

当析构函数为虚函数时，在删除基类指针时，会调用该指针指向派生类的析构函数，同时派生类的析构函数自动调用基类析构函数，保证对象被完全释放。

# 4. 虚函数和纯虚函数有什么区别

**虚函数**：在基类中存在定义，可以直接使用，也可以被派生类重写后使用。

**纯虚函数**：在基类中不存在定义，只有声明，必须在子类中定义后才能使用。

# 5. 虚函数的实现机制

编译器自动为存在虚函数的类生成一个虚函数表，当声明该类的对象时，放入一个隐式指针变量，指向虚函数表。

在调用方法时，系统根据不同对象的指针，寻找到对应的虚函数表，进而找到所需的函数地址进行调用。

# 6.野指针怎么出现的

指针变量未初始化。

指针释放后未置空。

返回指向栈内存的指针。

# 7. 类和结构体有什么区别

class中默认成员访问权限为private，而struct中为public。

class可以用于表示模板类型，sruct不行。

class是引用类型，struct是值类型。

class多用来存储数据量大、逻辑复杂的对象，struct多用来存储轻量级对象。

class多用于表现抽象和多级别的对象层次。

# 8. 什么情况会导致内存泄漏

程序循环new创建出来的对象没有及时delete掉。

delete掉一个void*类型的指针，导致没有调用到对象的析构函数。

new创建了一组对象，回收时未调用delete[]，而调用了delete，导致只有对象数组的第一个对象的析构函数得到执行并回收了内存。

# 9. 五种IO模型

**阻塞IO**：进程发起IO系统调用后，进程被阻塞，转到内核空间处理，处理完毕后返回进程。

**非阻塞IO**：进程发起IO系统调用后，如果内核缓冲区没有数据，返回给进程一个错误，而不会阻塞进程，如果缓冲区有数据，则将数据返回给进程。【发起IO后，内核便开始处理，一直有返回值，但是直到内核处理完才有数据。】

**IO复用**：多个进程的IO注册到一个复用器（select）上，select监听所有进来的IO。【同时负责很多水龙头，哪个水龙头要来水了，就打开哪一个。】

**信号驱动IO**：进程发起IO系统调用后，向内核注册信号处理函数，然后进程返回不阻塞，当内核数据就绪则通知进程发起IO调用读取数据。【首先用信号通知内核空间，等到数据就绪再发起IO。】

**异步IO**：进程发起IO系统调用后，进程返回不阻塞，等内核将IO处理完，通知进程数据结果。

# 10. TCP如何保证传输的可靠性

**校验和**：接收方和发送方均进行校验和的计算，并进行对比。

**序列号**：TCP传输时将每个字节的数据都进行编号。

**确认应答**：TCP传输过程中，每次接收方收到数据后，均对传输方进行确认应答（ACK）。

**超时重传**：发送方在发送完数据后进行等待，一段时间后没有收到ACK，则对刚才的数据进行重新发送。

**连接管理**：三次握手与四次挥手。

**流量控制**：在回复ACK时，接收端介绍自己接受数据的缓冲区剩余大小。

**拥塞控制**：慢开始、拥塞避免等操作。

# 11. TCP快速重传的实现

举例：发送方发出1、2、3、4、5五份数据，1送到了，则回复ACK2，但是2没送到，3送到了，于是继续回复ACK2，后面4和5都送到了，继续回复ACK2，直到发送端收到三次ACK2，则重新发送2，然后接收端收到2，因为3、4、5都已经收到，所以回复ACK6。

# 12. 两个有序链表合并成一个(leetcode 21)

```c++
struct ListNode {
   int val;
   ListNode *next;
   ListNode(int x) : val(x), next(NULL) {}
};

ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
   if(l1 == NULL){
      return l2;
   }
   if (l2 == NULL){
      return l1;
   }
   if (l1->val < l2->val){
      l1->next = mergeTwoLists(l1->next, l2);
      return l1;
   }
   else {
      l2->next = mergeTwoLists(l1, l2->next);
      return l2;
   }
}
```

# 13. GET和POST的区别

GET所发送的数据是URL的一部分，POST数据不会显示在URL中。

GET和POST方法没有本质区别，只是报文格式不同，两者都使用HTTP，都是不安全的，想要安全传输需要使用HTTPS。

# 14. HTTPS的实现原理

HTTPS原理：在传输层（TCP）和应用层（HTTP）之间加了一层SSL/TLS。

具体加密过程：1. 服务器端发送公钥证书；2. 客户端检验证书是否有效，是，则生成一个随机密钥，并用服务端的公钥进行加密后发送；3. 服务器端用自己私钥加密，取出客户端的随机密钥，将需要发送的内容用该密钥加密并发送。

# 15. Linux查看最近的日志用什么指令

**tail**：

> tail -f test.log

**head**：

> cat test.log | tail -n +3000 | head -n 1000

**cat**：

> cat filename

**tac**：把cat的内容反写过来

> tac filename

**echo**：

> echo "the echo command test!"

# 16. hash冲突解决

**开放地址法**：再散列函数：

> Hi = (H(key) + di) % m, i = 1, 2, ..., n

不同di值对应不同散列方法。

**再哈希法**：同时构造多个不同的哈希函数，某一个发生冲突时计算下一个，直到冲突不再产生。

**链地址法**：将所有哈希地址为i的元素构成一个单链表。

**建立公共溢出区**：将哈希表分为基本表和溢出表，和基本表发生冲突的元素填入溢出表。

# 17. 快排的时间复杂度和空间复杂度

平均情况下快速排序的时间复杂度是O(nlgn)，最坏情况是n的平方，可通过随机算法避免最坏情况，或者可先求序列的中值，然后选取中值作为主元素。

由于递归调用，快排的空间复杂度是O(lgn)。

# 18. 堆排序的时间复杂度和空间复杂度

第一次建堆时间复杂度：O(n)。

更改元素时建堆时间复杂度：O(nlgn)。

堆排序平均时间复杂度：O(nlgn)。

空间复杂度：O(1)。

# 19. B树和B+树的定义

B树中每个节点的关键字都有data域。

B+树除了叶子节点，其他节点只有索引。

# 20. C++ vector里size和capacity的区别

size是当前vector容器的真实占用大小。

capacity是当前允许的最大元素数。

# 21. 计算机网络分层模型

> **7层** (osi国际标准组织定制)：

**应用层**：为程序提供网络服务。

**表示层**：数据格式化，加密、解密。

**会话层**：建立、维护、管理会话链接。

**传输层**：建立、维护、管理端到端链接。

**网络层**：IP寻址和路由选择。

**数据链路层**：控制网络层与物理层之间的通信。

**物理层**：比特流传输。

> **四层** (TCP/IP)：

**应用层**：ping、DNS、telnet

**传输层**：UDP、TCP

**网络层**：ICMP、IP

**数据链路层**：ARP、DataLink、RARP

# 22. HTTP请求包含哪几个部分

> **请求行**：

**请求方法**：HTTP最常见的请求方法为GET和POST。

**请求URL**：请求对应的URL地址。

**HTTP协议及版本**：协议名称及版本号。

> 请求头：

包含多个属性，格式为“属性名：属性值”，服务器根据请求头来获取客户端的信息。

> 请求体：

将一个页面表单中的组件值通过param1=value & param2=value2的键值对形式编码成一个格式化串，承载多个请求参数的数据。

# 23. TCP拥塞控制

主要为四个算法：

**慢开始**：在TCP链接刚建立时，一点一点地增大拥塞窗口cwnd，慢慢变为指数增长，试探网络的承受能力，直到cwnd大于等于ssthresh（slow start threshold）则进入**拥塞避免**。

**拥塞避免**：收到一个ACK，即每经过一个往返时间RTT，就把发送方的cwnd加1，使其按线性规律缓慢增长。

**乘法减小**【TCP Tahoe】：不论在慢开始阶段还是拥塞避免阶段，只要出现超时，即可能发生了阻塞，发生丢包，就把慢开始门限ssthresh的值减半，即设置为当前cwnd的一半，并开始执行**慢开始**算法。

**快速重传**【TCP Reno】：发生丢包时，把cwnd设置为当前的一半，ssthresh设置为缩小后的cwnd大小，进入**快速恢复**算法。

**快速恢复**【TCP Reno】：设置cwnd=cwnd+3*MSS（因为收到3个重复的ACK，所以加三个MSS），重传DACKs指定的数据包，如果再收到DACKs，则cwnd增加1，若收到新的ACK，表明重传包成功，退出快速恢复，将cwnd设置为ssthresh，进入**拥塞避免**算法。

# 24. 死锁与死锁的处理

> 形成死锁的四个必要条件：

**互斥**：在某段时间内某资源只由一个进程占用。

**持有并等待**：某进程已经持有一个或多个资源，但是还需请求其他资源，而它请求的资源不能立即获得，需要等待。

**不可抢占**：进程已经获取的资源在使用过程中不能被其他进程抢占，只能在使用完后，由该进程自己释放。

**环路等待**：形成进程和请求资源之间的环路。

> 死锁的预防：

**互斥**：不易预防

**占有并等待**：方法一：不持有并等待，如果一个进程一次请求获取不了所有资源，那么它不可占用任何资源，即释放掉它已经占有的资源；方法二：持有不等待，保证资源充足，只要请求资源，就分配给资源。

**不可抢占**：如果一个进程所请求的资源被另一进程占有，使它可以抢占另一进程占有的资源。

**环路等待**：对资源进行排序，每个进程按照固定的顺序访问资源。

> 死锁的避免：

**资源请求图算法**：利用资源分配图，引入需求边表示进程可能在将来某个时候申请资源，只有申请边变为分配边而不会导致资源分配图形成环时，才允许申请。

**银行家算法**：当新进程进入系统，系统对其所需资源的最大数量进行统计，若超过当前资源综合，则该进程必须等待直到其他进程释放资源。

# 25. 什么是关系型数据库

关系型数据库建立在关系型数据模型的基础上，借助于集合、代数等数学概念和方法来处理数据的数据库。

# 26. KV存储

举例：Redis、MongoDB

不经常更新的、重要的数据一般使用关系数据库存储。

数据结构简单、有分布式数据存储的需求使用KV数据库。

# 27. 非递归前中后序遍历二叉树

```c++
struct TreeNode {
  int val;
  TreeNode * left;
  TreeNode * right;
};

void PreOrder (TreeNode * root) {
  stack<TreeNode *>s;
  TreeNode * ptr = root;
  
  while (ptr != nullptr || !s.empty()) {
    if (ptr != nullptr) {
      cout << ptr->val << endl;
      s.push(ptr);
      ptr = ptr->left;
    }
    else {
      ptr = s.top();
      s.pop();
      ptr = ptr->right;
    }
  }
}

void InOrder (TreeNode * root) {
  stack<TreeNode *> s;
  TreeNode * ptr = root;
  
  while (ptr != nullptr || !s.empty()) {
    if (ptr != nullptr) {
      s.push(ptr);
      ptr = ptr->left;
    }
    else {
      ptr = s.top();
      cout << ptr->val << endl;
      s.pop();
      ptr = ptr->right;
    }
  }
}

void PostOrder (TreeNode * root) {
  stack<TreeNode *> s;
  TreeNode * ptr = root;
  TreeNode * TemNode = nullptr;
  
  while (ptr != nullptr || !s.empty()) {
    if (ptr != nullptr {
      s.push(ptr);
      ptr = ptr->left;
    }
    else {
      ptr = s.top();
      if (ptr->right != nullptr && ptr->right !- TemNode){
        ptr = ptr->right;
      }
      else {
        cout << ptr->val << endl;
        s.pop();
        TemNode = ptr;
        ptr = nullptr;
      }
    }   
  }
}
```

# 28. 如何实现一个栈

```c++
class QueueStack {
private:
  queue<int> first;
  queue<int> second;
  
public:
  bool empty() {
		if (first.empty() && second.empty()){
      return true;
    }
    else {
      return false;
    }
  }
  
  int top() {
    if (first.empty()){
      return second.front();
    }
    else {
      return first.front();
    }
  }
  
  void pop() {
    if (first.empty()) {
      second.pop();
    }
    else {
      first.pop();
    }
  }
  
  void push (int x){
    if (frist.empty()){
      first.push(x);
      while (!second.empty()) {
        first.push(second.front());
        second.pop();
      }
    }
    else {
      second.push(x);
      while(!first.empty()) {
        second.push(first.front());
        first.pop();
      }
    }
  }
}
```

# 29. HTTP状态码

> 1xx：收到请求，需要请求者继续操作。

**100**：继续。

**101**：切换协议。

> 2xx：操作被成功接收并处理。

**200**：请求成功。

**201**：已创建。

**202**：已接受。

**203**：非授权信息。请求成功。

**204**：无内容。

**205**：重置内容。

**206**：部分内容。

> 3xx：重定向，需要进一步操作以完成请求。

**300**：多种选择。

**301**：永久移动。

**302**：临时移动。

**303**：查看其他地址。

**304**：未修改。

**305**：使用代理。

**307**：临时重定向。

> 4xx：客户端错误，请求包含语法错误或无法完成请求。

**400**：Bad Request。

**401**：Unauthorized。

**403**：服务器理解客户端的请求，但是拒绝执行。

**404**：无法根据请求找到资源。

**405**：客户端请求中的方法被禁止。

**406**：Not Acceptable。

**407**：Proxy Authentication Required。

**408**：Request Timeout。

**409**：服务器处理请求时发生了冲突。

**410**：客户端请求的资源已经不存在。

**411**：Length Required。

**412**：Precondition Failed。

**413**：Request Entity Too Large。

**414**：Request URI Too Large。

**415**：Unsupported Media Type。

**416**：客户端请求的范围无效。

**417**：Expectation Failed。

> 5xx：服务器错误，服务器在处理请求的过程中发生了错误。

**500**：服务器内部错误，无法完成请求。

**501**：服务器不支持请求的功能。

**502**：Bad Gateway.

**503**：Service Unavailable.

**504**：Gateway Timeout.

**505**：HTTP version not supported.

# 31. 黑盒测试和白盒测试

> 黑盒测试：即功能性测试

**等价类划分**：有效等价类即对于程序的规格来说是合理的、有意义的；无效等价类即对程序的规格来说是不合理的、每有意义的。

**边界值分析**：对各种边界情况设计测试用例。

**因果图法**：根据输入的各种组合来设计测试用例，用于检查程序输入条件的各种组合情况。

**场景法**：通过对正常场景和中断操作的场景进行实验来完成测试。

> 白盒测试：即结构测试或逻辑驱动测试

**静态测试**：代码检查、结构分析、文档测试等。

**动态测试**：功能确认、接口测试、性能分析等。

# 31. 单元测试、集成测试和系统

**单元测试**：对函数、类的某一个方法等基本单元进行正确性检验的测试。

**集成测试**：对组装好的模块进行功能性验证的测试。

**系统测试**：对继承好的软件作为计算机系统的一部分与外围设备或支持性软件一起进行的实际测试。

# 32. 如何设计测试用例

利用**1.**中方法进行分析设计，需要包含用例编号、用例标题、功能模块名称、前置条件、输入数据、操作步骤、预期结果、优先级、执行结果、编写人、执行人、其他补充。

# 33. 如何测试微信的点赞功能

> 功能测试

点赞朋友圈，是否成功。

取消点赞，是否成功。

多次点赞，有何结果。

多人点赞，以何顺序呈现。

> 接口测试

被点赞人能否收到消息。

点赞人能否收到后续消息。

> 性能测试

点赞后，结果显示时间是否符合规范。

> 兼容测试

在安卓、ios上点赞，结构是否有差异。

> 可用性测试

网络连接不稳定时，点赞的结果。

# 34. MySQL查询10-20条的数据

```mysql
select * from table limit 10, 20
```

# 35. 查找二叉树最大深度

```c++
struct TreeNode {
  int val;
  TreeNode * left;
  TreeNode * right;
  TreeNode(int x) : val(x), left(NULL), right(NULL){}
};

int dfs (TreeNode * root, int result) {
  if (!root) {
    return result;
  }
  int left_res = dfs(root->left, result + 1);
  int right_res = dfs(root->right, result + 1);
  return max(left_res, right_res);
}

int MaxDepth(TreeNode * root) {
	int result = 0;
  return dfs(root, result);
}
```

# 36. 判断IP地址是否合法

```c++
using namespace boost::xpressive;  
bool CheckIP(char *ip) {  
	cregex expression = cregex::compile("(25[0-4]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[1-9])[.](25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[0-9])[.](25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[0-9])[.](25[0-4]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[1-9])");   
	return regex_match(ip, expression);  
}  

```

# 37. udp如何实现可靠连接

在应用层参照TCP实现超时重传、有序接受、应答确认、滑动窗口、流量控制等功能。

现已实现的程序有RUDP、RTP、UDT。

# 38.MySQL 查询以135开头的手机号

```mysql
select * from test where shouji like '135%';
```

# 39. Linux和端口号、进程、文件相关的命令

**静态进程查看**: ps

例：通过进程名查看进程号

```shell
ps ax | fgrep [进程名]
```

**网络查看**: netstat

例：通过进程号查看进程正在监听的端口

```shell
netstat -antp | fgrep [进程号]
```

例：查看端口是否正在监听

```shell
netstat -antp | grep [端口号]
```

**搜索指定文件内容**: grep (global regular expression print)

例：搜索as在123.txt中的行号位置

```shell
grep -n as 123.txt
```

# 40. 查找二叉树最大深度

```c++
struct TreeNode {
  int val;
  TreeNode * left;
  TreeNode * right;
  TreeNode(int x) : val(x), left(NULL), right(NULL){}
};

int dfs (TreeNode * root, int result) {
  if (!root) {
    return result;
  }
  int left_res = dfs(root->left, result + 1);
  int right_res = dfs(root->right, result + 1);
  return max(left_res, right_res);
}

int MaxDepth(TreeNode * root) {
	int result = 0;
  return dfs(root, result);
}
```

# 41. 判断IP地址是否合法

```c++
using namespace boost::xpressive;  
bool CheckIP(char *ip) {  
	cregex expression = cregex::compile("(25[0-4]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[1-9])[.](25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[0-9])[.](25[0-5]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[0-9])[.](25[0-4]|2[0-4][0-9]|1[0-9][0-9]|[1-9][0-9]|[1-9])");   
	return regex_match(ip, expression);  
}  

```

# 42. udp如何实现可靠连接

在应用层参照TCP实现超时重传、有序接受、应答确认、滑动窗口、流量控制等功能。

现已实现的程序有RUDP、RTP、UDT。

# 43.MySQL 查询以135开头的手机号

```mysql
select * from test where shouji like '135%';
```


