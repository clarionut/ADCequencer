# ADCequencer
An 8 step dual channel sequencer with voltage controlled step pattern, based on the Fonitronik VCPS8 (http://www.modular.fonik.de/pdf/VCPS8_doc_v2.pdf - the predecessor of the MH11) but with significant modifications.

Most obviously, there are two potentiometers to set CV voltages for each step and two CV output channels. This gives considerable flexibility - e.g. controlling two VCOs, a VCO and filter cutoff, or (in conjunction with an external clock divider / analogue switch module) operation as a 16-step sequencer.

Another significant visible change is the addition of a 'freeze' circuit operated by switch or a gate input allowing the ADC to be stopped under voltage control. This gives real value to the gate output from the VCPS8 (which is on continously through a sequence of active steps) as it allows the sequencer pattern to be updated only when the trigger output is low (generally meaning that no note is sounding). This avoids a serious glitchy effect when a step is turned off while it's active.

Cosmetically, the LED arrays have been replaced by red/white common-cathode bicolour LEDs associated with each step (red shows the active steps and white the current step) plus a red/blue common-anode LED as an indicator for out-of-range pattern control voltages.

Behind the scenes there are also significant changes:
- the PCV out-of-range protection circuit in the original is essentially a zener diode crowbar across an op-amp output. This has been replaced by an in-line resistor and Schottky diodes to +5V and ground. The PCV out is not clipped by these, so it's easy to use an external voltmeter to check and adjust the incoming control voltage. The out-of-range LED circuitry is also modified so the LEDs are never reverse biased.
- the Gray-coding circuitry is included but can be bypassed by connecting to an alternative header on the PCB. The CD4030 XOR gates can be omitted altogether if Gray-coding is not required.
- the gate/trigger driver circuit has been significantly revised, doing away with the need for the CD40106 in the original (discussion at https://electro-music.com/forum/topic-52774-50.html). A simple RC filter on the base of the trigger-driver transistor removes the very fast pulse from the AND gates which can cause double-triggering. The CD40106 is not needed for the ADC clock either, as the ADC802 contains an inverter gate and just needs an external resistor and capacitor to provide its own clock. The gate and trigger outputs are taken from a dedicated 9V supply rather than the raw 12V supply.
