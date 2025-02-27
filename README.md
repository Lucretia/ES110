# ES110

Reverse engineering and drawing schematics in KiCAD for a broken Kawai ES110 in an attempt to use parts of it.

Kawai, as with other manufacturers used to provide schematics in their service manuals, now they have a walled garden.

The aim here is to document enough to be able to create a new board for a new project.

If you can help to make these better, please do.

## Notes

* The +5v signal to pin 2 of CN7/CN11 is taken as true as there is continuity between these pins and the positive leg of the electrolytic capacitor next to CN7. This cap is connected to the step-down converter.

* The power input is centre positive.

* I need to double check the KKB-034 schematics again as I'm not sure I have them correct.

### KEP-692

This is the motherboard to the whole piano. The two connectors we are interested in are CN11 (bottom left) and CN7 (Bottom right).

[![KEP-692](https://i.imgur.com/kw21f87.jpg)](https://imgur.com/kw21f87)

* CN11 - The control panel, KEP-643 and KEP-644 connects here.
* CN7  - The keybed connects here.

#### Keybed connector (CN7)

The pinout seems to match that of the Kawai ES4/ES1, which can be seen on page 30 of the [service manual](./docs/es4es1p.pdf). Page 31 shows the key table.

### KEP-643

On the motherboard, pin 2 of CN11 has continuity with the positive side of C88 electrolytic capacitor next to the SI-8008TM step down converter, so this is 5v, right? But pin 2 of CN6 on KEP-643 which is connected via a cable, is not connected to anything., as can be seen here (pin 1 is on the right):

![KEP-643](https://i.imgur.com/GNB6Hiq.jpg)

![KEP-643 rear](https://i.imgur.com/2M9kh3h.jpg)

### KEP-644

This is the second of the control panel boards, this has the power button/led and the volume slider.

The slider seems to be a custom Alps potentiometer, labelled 825C-10KB.

The capacitor is connected to the button via a resistor and seems to be a debounce circuit.

![KEP-644](https://i.imgur.com/Xlv9WfC.jpg)

![KEP-644 rear](https://i.imgur.com/ov3erFO.jpg)

## The key matrix

By examining the layout of CN7 in the image above, i.e. where the resistors are aligned with which pins, they do conect to, btw, see the schematics. they just seem to match the pinout of the ES4 connector. It could well be different, the order of hte pins may differ for example.

![ES4 Schematic](./imgs/ES4_KKB-015.png)

This would then result in the following key matrix:

![ES4 Key Matrix](./imgs/ES4_Key_Switch_Matrix.png)

In fact, I wonder if KD1 is pin 8 of CN7, but this depend entirely on the output of U15 which all enter U4, the Kawai K023-FP tone generator custom ASIC.

## TODO

To make the first part of this project a reality, i.e. MIDI controller, the following needs to be determined:

* [ ] Control panel needs to be tested with a real Arduino/AVR/whatever program.
* [X] MIDI schematics from CN3 (KEP-641) to the MIDI out.
* [X] MIDI schematics from CN10 (KEP-692) to CN3 (KEP-641) via the purple 7 pin cable, this will be the cable which transmits the BT MIDI as CN10 is next to the BT antennae.
* [X] I'm pretty sure the damper pedal signals go through CN3 or CN1 on KEP-641 back to the mainboard.
* [ ] Put 5v through the MIDI out, pin 4, on CN3 (KEP-641), along with GND and +5v and test to see if 5v comes out of the MIDI port.
* [ ] Do the same in the opposite direction on the MIDI in port, and test on the voltage of pin 3 on CN3.
* [ ] Read the values from the damper on CN3, pins 5 & 6 to see what values come in.

To make the second part of this project a reality, i.e. the synthesiser board, the following needs to be worked out:

* [ ] Audio schematics from CN3 (KEP-692) to CN1 (KEP-641), the blue 6 pin cable.
* [ ] Headphone sockets connector, CN2 (KEP-641).

## Disclaimer

1. I cannot guarantee the accuracy of these schematics.

2. They've been traced with a multimeter and by eye.

3. I'm a programmer, not an EE.
