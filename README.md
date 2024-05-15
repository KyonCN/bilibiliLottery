## 转发动态原理

爬取某个用户的页面来转发动态。支持多人，获取数据跟着转发，前提条件是这个人只转发抽奖，并且重复度不高。

## 活动抽奖原理

抓取up主转发抽奖娘更新的最新抽奖列表。

## 日志报错

如果出现日志报错，只要程序没有中断，就可以忽略。

# 使用方法

## 第一步：修改config.ini配置

| 配置项        | 说明                  |
|------------|---------------------|
| **cookie** |
| csrf       | 自己的bili_jct         |
| sess_data  | 自己的SESSDATA         |
| uid        | 自己的uid              |
| **data**   |
| host_uid   | ta人uid，多个uid用英文逗号隔开 |
| sync_dynamic_interval   | 同步动态时间间隔，默认5分钟      |
| forward_interval   | 转发动态时间间隔，默认43分钟     |
| **mysql**  |
| host   | 自己本地的mysql          |
| user       | 账号                  |
| pwd        | 密码                  |
| name        | 数据库名称               |
| **log**   |
| path       | 日志路径，写绝对路径          |

如果是自己编译的，还需要更改`env.go`文件里的`viper.AddConfigPath("/files/go/bilibiliLottery/config")`配置文件路径。

## 第二步：运行初始化命令

```bash
go run main.go -init
```

## 注意事项

- 转盘抽奖一天获取一次，并且根据获取到的抽奖次数进行抽奖，一天运行一次即可；
- 可以自己编译运行，`go build main.go`，注意更改`env.go`文件里的`viper.AddConfigPath("/files/go/bilibiliLottery/config")`配置文件路径。

# 可用命令

以下是可用的命令列表：

- 初始化命令
```bash
go run main.go -init
```
- 扫码登录，该功能只是为了方便自己cookie过期后更换
```bash
go run main.go -login
```
- 开始转盘抽奖
```bash
go run main.go -draw
```
- 开始转发
```bash
go run main.go -start
```
- 删除动态，该功能默认删除第二页数据第一条，原因是有些抽奖工具是根据动态数量判断的，所以定期删掉一些动态
```bash
go run main.go -del
```
- 批量取关up，从后往前取关
```bash
go run main.go -cancel-modify
```

