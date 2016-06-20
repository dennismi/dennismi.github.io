---
layout: post
title: "Setting up the environment"
description: ""
category: 
group: LegoAutomation
tags: [lego,arduino,60051]
theme_name: dmal
---
{% include JB/setup %}
This is fairly easy :) 

Download the Arduino software. Install it.

# The Anatomy of an Arduino program
The anatomy of an Arduino program, is fairly simple. There are two methods that need to be implemented, they are called

```
void setup() {
  // put your setup code here, to run once:

}

void loop() {
  // put your main code here, to run repeatedly:

}
```

The comments are pretty self-explanatory. One issue here is that when coding the main loop, is the fact that the code will run in a loop.    
This is a fact that need to be accounted for. This is especially true, if you are working in an object oriented/event driven world in your day job, like me :) 

I am pretty sure that when i get the RFID tag reader in the loop, I can better control the flow of events. 
