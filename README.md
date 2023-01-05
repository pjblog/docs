# PJBlog 情怀版

`PJBlog Feelings` 一套历史20年的博客程序开启全新之旅。程序采用nodejs作为服务端，通用的前端技术作为客户端，以简洁轻量方便为主旨构建的强大的博客系统。

## 前期准备

当你使用PJBlog搭建一整套完整博客程序的时候，你需要准备以下的资源：

1. 一个服务器 (linux或者window server都可以，官方推荐linux)
1. 一个数据库 (`mysql` `mssql` `mongodb` `oracle` `postgres`其中之一)
1. 一个Nodejs环境
1. 一个Redis（可选，博客内置文件缓存，如果需要提升博客性能的话，建议使用redis）

与大众的独立博客程序相同，一般地，只需要一个服务器+一个数据库即可满足。

## 安装

第一步，安装过程采用命令行方式。你所需要做的是使用官方提供的工具。

```bash
npm i -g @pjblog/cli
```

第二步，选择你需要安装的目录，创建一个博客目录，并且进入此目录。

```bash
evioshen@shenyunjiedeMBP test % mkdir pjblog && cd pjblog && pwd
/Users/evioshen/code/test/pjblog
evioshen@shenyunjiedeMBP pjblog % 
```

- `mkdir pjblog` 用户创建`pjblog`博客目录
- `cd pjblog` 进入目录
- `pwd` 查看当前目录路径

第三步，初始化博客。

```bash
pjblog init
```

根据提示一步步配置博客即可。

```bash
evioshen@shenyunjiedeMBP pjblog % pjblog init
? 数据库类型 MySQL
? 数据库地址 127.0.0.1
? 数据库端口: 3306
? 数据库名称 pjblog
? 数据库用户名 root
? 数据库密码 ******
? 数据库表前缀 pjblog_
? 缓存模式 文件缓存
? 博客启动端口 8866
? 管理员账号 admin
? 管理员密码 admin888
```

工具会自动安装博客直到出现

```bash
[PJBlog] › ✔  success   [4/4] - 安装成功
```

表示博客安装成功。

第四步，启动博客。

```bash
pjblog start
```

启动完毕后会提示以下信息，表示已启动的模块。

```bash
evioshen@shenyunjiedeMBP pjblog % pjblog start
2023-01-05T10:55:46.170Z info: Cache.File Initialized.
2023-01-05T10:55:46.178Z info: Tags initialized.
2023-01-05T10:55:46.179Z info: Http Initialized. Port:8866
2023-01-05T10:55:46.374Z info: TypeORM Initialized.
2023-01-05T10:55:46.378Z info: User initialized.
2023-01-05T10:55:46.379Z info: Configs initialized.
2023-01-05T10:55:46.380Z info: Category initialized.
2023-01-05T10:55:46.485Z info: Markdown Initialized.
2023-01-05T10:55:46.486Z info: Article initialized.
2023-01-05T10:55:46.488Z info: Widgets initialized.
```

当然，如果需要进程守护，可以使用`pm2`来进行进程守护。

```bash
npm i -g pm2
pm2 start pjblog -- start
```

我们可以通过`pm2 list`查看是否已启动和状态

```bash
pm2 list
┌────┬────────────────────┬──────────┬──────┬───────────┬──────────┬──────────┐
│ id │ name               │ mode     │ ↺    │ status    │ cpu      │ memory   │
├────┼────────────────────┼──────────┼──────┼───────────┼──────────┼──────────┤
│ 0  │ pjblog             │ fork     │ 0    │ online    │ 0%       │ 14.3mb   │
└────┴────────────────────┴──────────┴──────┴───────────┴──────────┴──────────┘
```

至此，博客已启动，我们最后需要做的事情是将本地的端口反向代理，供域名使用。一般我们使用`nginx`来做反向代理。我们可以参考这篇文章来做 [https://blog.csdn.net/weixin_42751488/article/details/124165105](https://blog.csdn.net/weixin_42751488/article/details/124165105)。

## 贡献

PJBlog是一个老牌的独立博客程序。从ASP语言迁移到Nodejs过程中提升了很大的性能，同时也提供了很多可扩展的能力。希望志同道合的朋友可以一起来维护这套程序。如果觉得这套程序不错，请给个star。