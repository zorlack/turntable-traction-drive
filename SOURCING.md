# Sourcing Parts For The Turntable Traction Drive

Finding reliable sources for parts is a challenging problem. If you pick a vendor like Amazon you may find that your item SKUs are no longer available weeks after you've made a purchase. On the other hand if you source parts exclusively from McMaster-Carr and Grainger you'll be paying top-dollar for that consistency.

In order to make parts-sourcing consistant I've chosen McMaster-Carr for most pieces of hardware. The Motor, Gearbox, VFD and Custom Steel you will need to source independently.

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
