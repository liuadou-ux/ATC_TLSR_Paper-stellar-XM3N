<h1 align="center">hanshow stellar XM3N 电子价签固件</h1>

### 适用型号 汉硕XM3N@ 


### 刷入固件步骤

- 1. 拆开电池后盖观察主板是否是如下图所示。（或者查看主控是否为TLSR8359）

![焊接图示](/USB_UART_Flashing_connection.jpg)

- 2. 焊接 GND, VCC, RX, RTS四根线。
- 3. 使用usb2ttl模块(CH340)链接焊接的四根线。其中rx 链接 tx, tx链接 rx, vcc链接3.3v, GND链接 GND。RTS飞线和芯片CH340G第三脚链接（也可不焊，烧录前手动和GND连一下）。
- 4. 打开https://atc1441.github.io/ATC_TLSR_Paper_UART_Flasher.html, 波特率选择默认 460800，Atime默认，文件选择Firmware/ATC_Paper.bin
- 5. 先点击unlock,再点击write to flush,等待完成。成功后，屏幕会自动刷新。

### 项目编译

```cmd

    cd Firmware
    makeit.exe clean && makeit.exe -j12

```

> 注：
> 基于该项目 [ATC_TLSR_Paper](https://github.com/atc1441/ATC_TLSR_Paper) 和[stellar-L3N-etag](https://github.com/reece15/stellar-L3N-etag)修改。

### 微信小程序使用

- 1.获取蓝牙

![小程序主页](https://github.com/liuadou-ux/ATC_TLSR_Paper-stellar-XM3N/blob/main/images/1.png)

点击获得蓝牙，如果没有出现蓝牙列表，则再次点击获得蓝牙，出现蓝牙列表后，没有墨水屏上显示的BLE_******的蓝牙就下拉界面直到出现BLE开头的蓝牙

- 2.连接蓝牙

![连接蓝牙](https://github.com/liuadou-ux/ATC_TLSR_Paper-stellar-XM3N/blob/main/images/2.jpg)

点击BLE开头的蓝牙

- 3.获取蓝服务

![连接服务](https://github.com/liuadou-ux/ATC_TLSR_Paper-stellar-XM3N/blob/main/images/3.jpg)

一定要连接 **00001F10** 这个开头的服务特征值，当然了有人就会说了，咋不整一个一件链接的，关键是我不会啊（doge）

- 4.获取特征

![连接特征值](https://github.com/liuadou-ux/ATC_TLSR_Paper-stellar-XM3N/blob/main/images/4.jpg)

特征值就一个直接连接

- 5.设置为设备

![设备](https://github.com/liuadou-ux/ATC_TLSR_Paper-stellar-XM3N/blob/main/images/5.jpg)

- 6.设置

![设置界面]()

