# This file is part of Mini-Coil open source DRSSTC project
If you want to build one have a look at the entire project here: ...link TBD...
Are you building one right now and need info on it? Then keep reading :)

# How to build this part of the coil
This board is the board that connects the UD3 with the bridge and has the gate resistors and GDTs on it.

Here's what you'll need to build it:
 - Soldering Iron
 - Solder (I suggest leaded solder if you don't have a powerful iron)
 - PCB Components (listed below)
 - at least one Signal Board PCB and two GDT PCBs
 - the cores for the GDTs and CTs (listed in the BOM too)
 - wire for winding the GDTs and the CT
 - two narrow (~3mm) caple ties
 - two brass 15mm long m3 male-female standoffs
 
# BOM (bill Of Material)
The BOM can be found in the file "Bill of Materials-Mini-Coil - Signal Board.xlsx". It contains part numbers of some of the specialised components for ordering on digikey.
There is a seperate line for items you can get from Wuerth Elektronik directly if you are in contact with them (ask for samples, they will probably give you the parts for free).
If you can't order from wuerth directly you can also order those parts on digikey.

The parts without a specified part number you need to search for yourselves as there are many different alternatives and its likely you already have some laying around anyway ;)

**NOTE** The gate resistor values were empirically chosen for the FGH75T65SQD IGBTs. If you change to different IGBTs you will need to figure out the right values yourself.

### non-critical components
In general it is almost always possible to substitute parts for other ones if you can't get/don't want to buy the specified ones. Here are some notes however:
 - The pin headers used for connecting the GDTs can be easily substituted by cheap ebay/aliexpress knockoffs (search for KF2512). You can get sets that come with connectors, crimp contacts and a crimp tool for maximum convinience.

### critical components
Unlike most components these cannot really be substituted easily
 - The opto-transmitter for the WS2812 output obviously needs to be the exact model that fits onto the board ;)
 - GDT Cores (todo)
 
# Assembly notes
**caution** the pin socket placing is a bit weird here, pay attention or you will ruin your board ;)

Just like with the other boards you should start with the SMD components. So thats all of the gate resistors (make sure to pay attention to where the values go ;) ), the diodes and the small other parts. 

Then solder all of the molex kk pinheaders (J14,J15,J17,J18,J21,J22) as well as the fan headers and input terminals (J1,J2,J3,J4) onto **the top side** of the board. 

*now the tricky (and annoying) part)*
Next we need to solder down the sockets for the connections to the power board. These must go onto the **bottom side** of the board and also be perfectly square or they will be even more of a pain to plug in than the board is with then soldered properly.

The same needs to be done for the connections to the UD3. Here I would just recommend that you assemble the UD3 first (including the standoffs!), then plug pre-cut pieces of the sockets onto the pins on the bottom of the UD3 and screw it down to the signal board (it must be on the side that has the facepalm meme from picard on it), that way they already sit square and won't fall out while soldering.

And then solder on all other missing components. This includes the two M3 standoffs. You should cut all but 1mm of thread off the male end of each and solder it into the holes for the GDTs here: (picture)

### GDT assembly
In the next step we need to prepare the GDTs. 

Since I have no actual data on my cores you will need to verify this works properly with the ones you got! Dimensions of mine (which is what the PCB is roughly designed for) are: od x id x l    27mm x 14mm x 15,5mm. Make sure the cores you buy are ferrite (not metal powder or something similar) and aren't drastically smaller (as that might result in saturation) or larger (as they might just not fit onto the board). If you want to you can test fit your cores in CAD with the STEP model of the entire assembly I provided here (link TBD), but keep in mind that the windings will make the finished GDT significantly larger!

Regarding wire choise: I use solid core wire with normal insulation for mine, no idea what thickness though as the reels are unlabled :P Use something that feels sensible to you. To measure the length wind on a single turn, measure how long the wire is and multiply by the number of turns you need. Add a bit of safety margin and 30cm for the connection to the IGBTs and you should be good. Just remember: you can always cut it shorter, but extending it is a pain ;) I do recommend pre twisting the wires slightly, as not doing that will increase your stray inductance, which is a serious problem in a fast little coil. Just put them in a drill and the other side into your bench vice and twist them **a little**. Don't overdue it or you might damage the insulation. Remember: it still needs to withstand >300V between the windings.

When you have all the stuff you need wind them with anything between 8-10 turns (I did 10), and a ratio of 1:1:1. But be careful: the winding count only works if your cores have a similar saturation flux density, mu_r and size as mine. I've written about testing wether your GDTs are adequate in the testing section.

When your finished you can insulation test them if you have the equipment or hope for the best that you didn't squish any insulation too far. Finally mount them to the PCB by sticking them onto the soldered in standoffs and screwing the mounting PCBs down with a sufficiently long M3 screw (how long depends of the final height of your GDTs). 
**Note:** The connections to the IGBTs must be done in a crossed over sort of way as seen here: (picture)

### CT Assembly
We do of course also need a current transformer. This is split into two cores to reduce the likelyhood of saturation, and is made up of the same cores used for the GDTs. For the wire you should go with something thicker than the GDT windings as (especially the first stage) actually carries quite a bit of current. I've used 0.75mm enammel wire but that is probably not the best choice as the insulation degrades when bending it and much more importantly: it's a pain to connect :P

First wind the two cores with 20 turns each (value needs verification just a quick count!) and then mount to the PCB. For this you should probably first pull one cable tie through the hole until its head is blocking it from going further, then put the other side of the cable tie through the other hole from the side that it is currently on and insert into the head **of the second cable tie** right after the hole. Don't pull it tight yet, instead put in one of your pre-wound cores and then pull it tight agains the PCB. Rinse and repeat with the second core, but on the other side of the PCB. **Note:** the core on the top side must be offset to teh side to not interfere with the mount for the cap board.

In the end it should look somewhat like this (just ignore the cable to the resonant cap for now :P):
(picture tbd)

Then loop the wire from the bottom CT through the top one and solder it together (prob should add some heatshrink too) and solder the two wires from the top one to the PCB (the two pads right next to it).

# Testing
For once there is actually quite a bit of stuff you should test here, although most relies on other parts of the coil. To run these tests, you will need to have finished assembling:
 - the UD3
 - the power board
 - the heatsink assembly (including transistors)
 - the main power module of the coil (so heatsink, power board, signal board and ud3)
 
Since we are performing a first test of the bridge that part of the assembly instructions links here too, incase you are coming from that and are confused :)

**what are we testing for?** The main thing we want to know is if the GDTs are working properly without saturating and if their phasing is correct. While checking for that we also test part of the UD3, the soldering of the gate resistors and the igbts.

To do this we first power on the bridge. Just apply 24V to the 24V in terminal block (the bottom one), probably with some current limiting to prevent a catastrophe if something was soldered wrong ;) Just to be sure: the bus **must not be powered** during this test, not form a lab power supply and certainly not from the mains.

Then connect your oscilloscope ground to both "vbus -" and both bridge outputs. (i recommend just clipping one groundlead onto a source pin of one of the IGBTs). **This is only safe if there is no power on the bus**.
We will be measuring the voltages on the IGBT gates, but that is easiest to measure on the output side of the gate resistors on the signal board (so the one facing towards the connectors). I just use the probe tip instead of the hook, you won't need to hold it there for long anyway. We first measure the signals on the gates connected to "GDT1 Out B" and "GDT1 Out A". But first we need to setup the UD3.

Once the UD3 has powered up fully you can connect it to you PC with USB and open the serial port it creates in a terminal (baud rate doesn't matter). For testing we only need to excecute the following commands (full setup will be done later).
 - set the drive voltage to something reasonable and enable vDrv regulator: "set vdrive 19"
 - disable startup fail protection: "set max_fb_err 0"
 - set the resonant frequency to the value expected for your coil (so 200kHz for the recommended resonator): "set fres 200"
 - set pulsewidth to 0: "set pw 0"
 - start transient output: "tr start"

Once you ran those commands we are ready to test. Run the command "set pw 100" to set the pulsewidth to 100 microseconds and check with your scope if you see the signal on all eigth gates. If the signal is there it means that the UD3 is working and there are at least no other major problems with your wiring.
Btw, if at any point during the test the GDTs start clicking loudly (usually it should just be a slight noise) you'll probably want to shut the output off again (so "set pw 0") and check your wiring, as something might be shorted. It shouldn't kill the UD3 but isn't really good for it either.

Now its time to test how good your cores are ;) With your oscilloscope connected to one of the gates (might want to use a hook, this takes a while) slowly decrease the resonant frequency until you either hear your GDTs klicking angrily or you see the voltage on the gate sag before the end of one cycle.
To do this you will need to run the following sequence:
 - "tr stop"
 - "set fres {new fres}"
 - "tr start"
 - "set pw 100"
 
Take fres down in steps of perhaps 25kHz and check if they are saturating every time. Once they do you know roughly the lower limit of fres they can support, the lower the better your cores are :D. But there's a catch... during pulseskipping the GDTs see the same signal for two periods, so effectively like a signal at fres**/2**. So the GDTs absolutely must not saturate until well below a set frequency of fres/2 (mine start to do so around 50kHz, so good for coils down to 100kHz).
If your GDTs failed this (so the test frequency you got to was higher than half of the planned resonant frequency) you will need to wind you GDTs with more turns or get better cores (>10 turns starts having excessive stray inductance).

So at this point you should have two beatuiful GDTs ready for phasing ;)
To do this simply set the UD3 up for testing as before (but remember to get fres back to the target value ;)) and let it run at a pulsewidth of 100us. Go ahead and measure the signal at GDT1 Out A and B (note: if the high side signal looks weird make sure you have grounded the correct bridge output). These should be the inverse of each other (btw. make sure you haven't acidentally turned on channel invert on your scope).
If they aren't, unplug one of the output connectors and pull out the contacts (you will need to unlatch them with a screwdriver or something similar by pressing in the little tab on the one side of the connector), swap them over and plug them back in. Then re-measure the signal and the two should now be phased correctly.
Repeat the same process for GDT2 Out A&B.

Then we need to check if the phasing between the two half bridges. For that connect the scope the both low sides (so GDT1 B and GDT2 A) and check the phasing as before. But if this is incorrect we now pull out the input connector to one of the GDTs (doesn't matter which) and swap it. After that all four gates should be phased correctly.

Final check (almost done ;)) is to verify that all gates are connected properly. With the UD3 output running measure each gate in turn, making sure that the waveform looks like an rc-charging waveform that reaches the end voltage at no more than 10% of the half wave and no less than 2% (numbers pulled out of my bum... it just shouldn't look like a square wave or a super slow triangle). I'll post a picture of how it should look when I have my small coil apart next time. If any signal looks too slow, check for shorts. If a signal looks like a rectangle make sure the IGBTs gate is actually connected (verify for example the pin headers, they like to miss the holes)

If all eight IGBTs (don't just test four :P) check out the signal board and the power board have passed the tests :D We'll test the rest (so mainly the CT) later.

Oh do you like relay sounds? Type "bus on", that should switch on one of the relays ;)

# Disclaimer
This project utilises dangerous (lethal!) voltages! There is a high likelyhood of fire/personal harm if you don't know what you are doing. Use these files at your own risk. Any damage you do to yourself or other people with this project is not my responsibility.

I also make no promises about the correctness of any of the info given in this project or any of its files. It is also your responsibility to verify all of the data in this when building your own coil. You are thus responsible for any damage caused even by mistakes in these files.

Ensue the standard legal disclaimer text just to be sure... (modified for open hardware)

Permission is hereby granted, free of charge, to any person obtaining a copy of this data and associated documentation files (the “data”), to deal in the data without restriction, including without limitation the rights to use, copy, modify, merge, publish, distribute, sublicense, and/or sell copies of the data, and to permit persons to whom the data is furnished to do so, subject to the following conditions:

The above copyright notice and this permission notice shall be included in all copies or substantial portions of the data.

THE DATA IS PROVIDED “AS IS”, WITHOUT WARRANTY OF ANY KIND, EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE DATA OR THE USE OR OTHER DEALINGS IN THE DATA.
