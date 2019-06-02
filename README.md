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

