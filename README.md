# Homebridge Plugin for LAN Control of Fujitsu Anywair devices

This project was an **experimental** fork of https://github.com/rchrch/homebridge-mhacwifi1-lan/fork intended
to remove certain accessories that don't work with the Fujitsu implementation. Unfortunately, this approach
is not going to work.

## Why it won't work

Our Fujitsu units use a Wifi module created by Intensis which provides the ability to control the air conditioners
over the LAN. The ideal would be to use this API to allow control via Apple's HomeKit.

While it is certainly possible to read and control the air conditioning units over the LAN, unfortunately, HomeKit
requires the current temperature to be included in the HeaterCooler implementation. Sadly, the Fujitsu units do
not provide this data to the Intensis dongles (the dongles themselves do support this).

While it's possible to do hacky things such as using the set point temperature as the ambient temperature, this
approach will provide a crappy experience in my home, which is not really something I want to do. It's possible,
but it's not good enough for me.

So, unfortunately, from what I've been able to tell, it will be very difficult to create a single, stand-alone
HomeKit plugin for Fujistu air conditioners that works the way Apple intended.

## What can we do instead?

All is not lost!

I'm currently considering a port of the original JavaScript code to an MQTT based data collector
which can run as a daemon and monitor my air conditioning units. My current plan is to combine the Fujitsu
control data with data from a separate ZigBee sensor, into a combined HomeKit control that's published
using Node-Red.

I've already got the bones of this working, so the MQTT interface is really the last step.

I'll post an update to this page if I am able to get it to work.