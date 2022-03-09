# Turntable Traction Drive Integration Guide

This guide is designed to help scenic designers and technical directors integrate the Turntable Traction Drive into their sets.

## Safety

As it's intended use involves live actors on a rotating stage, safety must be considered seriously. 

:warning: **The Turntable Traction Drive is a powerful machine. Using it should not be taken lightly. Caution and care must be taken in every integration to ensure that safe operating parameters are configured.**

A turntable may pose a hazard on set even when operated manually by backstage technicians, however, unlike backstage technicians this machine has no brain. It doesn't know to stop because a piece of scenery is late during a scene-shift. It is not context-aware. Also, unlike a backstage technician, under the right circumstances this machine can summon inhuman amounts of torque.

:warning: **Due to its power and remoteness this machine is not designed as part of an automation system. Rather, it is intended to be manually operated by a user with a clear view of the turntable.**

As some risk is unavoidable, my analysis will focus on mitigation strategies.

| Risk | Mitigation Strategy |
| -- | -- |
| Electrical shock hazard | **Requirements:** Ground VFD appropriately to input mains. Ground motor appropriately to VFD. Ground chassis appropriately to the motor chassis. |
| Pinching hazards from rotating internal equipment and rotating top sprocket |  **Requirements:** Turntable Traction Drive must be in a fully enclosed secure area during operation. |
| Pinching/Crushing hazards between traction wheels and turntable edge | **Requirements:** Interface between the turntable and the traction drive must be fully enclosed during operation. |
| Risk of unexpected start | **Requirements:** Enable Unattended Start Protection in VFD by setting `c04` to `13` and short `P24` to `PIN 4` |
| Risk of fall due to sudden acceleration | Use conservative values for `f01`, `f02`, and `f03`. |
| Risk of fall due to overspeed | Set a conservative hard frequency limit using `a61` |
| Risk of crushing | #UNKNOWN# Investigate `B_12` and current overload protection. |
| Risk of crushing because of external scenery-based crush points. | **Requirements:** Turntables must maintain a raidal safety margin sufficient to prevent a person from being caught between a rotating piece of scenery and an adjacent non-rotating piece of scenery. Emergency Stop button must located near the turntable. Cast and crew must be trained on the location of the e-stop button. |
| Risk of entanglement | **Requirements:** Operator must have a clear view of the turntable. Emergency Stop button must located near the turntable. Cast and crew must be trained on the location of the e-stop button. |
| Risk of slipping on a free-rotating turntable | **Requirement** A parking brake must be employed when the Turntable Traction Drive is not in use. All on-stage personel must be instructed on the free-rotating-nature of the turntable. |
| Risk of operator/integrator ignorance | **Requirements:** All safety requirements and warnings must be clearly printed on a label applied to the machine. Documentation must be made available. |

## Integration Checklist

To help ensure safe operation of this Turntable Traction Drive please ensure the following **REQUIRED** conditions have been met:

| Requirement | Complete |
| -- | -- |
| Turntable Traction Drive chassis grounded to motor frame | :black_square_button: |
| Motor frame grounded to VFD | :black_square_button: |
| Turntable Traction Drive is fully enclosed in a secure area | :black_square_button: |
| Drive-wheel interface points are fully enclosed | :black_square_button: |
| Turntable hard-scenery elements don't create opportunities for shearing or crushing | :black_square_button: |
| Emergency stop button located within 6' of Turntable Traction Drive | :black_square_button: |
| Turntable fitted with an external parking brake. | :black_square_button: |

### Liability

This design is available for use under the [Creative Commons Attribution 4.0 International license](LICENSE). By using this design you agree to the terms of this license.

The license includes the following language, which you should read:

    Section 5 -- Disclaimer of Warranties and Limitation of Liability.

      a. UNLESS OTHERWISE SEPARATELY UNDERTAKEN BY THE LICENSOR, TO THE
         EXTENT POSSIBLE, THE LICENSOR OFFERS THE LICENSED MATERIAL AS-IS
         AND AS-AVAILABLE, AND MAKES NO REPRESENTATIONS OR WARRANTIES OF
         ANY KIND CONCERNING THE LICENSED MATERIAL, WHETHER EXPRESS,
         IMPLIED, STATUTORY, OR OTHER. THIS INCLUDES, WITHOUT LIMITATION,
         WARRANTIES OF TITLE, MERCHANTABILITY, FITNESS FOR A PARTICULAR
         PURPOSE, NON-INFRINGEMENT, ABSENCE OF LATENT OR OTHER DEFECTS,
         ACCURACY, OR THE PRESENCE OR ABSENCE OF ERRORS, WHETHER OR NOT
         KNOWN OR DISCOVERABLE. WHERE DISCLAIMERS OF WARRANTIES ARE NOT
         ALLOWED IN FULL OR IN PART, THIS DISCLAIMER MAY NOT APPLY TO YOU.

      b. TO THE EXTENT POSSIBLE, IN NO EVENT WILL THE LICENSOR BE LIABLE
         TO YOU ON ANY LEGAL THEORY (INCLUDING, WITHOUT LIMITATION,
         NEGLIGENCE) OR OTHERWISE FOR ANY DIRECT, SPECIAL, INDIRECT,
         INCIDENTAL, CONSEQUENTIAL, PUNITIVE, EXEMPLARY, OR OTHER LOSSES,
         COSTS, EXPENSES, OR DAMAGES ARISING OUT OF THIS PUBLIC LICENSE OR
         USE OF THE LICENSED MATERIAL, EVEN IF THE LICENSOR HAS BEEN
         ADVISED OF THE POSSIBILITY OF SUCH LOSSES, COSTS, EXPENSES, OR
         DAMAGES. WHERE A LIMITATION OF LIABILITY IS NOT ALLOWED IN FULL OR
         IN PART, THIS LIMITATION MAY NOT APPLY TO YOU.

In plain language: **I don't guarantee that this design works as intended, and I am not liable for any harm resulting from your use of this design.**

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

