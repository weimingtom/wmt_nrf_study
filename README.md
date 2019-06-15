# wmt_nrf_study
My nRF52 study

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

## windows xp下安装nrf52840 usb dongle开发板的开发环境  
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

## MDK5，迅联电子nrf52832 breakout  
(1) 打开E:\mcu\nrf\nrf52832_xunlian\3.软件开发包(SDK)\nRF5_SDK_15.0.0_a53641a\examples\peripheral\blinky\pca10040\blank\arm5_no_packs  
(2) 连接j-link ob 四线（不接usb供电）, 勾选Debug(选 jlink)-Settings-Flash Download-Erase Full Chip  
(3) mdk5编译下载  

## MDK5，迅联电子nrf52832 breakout, weibo    
(1) 首先你要去迅联电子买个nrf52832开发板和j-link ob烧录器。我为了省钱买了nrf52832，实际上nrf52应该是通用的，我觉得区别可能只有很少。其次你需要有个j-link ob或者j-link加JTAG转SWD转换器作为烧录器。我这里用的是中景园的j-link ob，迅联推荐买它自家的j-link v9，其实是一样的效果（我为了省钱所以没另外买）。接好SWD 4线（开发板上有标明DIO和CLK）。装好j-link驱动和烧录软件——如果你比较聪明，可以通过下载安装nrf5 command line tools（带有nrfjprog命令行），因为nrfjprog依赖j-flash的dll，所以安装的时候会自动装上j-flash。  
(2) 其次，通过官方提供的SDK，里面的mdk5工程实现blink闪烁LED灯效果。这里需要靠迅联电子提供的资料，否则会很迷茫（这方面nrf官方做得比较混乱，初学者一般很难找得到头绪）。我这里是打开这个工程：  
nRF5_SDK_15.0.0_a53641a\examples\peripheral\blinky\pca10040\blank\arm5_no_packs  
并且在MDK5的工程设置中，勾选Debug(选 jlink)-Settings-Flash Download-Erase Full Chip。迅联没有提及到Erase Full Chip的问题，我是发现了这个问题，如果不选全清的话，无法解除上一个程序的运行效果（我是从nrfjprog的全清中获取这个灵感）。  
(3) 通过MDK5的download按钮，即可完成固件的下载，并且立即看到运行效果。注意，pca10040文件夹中还有mbr和s132这两种MDK5工程，我试过无法看到闪灯的运行效果，估计可能需要刷对应的mbr和softdevice固件才能看到正确的运行效果。  
(4) 如果查看源代码的定义，可以发现boards.c和pca10040.h这两个定义板载资源的源文件，里面会提到LED_1, LED_2, LED_3, LED_4这四个脚，对应的是17、18、19、20这四个脚。这时候就可以看到迅联的开发板的优点——板上印的数字编号即对应代码里面的编号，不需要自己想办法对应。由于迅联的开发板跟nrf官方的开发板pca10040有出入，所以我这里的电路接法是接了19和20这两个针脚，至于17和18的两个灯是板载的LED灯。照片中板载的三个LED灯，最上方红灯是电源灯，下面的两个红灯分别对应17和18脚  

## Arduino Core for nRF5    
* https://github.com/sandeepmistry/arduino-nRF5  

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

