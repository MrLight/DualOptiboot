## DualOptiboot Bootloader for miniwireless Boards ##

This is a custom Optiboot Bootloader, which adds support for wireless programming.
This bootloader is strongly based on the DualOptiboot from lowpowerlab.
(Copyright Felix Rusu (2013-2014), felix@lowpowerlab.com
More at: http://lowpowerlab.com/Moteino)

This DualOptiboot version is modified to support the miniwireless boards from http://http://anarduino.com/.
Since the Flash-Chip is a bit different then on the Monteinos from LowPowerLab. this is fixed here.
This Bootloader is also based on the latest Optiboot.
It supprots compiling with AtmelStudio 7. For that you can find two prepared Projects in the AtmelStudio Folder.
One for the compressed bootloader version with no debugging capability. This fits into 1k.
The second one adds some kind of debugging. You can see some characters on the UART. But this version is larger than 1k.

To quickstart you can find two hex files in the AtmelStudio Folder. One with and one without Debugging. Both for the miniwireless boards.

Fuses for the normal 1k version are:
EXTEND: 0xFD
HIGH: 0xDA
LOW: 0xDE

Fuses for the debugging version are:
EXTEND: 0xFD
HIGH: 0xD8
LOW: 0xDE

Secondly you should be able to use make
- "omake.bat miniwireless" for the normal Bootloader
- "omake.bat miniwireless_debug" for the debug Version
- "omake.bat miniwireless_isp" for the normal Bootloader with isp flashing (adjust makefile.isp for your programmer / Port)
- "omake.bat miniwireless_debug_isp" for the debug Version with isp flashing (adjust makefile.isp for your programmer / Port)

When isp flashing the miniwireless take care to add two 10k resistors at D5 and D10. This is needed to deselect the Flash and the RFM from SPI. If you don't do this you will get verification errors.

-------------------------------------------------------------------------------------------------------------
Here is the original README from LowpowerLabs and Arduino...

DualOptiboot
============

Custom Optiboot to add wireless programming capability to Moteino
Copyright Felix Rusu (2013-2014), felix@lowpowerlab.com
More at: http://lowpowerlab.com/Moteino

This Optiboot version is modified to add the capability of reflashing 
from an external SPI flash memory chip. As configured this will work 
with Moteino (www.lowpowerlab.com/Moteino) provided a SPI flash chip
is present on the dedicated onboard footprint.
Summary of how this Optiboot version works:
- it looks for an external flash chip
- if one is found (SPI returns valid data) it will further look
  for a new sketch flash image signature and size
  starting at address 0:   FLXIMG:9999:XXXXXXXXXXX
  where: - 'FLXIMG' is fixed signature indicating FLASH chip
           contains a valid new flash image to be burned
         - '9999' are 4 size bytes indicating how long the
           new flash image is (how many bytes to read)
         - 'XXXXXX' are the de-hexified bytes of the flash 
           pages to be burned
         - ':' colons have fixed positions (delimiters)
- if no valid signature/size are found, it will skip and
  function as it normally would (listen to STK500 protocol on serial port)

The added code will result in a compiled size of just under 1kb
(Originally Optiboot takes just under 0.5kb)

-------------------------------------------------------------------------------------------------------------

To compile copy the Optiboot.c and Makefile files where Optiboot is originally located, mine is at:
arduino-install-dir\hardware\arduino\bootloaders\optiboot\
Backup the original files andbefore overwrite both files.
Then compile by running:
make atmega328
make atmega1284p

##License
GPL 3.0. See License.txt file.

Optiboot is an easy to install upgrade to the Arduino bootloader within Arduino boards. It provides the following features:

  * Allows larger sketches. Optiboot is a quarter of the size of the default bootloader, freeing 1.5k of extra space.
  * Makes your sketches upload faster. Optiboot operates at higher baud rates and has streamlined programming.
  * Adaboot performance improvements. Optiboot runs your sketches sooner, with no watchdog issues.
  * Compatible with 168 and 328 Arduinos including Lilypad, Pro, Nano
  * Believed to work with ATmega1280 ("Mega"), ATmega644 ("Sanguino"), and ATmega1284 ("Mighty")
  * Supports several additional AVR chips (ATmega88, ATmega32)

Optiboot is now installed by default on the Arduino Uno. It can be installed on all older mega8, 168 or 328 based Arduinos.

## Additional Documentation
More detailed documentation is being added (slowly) to the [repository wiki](https://github.com/Optiboot/optiboot/wiki).

## To install into the Arduino software ##
  1. Download the latest using Git or the Zip download feature of GitHub.  If you download as a zip, also extract it.
  1. You will need to be using a recent version of the [Arduino environment](http://arduino.cc), version 18 or later.
  1. Create a 'hardware' directory inside your sketches folder.
  1. Copy the optiboot directory into the hardware directory.
  1. Restart the Arduino software. New boards will appear in the Tools>Board menu.

## To burn Optiboot onto an Arduino board ##
  1. Select the appropriate Optiboot board type (or non-Optiboot if you want to change back)
  1. Connect your Arduino to an ISP programmer [[Installing]]
  1. Use the 'Burn Bootloader' item in Arduino.
  1. You can then upload sketches as normal, using the Optiboot board type.

----

> Although it has evolved considerably, Optiboot builds on the original work of Jason P. Kyle (stk500boot.c), [Arduino group (bootloader)](http://arduino.cc), [Spiff (1K bootloader)](http://spiffie.org/know/arduino_1k_bootloader/bootloader.shtml), [AVR-Libc group](http://nongnu.org/avr-libc) and [Ladyada (Adaboot)](http://www.ladyada.net/library/arduino/bootloader.html).

> _Optiboot is the work of Peter Knight (aka Cathedrow). Despite some misattributions, it is not sponsored or supported by any organisation or company including Tinker London, Tinker.it! and Arduino._  
> Maintenance of optiboot was taken over by Bill Westfield (aka WestfW) in 2011.
