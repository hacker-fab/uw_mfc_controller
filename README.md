Arduino nano based controller board for the MKS 1480A-25078 MFC

---

### design review notes

- CR1 (SMBJ24A) should almost certainly be connected reverse biased. i'm guessing it's there to protect the downstream 24V from surges. speaking of which, what's the 24V rail for? it's not connected to anything on the sheet
- In this design splitting the GND plane sorta creates more problems than it solves. It'd be simpler and better to just have a singular GND and keep the dac, vref, etc grouped. And also even when they're split they should be connected a singular, documented point with a net-tie or 0ohm resistor (for optionality)
- curious why 0.1uF and 10uF on the VOUT for U2 (the dac). the datasheet specifies 0.1uF optionally.
- also what's the reason for placing the 220ohm R2 in series on pin 2 of the LCD connector? it's Vdd so that's the actual power input right? not like a random pullup
- U2 (ADR02CRZ) is listed obsolete so make sure to check part availability on digitkey & mouser before selecting parts. (+ confirm that
  - also the DAC's references input range is between 0.04V to VDD - 0.04V, so the stable 5V generated from U2 would be too close no?
  - ++ it might be simpler to use smth like TI DAC60501, or AD5691R with an internal ref. unless you've mathed out the full DAC + mfc range and theres specifc reasons for the selections.

**on organizing schematics**
- Arrange the page left-to-right: power inputs → reference/DAC → MFC connector, with the Nano and LCD as separate blocks (look into hierarchical sheets for larger projects).
- Label connector pins / nets by function directly beside them; eg: MFC_CMD, MFC_FEEDBACK, VREF_5V, LCD_R/W etc instead of D9 or smth
- when downloading schematic symbols for components not in Kicad's library use smth like Ultralibrarian for consistant symbols. also make ur own symbols if it's hard to find them online and like use kicad's default library symbols for inspiration. i find the symbols well drawn and pins arranged well usually
- also just like minor notes about gender etc make it easier to review design and avoid mistakes later.
- oh and most compnonets don't seem to have footprints assigned yet btw. 
