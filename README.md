# AlphaLite
Full featured single node RotorHazard timer

Usage Information

Power

There are two inputs to the device; a USB C connector and an MR30 connector. Both inputs are directly connected together. DO NOT connect power input at both connectors at the same time!

Unit will power on when it receives 5v at either input. You may shut the unit off by using the shutdown button in the RotorHazard admin page, or pressing and holding the button on the bottom of the unit labeled "shtdwn" for 4 seconds. Once the green light on the top of the unit(pi) turns off ~10sec, you may safely unplug your unit. 

At power on(plug in), you will first be greeted by a Red led on the bottom of the unit to indicate a valid power supply. The White led on the bottom of the unit represents the stm32 processor activity. It should be slowly blinking white. Once connected to the RotorHazard web server the stm32 led should be rapidly blinking.

Connect

   Wireless - WiFi
   
The pi is running a script named accesspopup to handle automatic wifi hotspot. More info available at https://www.raspberryconnect.com/projects/65-raspberrypi-hotspot-accesspoints/203-automated-switching-accesspoint-wifi-network
please read it!
   
When the pi boots up, it will first try to connect to a known local wifi network. If no known network is available, the pi will start its own wifi hotspot. You can access this hotspot with these credentials
   Name: alphaLite timer
   Password: password

   Wired

You may connect to a wired network in two ways. 
First, you may power the unit via its mr30 connector and then connect a simple ethernet to usb c adapter.
You may also choose to use an ethernet + poe to usb c + pd converter to supply both power and data to your unit over one cable.

Control

When connected to the timer via its local hotspot, you may connect to it @    IP address: 192.168.50.5
This ip address may be used to ssh, or sftp into the timer should you need.
   Username: administrator
   Password: password

The RotorHazard server will be available @
IP address: 192.168.50.5:5000
via your web browser.
   Username: admin
   Password: rotorhazard

When connected to a known wifi network you must currently determine your own IP address. No static IP is currently implemented.

RGB LED!

The unit provides a 5v logic RGB led control output, compatible with ws2812 etc on the MR30 connector. 
Our preference is that you DO NOT power your leds through the unit. However, the unit is specified to condfidently handle the maximum current availabe in the USB spec of 3A @ 5v passed from USB through to the MR30 output, if your power source is capable.
The unit itself needs ~1A,+ more at startup.
This should leave enough headroom to run a 24" flag pole of about 34 leds at max brightness or a RaceGOW gate of 110 leds at medium brightness.
You are responsible for safe operation of your unit. An led power draw calculator can be found at https://wled-calculator.github.io

Hardware Info

The stm32f103 is connected to the Raspberry Pi Zero 2 W via its primary UART. Under RotorHazards advanced settings you will need to set the node address as "/dev/serial0"; "serial0" alone is not sufficient and may cause a lockout requiring you to manualy delete the config.json file located in /RHdata to restore operation. 

Power Schemes

There are several configurations in which this unit may be operated in.
First is to use a usb pd board which then splits power to the timer's mr30 and gate leds individualy. This powers the led's directly rather than running the current through the timer.
Secondly, you may power the timer via usb c, and directly power either a flag or a 24" gate via the mr30 for both power and signal. A minimum of 5v 1.5a supply needed, 3a recommended.
You may provide both power and data over the usb c port. With the correct adapter you can run poe to your location, then convert to usb c + pd and get both hardwire data and power. i.e. xxxxx

Backpack

An external ESP32 ELRS backpack may be connected to the USB port provided the connection is unused. 
