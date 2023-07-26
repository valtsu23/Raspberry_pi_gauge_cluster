# Raspberry_pi_gauge_cluster

![image1](/Pictures/IMG_20230724_183946.jpg)

Video: https://youtu.be/ISC5q4k9wDg

# How it works
Feather receives messages from Can Bus and picks rpm signal for shift light. Feather sends same can bus data bytes over Uart to Raspberry pi. 
Feather reads amount of ambient light from photodiode and controls screeen broghtness with pwm. 
Device needs switched 12V and continous 12v from battery to work correctly. Switched power wakes up the device and Raspberry pi starts booting. When Can Bus stream is lost Raspberry pi automatically starts shutdown process and sends message to Feather. After specified time Feather turns off the relay connected to continous 12v and cuts power from the device. The device doesn't consume any power after shutdown. 

# Something to improve
- More testing needed
- Adding Raspberry pi setup guide
- Shortening the start up time (about 25 seconds now)
- More pictures
- Case needs better desing and I'll publish .stl and Freecad files after that

### Technical specs:
- Raspberry Pi 4 Model B 4GB
- 5" sunlight readable display with touchscreen from Makerplane:
  - https://store.makerplane.org/5-sunlight-readable-touchscreen-hdmi-display-for-raspberry-pi/
- DIY PCB inside the enclosure controls power for all devices and receives Can Bus messages and sends them over UART to Raspberry pi
  - DC-DC converter
  - Adafruit Feather M4 CAN Express with ATSAME51
  - Adafruit DS3231 Precision RTC - STEMMA QT
  - Screen brighness control
  - Adafruit Neopixel shiftlight control
  - Small relay for power

### Software specs
- Raspberry Pi OS Lite 64bit (bullseye)
  - X server: X.Org
  - Window manager: Openbox
  - Gauge cluster software is based on Pygame graphics library
### Graphic software functions
- There is 6 sensors data (3 left and 3 right) that you can choose to display with touscreen
- bar on the bottom of the screen in normal situation is blue and shows Raspberry pi CPU temperature
- If there is some error detected by ECU or battery voltage is low. Error flags are shown on the bottom of the screen and the bar is red
  
### Can bus data
- Most of the data needed is read from Ecumaster Emu Black can stream
- There is also DIY can bus device sending message id 0x400, which contains
  - turn signals
  - high beam
  - fuel level
  - ambient temperature

### Case (files are not ready to publish)
- filament is PETG

![image1](/Pictures/Raspi_Feather.png)

### Part list for PCB:
  #### From www.partco.fi
    - PCH2596S DC-DC converter (LM2596S)
    - 3A diode 
    - 1A diode 2pcs
    - FTR-F3AA005V (small 5V relay)
    - BPW42 3mm phototransistor or similar
    - 2N3904 NPN transistor or similar
    - B3F-31XX Omron switch or SKH KKK 2 from partco.fi
    - 2k2 0,6w resistor
    - 150k 0,6w resistor 
    - 2x13 male pin header with long pins (20mm total length)
    - 2x13 female smd pin header (soldered to display pcb)
    - 1x40 female pin header
    - 1x40 male pin header
    - 0,22mm2 - 0,5mm2 wires (0,5mm2 recommended for power and ground)
#### From Adafruit
    - Adafruit DS3231 Precision RTC - STEMMA QT
    - Adafruit Feather M4 CAN Express with ATSAME51
  #### From Ebay
    - 5pin JST-SM connector pair

