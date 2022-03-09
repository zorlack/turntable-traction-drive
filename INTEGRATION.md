# Turntable Traction Drive Integration Guide

This guide is designed to help scenic designers and technical directors integrate the Turntable Traction Drive into their sets.

:warning: **Before Proceeding, make sure you have read and understood the [SAFETY](SAFETY.md) section of the documentation.**

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

### Liability

This design is available for use under the [Creative Commons Attribution 4.0 International license](https://github.com/zorlack/turntable-traction-drive/blob/master/LICENSE). By using this design you agree to the terms of this license.

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

