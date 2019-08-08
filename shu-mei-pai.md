1） 大于64G的sd卡处理，windows会默认格式化未exFat格式，树莓派识别不了，需要格式化成FAT32（mac）

```SHELL
diskutil partitionDisk /dev/disk2 MBR FAT32 UNTITLED 0b
```

2） 开启SSH

在根目录下touch一个SSH文件

```SHELL
touch SSH
```

3）设置wifi

当你没有网线的时候，就算开启了ssh连接，由于无法与电脑处于同一局域网，此时电脑也无法通过ssh连接树莓派，此时就需要在树莓派开启的时候先连接上wifi。同样的，首先在内存卡中的boot分区中新建一个wpa\_supplicant.conf的文件，并在里面写上树莓派的wifi配置命令。 

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



