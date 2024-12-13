# alpine-image-for-uz801
alpine image for uz801

超低系统占用；支持cpu超频；去除蜂窝网络模块释放内存

## 环境要求
Linux系统（虚拟机也可以），uz801设备

## 刷入Alpine
> [!WARNING]
> 以下操作可能会破坏您的设备，使其无法启动。谨慎行事，风险自负！确保开始前已对原始固件进行备份！

克隆本仓库，执行flash.sh脚本，按照提示刷入即可
```
git clone https://github.com/kshipeng/alpine-image-for-uz801.git && cd alpine-image-for-uz801 && chmod +x ./flash.sh && ./flash.sh
```

## 登录Alpine
- 查看Alpine设备ip信息
  ```
  ip addr
  示例输出信息：3: usb0: <BROADCAST,MULTICAST> mtu 1500 qdisc noop state DOWN group default qlen 1000
    link/ether ea:66:5e:5c:a0:f6 brd ff:ff:ff:ff:ff:ff
  ```
- 如上所示`usb0`没有ip地址，则执行，否则略过
  ```
  dhclient usb0
  ip addr show usb0
  示例输出信息：3: usb0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc fq_codel state UNKNOWN group default qlen 1000
    link/ether ea:66:5e:5c:a0:f6 brd ff:ff:ff:ff:ff:ff
    inet 192.168.5.85/24 brd 192.168.5.255 scope global dynamic usb0
       valid_lft 3598sec preferred_lft 3598sec
    inet6 fe80::e888:5eff:f89c:a0f6/64 scope link 
       valid_lft forever preferred_lft forever
  ```
- ssh登录（默认密码：`uz801`）
  ```
  ssh root@192.168.5.1
  ```
  
#### LED灯设置
```
vi /etc/local.d/00-leds.start
```

#### 开机执行脚本
```
vi /etc/local.d/10-myservice.start
```

#### 关机执行脚本
```
vi /etc/local.d/10-myservice.stop
```

致谢、参考项目：[OpenStick-Builder](https://github.com/kinsamanka/OpenStick-Builder)
