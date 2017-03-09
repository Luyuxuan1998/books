# books
第一个在github上的项目，也是我的毕业设计，一个图书管理、借阅、销售网站。使用`vue-router`作为路由管理，`isomorphic-fetch`请求接口，`element-ui`作为样式库。后端使用`php`+`mysql`，并配置好了`sh`脚本方便直接部署在服务器上。

> 该项目从 2016-3 开始，那个时候还是`vue 1.0`而且还没有`element-ui`，所以现在是正在将代码迁移到`vue2.0`，暂时只完成了部分。

## 使用

先将代码下载
```bash
git clone https://github.com/ltaoo/books.git
```

会在当前目录生成`books`文件夹，进入该文件夹安装依赖
```bash
npm i
```

安装依赖完成后需要使用 docker 运行 php 容器和 mysql 容器提供接口，进入`books/database`文件夹，首先是构建镜像：
```bash
docker build -t bookshop .
```

运行数据库容器与 php 容器：
```bash
./start.sh
```

开启名为`books`的`php`容器和名为`books_db`的`mysql`容器，再初始化数据表
```bash
docker exec -i books_db mysql -uroot -p123 bookshop < setup.sql
```

然后就可以运行前端开发服务器了
```bash
npm run dev
```

## 功能

### 后台

#### 管理员登录

进入`http://localhost:8080/#/adminLogin`，使用`admin`，`123456`登陆后台。

### 书籍管理
登陆后台后可以进入"书籍列表"添加新书籍，点击"添加新书籍"，输入书籍名称或者 ISBN 码搜索后添加。
添加书籍成功后可以在前台首页与书籍列表页看到新添加的书籍。

#### 会员管理

登录后台后可以进入"会员列表"添加新会员，同上。可以使用新增加会员的**学号**和**联系方式**作为前台登录用户名和密码进行登录。

#### 书籍借阅

在后台首页，首先查询好会员，再查询需要借阅的书籍，点击借阅即可生成借阅记录。

#### 借阅记录管理

用户借了书后，会生成对应的借阅记录，可以直接在后台看到应还时间，计算规则为：
- 如果用户是周卡，则应还时间为借阅时间 + 7天
- 如果用户是月卡，应还时间为借阅时间 + 30天
- 如果用户为期卡，没有应还时间
- 如果用户已还，则显示已还

#### 书籍归还

可以在后台还书页，使用会员名、书籍名、书籍 ISBN 码进行查询借阅记录，并选择相应记录进行归还操作。

### 前台

#### 用户登录

在前台首页点击"用户中心"使用`123456`和`123456`即可登录。


## 正在完善

- 添加到购物车
- 结算
- 订单列表
- 用户中心



