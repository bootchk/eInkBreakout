EInkBreakout

A breakout board for eInk brand, 5 segment, bar graph display.

The display plugs into a FFC connector, and the board breaks out to standard pin headers.
Alternatively, you can just solder wires to a FFC connector, but it is difficult.

The use case is in a nano power system,
where you need an indicator that takes zero power to maintain.
Once you set the display, it retains its visibility using no power (unlike an LED.)

A nano power system sleeps mostly.
A nano power system can enter a state such as a fault, or a brownout condition.
You want to be able to indicate that state.
Using eInk, the indication remains even after power is exhausted.
You don't need to plug a debugger into the system to know what happened.

I also discuss at https://plashless.wordpress.com/


### References, Datasheets, and Distributors

A good datasheet is hard to find for the eInk display.
Digikey points to:  dhttps://media.digikey.com/pdf/Data Sheets/E Ink PDFs/SDC722002_DS_12-7-16.pdf
That datasheet seems to have errors, it says the part number is SDC...!

The manufacturer's part number is actually SCD722002.

Digikey seems to stock it, part no. 1272-1006-ND, at $4.

http://essentialscrap.com/eink/ gives good information about all the eInk displays.

It has a link to a Renesas talk.

https://www.omotronic.com/details/E-Ink/SCD722002.html has a link to a drawing.


### Pinout

The datasheet does not give the pin out.
An eInk drawing does.

All directions are with respect to the device when the connector is pointing down.

Pin 1 is to the right.

    1  Top electrode (above, covering the entire device)
    2  Background/field segment ( not a dot, surrounds all other dots)
    3  Segment 1 (the bottom most dot, of five total dots)
    4  Segment 2
    5  Segment 3
    6  Segment 4
    7  Segment 5 (the top most dot.  The distal dot, most distant from the cable.)


### The connector

Is a FFC/FPC type (Flat Flexible Cable.)
The cable which fits into the connector is also called a tail.

The eInk device data sheets says the connector part number is Tyco 5-1734592-6.
Evidently, Tyco is owned by TE Connectivity.

The "TE Connectivity" datasheet for their connectors is drawing C-1734592.

The device FFC cable is 8.4 mm wide.
This is a 16 position cable.
This means the device cable is wider than needed, and has unused contacts
(it only uses 7 of 16 contacts.)

(Note that the "-6" in the connector part number is the second digit of the count of contacts.
The "1-" in the part number is the first digit.
So the TE Connectivity part number is 1-1734592-6.)

This is a "bottom contact" type of connector.
The contact in the connector is facing up, near the PCB board, looking down on the PCB board.
The contact in the cable is underneath the cable, looking down on the device as a viewer would see the segments.
Thus this breakout board is designed to mount the display facing up, on top of the PCB board.

(Alternatively, you could use a connector with top contacts, and then view the eInk device from the back of the PCB?
Note that 1-1734839-6 is a "top contact" type.)

I chose not to mess with cutting the cable to width.
Cutting the cable to a width of 7 contacts would be difficult, even using a microscope.
Thus the board uses TE Connectivity 1-1734592-6.
The Digikey part number is the same, 1-1734592-6.


### KiCad project

This is a KiCad project.
See it for details: a BOM, footprints, schematic, etc.


## Driving the display

See http://essentialscrap.com/eink/Driving_E_Ink_Displays.pdf

It requires a single positive voltage.
Use GPIO pins.
You drive the top high and a segment low to make a segment white.
You drive the top segment low and a segment high to color the other way, black.

### Voltages

The eInk part wants 5V or 15V.  
5V gives only 80% of available contrast.
I have found that even 3.3V gives some visible contrast.

### Timing

eInk specifies pulses of 0.5 to 2 seconds at 5V.
Even shorter pulses give visible changes.


### Balanced switching

Some sources say:

Quote:
Do drive the ink in a DC-balanced manner
Net impulse across ink should sum to zero
At constant-voltage, this means equal pulses in opposite directions.
Do Not overdrive the ink
Do Not apply pulses longer than needed to reach saturated optical states.
Do Not re-drive ink in the same direction.

I think this means you should not repetitively turn on a segment,
instead you should turn it off then on.
I don't think this is a problem in practice.






