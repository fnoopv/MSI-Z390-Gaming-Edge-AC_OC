# MSI-Z390-Gaming-Edge-AC_OC

## 2020-04-19更新日志

1. 更新oc至0.5.7版本
2. 更新ketxs至最新版本
3. 添加USB定制（外部接口全部可用，内部USB2.0接口本人只用了一个，所以定制也只定制了一个)
4. 添加Intel蓝牙驱动kext,可驱动主板自带的Intel蓝牙，wifi无解

## 2020-05-23更新日志

1. 版本更新至2.0，不兼容1.0（因为添加了独立显卡）
2. 更换机型，从macmini8,1更换为macPro7,1  
3. oc版本更新至0.5.8
4. USB定制(即USBPorts.kext）删掉了内置蓝牙接口，使用94360cd蓝牙

msi mpg z390 gaming edge ac黑苹果OC引导  
本人配置如下:

```text
主板：MSI MPG Z390 Gaming Edge Ac
CPU：i5-9600k
显卡：AMD RX5700XT 白金
BIOS版本：7B17vA7
硬盘：Samsung 970 evo plus 500G
```

```text
OC版本：已更新至0.5.8
```

>使用之前请按照[黑果小兵的教程](https://blog.daliansky.net/OpenCore-BootLoader.html)设置好BIOS

## 实现功能如下

1. 声卡：板载声卡完美驱动，~~DP声音能够正常输出~~，不使用核显输出
2. 网卡：
    - 板载有线网卡完美驱动  
    - 板载Intel无线网卡wifi无解，不能驱动
    - ~~不使用板载intel蓝牙，如果需要，看[这里](https://github.com/zxystd/IntelBluetoothFirmware/releases)的蓝牙注入，本人对蓝牙没需求，所以没有修复.~~
    - 无线网卡：使用bcm94360CD无线网卡，蓝牙和wifi免驱，
3. 显卡：5700XT免驱
4. 其他实现的功能：  
    - 原生电源管理  
    - 原生nvram加载使用
    - 节能设置中第五项加载
    - EC控制器禁用（按照XJN大佬的说法，台式机不需要)
    - USBX供电（可为苹果自家设备快速充电）
    - RTC修复（禁用AWAC）
    - CPU变频优化（只针对i5-9600k，其他cpu请自行设置，参考XJN大佬文章）
    - 引导修复（为了把mac引导项始终排在第一项，oc扫描策略为只扫描mac盘；windows引导请自行添加，方法参考XJN大佬的文章）

## 存在的问题

1. ~~HDMI接口未测试，不确定是否能正常使用~~,因为使用独立显卡，屏蔽了核显，确定不能用
2. ~~睡眠目前没有问题，有问题可参考XJN大佬的文章进行修复~~ 确定睡眠没有问题
3. ~~使用了USBInjectAll.kext进行usb注入，没有做USB定制，后续再做~~ 已进行定制

>注意：config.plist文件关闭了-v跑码，关闭了OC引导菜单显示，初次安装时请选择打开，方便排查问题
