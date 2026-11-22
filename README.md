# 我的图书数据库作业

## 环境
- MySQL 版本：8.4
- 本地安装 / Docker：Docker
- 数据库名称：`bookshop`

## 从空库复现
1. 克隆本仓库
2. 在本仓库目录运行 `docker compose up`，启动 MySQL 服务器
3. 复制 `.env.example` 为 `.env`，并在其中填入用户名和密码
4. 连接到 3306 端口的 MySQL 服务器
5. 依次执行 `sql` 文件夹的 4 个 SQL 文件

## 设计解释
- 主键为什么存在：用来唯一地识别一行数据；如果没有主键，外键也没法声明，就无法表达表间关系
- 外键引用哪张表的哪一列：`books.author_id` 外键引用 `authors` 表的 `id` 列
- 价格为什么选择这个类型：用 decimal 存储小数，并指定共8位，2位小数，避免精度丢失

## 主键和外键

主键是用作行的唯一身份的键，必须是 `NOT NULl` 且 `UNIQUE` 的；而外键表示一种指向关系，从某一行指向另一个表的唯一键。

## 六道题的预期结果

见 [sql/03-queries.sql](sql/03-queries.sql)。

## 排错或边界验证

在 CachyOS 上安装 docker 时，执行 `sudo pacman -S docker` 无法安装，因为过久未进行系统更新，镜像已经删除了较旧版本的 docker。执行 `sudo pacman -Sy docker` 依然无法安装，因为存在冲突。于是只能执行 `sudo pacman -Syu docker`，安装后发现 docker 无法启动。使用 `journalctl -xeu docker.service` 查看错误原因，发现是因为 `xt_addrtype` 模块无法被找到。于是想到可能是因为 `pacman -Syu` 同时更新了内核，重启系统后即可正常使用 docker。

## AI 辅助使用说明

`docker-compose.yml` 由 AI 辅助编写。
