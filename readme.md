# OpenHUDware.sky

V2 This updated version is based on my first DIY drone. Built on the cheap using an untested flight controller I banged together out of a couple of dev boards and the ARDUPILOT code.

The new version replaces the STM32 flight controller with an ESP32 flight controller. I've been messing around with ESP32 for computer vision (including for the drone) and wanted to try it out as a flight controller.

## Goals
* basic remote control flight
* autonomous flight (GPS waypoint etc)
* camera feed (only while within TX distance)
* object avoidance
* facial recognition
* target tracking
* gesture control


### components
	brain
    ▪ ESP32-cam w/5MP PLUS OV5642
    ▪ ESP32-S3 devkit C
    ▪ GPS MODULE W/ ANTENNA (NEO-M8N) AU$54.88
    ▪ MPU-9250 GY-9250 9-axis gyro AU $11.79

Existing flight controllers supported by the ArduPilot project (i.e. PixHawk Standard) are based on the STM32 series of microcontrollers. In this iteration of the project (v2), an ESP32 development board (ESP32-s3 Devkit C) was chosen as a substitute as it provides improved processing speeds (compared to PixHawk4 standard) at a fraction of the cost, while still allowing easy wiring and not requiring custom PCB manufacture (which would be required if building from the chip up). The ESP board also offers integrated wifi, plenty of RAM and dual core processing. 

Most FPV drones use analog video and video transmitters as well as RC transmitter and revceiver pairs. For this design digital video and digital transmission were chosen to facilitate easy image processing for AI integration. A digital control system was also chosen as direct user control is a minor focus of the project and can still be acheived digitally without dedicated RC componentry. 

	base
    • F450 Flame Wheel KIT Drone With Camera 450 Frame For RC MK MWC 4 Axis RC Multicopter Quadcopter Heli Multi-Rotor with Land Gear AU$22.31
    • 2205 2300KV CW CCW Brushless Motor With LittleBee 20A/30A BLHeli_S ESC for FPV RC QAV250 X210 Racing Drone Multicopter AU $63.25x1
    • Youme 3S Lipo Battery 11.1V 5200mah 4500mah 3300mah 6500mah 50C 60C with T Plug XT60 XT90 For RC Drone Car Monster Boat Airplane AU $37.90x1 

    controller
Manual control is acheived using an android app connected to the ESP32
Looking at building a controller with another esp32 and some joysticks. 

 

## Firmware/Software
Ardupilot for ESP32 is build according to [these](https://github.com/ArduPilot/ardupilot/tree/master/libraries/AP_HAL_ESP32) instructions.
Note that I encountered bugs during my build. 
These are reported 
* [here](https://github.com/ArduPilot/ardupilot/issues/21843)
* [here](https://github.com/ArduPilot/ardupilot/issues/21842)
* [here](https://github.com/ArduPilot/ardupilot/issues/21695), and 
* [here](https://github.com/ArduPilot/ardupilot/issues/21675), with my workarounds. 


### .construction()
The basic build process followed common self-build drone steps, such as those outlined in [this](https://create.arduino.cc/projecthub/akarsh98/diy-arduino-based-quadcopter-drone-948153) tutorial.
There is no need for an external telemetry / control module as in the previous build, as the flight control software can connect directly to the ESP 32 over wifi.

