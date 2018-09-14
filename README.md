# MQTT-Arduino-MEGA-I-O
Arduino Mega 2560 as an MQTT client

This code should be considered ALPHA and use at your own risk.  The code is here to keep a backup.
There is considerable cleanup to be done however it is functional

Lots of debug available on the serial port.

The configuration allows for 24 Digital outputs and 24 Digital inputs.
You can set the PANEL ID hence multiple units can sit on the same MQTT broker.

When the unit powers up it will send all of its inputs via MQTT
If outputs have a retain flag set, the output will follow the MQTT retain flag

Inputs: 
Numbered from 1-24
When the pin is grounded the MQTT payload is 0, when open the payload is 1

Outputs:
Numbered from 1-24
When a payload 1 is sent the output goes HIGH, I did it this way for the cheap chinese relay boards

Useage:
Inputs will automatically send status on pin toggle
stat/20/Input/1 0 for pin shorted to ground
stat/20/Input/1 1 for pin open circuit (has pullups enabled)

Outputs follow the following command **panelID=20**
cmnd/20/Output/1 0  this will turn output 1 on
cmnd/20/Output/1 1  this will turn output 1 off

When an output is turned on, a response is sent back to the broker so you know the output turned on (great for NodeRed)
stat/20/Output/1 0 this ensures the output was turned on
stat/20/Output/1 1 this ensures the output was turned off

When the watchdog times trips it sends an "alive" tele command
tele/20/Status Alive

Known Bugs: Input A0 always reports status on boot, need to find that


