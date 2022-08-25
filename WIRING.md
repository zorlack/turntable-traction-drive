# Wiring Guide

For the sake of reusability we have wired our VFD into a semi-permanent control panel using DIN terminal blocks to connect the user wiring. **This control panel is designed to be fully enclosed in scenery during use.**

<image alt="Assembled Chassis Before Welding (photo)" src="images/control-panel.jpg" width=400 />

Be sure to follow the VFD manufacturer's specifications when selecing wiring materials. You don't want to under-spec the mains or motor wiring.

## Wiring Guide (For Durapulse GS20)

| Terminal Number | End Point | Name |
| -- | -- | -- |
| **Input Side** |
| G | VFD Ground | Ground |
| T1 | L1 | Input Power Leg 1 |
| T2 | L2 | Input Power Leg 2 |
| T3 | L3 | Input Power Leg 3 |
| **Output Side** |
| G | VFD Ground | Ground |
| T4 | T1 | Motor Turns 1 |
| T5 | T2 | Motor Turns 2 | 
| T6 | T3 | Motor Turns 3 |
| **Safety** |
| T7 | STO +24V | 24V Source For Safety Switches |
| T8 | STO +24V | 24V Source For Safety Switches |
| T9 | STO1 | Safety Input 1 |
| T10 | STO2 | Safety Input 2 |
| **Control** |
| T11 | DCM | Digital Control Common |
| T12 | FWD | Forward Contactor |
| T13 | REV | Reverse Contactor |

## Control Wiring
| Wire | Pin | Terminal | Notes |
| - | - | - | - |
| Emergency Stop Button | 1 | T9 | STO disabled when shorted to +24VDC Source |
| Emergency Stop Button | 4 | T7 | STO +24VDC Source |
| Optional Second Emergency Stop Button | 1 | T10 | STO disabled when shorted to +24VDC Source |
| Optional Second Emergency Stop Button | 4 | T8 | STO +24VDC Source |
| Control Pendant | 1 | T11 | Voltage Sink for Digital Control |
| Control Pendant | 2 | T13 | REVERSE when shorted to votlage sink |
| Control Pendant | 3 | T12 | FORWARD when shorted to votlage sink |

*Note: When not using the optional second emergency stop button you must have a jumper between T8 and T10.*
