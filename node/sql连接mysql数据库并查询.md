## 实现功能

连接mysql数据库同时对查询执行封装。

## 具体代码

* 配置信息

```
config = {
    "host": "localhost",
    "port": "3306",
    "user": "root",
    "password": "lykmysql1",
    "database": "first"
}
```

* 查询逻辑封装
```
const mysql = require('mysql');
const wrapper = require('co-mysql');
const mysqlConfig = require('../config/mysql');

class mysqlClient {
    constructor() {
        this.createConnect();
    }
    /**
     * 创建数据库连接
     */
    createConnect() {
        const pool = mysql.createPool(mysqlConfig);
        this.p = wrapper(pool);
    }
    /**
     * 数据库查询接口
     * @param  {[type]} table   数据库表名
     * @param  {[type]} columns 需要查询的数据列
     * @param  {[type]} sql     查询条件
     */
    query(table, columns, sql) {
        var oThis = this;
        var querySql = 'SELECT ' + columns + ' from ' + table;
        if (sql) {
            querySql = querySql + ' where ' + sql;
        }
        return this.p.query(querySql);

    }

}
```

* 执行查询
```
var rows = await server.query('user', '*', 'id = ' + id);
```

## 代码来源

[git地址](https://github.com/easy-templates/koa2-demo)
