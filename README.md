# NetScan - IP/URL存活检测工具

## 程序简介

这是一个高效的IP和URL存活检测工具，支持批量检测、端口扫描和Web标题获取功能。

## 功能特点

- 支持单个IP地址、IP子网(CIDR格式)和URL检测
- 支持从文件读取多个IP地址或URL批量检测
- 支持自定义线程数，提高检测效率
- 支持端口扫描功能：
  - 使用-p参数扫描指定端口，多个端口用逗号分隔
  - 支持常用Web端口自动检测
- 支持Web标题获取功能（--include_titles参数）
- 支持敏感标题识别与红色标记（自动识别登录、admin、OA、后台等敏感内容）
- 检测结果自动保存到文本文件
- 支持Python 3环境运行

## 使用方法

### 基本语法

```bash
NetScan.exe [参数]
```

### 可用参数

- `-i, --host`：指定单个IP地址或CIDR格式的子网进行检测(如192.168.1.1或172.16.16.0/24)
- `-hf, --host_file`：指定包含IP地址的文本文件，每行一个IP
- `-u, --url`：指定单个URL进行检测
- `-uf, --url_file`：指定包含URL的文本文件，每行一个URL
- `-t, --threads`：指定线程数，默认500，最大值为检测的目标数量
- `-p, --ports`：指定要扫描的端口，多个端口用逗号分隔，如：80,443,8080
- `--include_titles`：获取Web服务的标题信息
- `--port_timeout`：设置端口扫描的超时时间（秒），默认2秒
- `--help`：显示完整的帮助信息并退出

### 示例

1. 检测单个IP地址：

   ```bash
   NetScan.exe -i 192.168.1.1
   ```

2. 扫描整个子网（如C段）：

   ```bash
   NetScan.exe -i 172.16.16.0/24
   ```

3. 从文件中读取IP地址进行检测：

   ```bash
   NetScan.exe -hf ip.txt
   ```

4. 自定义线程数进行检测：

   ```bash
   NetScan.exe -hf ip.txt -t 300
   ```

5. 检测指定端口：

   ```bash
   NetScan.exe -hf ip.txt -p 80,443,8080
   ```

6. 检测IP并获取标题：

   ```bash
   NetScan.exe -i 192.168.1.1 -p 80,443 --include_titles
   ```

7. 检测单个URL：

   ```bash
   NetScan.exe -u https://www.example.com
   ```

8. 从文件检测多个URL并获取标题：

   ```bash
   NetScan.exe -uf url.txt -t 100 --include_titles
   ```

9. 查看完整帮助信息：

   ```bash
   NetScan.exe --help
   ```

## 文件说明

- `NetScan.exe`：编译好的可执行程序
- `README.md`：使用说明文档

## 敏感标题识别

程序会自动识别以下类型的敏感标题并标记为红色：

- 登录相关：登录、login、logon、auth、认证、验证
- 管理相关：admin、管理员、管理、后台、控制台、console、dashboard
- OA系统：OA、办公自动化
- 用户相关：user、用户、账号、账户
- 系统相关：system、setting、配置

## 注意事项

1. 端口扫描和标题获取功能可能需要较长时间，特别是检测大量目标时
2. 扫描大量IP地址或URL时，建议适当调整线程数
3. 某些网络环境下，ICMP协议(ping)可能被禁用，此时工具会尝试使用TCP连接进行检测
4. 检测结果会保存在以日期时间命名的文本文件中
5. 请确保您有适当的授权进行网络扫描活动
