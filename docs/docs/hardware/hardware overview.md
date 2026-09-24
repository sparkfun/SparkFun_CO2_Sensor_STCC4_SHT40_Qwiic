# Hardware Overview

Let's take a closer look at this Qwiic breakout and the major components on it.

## STCC4 CO<sub>2</sub> Sensor

The STCC4 CO<sub>2</sub> sensor from Sensirion uses thermal conductivity (TC) to directly measure actual CO<sub>2</sub> concentrations from 400 to 5000 ppm (parts per million) with an accuracy of &plusmn;100ppm + 10% of the total readings. It outputs a calibrated digital signal that works with temperature and humidity data sent to it by the SHT40. It has a digital resolution of 1 ppm and a response time of ~20s. 

The STCC4 measures CO<sub>2</sub> with a digital resolution of 1ppm and a response time of 20s. It accepts a supply voltage between 2.7 to 5.5V (3.3V Typical) and consumes very little current. The STCC4 consumes an average of  Continuous Mode: 950&micro;A in continuous mode, 100&micro;A during single shot measurements, 55&micro;A during idle mode and 1&micro;A while in sleep mode (all values are with the internal heater OFF). The sensor communicates over I<sup>2</sup>C with two selectable addresses, **0x65** (Default) and **0x64**. The address can be adjusted using the ADDR jumper. Refer to the Solder Jumpers section below for more information. For a complete overview of the STCC4, refer to the [datasheet](/ref/STCC4.pdf)


### Calibration Algorithm

The STC44 features an automatic self-calibration (ASC) algorithm. This algorithm allows for stable readings over time with very little maintenance. The algorithm assumes the sensor is exposed to fresh air that contains a CO2 concentration of at least 400 ppm once a week. This algorithm requires an initial operation period of 12 hours for the sensor to achieve the sensor's measurement accuracy. Once this initial period completes, the sensor stores the first calibration state for subsequent power cycles. If the sensor is powered down for more than three hours, it's recommended to run the sensor for an hour to resume measurement accuracy.


## SHT40 Temperature and Humidity Sensor

The SHT40 is a highly accurate, low power temperature and humidity sensor that measures temperature with an accuracy of &plusmn;0.2&deg;C across a measurement range of -40 to +125&deg;C. It measures humidity with an accuracy of &plusmn;1.8% RH (relative humidity) from 0 to 100% RH. The sensor consumes very little power with a max current draw of 500&micro;A during measurements and a typical draw of 0.08&micro;A while the sensor's internal heater is off. Current draw with the heater on significantly raises the sensor's current draw to a max of 100mA.

## Connectors

### Qwiic Connectors

The board has a pair of Qwiic connectors to make it easy to integrate into a Qwiic circuit. These connect to the both the STCC4 and SHT40's I<sup>2</sup>C signals along with 3.3V and ground to power the board and communicate with the sensors.

### Plated Through-Hole (PTH) Header

The board also routes the same signals as the Qwiic connectors (SDA, SCL, 3.3V and Ground) to a 0.1"-spaced plated through-hole header for users who prefer a soldered connection.

## LED

The lone LED on this breakout is a red power status LED.

## Solder Jumpers

The board has three solder jumpers labeled <b>ADDR</b>, <b>I<sup>2</sup>C</b> and <b>LED</b>. The list below outlines their functionality, default states and any notes on their use:

* <b>ADDR</b> - The ADDR jumper sets the STCC4's I<sup>2</sup>C address to <b>0x64</b> by pulling the ADDR pin to GND. This jumper is CLOSED by default. Open the jumper to pull the ADDR pin to VDD and switch to the alternate address, <b>0x65</b>.
* <b>I<sup>2</sup>C</b> - The I<sup>2</sup>C jumper pulls the STCC4 and SHT40's SDA and SCL lines to 3.3V through a pair of <b>2.2k&ohm;</b> resistors. The jumper is CLOSED by default. Completely open this jumper to disable pullups if necessary.
* <b>LED</b> - The LED jumper completes the power LED circuit. It CLOSED by default. Open the jumper to disable the power LED.

## Board Dimensions

This breakout matches the Qwiic standard and measures 1" x 1" (22.5mm x 22.5mm) and has four mounting holes that fit a 4-40 screw.