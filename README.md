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

