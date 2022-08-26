# Wiring Guide

For the sake of reusability we have wired our VFD into a semi-permanent control panel using DIN terminal blocks to connect the user wiring. **This control panel is designed to be fully enclosed in scenery during use.**

<image alt="Assembled Chassis Before Welding (photo)" src="images/control-panel.jpg" width=400 />

Be sure to follow the VFD manufacturer's specifications when selecing wiring materials. You don't want to under-spec the mains or motor wiring.

## Wiring Guide (For Durapulse GS20)

| Terminal Number | End Point | Name |
| -- | -- | -- |
| **Input Side** |
| G | VFD Ground | Ground |
| `TERMINAL1` | L1 | Input Power Leg 1 |
| `TERMINAL2` | L2 | Input Power Leg 2 |
| `TERMINAL3` | L3 | Input Power Leg 3 |
| **Output Side** |
| G | VFD Ground | Ground |
| `TERMINAL4` | T1 | Motor Turns 1 |
| `TERMINAL5` | T2 | Motor Turns 2 | 
| `TERMINAL6` | T3 | Motor Turns 3 |
| **Safety** |
| `TERMINAL7` | STO +24V | 24V Source For Safety Switches |
| `TERMINAL8` | STO +24V | 24V Source For Safety Switches |
| `TERMINAL9` | STO1 | Safety Input 1 |
| `TERMINAL10` | STO2 | Safety Input 2 |
| **Control** |
| `TERMINAL11` | DCM | Digital Control Common |
| `TERMINAL12` | FWD | Forward Contactor |
| `TERMINAL13` | REV | Reverse Contactor |

## Control Wiring
| Wire | Pin | Terminal | Notes |
| - | - | - | - |
| Emergency Stop Button | 1 | `TERMINAL9` | STO disabled when shorted to +24VDC Source |
| Emergency Stop Button | 4 | `TERMINAL7` | STO +24VDC Source |
| Optional Second Emergency Stop Button | 1 | `TERMINAL10` | STO disabled when shorted to +24VDC Source |
| Optional Second Emergency Stop Button | 4 | `TERMINAL8` | STO +24VDC Source |
| Control Pendant | 1 | `TERMINAL11` | Voltage Sink for Digital Control |
| Control Pendant | 2 | `TERMINAL13` | REVERSE when shorted to votlage sink |
| Control Pendant | 3 | `TERMINAL12` | FORWARD when shorted to votlage sink |

*Note: When not using the optional second emergency stop button you must have a jumper between `TERMINAL8` and `TERMINAL10`.*
