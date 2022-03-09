# Safety and Liability

As it's intended use involves live actors on a rotating stage, the safety of the Turntable Traction Drive must be considered seriously. But before we dig into a risk assesment understand this: **I am not an engineer.** I write software for a living and am not formally trained to assess safety risks. 

In undertaking this project, and making it publicly available, it behoves me to draw attention to this fact and to the following: **I don't guarantee that this design works as intended, and I am not liable for any harm resulting from your use of this design.**

## Liability

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

## Key Safety Principals

:warning: **The Turntable Traction Drive is a powerful machine. Using it should not be taken lightly. Caution and care must be taken in every integration to ensure that safe operating parameters are configured.**

A turntable may pose a hazard on set even when operated manually by backstage technicians, however, unlike backstage technicians this machine has no brain. It doesn't know to stop because a piece of scenery is late during a scene-shift. It is not context-aware. Also, unlike a backstage technician, under the right circumstances this machine can summon inhuman amounts of torque.

:warning: **Due to its power and remoteness this machine is not designed as part of an automation system. Rather, it is intended to be manually operated by a user with a clear view of the turntable.**

The Turntable Traction Drive has exposed moving parts and therefore poses some first-hand risk of injury to operators. However, when attached to a turntable new hazards may appear.

:warning: **A scenic turntable creates risks of injury independant of the drive mechanism. Take care to evaluate the risks not just from the Turntable Traction Drive, but from the system as a whole.**

## Risk Management

As some risk is unavoidable, my analysis will focus on mitigation strategies. Any requirement layed out in this section must be specifically required in either the Integration Checklist or Operations Checklist.

| Risk | Mitigation Strategy |
| -- | -- |
| Electrical shock hazard | **Requirements:** Ground VFD appropriately to input mains. Ground motor appropriately to VFD. Ground chassis appropriately to the motor chassis. |
| Pinching hazards from rotating internal equipment and rotating top sprocket |  **Requirements:** Turntable Traction Drive must be in a fully enclosed secure area during operation. |
| Pinching/Crushing hazards between traction wheels and turntable edge | **Requirements:** Interface between the turntable and the traction drive must be fully enclosed during operation. |
| Risk of unexpected start | **Requirements:** Enable Unattended Start Protection in VFD by setting `c04` to `13` and short `P24` to `PIN 4` |
| Risk of fall due to sudden acceleration | Use conservative values for `f01`, `f02`, and `f03`. |
| Risk of fall due to overspeed | Set a conservative hard frequency limit using `a61` |
| Risk of crushing | Where possible tune-narrowly the current limiting features of your VFD. |
| Risk of crushing because of external scenery-based crush points. | **Requirements:** Turntables must maintain a raidal safety margin sufficient to prevent a person from being caught between a rotating piece of scenery and an adjacent non-rotating piece of scenery. Emergency Stop button must located near the turntable. Cast and crew must be trained on the location of the e-stop button. |
| Risk of entanglement | **Requirements:** Operator must have a clear view of the turntable. Emergency Stop button must located near the turntable. Cast and crew must be trained on the location of the e-stop button. |
| Risk of slipping on a free-rotating turntable | **Requirement** A parking brake must be employed when the Turntable Traction Drive is not in use. All on-stage personel must be instructed on the free-rotating-nature of the turntable. |
| Risk of operator/integrator ignorance | **Requirements:** All safety requirements and warnings must be clearly printed on a label applied to the machine. Documentation must be made available. |
| Risk of structural collapes on turntable | **Requirement:** Ensure that all scenery is constructed such that it can absorb axial load such as might result from a sudden change in rotational speed. |
