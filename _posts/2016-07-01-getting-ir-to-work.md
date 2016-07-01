---
layout: post
title: "Getting IR to work"
description: "Lego 60051 automation arduino"
category: "Lego Automation"
group: LegoAutomation
tags: [lego,arduino,60051]
theme_name: dmal
---

I was pondering reading the spec for the [Lego Power Functions](https://github.com/jurriaan/Arduino-PowerFunctions) remote, and creating my own library to talk to the train.    
But I have found a library for communicating with [Lego Power Functions](https://github.com/jurriaan/Arduino-PowerFunctions) devices.
It seems rather robust, so I am going with this.

However most tutorials injects a resistor between the LED and the board, but I want good range on these LEDs so I am going without. Still the range does not appear to be that amazing. Still need to do some more testing on range. 





# This is a full test program 
```c
#include <PowerFunctions.h>

PowerFunctions pf(12, 0);

void setup() {
  // put your setup code here, to run once:
  Serial.begin(9600);  
    while (!Serial);  
}

void loop() {
  // put your main code here, to run repeatedly:
  Serial.println(F("Going full speed"));
  ZeroToFull(RED);
  Serial.println(F("Running for 5 sec"));
  delay(5000);
  Serial.println(F("Slowing"));
  FullToZero(RED);
  Serial.println(F("Stopped for 2 sec"));
  delay(2000);
  Serial.println(F("Stopped for 2 sec"));
  delay(2000);
}

void ZeroToFull(uint8_t channel){
  pf.single_pwm(channel,PWM_FWD1);
  delay(1000);
  pf.single_pwm(channel,PWM_FWD2);
  delay(1000);
  pf.single_pwm(channel,PWM_FWD3);
  delay(1000);
  pf.single_pwm(channel,PWM_FWD4);
  delay(1000);
  pf.single_pwm(channel,PWM_FWD5);
  delay(1000);
  pf.single_pwm(channel,PWM_FWD6);
  delay(500);
  pf.single_pwm(channel,PWM_FWD7);
}

void FullToZero(uint8_t channel){
  pf.single_pwm(channel,PWM_FWD7);
  delay(500);
  pf.single_pwm(channel,PWM_FWD6);
  delay(500);
  pf.single_pwm(channel,PWM_FWD5);
  delay(600);
  pf.single_pwm(channel,PWM_FWD4);
  delay(700);
  pf.single_pwm(channel,PWM_FWD3);
  delay(800);
  pf.single_pwm(channel,PWM_FWD2);
  delay(1000);
  pf.single_pwm(channel,PWM_FWD1);
  delay(1000);
  pf.single_pwm(channel,PWM_FLT);
}
```

This is a good test program for a stationary train, which is lifted above the ground/tracks.
Which equals a stationary LED and stationary train. This is fine, but in the real world, the train moves. 
This gives me the reason to believe that the range on the LEDs is not that great. 
But more on that later

{% include JB/lego %}