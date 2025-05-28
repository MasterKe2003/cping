# CPing - IP监控工具

CPing 是一个用于监控多个IP地址的bash脚本工具，支持配置监控时间段，可以同时监控多个IP地址。

## 功能特点

- 支持配置多个监控时间段
- 支持同时监控多个IP地址
- 支持动态添加/删除监控IP
- 自动记录监控日志
- 支持启动/停止/重载配置
- 支持查看监控状态
- 支持查看监控日志
- 为每个IP单独记录日志

## 安装

1. 将脚本复制到任意目录：
```bash
cp cping /path/to/your/directory/
chmod +x cping
```

2. 脚本会自动创建必要的目录和文件：
- `config.conf` - 配置文件
- `log/` - 日志目录
  - `cping.log` - 总日志文件
  - `IP地址/` - 每个IP的日志目录
    - `success.log` - 成功记录
    - `error.log` - 失败记录
- `cping.pid` - 进程ID文件

## 使用方法

### 基本命令

- 启动监控：
```bash
sudo ./cping start
```

- 停止监控：
```bash
sudo ./cping stop
```

- 重载配置：
```bash
sudo ./cping reload
```

- 查看状态：
```bash
sudo ./cping status
```

### 查看日志

- 查看所有日志（默认显示最近50行）：
```bash
sudo ./cping log
```

- 查看成功的监控记录：
```bash
sudo ./cping log success
```

- 查看失败的监控记录：
```bash
sudo ./cping log error
```

- 查看特定IP的监控记录：
```bash
sudo ./cping log ip 192.168.1.1
```

- 指定显示行数（例如显示最近100行）：
```bash
sudo ./cping log success 100
```

### 管理监控IP

- 添加监控IP：
```bash
sudo ./cping add 192.168.1.1
```

- 删除监控IP：
```bash
sudo ./cping del 192.168.1.1
```

### 配置监控时间段

设置监控时间段（使用24小时制）：
```bash
sudo ./cping time 07:00 11:00
sudo ./cping time 12:00 18:00
```

## 配置文件

配置文件位于脚本同目录下的 `config.conf`，格式如下：

```
IP=192.168.1.1;192.168.1.2;192.168.1.3
TIME_RANGE=07:00,11:00;12:00,18:00
```

## 状态查看

使用 `status` 命令可以查看以下信息：
- 监控服务的运行状态
- 当前监控的IP地址列表
- 配置的监控时间段
- 当前是否在监控时间段内
- 最近的监控日志记录

## 日志查看

使用 `log` 命令可以查看以下信息：
- 所有监控记录
- 仅显示成功的监控记录
- 仅显示失败的监控记录
- 特定IP的监控记录
- 可以指定显示的行数

## 日志结构

监控日志保存在脚本目录下的 `log` 目录中：
- `log/cping.log` - 所有监控记录的总日志
- `log/IP地址/success.log` - 每个IP的成功记录
- `log/IP地址/error.log` - 每个IP的失败记录

日志文件使用追加模式，重启不会清空历史记录。每个IP的日志包含：
- 监控启动/停止时间
- IP地址可达性状态
- 配置更改记录

## 注意事项

1. 脚本需要root权限运行
2. 时间格式必须为24小时制（HH:MM）
3. IP地址格式必须正确
4. 建议定期检查日志文件大小
5. 所有文件都保存在脚本所在目录下
6. 每个IP的日志单独保存，方便查看和分析
