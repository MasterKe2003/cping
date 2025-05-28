# CPing

CPing 是一个基于 systemd 的持续 ping 监控工具，支持按时间段监控和全天候监控。

## 功能特点

- 支持多 IP 地址监控
- 支持全天候监控和时间段监控
- 基于 systemd 服务管理
- 实时日志记录
- 监控状态实时查看
- 支持成功/失败日志分离

## 系统要求

- Linux 系统（支持 systemd）
- bash shell
- root 权限
- jq 工具（用于 JSON 处理）

## 安装

1. 下载脚本：
```bash
git clone https://github.com/MasterKe2003/cping.git
cd cping
```

2. 安装服务：
```bash
bash cping install
```

安装过程会：
- 创建必要的目录（/etc/cping、/var/log/cping）
- 创建默认配置文件
- 安装 systemd 服务
- 设置适当的权限

## 配置文件

配置文件位置：`/etc/cping/config.json`

默认配置示例：
```json
{
    "ips": [],
    "time_ranges": [
        "08:00-12:00",
        "14:00-18:00"
    ]
}
```

## 使用方法

### 服务管理

```bash
# 启动服务
systemctl start cping

# 停止服务
systemctl stop cping

# 重启服务
systemctl restart cping

# 查看服务状态
systemctl status cping

# 设置开机自启
systemctl enable cping

# 取消开机自启
systemctl disable cping
```

### IP 管理

```bash
# 添加按时间段监控的 IP
cping add 192.168.1.1

# 添加全天候监控的 IP
cping add 192.168.1.2:true

# 批量添加 IP
cping add 10.0.0.1 10.0.0.2:true 10.0.0.3

# 删除指定 IP
cping del 192.168.1.1

# 删除所有 IP
cping del all
```

### 状态查看

```bash
# 查看监控状态
cping status

# 查看成功日志
cping status success

# 查看错误日志
cping status error
```

## 日志文件

- 主日志目录：`/var/log/cping/`
- 每个 IP 的日志存放在独立目录中：
  - 成功日志：`/var/log/cping/<ip>/success.log`
  - 错误日志：`/var/log/cping/<ip>/error.log`

## 注意事项

1. 需要 root 权限运行
2. 添加或删除 IP 后需要重启服务：`systemctl restart cping`
3. 全天候监控的 IP 不受时间段限制
4. 时间段监控的 IP 只在配置的时间范围内进行监控

## 卸载

```bash
cping uninstall
```
卸载时可选择是否保留配置文件和日志。

## 维护

```bash
# 更新服务
cping update

# 重新加载配置
systemctl restart cping
```

## 作者

@MasterKe(http://masterke.cn)

## 源码

https://github.com/MasterKe2003/cping

## 许可证

MIT License
