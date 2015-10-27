<h2 id="DataBase">简介</h2>

* [MySql](#MySql)
* [Oracle](#Oracle)
* [Sqlite](#Sqlite)

<h3 id="mysql">MySql</h3>

    MySQL客户端和服务器之间的通信协议是“半双工的”
    向MySQL发送一个请求的时候，MySQL到底做了什么：
    1. 客户端发送一条查询给服务器
    2. 服务器先查询缓冲，如果命中了缓存，则立刻返回缓冲的结果，否则进入下一阶段
    3. 服务器进行SQL解析、预处理，再由服务器生成对应的执行计划
    4. MySQL根据优化器生成的执行计划，调用存储引擎的API来执行查询。
    5. 将结果返回给客户端

 *   [MySql](/DB/MySql/README.md)
    
<h3 id="oracle">Oracle</h3>

    Oracle
    
 <h3 id="sqlite">Sqlite</h3>

    Sqlite
