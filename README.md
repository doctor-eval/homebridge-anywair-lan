# Homebridge Plugin for LAN Control of Fujitsu Anywair devices

This project was an **experimental** fork of https://github.com/rchrch/homebridge-mhacwifi1-lan intended
to remove certain accessories that don't work with the Fujitsu implementation. Unfortunately, for
a variety of reasons, I've decided to deploy my air conditioning controls using node-red instead of homebridge. 

The code in this repo should still work, but it's very much a hack job. You will probably be better off forking
the original code. I was half way through working out how it all hangs together when I decided not to continue
down the path.

Nevertheless, I did discover how to get the air con units working under Homebridge with this one weird trick...

## Current Temperature

Our Fujitsu units use a Wifi module created by Intesis which provides the ability to control the air conditioners
over the LAN.

One of the biggest challenges I had was that these modules were not reporting current temperature.
This is required by HomeKit... simulating the current temperature (say by using the set point)
results in a very poor experience.

It turns out that the installer had simply not configured the units to use the remote control
sensors, so it wasn't reporting the room temperature. Apparently this is a common problem, and it's
what initially lead me to stop working on this project.

However, it turns out that there is a super-simple fix if you have wall-mounted (wired) remote controls:

    Menu -> Next/Initial Setting -> Next/R.C. Sensor Setting -> *Used

This made the wifi units start transmitting the current temperature immediately, which I picked up
using the REST API. This would make the units compatible with HomeKit using either this module or the original
MHACWIFI1-LAN module.

So it turns out that these units are compatible with the HomeKit module after all! But by the time
I discovered this, I'd moved on.

## Next Steps

While there's nothing wrong with the original code, my requirements are a bit more complex
than is allowed for by the MHACWIFI code - in particular, I want to be able to control multiple units around
the house (kids rooms, living room, etc). This is not supported with the original code and I'd need to make
a bunch of changes to get it working effectively, as well as learning a bunch about HomeKit that I probably
don't care about.

Because I thought I needed to integrate individual sensor reading with the air conditioner units, I
started working on an MQTT integration with the Fujitsu units with the goal of integrating
with node-red and deConz. I like the flexibility of node-red, in particular because it's more configurable than the
Homebridge module, which exposes a lot of settings that don't make sense in my (hardware) case.

Since I got a long way down this path before discovering the R.C. temperature sensor
setting, I'll probably continue with MQTT rather than continue to work on a fork of the homebridge module.

The MQTT module is almost complete, and I'll post a link here once its done.