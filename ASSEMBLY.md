# Turntable Traction Drive Assembly Guide

I've tried to use off-the-shelf parts as much as possible in order to make this design accessible. The vast majority of the hardware is sourced from McMaster-Carr. This should provide a reliable source for maintenance and customizations. In some cases I've gone to Amazon and Ebay to get parts which are otherwise too expensive.

A Complete Bill Of Materials is available here: [Bill Of Materials](BOM.md)

## Note to Makers

By following these instructions and building this machine you will be creating a powerful piece of machinery which will last a long time. Pause to consider both the longevity of the machine and how that may impact your continuing liability.

:warning: **Before Proceeding, make sure you have read and understood the [SAFETY](SAFETY.md) section of the documentation.**

:warning: **Before Proceeding, make sure you have read and understood the [Limitations](SAFETY.md#Limitations) section of the documentation.**

## Sourcing The Motor

The motor, and gearbox can be the most difficult parts to source. If you try to match precisely what I have used you will end up paying top-dollar. A more economical way to source the powertrain is to go on ebay and look for a used parts. Here are the important parameters:

| Feature | Value |
| -- | -- |
| NEMA Frame | 145TC |
| RPM | 1725 |
| Voltage | 208-230 |
| Phases | 3 |

The frame designation describes the precise size and layout of the motor bolts and face. Motor RPM is listed because a 1725 (or 1800RPM) motor is better suited for high-torque applications. Voltage isn't really your problem (since the VFD will be creating the motor voltage) all you really want to do is make sure you're selected a 200V class motor. Three phase is specified because this is necesary for the inverter to control the speed of the motor.

If you deviate too much from this prescription you may have to customize the `Base Plate` and `Motor Gusset` parts in order to fit your motor. You will also have to make sure your gear-reduction fits correctly.

## Sourcing The Gearbox

The gearbox we're using, a Morse 175Q140LR5, has a couple of important features:

| Feature | Value |
| -- | -- |
| Drive Ratio | 5:1 |
| Frame | 143/145TC |
| Shaft Output | Left + Right |
| Output Shaft Diameter | 7/8" |

This may be the hardest part to source cheaply. Ebay may be your best bet. You can be a bit flexible regarding the drive ratio and the output shaft diameter (if you vary the output shaft diameter you will have to choosed different sprockets from the BOM.)

## Sourcing The Variable Frequency Drive (VFD)

The Variable Frequency Drive (also commonly called an inverter) is an esential component of this system. It provides speed control and safety features neceesary to safely operate the Turntable Traction Drive.

For our implementation we have selected AutomationDirect's DURApulse GS23-22P0 VFD. We used the following selection criteria:

| Feature | Value | Note | Required |
| -- | -- | -- | -- |
| Number of Input Phases | 3&nbsp;(or&nbsp;1) | **This matches the supply we have access to.**<br/>We have easy-access to three-phase power, so this is a good choice for our environment. | YES |
| Nominal Input Voltage | 230&nbsp;VAC | **This matches the supply we have access to.**<br/>We have 3-phase 208VAC so this is the correct model. | YES |
| Horsepower By Phase | 2&nbsp;(or&nbsp;1) | **This matches the motor we have selected.**<br/>We have selected a 2HP motor, so we want a VFD rated for 2HP. The parentheses indicates that this VFD can power a 1HP motor when configured for single-phase 200VAC service. | YES |
| Safe Torque Off (STO) | YES | **This is safety requirement used by our e-stop system.**<br/>Having an STO feature means that our e-stop wiring will protect us even from a malfunction of the VFD itself. | YES |
| Current Limit Capability | 10%-250% | **This is a safety requirement.**<br/>This feature allows us to tune the max current available to the motor. This can help stall the system if there's an unexpected jam. | YES |
| UL/CE Listed | YES | Someone has looked at this device to make sure it meets minimum requirements for electrical safety. | NO |
| Freely available software. | YES | Having good software makes integration easier and can improve safety. | NO |
| Software Interface | USB | For PC-based configuration, USB is slightly easier to interface with than RS485. Even USB-B. | NO |
| Cost | $208 | That's a great price for the feature-set we're looking for. | NO |
| SEO | Excellent | Let's be honest, the reason I zeroed in on this VFD is that Automation Direct has good online advertising and search engine optimization. | NO |

### 120VAC Power Single Phase

We have successfully powered our traction drive using a single 20A 120VAC mains circuit connected to a Hitachi L-100 VFD. If you only have access to single-phase 120VAC power you should seek a VFD which matches this configuration. Be aware that you will never be able to run a 2HP motor at maximum power using a 1HP VFD. You will likely also want to reduce your duty cycle in this configuration and should expect to produce extra heat. **That said, we had no difficulty in rotating our 23' turntable on a single 120VAC 20A circuit.**

Also be aware that VFDs under load have a nasty habbit of tripping residential breakers (especially RCD/GFCI circuits.)

## Sourcing the Custom Steel Parts

I found that it was a relatively simple matter to provide a local steel shop with the [2D DXFs](dxfs/) and the [Custom Parts Overview](TurntableTractionDrive-PartsOverview.pdf). The PDF makes it easy for a sales guy to quote the job without needing CAD. The PDF also communicates expectations around minimum hole diameter and tolerances.

The design allows for 1/16 of slop between slots and tabs. The steel fabiractor must be able to hold 1/16th tolerance.

## Welding

Assembly took two days, with the majority of time being spent drilling and tapping holes. The welding of the chassis was a bit time consuming owing to underpowered welder. We used flux-core .030 wire on our 120VAC Hobart Handler 140. 

We first welded the `Motor Gusset` to the base plate using c-clamps for hold-down. The `Motor Gusset` has two long weld slots cut into it in front of and behind the motor bolts. These slots allow for a good strong hold to prevent the gusset from separating from the baseplate.

<image alt="Right Caster Gusset Welded" src="images/right-gusset.jpg" width=400 />

Next the `Caster Gussets` were welded into place. We used the tabs on the `Pusher Plates` to locate the slots before welding. C-clamps were used for hold-down. A generous weld-pocket is provided in the drawing in between the slot for the `Pusher Plate` and the hole for the axle.

<image alt="Initial Welds" src="images/initial-welds.jpg" width=400 />

Next the two `Side Panels`, the `Front Plate`, and the `Pusher Plates` are welded. We set them all in their slots and put the `Top Plate` on top to lock them in place. 90-degree mag-clamps locked everything in place while we put in tack welds. We then then layed about 3" of bead down on either side of each piece. 

In almost all cases we're welding an edge to a non-edge piece of steel. **It's important to manage your heat to avoid blasting away the edges of the steel.** Even on our low-powered welder we had to take care.

:warning: **IMPORTANT! Don't weld the top on until you've tapped the holes!**

## Hardware

In order to mount hardware you must drill then tap the bolt holes. In this design, all bolt holes are undersized for 3/8-24 with the idea being that plasma-cut holes are not very accurate so it's better to drill them after the fact and then tap the perfectly drilled holes. This worked fairly well but we broke plenty of bits and taps.

<image alt="Drilling and Tapping" src="images/drilling-tapping.jpg" width=400 />

We found that the steel fit together perfectly on the day it arrived, but on the second day the top plate no longer fit perfectly on the welded-up sides. It seems like everything moved a little bit as it cooled down from being welded and this caused us some difficulty in assembly. Next time around we will weld the whole machine in a single session. Or perhaps keep the top tacked after the bottom is assembled.

<image alt="Right Drive Wheel" src="images/bottom-chain.jpg" width=300 />

The right-angle (Left/Right AKA Top/Bottom) configuration of the gear-reducer allows us to run one sprocket on top and another sprocket on the bottom. This is useful since 7/8" ID sprockets are quite beefy. Too beefy to fit both chains on a single output shaft from the gear-reducer. For the right-hand drive wheel we connected a ANSI #40 chain to an 11 tooth sprocket mounted on the bottom shaft.

<image alt="Left Drive Wheel" src="images/top-chain.jpg" width=400 />

On the left-hand of the machine we ran chain from a sprocket mounted on the top shaft of the gear-reducer. On this machine the chain is a bit too close to the top plate. In our next revision we'll try to lower the motor 1/4" by eliminating the motor gusset.

<image alt="Painted with handles" src="images/painted-chassis.jpg" width=300 />

During our initial assembly we waited to weld the top until we verified that everything fit correctly. This isn't neccesary since all the hardware can be swapped-out even after the chassis is fully welded. After our test assembly we ran the machine at speed, adjusted it and then removed all the hardware for paint. We painted the chassis using oil-based black satin-finish paint.

<image alt="Painted with handles" src="images/painted-with-handles.jpg" width=300 />

We also welded on some store-bought handles in order to make moving the machine slightly less cumbersome.

## Drive Chain

Connecting the input and output sprockets can be a bit tricky for a few reasons:

- There isn't that much room between the top plate of the machine and where the top chain wants to run. 
- The hub-to-hub distance on the left side of the machine is different on the right side. You may have to experiment by adding links until you find a length of chain that fits evently on both sides.

Move the motor forward and backwards as needed using the motor mount sled. When you find the correct chain length and tension tighten the bolts on the motor flange to lock the motor spacing into the system.

While some chain noise is expected, if your machine is much louder than you expect look for the following defects:

- Chain is too close to the top plate and rubbing against it.
- Sprockets are not at the same height.

If you're still having chain noise try adding grease.

## Motor Wiring

Generally speaking wiring up a 3-phase motor is a matter of consulting the label on the side of the motor and connecting the appropriate wires to the VFD. Typically you will connect 3 hot legs and a ground to the VFD. There is no need for a seperate neutral connection.

<image alt="Motor Wiring" src="images/motor-wiring.jpg" width=300 />

In our General Electric motor the connections look like this:

| VFD Connection | Motor Connection |
| -- | -- |
| Ground | Chassis Ground |
| Leg 1 | Brown and Orange |
| Leg 2 | Blue and Pink | 
| Leg 3 | Tan and Red |
| (No Connection)     | Yellow, Black, Purple (Connected together for Wye configuration) |

Be sure to use an appropriate strain relief or grommet to prevent the knockout of the motor's wiring box from abrading the power cable.

## VFD Wiring

For control wiring we have decided used 4-pin XLR. **Industrial automation hardware tends to work with 24VDC reference signals which we intend to use in our control pendant.** For this reason it's important that our choice of cabling no be prone to confusion. 4-pin XLR is unlikely to be accidentally plugged into a dimmer or a soundboard. There is some risk of confusion around theater headsets and around scrollers and TV cameras, but generally it's a lightly-used form factor.

Follow your VFD's instructions for mains wiring. We are using a DURApulse GS23-22P0 in our 3-phase environment. This is a 3phase VFD with a 2HP rating and a STO feature. For reference, we have tested the Turntable Traction Drive on a Hitachi L100 connected to a single 20A 120VAC circuit. So you can definitely use a smaller VFD where required.

### DURApulse GS23 Wiring

**To Begin: Configure the DI pins into `SOURCE` mode my adjusting the toggle switch to `PNP`.**

| XLR Pin Number | VFD Pin | Note |
| -- | -- | -- |
| `XLR Pin 1` | `+24` Digital Common | |
| `XLR Pin 2` | `FWD/DI1` Forward RUN | 3-Wire Configuration |
| `XLR Pin 3` | `REV/DI2` Reverse RUN | 3-Wire Configuration |
| `XLR Pin 4` | `STO1` Safe Torque Off 1 | Interrupting +24V to STO will send e-stop the device. |

| Operation | Condition |
| -- | -- |
| Run Forward | Short `XLR Pin 1` to `XLR Pin 2` |
| Run Reverse | Short `XLR Pin 1` to `XLR Pin 3` |
| Emergency Stop (STO) | Interrupt +24v between `XLR Pin 1` to `XLR Pin 4` |

### Hitachi L100 Wiring

| XLR Pin Number | VFD Pin | Note |
| -- | -- | -- |
| `XLR Pin 1` | `P24` 24VDC Reference | |
| `XLR Pin 2` | `Terminal 1` Forward RUN | Default Configuration |
| `XLR Pin 3` | `Terminal 2` Reverse RUN | Default Configuration |
| `XLR Pin 4` | `Terminal 3` External TRIP | Configure to `EXT` by setting `C_03` to `12` |

In this configuraion you may peform the following operations:

| Operation | Condition |
| -- | -- |
| Run Forward | Short `XLR Pin 1` to `XLR Pin 2` |
| Run Reverse | Short `XLR Pin 1` to `XLR Pin 3` |
| Emergency Stop | Short `XLR Pin 1` to `XLR Pin 4` |

## Control Pendant Wiring

Rather than designing a bespoke pendant I decided to choose from one of the many "Lift Control" pendants available on Amazon. These pendants all seem to feature a rugged enclosure, an e-stop switch and two momentary push buttons. (One added benefit of some crane controls is that they tend to feature mechanical interlocks to prevent the clockwise button and the counter-clockwise button from being pressed at the same time. This isn't strictly necessary but may prevent operator confusion.)

<image alt="Left Drive Wheel" src="images/pendant.jpg" width=300 />

For our implementation we have made the top momentary switch the `RUN FORWARD` button. The bottom momentary switch is the `RUN REVERSE` button:

### Pendant Wiring for DURApulse GS23

| Connection | Purpose |
| -- | -- |
| `XLR Pin 1` TO `EMERGENCY STOP LEFT SIDE` | 24VDC for the pendant will travel through the e-stop button. If e-stop is activated power is interrupted. |
| `XLR Pin 1` TO `RUN FORWARD LEFT SIDE` | Send 24VDC to the `RUN FORWARD` button when e-stop is not engaged. |
| `XLR Pin 1` TO `RUN REVERSE LEFT SIDE` | Send 24VDC to the `RUN REVERSE` button when e-stop is not engaged. |
| `EMERGENCY STOP RIGHT SIDE` TO `XLR Pin 4` | If e-stop is activated interrupt 24VDC to STO1. STO will engage. |
| `RUN FORWARD RIGHT SIDE` TO `XLR Pin 2` | Send 24VDC to the VFD when `RUN FORWARD` is pressed. |
| `RUN REVERSE RIGHT SIDE` TO `XLR Pin 3` | Send 24VDC to the VFD when `RUN REVERSE` is pressed. |

### Pendant Wiring for Hitachi L100

**The Hitachi L100 has no STO device. This configuration does not protect against a malfunctioning VFD.**

| Connection | Purpose |
| -- | -- |
| `XLR Pin 1` TO `EMERGENCY STOP LEFT SIDE` | 24VDC for the pendant will travel through the e-stop button. If e-stop is activated power is interrupted. |
| `EMERGENCY STOP RIGHT SIDE` TO `RUN FORWARD LEFT SIDE` | Send 24VDC to the `RUN FORWARD` button when e-stop is not engaged. |
| `EMERGENCY STOP RIGHT SIDE` TO `RUN REVERSE LEFT SIDE` | Send 24VDC to the `RUN REVERSE` button when e-stop is not engaged. |
| `RUN FORWARD RIGHT SIDE` TO `XLR Pin 2` | Send 24VDC to the VFD when `RUN FORWARD` is pressed and the e-stop is not engaged. |
| `RUN REVERSE RIGHT SIDE` TO `XLR Pin 3` | Send 24VDC to the VFD when `RUN REVERSE` is pressed and the e-stop is not engaged. |
