## Locating Your Device USB Port
Windows and MAC should automatically install the necessary drivers and the
Arduino IDE
will tell you the COM port. Linux can potentially require a few extra steps if
the IDE can't recognize the port.

### Linux:

1. Disable BRLTTY, which will reject the arduino as a serial device.
> $ systemctl stop brltty-udev.service
> 
> $ sudo systemctl mask brltty-udev.service
> 
> $ systemctl stop brltty.service
> 
> $ systemctl disable brltty.service

2. Make sure your USB-B connector is fully inserted into the arduino board.

The arduino board should now appear in the Arduino IDE. In case it does not, here are some commands and outputs that may be helpful:

4. Run lsusb. The arduino should sho up as QinHeng Electronics CH340 serial converter. 
> $ lsusb
> 
> Bus 001 Device 035: ID 1a86:7523 QinHeng Electronics CH340 serial converter

4. You can locate the USB comms using the following commands, with their exp
> $ find /dev/ttyUSB*
> 
> /dev/ttyUSB0

> $ find /sys/bus/usb/devices/usb*/ -name dev
> 
> /sys/bus/usb/devices/usb1/1-4/1-4:1.0/ttyUSB0/tty/ttyUSB0/dev



## Programming Your Device
The easiest way to run avrdude for your filesystem is to Download the Arduino IDE and directly view the programming command for your filesystem.

1. Navigate to https://www.arduino.cc/en/software and download the Arduino IDE for your respective operating system.
2. Follow the instructions to install for your operating system.
3. Once installed go to the top left of the IDE window and hover over the file tab and select "Preferences"
4. Halfway down the pop up there are check boxes labeled "Show Verbose Output during", here check the box beside upload.
5. Flash an empty or Hello World program onto the board. 
	5a. "Tools"->"Board"->"Arduino AVR Board"-> Select "Arduino Uno"
	5b. "Tools"->"Port"-> Select your port
	5c. "Sketch"->"Upload"
6. Once the test has uploaded click on the "Output" tab at the bottom left of the IDE and scroll up until you see red text from the upload process.
7. At the top of the upload process there should be a command of the following form:

Linux:
> $ avrdude  -v  -patmega328p -carduino -P/dev/ttyUSB0 -b115200 -D -Uflash:w:test_code.ino.hex:i
	
 Windows:
 > $ C:\Users\User\AppData\Local\Arduino15\packages\arduino\tools\avrdude\6.3.0-arduino17\bin\avrdude -C C:\Users\User\AppData\Local\Arduino15\packages\arduino\tools\avrdude\6.3.0-arduino17/etc/avrdude.conf -v -V -patmega328p -carduino -P COM3 -b115200 -D -Uflash:w:C:\Users\User\desktop\file.hex:i
8. Copy this command and save it. To upload the binary hex files provided for the challenges use this command in your OS's command terminal and change the file (using an absolute path) to upload the files once downloaded.
	8a. You may need to add avrdude to PATH or install avrdude directly (e.g. sudo apt-get install avrdude).
	
## Serial Communication
Challenge messages will be printed out over the serial port, and several challanges require you to send messages to the board over serial. We configure the commuication to be at 115200 baud rate. You can use the Arduino IDE to send and recieve messages ("Tools"->"Serial Monitor"), or you can use you own terminal (i.e. minicom, PUTTY). 