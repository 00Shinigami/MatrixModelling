# MatrixModelling
repository about planing and programming my Matrix Project
I will program the codes once for Raspberry Pi and for Arduino


Helped Sites: 
- https://max7219.readthedocs.io/en/0.2.3/
- https://pinout.xyz/
- https://www.amazon.de/-/en/AZDelivery-MAX7219-Parent-32/dp/B079HVW652/ref=sr_1_22?crid=11HHEH02H8Y1P&keywords=pi%2Bmatrix%2Banzeige%2B4fach&qid=1649250100&s=computers&sprefix=pi%2Bmatrix%2Banzeige%2B4%2Bfach%2Ccomputers%2C60&sr=1-22&th=1


Raspberry Pi:

- Library installation:
```sh
sudo apt-get install python-dev python-pip
```

```sh
sudo pip install max7219
```


- Or alternative clone from github.com:

```sh
git clone https://github.com/rm-hull/max7219.git
```
```sh
cd max7219
```
```sh
sudo pip install -e .
```

For the next step you have to do some settings in ur raspbian system:
```sh
cd max7219
```
```sh
sudo apt-get install python-dev python-pip
```
```sh
sudo pip install spidev
```
```sh
sudo python setup.py install
```

The GPIO pin-outs are connect as showed:

|Board Pin | Name | Remarks   |  RPiPin | RPi   | Function|
|1	        |VCC  |+5V Power  |2	    |5V0    | +V      |
|2	        |GND  |Ground	  |6	    |GND    |-V       |
|3	        |DIN  |Data In	  |19	    |GPIO 10|(MOSI)   |
|4	        |CS	  |Chip Select|24	    |GPIO 8 |(SPI CE0)|	     
|5          |CLK  |Clock	  |23       |GPIO 11|(SPI CLK)|


 Pre-requisites:
 By default, the SPI kernel driver is NOT enabled on the Raspberry Pi Raspian image. You can confirm whether it is enabled using the shell commands below:
 
```sh
$ lsmod | grep -i spi
spi_bcm2835             7424  0
```
Depending on the kernel version, this may report spi_bcm2807 rather than spi_bcm2835 - either should be adequate.
And that the devices are successfully installed in /dev:

```sh
$ ls -l /dev/spi*
crw------- 1 root root 153, 0 Jan  1  1970 /dev/spidev0.0
crw------- 1 root root 153, 1 Jan  1  1970 /dev/spidev0.1
```


max7219 cascaded:
If you have more than one device and they are daisy-chained together, you can initialize the library with:

```sh
import max7219.led as led

device = led.matrix(cascaded = 3)
device.show_message("Hello world!")
```

Online References:

- http://hackaday.com/2013/01/06/hardware-spi-with-python-on-a-raspberry-pi/
- http://gammon.com.au/forum/?id=11516
- http://louisthiery.com/spi-python-hardware-spi-for-raspi/
- http://www.brianhensley.net/2012/07/getting-spi-working-on-raspberry-pi.html
- http://raspi.tv/2013/8-x-8-led-array-driven-by-max7219-on-the-raspberry-pi-via-python
- http://quick2wire.com/non-root-access-to-spi-on-the-pi
- https://max7219.readthedocs.io/en/0.2.3/

 Arduino:

 The MAX7219 LED display driver communicates with the Arduino through SPI (Serial Peripheral Interface).
 With an SPI interface there is always one master device (the Arduino) that controls the peripheral devices (also known as slaves). You can control the display either through the Arduino’s AVR microcontroller hardware SPI interface or three arbitrary digital pins (software SPI).

The hardware SPI pins (MOSI, MISO, and SCK) are at a specific location on each Arduino board. This interface is faster than using software SPI, but you will need to use the following fixed output pins:
 | Board | MOSI | MISO | SCK | Level |
 | Aduino Uno | 11 or ICSP-4 |	12 or ICSP-1 |	13 or ICSP-3 |	5 V
 -
 To control MAX7219 displays you only need to make three connections:

- MOSI (Master Out Slave In) connected to DIN – The Master line sending data to the peripherals.
- SCK (Serial Clock) connected to CLK – The clock pulses which synchronize data transmission generated by the master.
- SS (Slave Select) connected to CS – The pin on each device that the master can use to enable and disable specific devices.

You can daisy chain multiple displays to create one large display by connecting DOUT of the first display to DIN of the next display. VCC, GND, CLK, and CS are shared between all of the displays.

| MAX7219 Display | Arduino  |
| VCC             | 5V       |
| GND             | GND      |
| DIN             | 11 (MOSI)|
| CS              | 3 (SS)   |
| CLK             | 13 (SCK) |

Installing the MD_Parola and MD_MAX72XX Arduino libraries:

This are some functions and features of the library:
- Left, right, or center text justification
- Text scrolling with entry and exit effects
- Control display parameters and animation speed
- Multiple virtual displays (zones) in each string of LED modules
- Support for hardware SPI interface
- User-defined fonts and/or individual characters substitutions
- Support for double-height displays
- Support for mixing text and graphics on the same display

You can install the libraries via the Library Manager of the Arduino IDE. Go to Tools > Manage Libraries… or type Ctrl + Shift + I on Windows. The Library Manager will open and update the list of installed libraries.
Search for ‘MD_MAX72XX’ and look for the libraries by majicDesigns. Select the latest version and then click install. Make sure that you install both the MD_MAX72XX library and the MD_Parola library.

Online References:
- https://how2electronics.com/8x8-led-matrix-max7219-arduino/
- https://microcontrollerslab.com/max7219-dot-matrix-display-arduino-tutorial/
