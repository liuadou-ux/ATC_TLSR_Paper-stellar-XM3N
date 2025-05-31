<h1 align="center">hanshow stellar L3N 电子价签/airtag固件</h1>

### 适用型号 L3N@ (注意：只适配了L3N@ 2.9寸设备，原项目的其他型号可能已经不再兼容)

### 最终效果

- [web 上传图片](https://javabin.cn/stellar-L3N-etag/web_tools/)
  ![蓝牙管理](/images/web.jpg)
- 时钟模式2，图片模式
  ![时钟模式2，图片模式](/images/1553702163.jpg)

![时钟模式2，图片模式](/images/1587504241.jpg)

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

成功后提示内容:

```
'Create Flash image (binary format)'
'Invoking: TC32 Create Extended Listing'
'Invoking: Print Size'
"tc32_windows\\bin\\"tc32-elf-size -t ./out/ATC_Paper.elf
copy from `./out/ATC_Paper.elf' [elf32-littletc32] to `./out/../ATC_Paper.bin' [binary]
   text    data     bss     dec     hex filename
  75608    4604   25341  105553   19c51 ./out/ATC_Paper.elf
  75608    4604   25341  105553   19c51 (TOTALS)
'Finished building: sizedummy'
' '
tl_fireware_tools.py v0.1 dev
Firmware CRC32: 0xe62d501e
'Finished building: out/../ATC_Paper.bin'
' '
'Finished building: out/ATC_Paper.lst'
' '
```

### 蓝牙链接和OTA升级

- 1. 必须先断开TTL TX线，不然蓝牙链接不上。
- 2. OTA升级： https://atc1441.github.io/ATC_TLSR_Paper_OTA_writing.html

### 上传图片

- 1. 运行 `cd web_tools && python -m http.server`
- 2. 打开 http://127.0.0.1:8000 后在页面上链接蓝牙
- 3. 选择图片并上传，上传后可添加文字或者手动绘制文字。也可设置抖动算法。
- 4. 发送到设备，等待屏幕刷新

### 接入苹果findmy网络，模拟airtag
- 设备已支持接入苹果findmy网络，(设备会通过蓝牙广播自动发送符合airtag协议的公钥，当设备附近的苹果设备接受到公钥时，就会使用公钥加密自己的位置信息然后发送到findmy服务器，用户可使用自己的私钥从苹果服务器获取设备的位置信息）
- 该功能默认关闭
- 打开该功能 需要修改ble.c文件 PUB_KEY=后的数据，改为你自己的公钥。PUB_KEY获取方法可参考项目(https://github.com/dchristl/macless-haystack 或者 https://github.com/malmeloo/openhaystack)
- 打开该功能 还需要修改ble.c文件 AIR_TAG_OPEN=1

### 已解决/未解决问题

- [X]  编译报错
- [X]  刷入不生效
- [X]  屏幕区域不对/异常
- [X]  蓝牙无法链接/蓝牙OTA升级
- [ ]  自动识别型号
- [X]  python 图片生成脚本
- [X]  蓝牙发送图片, 显示大小不对问题解决
- [X]  添加蓝牙上传图片后notify
- [X]  添加场景且支持切换
- [X]  图片模式
- [X]  web 支持图片切换
- [X]  添加新的时间场景
- [X]  支持设置年月日
- [X]  web 支持画图编辑，直接上传图片，黑白抖动算法
- [X]  三色抖动算法、设备端三色显示支持，蓝牙传输支持
- [X]  epd buffer刷新后 数据异常（左或右偶尔有黑条）？
- [X]  中文显示 （部分中文以bitmap显示，不支持全部中文）
- [X]  支持接入苹果findmy网络，模拟airtag

### 原始readme.md

[README_EN.md](/README_en.md) （其他型号请参考原始项目，这个项目只支持L3N@ 2.9寸设备）

> 注：
> 基于该项目 [ATC_TLSR_Paper](https://github.com/atc1441/ATC_TLSR_Paper) 修改。

### 资料

- [TLSR8359规格说明书](/docs/DS_TLSR8359-E_Datasheet for Telink ULP 2.4GHz RF SoC TLSR8359.pdf)
- [tlsr8x5x蓝牙开发说明书（中文）](/docs/Telink Kite BLE SDK Developer Handbook中文.pdf)
- [屏幕驱动说明书 SSD1680.pdf](/docs/SSD1680.pdf)
