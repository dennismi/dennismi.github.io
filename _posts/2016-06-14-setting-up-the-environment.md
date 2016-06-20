---
layout: post
title: "Setting up the environment"
description: "Lego 60051 automation arduino"
category: LegoAutomation
group: LegoAutomation
tags: [lego,arduino,60051]
theme_name: dmal
---
{% include JB/setup %}

This is fairly easy :) 

Download the Arduino software. Install it.

# The Anatomy of an Arduino program
The anatomy of an Arduino program, is fairly simple. There are two methods that need to be implemented, they are called _setup_ and _loop_. 

The language looks alot like C, and I cannot tell the difference between Arduino C, and standard C, so for me they are the same.

{% highlight c %}
void setup() {
  // put your setup code here, to run once:
}

void loop() {
  // put your main code here, to run repeatedly:
}
{% endhighlight %}

The comments are pretty self-explanatory.    
One issue here is that when coding the main loop, is the fact that the code will run in a loop.    
This is a fact that need to be accounted for. This is especially true, if you are working in an object oriented/event driven world in your day job, like me :)
There is a way to use the [RFID readers](http://www.electrodragon.com/product/mifare-rc522-rfid-card-readerdetector-ic-card/) with [IRQ](https://en.wikipedia.org/wiki/Interrupt_request_(PC_architecture))  

My first thought will be to just getting it to read the [RFID tag](http://www.electrodragon.com/product/mifare-rc522-rfid-card-readerdetector-ic-card/) in the loop, then I will try and do the IRQ thing.

 
