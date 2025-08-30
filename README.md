# Voltage controlled ADSR using AS3310

<img width="314" height="758" alt="image" src="https://github.com/user-attachments/assets/1e044e15-837f-4e2f-a648-28ea6051b577" />


I was particularly interested in the versatility of the [Digisound 80-18 multifunction envelope generator]( http://www.digisound80.co.uk/digisound/modules/80-18.htm) with its three operating modes
- normal (standard ADSR)
- automatic (gives a complete ADR cycle following a brief trigger input)
- damped (gives a piano-like envelope with initial attack and decay, but instead of a constant sustain while the gate is high the envelope continues to decay at a rate determined by the release setting, finally shutting off the envelope when the gate goes low)

Curiously, given that the 3310 chip is intrinsically voltage controlled, the Digisound 80-18 module only allowed control of the envelope by potentiometers rather than allow external CV control, although there are other designs (e.g. by [gerb-ster](https://github.com/gerb-ster/Curtis-VC-ADSR)) which do allow external control.

## Issues
There is a known issue with the Digisound 80-18 module leading to repeated AD triggering with relatively weak gat inputs. The Digisound 80-18A documentation suggests using two gates from a CD40106 in series to condition the gate signal and [Eddy Bergman used a switch](https://www.eddybergman.com/2020/05/synthesizer-build-part-33-digisound-80.html) to break the loop responsible for multiple triggering. I chose to feed the gate input into an op-amp comparator so even rather low-level gates trigger the ADSR reliably.

Note that I have not encountered any of the odd behaviour in Auto mode as described by Eddy Bergman, in my case this mode works exactly as described in the Digisound 80-18 documentation.

Running the circuit on a breadboard showed that with linear potentiometers much of the travel of the pot covered only very short time intervals, leaving the useful longer times quite hard to adjust. This was easy to fix using fake C-taper pots (500k linear pot with a 100k resistor from the wiper to the +ve supply end of the pot).

## Additional features
I found that in Damped mode the final release was very rapid producing an audible click. Adding a 510R resistor between the AS3310 chip pin 13 and transistor TR2 (Digisound schematic) / Q2 (my schematic) gives a rapid release without clicking. In the end I added a 2k 'Release 2' pot to make this final release phase at least manually adjustable.

Coincidentally, at the time I was working on this circuit I was also fixing an issue with the envelope generator of my Polivoks filter. This has an autorepeat mode, enabled by setting the envelope to AD mode and the sustain level to zero. It uses an op-amp comparator to generate an internal trigger signal when the envelope voltage falls below a threshold of a few mV. I included this feature in this ADSR, providing and 'end of envelope' output to trigger other events in the synth, and included a LOOP option on the mode switch allowing the module to run continously as an LFO in Automatic mode.

The decay CV input is normalled to the attack input and the release input is normalled to decay, allowing flexibility in external CV control.

There are out-of-range monitor LEDs on the four CV inputs to warn if the combined potentiometer & external CV levels exceed the maximum useful control voltage (no damage would result, it simply wouldn't be effective).
