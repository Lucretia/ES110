# ES110

Reverse engineering and drawing schematics in KiCAD for a broken Kawai ES110 in an attempt to use parts of it.

Kawai, as with other manufacturers used to provide schematics in their service manuals, now they have a walled garden.

If you can help to make these better, please do.

## Notes

### KEP-692

This is the motherboard to the whole piano. The two connectors we are interested in are CN11 (bottom left) and CN7 (Bottom right).

[![KEP-692](https://i.imgur.com/RsQSE3i.jpg)](https://imgur.com/RsQSE3i)

* CN11 - The control panel, KEP-643 and KEP-644 connects here.
* CN7  - The keybed connects here.

#### Keybed connector (CN7)

The pinout seems to match that of the Kawai ES4/ES1, which can be seen on page 30 of the [service manual](./docs/es4es1p.pdf). Page 31 shows the key table.

### KEP-643

On the motherboard, pin 2 of CN11 has continuity with the positive side of C88 electrolytic capacitor next to the SI-8008TM step down converter, so this is 5v, right? But pin 2 of CN6 on KEP-643 which is connected via a cable, is not connected to anything., as can be seen here (pin 1 is on the right):

![KEP-643](https://i.imgur.com/2M9kh3h.jpg)

### KEP-644

This is the second of the control panel boards, this has the power button/led and the volume slider.

The slider seems to be a custom Alps potentiometer, labelled 825C-10KB.

The capacitor is connected to the button via a resistor and seems to be a debounce circuit.

![KEP-644](https://imgur.com/Xlv9WfC)

![KEP-644 rear](https://imgur.com/ov3erFO)

## Disclaimer

I cannot guarantee the accuracy of these schematics.

They've been traced with a multimeter and by eye.

I'm a programmer, not an EE.
