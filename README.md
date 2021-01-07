# MSI-Z390-Gaming-Edge-AC_OC

## 一定要记得更改序列号什么的

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

## 2020-06-19更新日志

1. 版本更新至3.0（MacPro机型会一直提示内存问题，所以直接换机型了）
2. OC更新至0.5.9版本
3. 所有kext更新至最新版本（截至2020-06-19）
4. USB定制删除Intel蓝牙，使用BCM94360CD蓝牙，免驱
5. 由于机型变化，重新生成了CPU变频优化文件(kext中的CPUFroendProvider.kext,针对i5-9600k,其他CPU请自行生成)
6. 添加weg,boot-args增加参数`agdpmod=pikera`（修复独显启动后无输出)、`shikivga=80`(修复独显启动后无输出)及`igfxfw=2`(核显优化，加入weg后不加此参数会导致核显锁频在0.33，加了此参数后核显`请求频率`会锁定在1.13，请自行斟酌是否添加此参数)
7. 独显优化(参考[Bugprogrammer](https://www.bugprogrammer.me/2020/05/27/Hackintosh_for_Z490_10900K.html)博客)

## 2020-07-19更新日志

1. 强烈建议更新`BIOS`版本至`7B17vA9`，该版本主要改进了内存兼容性

2. 去除无用的`ACPI`补丁`dsdt-no-ec.aml`,因为`dsdt`中的`EC`部件本就无效

3. `ACPI`添加`SSDT-DMAC` `SSDT-MCHC` `SSDT-MEM2` `SSDT-PMCR` `SSDT-PPMC`五个补丁，用于添加缺失的部件，详见[OC-little](https://github.com/daliansky/OC-little/tree/master/06-%E6%B7%BB%E5%8A%A0%E7%BC%BA%E5%A4%B1%E7%9A%84%E9%83%A8%E4%BB%B6)

4. `ACPI`添加`SSDT-GPRW`以及`patch`补丁，用于修复睡眠问题

5. 去除`CPU`变频优化，因为可能导致卡顿问题

6. 更新所有kexts至最新版本，截至`2020-07-19`

7. 引导参数去掉`shikigva=80`

## 2020-09-07 更新日志

1. OC更新至0.6.0

2. kext更新至最新，截至`2020-09-07`

## 2020-09-12 更新日志

1. OC更新至0.6.1

## 2020-10-06更新日志

1. OC更新至0.6.2版本
2. kexts更新至对应的最新版本

## 2020-11-13更新日志

1. OC更新至0.6.3
2. kexts更新至最新版本
3. 支持无痛升级至`bigsur`

## 2020-12-26更新日志

1. OC更新至0.6.4
2. kexts更新至最新版本

## 2021-01-07更新日志

1. OC 更新至0.6.5
2. kexts更新至最新版本

---

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
OC版本：已更新至0.6.1
```

>使用之前请按照[黑果小兵的教程](https://blog.daliansky.net/OpenCore-BootLoader.html)设置好BIOS

---

## 实现功能如下

1. 声卡：板载声卡完美驱动，~~DP声音能够正常输出~~，不使用核显输出
2. 网卡：
    - 板载有线网卡完美驱动  
    - 板载Intel无线网卡wifi无解，不能驱动
    - ~~不使用板载intel蓝牙，如果需要，看[这里](https://github.com/zxystd/IntelBluetoothFirmware/releases)的蓝牙注入，本人对蓝牙没需求，所以没有修复.~~
    - 无线网卡：使用bcm94360CD无线网卡，蓝牙和wifi免驱，
3. 显卡：5700XT免驱(添加优化)
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
4. 启动第二阶段黑屏10s左右

>注意：config.plist文件关闭了-v跑码，关闭了OC引导菜单显示，初次安装时请选择打开，方便排查问题

## 鸣谢

[bugprogrammer](https://www.bugprogrammer.me/)  
[黑果小兵](https://blog.daliansky.net)  
[XJN819](https://blog.xjn819.com/)  
[独行秀才](https://shuiyunxc.gitee.io/)  
以及提供驱动、引导、教程的[acidanthera](https://github.com/acidanthera)、[Rehabman](https://github.com/rehabman)等  
