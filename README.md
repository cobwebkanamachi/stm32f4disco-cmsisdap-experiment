# stm32f4disco-cmsisdap-experiment
※ Sorry, No warranty on this github every repositories.<BR>
Publication	Transistor Gijutsu<BR>
http://www.eandtechmedia.com/p-tg.php <BR>
http://toragi.cqpub.co.jp/ <BR>
OR <BR>
http://shop.cqpub.co.jp/hanbai/books/48/48131.htm <BR>
(BOARD, PARTS, articles) <BR>
<BR>
TORAGI ARM WRITER (MCU BOARD): LPC11U35/501 board this is.<BR> 
http://toragi.cqpub.co.jp/tabid/707/Default.aspx <BR>
http://www.nxp-lpc.com/lpc_boards/arm-writer/ <BR>
sale on MARUTSU (assembled) <BR>
http://www.marutsu.co.jp/pc/i/238834/ <BR>
<BR>
CMSIS-DAP firmware for TORAGI ARM WRITER(CMSIS-DAP article by nahitafu, URL bellow is
a firmware for TORAGI ARM writer only)<BR>
http://toragi.cqpub.co.jp/Portals/0/download/2014/TR1403N.zip <BR>
<BR>
misc info on this.<BR>
http://nahitafu.cocolog-nifty.com/nahitafu/2014/02/arm-6241.html <BR>
https://twitter.com/nahitafu/status/433133873975672832 <BR>
http://nahitafu.cocolog-nifty.com/nahitafu/2014/02/armjtag-b881.html <BR>
<BR>
Experiments<BR>
<BR>
I test on Windows8.1 on Virtualbox on OSX.<BR>
If you use usb on windows8.1 on this circumstances, you use
usb port passed to windows8.1.<BR>
If you use usb port on osx only, you could no signal on that.
<BR>
1. FlashMagic<BR>
You would bin to hex with arm-none-eabi-objcopy.<BR>
1.1 Connection<BR>
Please check by yourself misc docs(NO WARRANTY).<BR>
http://akizukidenshi.com/catalog/g/gK-01977 <BR>
AE-UM232R (FTDI serial-USB board) <BR>
pin assign:<BR>
 AE-UM232R    TORAGI ARM WRITER<BR>
 TxD          RxD (CN1:10)<BR>
 DTR  ▷|     pio0_0(CN1:4, RESET)<BR>
 RTS  ▷|     pio0_1(CN2:11, TARGET_RESET)<BR>
 RxD          TxD(CN1:9)<BR>
▷| : means diode (1n4148 like)<BR>
      GND-----VBUS(CN2:8pin)<BR>
      +5v-----EXTPOWER(CN1:2pin)<BR>
      GND-----GND(CN1:1pin)<BR>
power for TORAGI ARM WRITER is fed by AE-UM232R +5V to TORAGI ARM WRITER's 5v in.<BR>
LPC11U35 QuickStart BoardをFT232経由で書き込んでみたり<BR>
http://realteck458.blog117.fc2.com/blog-entry-146.html <BR>
VBUS(P0_3) ------ GND <BR>
I read this article, then test vbus--GND, that was right.
<BR>
1.2 Usage<BR>
 DTR, RTS tweak on Flash Magic option/Advanced<BR>
 FlashMagic on OSX (how to detect com port for FlashMagic) <BR>
 http://qiita.com/ynomura/items/9d7ce64585d2e9544f6e <BR>
 ls -l /Applications/FlashMagic.app/Contents/Resources/dosdevices/COM*<BR>
 (if FlashMagic on /Applications)<BR>
 I use 9600 baud for test.<BR>
 If you could make transfer, that would NRESET or VBUS conn. failed.<BR>
<BR>
2. MDK-ARM (debug STM32f4 Discovery)<BR>
2.1 Please read nahitafu's article on TORAGI 2014/3<BR>
http://www.amazon.co.jp/%E3%83%88%E3%83%A9%E3%83%B3%E3%82%B8%E3%82%B9%E3%82%BF%E6%8A%80%E8%A1%93-2014%E5%B9%B4-03%E6%9C%88%E5%8F%B7-%E9%9B%91%E8%AA%8C/dp/B00HUWUCRM <BR>
OR <BR>
http://shop.cqpub.co.jp/hanbai/books/48/48131.htm <BR>
(BOARD, PARTS, articles)<BR>
2.2 TIPS<BR>
2.2.1 PACKS are for STM32f4 Discovery uptodate, if update runs, remove old one if you could.<BR>
2.2.2 CPU is STM32F407vg like designated<BR>
STM32F407VGT6 used for STM32f4 Discovery, so KEIL's MCU selection is STM32F407vg.
2.2.3 CORE and Startup are designated<BR>
2.2.4 you may read and download these<BR>
http://www.keil.com/appnotes/docs/apnt_230.asp <BR>
Application Note 230 <BR>
MDK V5.10 Lab for the STM32F4 Discovery Board <BR>
2.2.5 connection board to board <BR>
Please check by yourself misc docs(NO WARRANTY).<BR>
ARM WRITER(CN5)      SWD(stm32f4 disco)  <BR>
1:NC<BR>
2:SWDIO(TGT) ------- 4:SWDIO<BR>
3:SWCLK(TGT) ------- 2:SWDCLK<BR>
4:NC<BR>
5:NC<BR>
6:NRESET     ------- 5:NRESET<BR>
7:NC<BR>
8:GND        ------- 3:GND<BR>
             ------- 1:NC<BR>
             ------- 6:NC<BR>
ARM WRITER's CN5 direction is surface of board, top of BOARD is cn5.<BR>
left is pin1, right is pin8<BR>
stm32f4 disco's SWD connector 's pin1 is near white circle.<BR>
<BR>
3.Screenshot<BR>
MDK-ARM(KEIL) debug view<BR>
https://twitter.com/cobwebkanamachi/status/626353159674302465 <BR>
MDK-ARM(KEIL) project property, esp. cmsis-dap and target view.<BR>
https://twitter.com/cobwebkanamachi/status/625969398797352960 <BR>
4.notices<BR>
4.1 Now, indeed test on ram only.<BR>
    (addendum) I read a notice on this issue (on Notes) .<BR>
    "Creating a Flash programming algorithm with MDK-Lite is not supported"<BR>
    CMSIS-Pack  Version 1.3.3 Delivery Mechanism for Software Packs<BR>
    Flash Programming Algorithms<BR>
    https://www.keil.com/pack/doc/CMSIS/Pack/html/_flash_algorithm.html <BR>
    You could know this if you read Flash/_Template/test and <BR>
    open it on MDK, you would have Flash Algorithm Files for F10x.<BR>
    I see this, then search that.<BR>
4.2 you should tweak PLL_P and misc macros.<BR>
    I edit codes, but too short time to publish(sorry, later if i could).<BR>
    Here it is shown as diff all in one.<BR>
    https://github.com/cobwebkanamachi/stm32f4disco-cmsisdap-experiment/blob/master/Blinky.diff <BR>
    Please see url shown bellow.<BR>
    http://stm32f4-discovery.com/2014/11/overclock-stm32f4-device-up-to-250mhz/ <BR>
<BR>
Cheers.<BR>
