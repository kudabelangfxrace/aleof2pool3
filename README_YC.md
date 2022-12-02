# Aleo使用手册

## 系统

安装系统版本Ubuntu 18.04-20.04,server版，不带GUI组件

## GPU

- NVIDIA(N卡): 驱动版本515及以上(例：515.78)

## 软件参数

    -g, --cuda          GPU 卡序号,从0开始“,”隔开；GPU显卡的驱动最好11.7的版本（无GPU时忽略）
    -p, --pool          矿池地址 
    --account_name      矿池用户名 [默认: accountname]
    --miner_name        矿池矿机名 [默认: minername]

## 启动命令

- 修改aleo.sh文件中`ACCOUNT_NAME=accountname`，将`accountname`设置为你的鱼池账号名称
- 修改aleo.sh文件中`POOL="xxx.xxx.xxx.xxx:xxxx"`，将`xxx.xxx.xxx.xxx:xxxx`设置为你的[stunnel](#stunnel安装)的代理地址。
- 启动软件`chmod +x aleo.sh && ./aleo.sh`

## 查看日志

- 版本号 1.0.0
- 产值
  - 1m:表示最近1分钟内，平均每秒产生的prover_solution个数
  - 5m:表示最近5分钟内，平均每秒产生的prover_solution个数
  - perf:后面跟着的数字表示，产生的prover_solution总个数

## stunnel安装

1. ubuntu 安装命令`sudo apt-get install stunnel4`

2. stunnel 配置文件

```
  cat <<EOF | sudo tee /etc/stunnel/stunnel.conf deb 
  client=yes
  pid=/etc/stunnel/stunnel.pid
  debug=7
  foreground=no
  verify=0

  [aleoclient]
  accept=13131
  connect=47.243.33.212:3350
  EOF
```

3. stunnel 启动:
  - 查看安装信息：`whereis stunnel`

```
stunnel: /usr/bin/stunnel /usr/lib/aarch64-linux-gnu/stunnel /etc/stunnel /usr/share/man/man8/stunnel.8.gz
```

- 启动stunnel：`sudo stunnel`

- 查看stunnel进程：`ps -ef|grep stunnel`
  
```
root        6818    1449  0 15:15 ?        00:00:00 stunnel
```

- 验证本地13131端口：`telnet localhost 13131`

```
Trying 127.0.0.1...
Connected to localhost.
Escape character is '^]'
```