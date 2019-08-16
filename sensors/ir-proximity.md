# Interfacing 'KY-032 (IR Proximity) sensor' with 'Raspberry Pi 4' using Shunya Interfaces


![](images/rpi4.jpg)


## Introduction

We are going to interface an KY-032 (IR Proximity) sensor on Raspberry Pi 4 
with Shunya O/S using Shunya Interfaces library.


# Materials required :
- Raspberry Pi 4B
- Raspberry Pi 4B compliant power supply
- 8GB or bigger micro SD card


# Connections :
![](images/-connections.jpg)

There are 3 pins to IR Proximity Sensor module KY-032
1. VCC (also called +) - Connect it to 3.3V on the dev Board
2. GND (also called -) - Connect it to GND on the dev Board
3. Signal (also called S) - Connect it to any GPIO pin on the dev Board

> Note: The physical pin number of the GPIO pin that you have connected to and replace #define sensorpin 11 with  #define sensorpin (your-GPIO-pin-number) in the code below.

- Connection between raspberrypi and KY-032 

| KY-032  |     <----->    | Raspberry Pi 4 |
| ------    | ----- |------- |
| S     | <----->  | GPIO |
| VCC     | <----->  | Vcc |
| GND     | <-----> | GND |


# Procedure 

## Step 1: Install Shunya OS on Raspberry pi 4
1. Download Shunya OS from the [official release site](http://shunyaos.org/beta-release/)
2. Shunya OS guys have a decent tutorial on [Flashing Shunya OS on Raspberry Pi 4.](http://docs.shunyaos.org/boards/Raspberry-Pi-4.ht)
3. Insert micro SD card into Raspberry Pi 4


## Step 2: Install Shunya Interfaces
1. Connect to the wifi using the command
```
    $ nmtui
```
2. Installing the Shunya Interfaces is easy, just run the command  
```
    $ sudo apt install shunya-interfaces
```

# Code :

```c

#include<stdio.h>
#include <shunyaInterfaces.h>

/*define sensor pin interface*/     
#define sensorpin 11 

int main()
{
        int val;     
        /*Initialize Shunya Interfaces library*/
        shunyaInterfacesSetup(); 
        /*Initialize physical pin connected to the Sensor*/
        pinMode (sensorpin, INPUT);
        while(1)           
        {
                /*Read the Sensor*/
                val = digitalRead(sensorpin); 
                if(val == HIGH) {
                	printf("Obstacle Detected!!");
                } else {
                        printf("No Obstacle Detected.");
                }
                delay (100);
        }

        return 0;
}

```

## Save the code
Save the code in .c


## Compile
1. Open terminal
2. Run command 

```
    $ gcc -o ir-proximity ir-proximity-sensor-example.c 
    $ -lshunyainterfaces
```

## Run 
1. Open terminal 
2. Run command

```
    $ ./ir-proximity
```

# Credits :

Check out this cool new library for creating your own iot projects - [Shunyainterfaces](https://github.com/shunyaos/Shunya-Interfaces)

[@ShunyaOS](http://shunyaos.org/) || [@iotiot.in](http://iotiot.in/)
