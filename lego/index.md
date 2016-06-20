---
layout: page
title: "Lego"
description: ""
group: navigation
---
{% include JB/setup %}

# The plan
My plan is to automate the operation of the [Lego 60051 Highspeed passenger train](http://brickset.com/sets/60051-1/High-Speed-Passenger-Train), without any alteration of the set it self.

I plan to put a RFID tag in the middle train car, to know when the train is arriving at the station. That is have one RFID reader at the station, and one before and after the station, to decelerate and accelerate the trains accordingly.

# The gear
* [Lego 60051 Highspeed passenger train](http://brickset.com/sets/60051-1/High-Speed-Passenger-Train)
* [Arduino (china clone)](http://www.electrodragon.com/product/edarduino-mega-c-arduino-compatible-r3-board-ch340/)
* [IR Transmittter](http://www.electrodragon.com/product/kit-universal-ir-receiver-gp1ux311qs-and-ir-led-transmitter/)
* [RFID Reader](http://www.electrodragon.com/product/mifare-rc522-rfid-card-readerdetector-ic-card/)
* And some wires, and resistors to connect the different items.

## The train
<img src="/assets/images/WP_20160612_09_53_52_Pro.jpg" style="width:50%;height:auto;">

## The Board
<img src="/assets/images/WP_20160612_09_54_01_Pro.jpg" style="width:50%;height:auto;">

## The RFID tag reader.
<img src="/assets/images/WP_20160612_09_54_11_Pro.jpg" style="width:50%;height:auto;">

# Software
This will contain the list of software and libraries I have used.

* [Power Functions library](https://github.com/jurriaan/Arduino-PowerFunctions)
* [RFID Library](https://github.com/miguelbalboa/rfid)
* [Arduino IDE](https://www.arduino.cc/en/Main/Software)
 

# The article index
The newest post is on top :)

<ul>
{% assign pages_list = site.posts %}
{% assign group = 'LegoAutomation' %}
{% include JB/pages_list %}
</ul>
