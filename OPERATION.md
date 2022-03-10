# Turntable Traction Drive Operation Guide

This guide is designed to provide procedures for operating the Turntable Traction Drive.

:warning: **Before Proceeding, make sure you have read and understood the [SAFETY](SAFETY.md) section of the documentation.**

:warning: **Before Proceeding, make sure you have read and understood the [Limitations](SAFETY.md#Limitations) section of the documentation.**

## Determining Safe Working Parameters

Once the Turntable Traction Drive has been integrated into your scenery you need to determine safe working values for the various parameters of your VFD.

In particular:
- Operating Frequency
- Acceleration Time
- Deceleration Time
- Current Limit

### Operating Frequency

The operating frequency is the speed at which the drive motor runs. If a motor has a 60Hz native frequency then you should consider 60Hz to be 100% speed.

Determining a safe operating speed involves many factors and there may not be simple way to determine what's safe. 

Observe the following:

- Always set an extremely slow Acceleration/Deceleration time when experimenting with speed.
- Always work your way up from a low speed to a high speed gradually.

Consider the following:

- Consider two people on a turntable may experiene different forces depending on their mass, height distance from the center.
- Consider that stepping on and off a moving turntable is dangerous and should be avoided.
- Consider that technicians working in proximity to a turntable may accidentally come into contact with it during shifts.

### Acceleration/Deceleration

The Acceleration Time and Deceleration Time control how long it takes the drive to come up to full speed and how long it takes to slow down. Anytime that the motor is changing speed there is additional risk to on-stage personel, particularly when acceleration itself changes.

Observe the following:

- Avoid sub-second acceleration/deceleration times.
- Do not change acceleration/deceleration times without rehearsing under the new parameters.

Consider the following:

- Changing accelerations cause a "jerk" sensation. Where possible use linear acceleration parameters.

### Current Limits

If your VFD permits it, consider setting as low a current limit as possible. This will allow your drive and motor to stall if your turntable meets unexpected resistance.

It may be neccesary to tune this parameter so that your VFD has suffient "starting torque" but will still stall if required.

## Operations Checklist

Before each use the Turntable Traction Drive should be inspected to ensure that it is properly installed and safe to use.

| Checkpoint | Ready |
| -- | -- |
| Check machine/turntable pressure on left and right sides. | :black_square_button: |
| Check to make sure drive-wheel is contacting the correct portion of the turntable on left and right sides. | :black_square_button: |
| Check to make output-shaft sprockets have not slipped and are aligned with the power-sprockets. | :black_square_button: |
| Visually inspect turntable circumference and remove any obstructions which may cause jamming. | :black_square_button: |
| Remove parking brake (or disablement device) | :black_square_button: |
| Connect controller to Drive | :black_square_button: |
| Connect drive to power | :black_square_button: |
| Test left and right rotation at performance speed. Listen for any unusual noises coming from the Turntable Traction Drive or the turntable itself.  | :black_square_button: |
| Test left and right rotation at performance speed. Watch for any unusual rubbing, slippage or stalling.  | :black_square_button: |
| Test local emergency stop button. | :black_square_button: |
