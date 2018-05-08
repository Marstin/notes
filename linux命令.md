## <font color=red text-align=center>linux常用命令</font>
### 文件操作
 * #### 删除
```
rm
    -f 强制进行操作
    -u 递归进行操作
    -i 删除前先询问用户
    -r/R 递归操作
    --preserve -root 不对根目录进行递归操作
    -v 显示指令的详细执行过程
```

 * #### 移动
 ```
 mv
 ```
 * #### 复制
```
scp 远程复制 username@ip:path
cp 直接复制
```
* * *
### ip命令
* #### 查看
```
ifconfig 全局查看
```
* #### 临时
```
ifconfig eth0 192.168.1.155 netmask 255.255.255.0
    #eth0 网卡名称
    #192.168.1.155 ip地址
    #255.255.255.0 网关
    即时生效，重启失效
vim /etc/network/interfaces
ifdown eth0
ifup eth0
    ubuntu修改网络配置文件，需要重启网卡
```

### 用户  <font color=grey size=4>(管理员权限)</font>
```
useradd {$username} 新增用户
passwd {$username} 设置密码
```

### 授权  <font color=grey size=4>(管理员权限)</font>
```
```
