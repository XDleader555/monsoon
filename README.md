# VW MKIV Monsoon Amplifier
I've been having a bit of fun reverse engineering the factory Monsoon amplifier. I'm just going to drop this here in case anyone's bored. If you have any requests or additional information you'd like to add, feel free to leave a reply. I'll update this post as I compile new information.

## After Market Head Units, Manual Amp Turn On, and Parasitic Draw
The factory Monsoon head unit applies a DC voltage to the positive front left output to switch on the amplifier. When the car is turned off, the front left output is grounded to shut off the amplifier.

Aftermarket head units obviously don't supply this DC signal. Speaker level voltage is enough to drive the transistor which turns on the amp, but since most cheap head units don't ground the output during standby the amplifier will most likely stay on after the car is shut off. This can result in a parasitic draw while the car is off.

The best solution for an aftermarket head unit, or to fix a factory Monsoon amplifier with parasitic draw, is to wire up the Manual Amp Turn On circuit. At the same time, the Automatic Amp Turn On circuit should be disconnected to avoid injecting DC voltage on the speaker input and frying your head unit.

Pin 12 on the Grey connector is for the turn-on wire. You'll need to source a repair pin to populate this connector, or hop on over to the parts yard and yank one yourself. You'll have to run this wire all the way up to your head unit amp turn-on wire or tap the accessory wire. If you run a wire, you might as well run the RCA/Power/etc. for a subwoofer.

In addition to the new turn-on wire, you'll also have to move the turn on resistor from the Left Front speaker signal to the Pin 12 traces. Take the amp out of the car, unscrew the four screws on the bottom of the amp, and pop off the bottom and top covers. De-solder the turn-on resistor and move it to the location indicated in the photo below. A good soldering iron, flux, and needle point tweezers highly recommended.

![Preview](https://github.com/XDleader555/monsoon/raw/master/res/MonsoonResistorMove.jpg)

## Line Level Input
Contrary to popular belief, the Monsoon amplifier will accept line level input. The input is isolated at the first op-amp, which is setup as a voltage follower. Since this circuit is high impedance, any line level input can be used to drive it.

Just make sure you wire up the Manual Amp Turn on mentioned earlier, since line level voltage isn't enough to drive the transistor for the Automatic Amp Turn On. It's also isolated from ground, so the amp also won't turn off after the car is shut off.

RCA connectors can be connected directly to the harness connector at the head unit. The example below uses Mini-Fit JR connectors in-between for cleanliness.

![Preview](https://github.com/XDleader555/monsoon/raw/master/res/RCA_harness_adapter.jpg)

## Crossover
Coming soon.

## Speaker compatibility
The amplifier should technically be 2 ohm stable on all channels since the factory rear woofers are 2 ohms. The rest of the woofers/tweeters are 4 ohms.

The tweeters on low-line cars have a high-pass filter capacitor soldered directly to the tweeter. This capacitor is missing on Monsoon equipped cars since the amplifier already has a crossover built into it.

# Pinouts
## 24 Pin Grey Input Connector
| Pin   | Description           | Color     |Notes                                      |
| :---: | --------------------- | --------- | ----------------------------------------- |
| 1     | Right Rear Tweeter +  |           | Circuit Not Populated Hands-free speaker? |
| 2     |                       |           |                                           |
| 3     |                       |           |                                           |
| 4     |                       |           |                                           |
| 5     |                       |           |                                           |
| 6     |                       |           |                                           |
| 7     |                       |           |                                           |
| 8     |                       |           |                                           |
| 9     |                       |           |                                           |
| 10    | Mute                  |           | Circuit Not Populated                     |
| 11    |                       |           |                                           |
| 12    | Amp Turn On           |           | Not Connected                             |
| 13    |                       |           |                                           |
| 14    | Left Rear +           | White     |                                           |
| 15    | Left Rear -           | Black     |                                           |
| 16    |                       |           |                                           |
| 17    | Right Rear -          | Black     |                                           |
| 18    | Right Rear +          | Brown     |                                           |
| 19    |                       |           |                                           |
| 20    | Left Front +          | Yellow    | Automatic Amp Turn On                     |
| 21    | Left Front -          | Black     |                                           |
| 12    |                       |           |                                           |
| 23    | Right Front -         | Black     |                                           |
| 24    | Right Front +         | Green     |                                           |

## 23 Pin Green Output/Power Connector
| Pin   | Description           | Color         | Notes     |
| :---: | --------------------- | ------------- | --------- |
| 1     | Left Rear Woofer +    | Red/Green     |           |
| 2     | Left Rear Woofer -    | Brown/Green   |           |
| 3     | Right Rear Woofer +   | Blue          |           |
| 4     | Right Rear Woofer -   | Brown/Blue    |           |
| 5     | Left Rear Tweeter +   | Brown         |           |
| 6     | Left Rear Tweeter -   | Black         |           |
| 7     | Right Rear Tweeter +  | Green         |           |
| 8     | Right Rear Tweeter -  | Black         |           |
| 9     | Left Front Tweeter +  | White         |           |
| 10    | Right Front Tweeter - | Black         |           |
| 11    | Left Front Tweeter -  | Black         |           |
| 12    | Right Front Tweeter + | Yellow        |           |
| 13    | Left Front Woofer -   | Brown/White   |           |
| 14    | Left Front Woofer +   | Blue/White    |           |
| 15    | Right Front Woofer -  | Brown/Red     |           |
| 16    | Right Front Woofer +  | Red           |           |
| 17    |                       |               |           |
| 18    | Constant 12 Volts     | Red           |           |
| 19    | Chassis Ground        | Brown         |           |
| 20    | Chassis Ground        | Brown         |           |
| 21    | Constant 12 Volts     | Red           |           |
| 22    | Chassis Ground        | Brown         |           |
| 23    | Constant 12 Volts     | Red           |           |

## Delco 82452 Audio Amplifier
I haven't been able to find any datasheets online for this chip. I may de-solder one and characterize it, but I haven't the need to yet.

TDA7396 should be a pin-compatible drop in replacement for the Delco 82452 (Coincidence?)

The diagnostics pin is setup to reduce the signal at the op-amp before it's fed into itself. This includes short-circuit protection, thermal overload, etc.

| Pin   | Description           | Notes                                           |
| :---: | --------------------- | ----------------------------------------------- |
| 1     | IN-                   |                                                 |
| 2     | IN+                   |                                                 |
| 3     | Vs+                   | 12v                                             |
| 4     | ? CD-DIA              | Clipping Detect - Diagnostics. Low during error |
| 5     | OUT-                  |                                                 |
| 6     | GND                   |                                                 |
| 7     | OUT+                  |                                                 |
| 8     | STANDBY               | Standby when Low                                |
| 9     | Vs+                   | 12v                                             |
| 10    | SYNC                  | Connected to all amplifier chips                |
| 11    | MUTE                  | Muted when high (5v)                            |

## Volkswagen Part Numbers
I have no clue why the Jetta and Golf have different amp part numbers. Perhaps they're tuned differently?
| Part Number   | Description                   |
| ------------- | ----------------------------- |
| 1J6 035 456 C | Golf 2 & 4 Doors Monsoon Amp  |
| 1J5 035 456 A | Jetta Monsoon Amp             |

Front woofers are held in by rivets.
| Part Number   | Description                                                   |
| ------------- | ------------------------------------------------------------- |
| 1C0 035 411 E | 2 Ohm 50W 140mm Monsoon Woofer Rear                           |
| 1C0 035 411 G | 4 Ohm 70W 140mm Monsoon Woofer Front                          |
| 3B0 035 411 E | 4 Ohm 19mm Monsoon Tweeter Rear (Todo: Confirm Part Number)   |
| 3B0 035 411 F | 4 Ohm 19mm Monsoon Tweeter Front (Todo: Confirm Part Number)  |

## Schematics
Coming soon.

## Interesting Stuff
- Unpopulated circuit for separate front/rear mute.
- Unpopulated circuit for Manual Mute on pin 10 of grey connector
- Unpopulated circuit leading to Right Rear Tweeter on pin 1 of grey connector. Perhaps for reducing echo for hands-free calling or navigation unit.
- Disconnected circuit for Manual Amp Turn On (see earlier section).

## Surface Mount Marking Decoding
Brief list of surface mount PCB components.
| Marking   | Description                                   |
| --------- | --------------------------------------------- |
| BA14741F  | Low Noise 4 Channel Operational Amplifier     |
| MAW/RBR   | SST6838 NPN Transistor                        |
| MAZ/RFQ   | SST6839 PNP Transistor                        |
| R23       | 2SC3356 NPN Transistor                        |