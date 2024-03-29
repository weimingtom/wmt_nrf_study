﻿# wmt_nrf_study
My nRF52 study

## msys  
search baidupan, msys_nrf52840-mdk.rar  

## micro:bit ref  
https://makecode.microbit.org/docs  
https://makecode.microbit.org/reference  
蓝牙, bluetooth    
https://github.com/microbit-foundation/microbit-blue  
https://leesei.github.io/micro-bit/  
search baidupan, microbit-blue-master  

## waveshare micro:bit bluetooth  
https://www.waveshare.net/wiki/Chapter_8_of_KitiBot_for_Micro:bit    
Com-bluetooth-mwoolley-microbitbledemo.7.apk  
```
def on_bluetooth_connected():
    basic.show_string("C")
bluetooth.on_bluetooth_connected(on_bluetooth_connected)

def on_bluetooth_disconnected():
    basic.show_string("D")
bluetooth.on_bluetooth_disconnected(on_bluetooth_disconnected)

bluetooth.start_accelerometer_service()
bluetooth.start_button_service()
bluetooth.start_led_service()
bluetooth.start_temperature_service()

def on_forever():
    pass
basic.forever(on_forever)
```
a) add bluetooth in makecode, removing radio  
b) close android app settings filter unpair  
c) change makecode project setting, NO Pairing  

## nrf52840-mdk-usb-dongle Ref  
* https://wiki.makerdiary.com/nrf52840-mdk-usb-dongle/  
* sdk ref to https://wiki.makerdiary.com/nrf52840-mdk/nrf5-sdk/  
* https://github.com/makerdiary/nrf52840-mdk-usb-dongle  
* nRF Connect  
* https://github.com/NordicSemiconductor/pc-nrfconnect-programmer  
* https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Connect-for-desktop  
* Flash < 892KB  
* nrfutil  
* https://github.com/NordicSemiconductor/pc-nrfutil  

## 造物小店，windows xp下安装nrf52840 usb dongle开发板的开发环境  
xp下测试  
(1) 解压安装msys_v11.7z  
(2) 解压nRF5SDK1500a53641a.zip到msys\home\a\nrf52840-mdk-usb-dongle\nrf_sdks\nRF5_SDK_15.0.0_a53641a  
(3) 安装gcc-arm-none-eabi-6-2017-q2-update-win32.zip，然后把安装目录复制到msys\home\a\gcc-arm-none-eabi-6-2017-q2-update-win32  
(3) 修改~/nrf52840-mdk-usb-dongle/nrf_sdks/nRF5_SDK_15.0.0_a53641a/components/toolchain/gcc/Makefile.windows:  
#GNU_INSTALL_ROOT := C:/Program Files (x86)/GNU Tools ARM Embedded/6 2017-q2-update/bin/  
GNU_INSTALL_ROOT := /home/a/gcc-arm-none-eabi-6-2017-q2-update-win32/bin/  
注意/home/a/修改为实际的用户名路径  
(4) 解压nrfutil_xp_patch_v1.rar里面的nrfutil.exe到bin/  
(5) 短接RESET脚和GND脚（或者长按reset按钮），然后插入到电脑usb口，红灯心跳亮暗  
(6) 在设备管理器中更改有问号的驱动，在对话框中把位置指向  
msys\home\a\nrf52840-mdk-usb-dongle\nrf_sdks\nRF5_SDK_15.0.0_a53641a\examples\usb_drivers  
，然后就能安装驱动成功  
(7) 编译和上传到串口COM10（修改为实际的串口号码）  
$ cd  ~/nrf52840-mdk-usb-dongle/examples/nrf5-sdk/blinky/armgcc  
$ make clean  
$ make  
$ make flash-usb-serial USB_SERIAL_DEVICE=COM10  
(8) 拔出reset和gnd的短接线，然后重新插拔usb重启开发板  

## 造物小店的nrf52840 usb dongle开发板救砖，救砖方法，weibo  
晚上终于把造物小店版的nrf52840 dongle救砖成功了，参考那个github issue的做法，用j-link ob刷入bootloader即可。  
https://github.com/makerdiary/nrf52840-mdk-usb-dongle/issues/5  
那个issue没有提及具体怎么做，我是参考网上的做法，用命令行刷的，需要先安装nRF5x-Command-Line-Tools，然后执行nrfjprog --program nrf52840_usb_dongle_open_bootloader_v1_1_0.hex --chiperase -f nrf52 --reset，这个命令行会调用j-link的dll执行刷写操作，然后就可以看到久违的红灯呼吸灯了（表示恢复原来的dfu串口模式）。不过我又发现一个别的问题，SDK里面的串口驱动居然无法在win7下正常安装，但在xp下是可以正常安装驱动，可能要装nrfgo才可以解决这个问题  

## 造物小店，错误刷了MDK编译工程后变砖，救砖方法（win7下，需要接好j-link ob的4线swd接口，可从中景园购买）：    
(1) 先安装nRF5x-Command-Line-Tools_9_8_1_Installer_64.exe  
(2) 加入PATH  
@set PATH=C:\Program Files\Nordic Semiconductor\nrf5x\bin;%PATH%  
@cmd  
(3) 刷bootloader  
https://github.com/makerdiary/nrf52840-mdk-usb-dongle/tree/master/firmware/open_bootloader  
nrfjprog --program nrf52840_usb_dongle_open_bootloader_v1_1_0.hex --chiperase -f nrf52 --reset  

## 造物小店的nrf52840 usb dongle开发板救砖，参考资料（与这个开发板无关）：  
https://learn.adafruit.com/bluefruit-nrf52-feather-learning-guide/flashing-the-bootloader  
https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF5-Command-Line-Tools/Download#infotabs  
https://devzone.nordicsemi.com/nordic/short-range-guides/b/getting-started/posts/nrf52840-dongle-programming-tutorial  
nrfjprog --program bootloader_binary.hex --chiperase -f nrf52 --reset  

## MDK5，讯联电子nrf52832 breakout  
(1) 打开E:\mcu\nrf\nrf52832_xunlian\3.软件开发包(SDK)\nRF5_SDK_15.0.0_a53641a\examples\peripheral\blinky\pca10040\blank\arm5_no_packs  
(2) 连接j-link ob 四线（不接usb供电）, 勾选Debug(选 jlink)-Settings-Flash Download-Erase Full Chip  
(3) mdk5编译下载  

## MDK5，讯联电子nrf52832 breakout, weibo    
(1) 首先你要去讯联电子买个nrf52832开发板和j-link ob烧录器。我为了省钱买了nrf52832，实际上nrf52应该是通用的，我觉得区别可能只有很少。其次你需要有个j-link ob或者j-link加JTAG转SWD转换器作为烧录器。我这里用的是中景园的j-link ob，讯联推荐买它自家的j-link v9，其实是一样的效果（我为了省钱所以没另外买）。接好SWD 4线（开发板上有标明DIO和CLK）。装好j-link驱动和烧录软件——如果你比较聪明，可以通过下载安装nrf5 command line tools（带有nrfjprog命令行），因为nrfjprog依赖j-flash的dll，所以安装的时候会自动装上j-flash。  
(2) 其次，通过官方提供的SDK，里面的mdk5工程实现blink闪烁LED灯效果。这里需要靠讯联电子提供的资料，否则会很迷茫（这方面nrf官方做得比较混乱，初学者一般很难找得到头绪）。我这里是打开这个工程：  
nRF5_SDK_15.0.0_a53641a\examples\peripheral\blinky\pca10040\blank\arm5_no_packs  
并且在MDK5的工程设置中，勾选Debug(选 jlink)-Settings-Flash Download-Erase Full Chip。讯联没有提及到Erase Full Chip的问题，我是发现了这个问题，如果不选全清的话，无法解除上一个程序的运行效果（我是从nrfjprog的全清中获取这个灵感）。  
(3) 通过MDK5的download按钮，即可完成固件的下载，并且立即看到运行效果。注意，pca10040文件夹中还有mbr和s132这两种MDK5工程，我试过无法看到闪灯的运行效果，估计可能需要刷对应的mbr和softdevice固件才能看到正确的运行效果。  
(4) 如果查看源代码的定义，可以发现boards.c和pca10040.h这两个定义板载资源的源文件，里面会提到LED_1, LED_2, LED_3, LED_4这四个脚，对应的是17、18、19、20这四个脚。这时候就可以看到讯联的开发板的优点——板上印的数字编号即对应代码里面的编号，不需要自己想办法对应。由于讯联的开发板跟nrf官方的开发板pca10040有出入，所以我这里的电路接法是接了19和20这两个针脚，至于17和18的两个灯是板载的LED灯。照片中板载的三个LED灯，最上方红灯是电源灯，下面的两个红灯分别对应17和18脚  

## Arduino IDE，讯联电子nrf52832 breakout  
see nrf52832breakout_xunlian\nrf52832_xunlian_arduino.zip  
(0) j-link ob连接4线（包括3.3V供电）, 不需要接usb口供电  
可以用j-flash测试是否能读出整片flash  
(1) 安装nrfjprog （安装时自动安装j-flash）  
nRF Command Line Tools (or nRF5x-Command-Line-Tools)  
https://www.nordicsemi.com/Software-and-Tools/Development-Tools/nRF-Command-Line-Tools  
C:\Program Files\Nordic Semiconductor\nrf5x\bin  
(2) 3个文件打补丁（基于nRF5DK）  
C:\Arduino\Portable\packages\sandeepmistry\hardware\nRF5\0.6.0  
(3) 选择Xunlian nRF52832 Breakout或者Xunlian nRF52840 Breakout，然后编译上传下面修改过的Blink示例程序：  
nrf52832breakout_xunlian/blink_nrf52840breakout.txt  
(4) 如果自己制作board，请复制Generic，不要复制nrf52dk，因为nrf52dk做了特定的端口映射，digitalWrite的数字参数不是对应实际官方定义的端口编号。另外NRF_GPIO_PIN_MAP可能会超出Generic的最大端口映射数，详细参考  
C:\Arduino\Portable\packages\sandeepmistry\hardware\nRF5\0.6.0\variants\Generic\variant.cpp  
中g_ADigitalPinMap的定义  

## Arduino Core for nRF5    
* https://github.com/sandeepmistry/arduino-nRF5  

## Adafruit code for the Nordic nRF52 BLE SoC on Arduino  
* https://github.com/adafruit/Adafruit_nRF52_Arduino  

## ARM toolchain  
* https://developer.arm.com/open-source/gnu-toolchain/gnu-rm/downloads  
* https://launchpad.net/gcc-arm-embedded  

## MSys2， tsinghua    
* https://mirrors.tuna.tsinghua.edu.cn/help/msys2/  

## Official Doc  
* https://www.nordicsemi.com/DocLib?Product=nrf52840  
* http://infocenter.nordicsemi.com/pdf/nRF52840_Dongle_User_Guide_v1.0.pdf  
* http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.tools%2Fdita%2Ftools%2Ftools.html  
* http://infocenter.nordicsemi.com/index.jsp?topic=%2Fcom.nordic.infocenter.tools%2Fdita%2Ftools%2Fnrfutil%2Fnrfutil_intro.html  


## 红旭开发板  
* https://github.com/xiaolongba/HX_DK_FOR_NORDIC_52840_BLE  

## 微雪 nRF52840开发板  
* http://www.waveshare.net/wiki/NRF52840_Eval_Kit  

## micro:bit offline    
* https://www.kittenbot.cn/software/  
* https://makecode.microbit.org/offline  
* https://makecode.microbit.org  

## 喵比特, kittenbot  
* http://www.kittenbot.cc/  
* https://kittenbot.github.io/meowbit-tutorials/  
* https://kittenbot.taobao.com  

## Mu Editor  
* https://codewith.mu  
* https://www.kittenbot.cn/software/  

## PyGame Zero  
* https://codewith.mu/en/tutorials/1.0/pgzero  
* https://pygame-zero.readthedocs.io/en/stable/  

## Micro:bit, 开源硬件商城    
* http://microbit.org/zh-CN/  
* https://makecode.microbit.org/  
* https://makecode.microbit.org/projects  
* https://microbit-micropython.readthedocs.io/en/latest/  
* http://microbit.org/ecosystem-bycountry/  
* http://microbit.org/resellers/  

## mixly  
http://mixly.org  

## makecode cli  
https://makecode.com/cli  

## Nordic NRF52-DK  
pca10040  
with nRF52832  

## Nordic NRF52840 DONGLE  
PCA10059  
https://www.nordicsemi.com/?sc_itemid={CDCCA013-FE4C-4655-B20C-1557AB6568C9}  

## nRF52840 DK  
PCA10056  

## 讯联电子  
http://infor-link.com/forum.php  

## Nordic DevZone  
https://devzone.nordicsemi.com  

## Bluefruit52  
https://github.com/Afantor/Afantor_Bluefruit52_Arduino  
https://blog.csdn.net/solar_Lan/article/details/88688451  
https://blog.csdn.net/solar_Lan/article/details/89034075  
http://www.afantor.cc  

## Adafruit Bluefruit nRF52 Feather  
https://learn.adafruit.com/bluefruit-nrf52-feather-learning-guide/bluefruit-nrf52-api  

## nRF24/RF24  
https://github.com/nRF24/RF24  

## makerdiary/nrf52840-mdk  
https://github.com/makerdiary/nrf52840-mdk/blob/master/docs/hardware/nrf52840-mdk-pinout-diagram-v1_0.pdf  
https://github.com/makerdiary/nrf52840-mdk/blob/master/docs/cn/nrf5-sdk/index.md  

## nRF5340 DK  
* D:\ncs\v2.3.0\nrf\include\dk_buttons_and_leds.h  
* https://devzone.nordicsemi.com/nordic/b/archives/posts/ncs-tutorial---temporary  
* https://developer.nordicsemi.com/nRF_Connect_SDK/doc/latest/nrf/working_with_nrf/nrf53/nrf5340.html  
* peripheral_lbs  
* D:\ncs\v2.3.0\nrf\samples\bluetooth\peripheral_lbs\src  

## wristband, nrf51822, nrf52832  
* https://github.com/sommer78/HeartRate/tree/master/document/nrf52832  
* https://github.com/sommer78/HeartRate/tree/master/wrist-rom-master-code  

## nrf remote control PC      
* https://github.com/NordicPlayground/shortcut-remote-demo
* https://www.hackster.io/videos/1108

## nrf-doom, micro:bit remote gamepad  
* https://github.com/NordicPlayground/nrf-doom
* RCmall 5V Gamepad Module with Buzzer onboard for BBC Micro:bit Microbit Joystick & Buttons  
waveshare, Joystick for micro:bit
* https://github.com/DFRobot/pxt-gamePad  

## nus, A Web Command Line Interface via NUS (Nordic UART Service) using Web Bluetooth.  
* https://github.com/makerdiary/web-device-cli  

## ESP32 SWD Flasher for nRF52  
* https://github.com/atc1441/ESP32_nRF52_SWD  

## (TODO) 未整理项目  
* https://github.com/Emeryth/sma-q2-oss  
* https://github.com/gbuzogany/nrf52-lvgl-st7735s  
* https://github.com/Lotlab/nrf52-keyboard  
* https://github.com/mafaneh/ble-ebook-project  
* https://github.com/edgeimpulse/example-standalone-inferencing-zephyr  

## makecode project  
* https://github.com/waveshare/WSLCD1in8
* https://www.waveshare.net/wiki/1.8inch_LCD_for_micro:bit
* https://github.com/waveshare/PXT-WSLCD1in8
* https://github.com/weimingtom/microbit_xmas_song
* https://github.com/DFRobot/pxt-gamePad
* https://wiki.dfrobot.com.cn/_SKU_DFR0536__micro_bit%E6%B8%B8%E6%88%8F%E6%89%8B%E6%9F%84%E6%89%A9%E5%B1%95%E6%9D%BF
* https://wiki.dfrobot.com.cn/_SKU_DFR0536__micro_bit游戏手柄扩展板
* https://makecode.microbit.org/_YdWVgV7j7LhA
* https://makecode.microbit.org/_Vot7AfUW7g6D
* https://makecode.microbit.org/_PtgDRughPidF
* https://makecode.microbit.org/_3WRLraYKPM2y
* https://makecode.microbit.org/_1WYL7aKctdav
* https://makecode.microbit.org/_eA13q2ao8W18
* https://makecode.microbit.org/_Txyh7tPzs5F9
* https://makecode.microbit.org/_eo52fw5ghMkX
* https://github.com/weimingtom/dfrobot_gamepad_demo3  
* How to import, 导入方法  
```
关于micro:bit的导入问题，网上会有一种说法是通过添加包来实现，例如这篇《1.8inch LCD for micro:bit》。
但其实这个功能可能makecode已经没有了，我怀疑这个导入功能被另外一个功能取代，这个功能不是在新建项目之后，
而是在新建项目之前，右上角有个导入按钮，然后选导入网址即可导入gh链接（或者你可以导入hex文件都行），
这样就可以看到别人的库——缺点是你只能导入一个第三方库。补注：可以通过扩展搜索导入gh链接，
应该只要是自己导出到gh的项目都可以这样做（在左下角有个gh图标的按钮，可以把项目文件存储到gh）
```
* https://github.com/sdjngyq/MFDLCD1in8  
vertical  
* https://github.com/sdjngyq/MFDLCD18_H  
horizon  
* 
