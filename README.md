# Voltage controlled ADSR using AS3310

<img width="314" height="758" alt="image" src="https://github.com/user-attachments/assets/1e044e15-837f-4e2f-a648-28ea6051b577" />


I was particularly interested in the versatility of the <a target="_blank" rel="noreferrer noopener" href="http://www.digisound80.co.uk/digisound/modules/80-18.htm">Digisound 80-18 multifunction envelope generator</a> with its three operating modes
- normal (standard ADSR)
- automatic (gives a complete ADR cycle following a brief trigger input)
- damped (gives a piano-like envelope with initial attack and decay, but instead of a constant sustain while the gate is high the envelope continues to decay at a rate determined by the release setting, finally shutting off the envelope when the gate goes low)
Curiously, given that the 3310 chip is intrinsically voltage controlled, the Digisound 80-18 module only allowed control of the envelope by potentiometers rather than allow external CV control.
