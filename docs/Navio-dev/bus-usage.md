#####Detecting I2C devices with i2cdetect tool
Tool called i2cdetect allows you to see devices connected to the I2C bus. It's avaiable in the package i2c-tools, to install it run:

```bash
sudo apt-get install i2c-tools
```
Run it like this:

```bash
sudo i2cdetect -y 1
```
Where 1 is the number of I2C bus.
The result should look like this:

```bash
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: 40 -- -- -- -- -- -- -- 48 -- -- -- -- -- -- --
50: 50 -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
70: 70 -- -- -- -- -- -- 77
```
You should see all devices that responded to their addresses.
####Addresses of onboard devices
I2C devices:

* ADS1115 - 0x48
* MS5611 - 0x77
* MB85R - 0x50
* PCA9685 - 0x40, 0x70 (allcall address)

SPI devices:

* U-blox NEO - /dev/spidev0.0
* MPU9250 - /dev/spidev0.1

#####Using UART port
By default UART on Raspberry Pi is used for serial console. To use UART for custom data serial console has to be disabled. It can be done by using the raspi-config utility:

```bash
sudo raspi-config
```
Open "Advanced options" -> "Serial console" and disable it. 
Now you can use /dev/ttyAMA0 as a UART.
