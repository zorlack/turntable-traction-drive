# Turntable Traction Drive Integration Guide

This guide is designed to help scenic designers and technical directors integrate the Turntable Traction Drive into their sets.

:warning: **Before Proceeding, make sure you have read and understood the [SAFETY](SAFETY.md) section of the documentation.**

:warning: **Before Proceeding, make sure you have read and understood the [Limitations](SAFETY.md#Limitations) section of the documentation.**

## Turntable Integration

The Turntable Traction Drive applies significant forces to the side of the turntable where it makes contact. This requires the following considerations:

- The Turntable Traction Drive should not be pressed against a surface which will bow or deflect under pressure. Ideally you'd want a 3" wide rigid band that the turntable can drive against. In practice we've found that the drive wheels can get plenty of traction when applied against the edge of a 1.5" laminated plywood floor.
- The drive wheels of the traction drive may cause maring or discoloration of surface finishes. You may need to apply a protective coating to traction surfaces if they are visible to the audience.

### Critical Dimensions

The two key factors when determining if this machine will work with your turntable are diameter and mass. At present we don't have sufficient information to give guidance about maximum turntable mass. Except to say that we had no difficulty moving a 23' turntable with a 2-story wood and steel "castle" on it.

| Dimension | Value |
| -- | -- |
| Minimum Turntable Diameter | 6' |
| Maximum Turntable Diameter | 23' Demonstrated (Maximum Unknown) |

If the diameter of your turntable is too large you may have difficulty running it fast enough with the as-designed gearing. If this is the case you have two options:

- You may increase the diameter of your drive rollers up to 12" in diameter (this size is quite extreme consider 8"). Increasing the diameter of the drive rollers will cause you to suffer a substantial loss of starting torque. The advantage is increased speed at your motor's native frequency without an increase in chain noise. 
- You may decide to overdrive your motor beyond 60Hz. Many VFDs will let you run the motor up to 400Hz, at this speed you would likely damage your gearbox, motor and chain drive. Many motors will be perfectly happy to run faster than 60Hz with reduced duty cycle. Consult your motor and gearbox documentation to determine the maximum safe operating speed of your Turntable Traction Drive.

Another critical factor is the height of the traction-bearing surface relative the bottom of the turntable traction drive. The vertical position of the drive wheels is adjustable, but is ultimately constrined by the spacing between the drive sprockets. That said drive wheels have about 4" of vertical adjustability.

| Dimension | Value |
| -- | -- |
| Minimum Traction Surface Width | 1.5" |
| Maximum Traction Surface Width | 3" (Drive Roller Width) |
| Lowest Possible Traction Surface | 3.25" to 4.75" from the bottom of the machine |
| Highest Possible Traction Surface | 5.75" to 7.25" from the bottom of the machine |


## Integration Checklist

To help ensure safe operation of this Turntable Traction Drive please ensure the following **REQUIRED** conditions have been met:

| Requirement | Complete |
| -- | -- |
| Technical Director/Integrator must read and understand the [safety](SAFETY.md) section of this documentation. | :black_square_button: |
| Turntable Traction Drive chassis grounded to motor frame | :black_square_button: |
| Motor frame grounded to VFD | :black_square_button: |
| Turntable Traction Drive is fully enclosed in a secure area | :black_square_button: |
| Drive-wheel interface points are fully enclosed | :black_square_button: |
| Turntable hard-scenery elements don't create opportunities for shearing or crushing | :black_square_button: |
| Emergency stop button located within 6' of Turntable Traction Drive | :black_square_button: |
| Turntable fitted with an external parking brake. | :black_square_button: |

## VFD Configuration

**Note:** These notes are only really useful for the Hitachi L-100. If you're using another VFD consult your documentation.

`P24` provides a 24V field reference voltage for use when powering the Control Terminals.

When configured correctly we desire the following outcome:

- To tell the turntable to run forward short `P24` to `PIN 1`.
- To tell the turntable to run in revers short `P24` to `PIN 2`.

### VFD Parameters

| Parameter | Value | Notes |
| -- | -- | -- |
| `a01` | `00` | `00`=Keypad/Potentiometer, `01`=Control Terminals, `02`=F01 Settings |
| `a02` | `02` | `01`=Control Terminals, `02`=Keypad Run Key |
| `a02` | `02` | `01`=Control Terminals, `02`=Keypad Run Key |
| `a61` | `60` | Set a hard limit on the output frequency of the VFD to never overdrive the motor. |
| `a04` | `60` | Set the "Base" Frequency. (The frequency at which the VFD emits full voltage) |
| `a05` | `60` | Set the "Max" Frequency (The frequency allowed during manual opeation) |
| `a97` | `00` | Set the Acceleration Curve: `00`=Linear, `01`=S-Curve |
| `a97` | `00` | Set the Deceleration Curve: `00`=Linear, `01`=S-Curve |
| `c01` | `00` | Configure Terminal 1: `00`=Run Forward
| `c02` | `01` | Configure Terminal 2: `01`=Run Reverse
| `f01` | `nn` | **Set the target frequency** |
| `f02` | `nn` | **Set the acceleration time** (The number of seconds it should take to get spin-up from 0Hz to `f01`Hz) |
| `f03` | `nn` | **Set the deceleration time** (The number of seconds it should take to get spin-down from `f01`Hz to 0Hz) |

