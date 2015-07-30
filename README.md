# stm32f4disco-cmsisdap-experiment
※ Sorry, No waranty on this github every repositories.
Publication	Transistor Gijutsu
http://www.eandtechmedia.com/p-tg.php
http://toragi.cqpub.co.jp/
OR 
http://shop.cqpub.co.jp/hanbai/books/48/48131.htm
(BOARD, PARTS, articles)

TORAGI ARM WRITER (MCU BOARD): 
http://toragi.cqpub.co.jp/tabid/707/Default.aspx
http://www.nxp-lpc.com/lpc_boards/arm-writer/
sale on MARUTSU (assembled)
http://www.marutsu.co.jp/pc/i/238834/

CMSIS-DAP firmware for TORAGI ARM WRITER(CMSIS-DAP article by nahitafu, URL bellow is
a firmware for TORAGI ARM writer only)
http://toragi.cqpub.co.jp/Portals/0/download/2014/TR1403N.zip

misc info on this.
http://nahitafu.cocolog-nifty.com/nahitafu/2014/02/arm-6241.html
https://twitter.com/nahitafu/status/433133873975672832
http://nahitafu.cocolog-nifty.com/nahitafu/2014/02/armjtag-b881.html

Experiments

I test on Windows8.1 on Virtualbox on OSX.
If you use usb on windows8.1 on this circumstances, you use
usb port passed to windows8.1.
If you use usb port on osx only, you could no signal on that.

1. FlashMagic
You would bin to hex with arm-none-eabi-objcopy.
1.1 Connection
Please check by yourself misc docs(NO WARANTY).
http://akizukidenshi.com/catalog/g/gK-01977
AE-UM232R (FTDI serial-USB board)
pin assign:
 AE-UM232R    TORAGI ARM WRITER
 TxD          RxD (CN1:10)
 DTR  ▷|     pio0_0(CN1:4, RESET)
 RTS  ▷|     pio0_1(CN2:11, TARGET_RESET)
 RxD          TxD(CN1:9)
      GND-----VBUS(CN2:8pin)
	  +5v-----EXTPOWER(CN1:2pin)
	  GND-----GND(CN1:1pin)
power for TORAGI ARM WRITER is fed by AE-UM232R +5V to TORAGI ARM WRITER's 5v in.
LPC11U35 QuickStart BoardをFT232経由で書き込んでみたり
http://realteck458.blog117.fc2.com/blog-entry-146.html
> VBUS(P0_3) ------ GND

1.2 Usage
 DTR, RTS tweak on Flash Magic option/Advanced
 FlashMagic on OSX (how to detect com port for FlashMagic)
 http://qiita.com/ynomura/items/9d7ce64585d2e9544f6e
 ls -l /Applications/FlashMagic.app/Contents/Resources/dosdevices/COM*
 (if FlashMagic on /Applications)
 I use 9600 baud for test.
 If you could make transfer, that would NRESET or VBUS conn. failed.

2. MDK-ARM (debug STM32f4 Discovery)
2.1 Please read nahitafu's article on TORAGI 2014/3
http://www.amazon.co.jp/%E3%83%88%E3%83%A9%E3%83%B3%E3%82%B8%E3%82%B9%E3%82%BF%E6%8A%80%E8%A1%93-2014%E5%B9%B4-03%E6%9C%88%E5%8F%B7-%E9%9B%91%E8%AA%8C/dp/B00HUWUCRM
OR 
http://shop.cqpub.co.jp/hanbai/books/48/48131.htm
(BOARD, PARTS, articles)
2.2 TIPS
2.2.1 PACKS are for STM32f4 Discovery uptodate, if update runs, remove old one if you could.
2.2.2 CPU is STM32F407vg like designated
2.2.3 CORE and Startup are designated
2.2.4 you may read and download these
http://www.keil.com/appnotes/docs/apnt_230.asp
Application Note 230
MDK V5.10 Lab for the STM32F4 Discovery Board
2.2.5 connection board to board
Please check by yourself misc docs(NO WARANTY).
ARM WRITER(CN5)      SWD(stm32f4 disco)  
1:NC
2:SWDIO(TGT) ------- 4:SWDIO
3:SWCLK(TGT) ------- 2:SWDCLK
4:NC
5:NC
6:NRESET     ------- 5:NRESET
7:NC
8:GND        ------- 3:GND
                     1:NC
					 6:NC
ARM WRITER's CN5 direction is surface of board, top of BOARD is cn5.
left is pin1, right is pin8
stm32f4 disco's SWD connector 's pin1 is near white circle.
