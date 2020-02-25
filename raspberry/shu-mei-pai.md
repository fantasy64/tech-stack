1） 大于64G的sd卡处理，windows会默认格式化未exFat格式，树莓派识别不了，需要格式化成FAT32（mac）

```SHELL
diskutil partitionDisk /dev/disk2 MBR FAT32 UNTITLED 0b
```

2） 开启SSH

在根目录/boot目录下touch一个SSH文件

```SHELL
cd /boot
touch SSH
```

3）设置wifi

当你没有网线的时候，就算开启了ssh连接，由于无法与电脑处于同一局域网，此时电脑也无法通过ssh连接树莓派，此时就需要在树莓派开启的时候先连接上wifi。配置/etc/wpa\_supplicant/wpa\_supplicant.conf 文件，并在里面写上树莓派的wifi配置命令。

配置如下,其中shumeipai是wifi的ssid，8888888是wifi密码：

```SHELL
country=CN
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

network={
    ssid="shumeipai"
    psk="88888888"
    key_mgmt=WPA-PSK
    priority=1
}
```

4\) 设置静态ip，修改/etc/dhcpcd.conf 文件，增加如下内容；

```SHELL
#####add by fantasy######
interface wlan0
static ip_address=10.0.0.25
static routers=10.0.0.1
```



5) 树莓派串口的使用

要参考如下两篇文章的介绍

https://blog.csdn.net/qq_36326623/article/details/79780061

https://www.cnblogs.com/uestc-mm/p/7204429.html

根据上面文章经验，主要进行如下修改：

a） 修改/boot/config.txt

b）修改/boot/cmdline.txt

```shell
#没有修改前
>ls -l /dev/seri*
/dev/serial1 -> ttyAMA0
#按上面的步骤修改后
>ls -l /dev/seri*
/dev/serial1 -> ttyS0
```

从上面的结果来，串口的位置确实换了，但是并没有出现两个串口设备，我用树莓派4的板子，通过检查官方的系统在config.txt文件中多了一行“uart = 0” 猜测是把串口关闭了，修改后打开串口

```shell
#这个配置会关闭硬件串口，需要改为如下：
uart = 1 
#再确认两个串口都看到，并且ttyAMA0对应到GPIO.14	和 GPIO.15
>ls -l /dev/seri*
/dev/serial0 -> ttyAMA0
/dev/serial1 -> ttyS0
```



6）