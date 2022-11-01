# **240p mode on the 3DO**

The 3DO is an interesting piece of hardware. Originally designed to output a standard definition video signal at 480i NTSC or 576i PAL. A while ago it was discovered that the 3DO could be modded to output its video signal in progressive mode at 240p NTSC or 288p PAL. For more detailed information on how the 3DO handles 240p check here https://3dodev.com/documentation/hardware/opera/240p_mode.
This method was originally documented here https://www.retrorgb.com/3do240p.html (original thread here https://assemblergames.org/viewtopic.php?t=816) but some 3DO models had trouble booting in 240p so users had to switch back from 480i after booting the console. This guide hopes to gather all the information I have found through my research and illustrate how to correctly modify a 3DO console to produce 240p video output. It will also hopefully dispel some of the misconceptions around it.

## **Background**

A while ago, before we had publicly available hardware docs on the different 3DO hardware, I decided to try and see if any other models besides 3DO containing the VP536 encoder could be switched into 240p mode. I discovered that the Panasonic FZ-1E (PAL) and FZ-1 released in Canada containing the Brooktree BT9103 encoder could also handle 240p. Upon further investigation I found that the 3DO VDP (CLIO) had a pin for controlling interlace/ progressive mode on the analogue video encoder. 

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/IMG_2038_Interlace.jpg)

I figured that this pin could be pulling the interlace/ progressive control pin high or low and conflicting with the 240p mod in some consoles, causing erratic behaviour. By removing R166, a 0 ohm bridging resistor, this would in theory stop the CLIO from interfering with the 240p switching. It turned out after further investigation that the CLIO Pin 197 is inactive. It is unclear if 3DO ever planned to utilise this feature. There is, however a weak pull up resistor (R167) which holds the line at 5V so removing R166 is recommended in all Panasonic consoles when performing the 240p mod. In Canadian 3DO it may be necessary to remove R164 instead.
There are two approaches to this mod. The first option is to lift the interlace switching pin altogether and wire your switch. This way there is no chance of any unwanted states on this pin. The disadvantage to this is the PLCC package pins can be tricky to lift which also increases the risk of damage to the console and soldering directly to the chip increases the risk of bridging pins. The second option is to remove a resistor and solder to empty pads. This removes the risk of damage to the encoder and looks more eloquent. 

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/BT9103_240p_crop.png)

### **Panasonic FZ-1 with BT9103 Encoder (PAL/ CAN)**

Panasonic FZ-1 from Europe (PAL) and Canada (NTSC) contain the BT9103 video encoder. The BT9103 video encoder can display non-standard progressive video by setting the Interlace pin (Pin 59) to a logical zero (GND). By attaching a switch, the Interlace pin can be switched between a logical one (5V) and a logical zero (GND) switching between 480i and 240p respectively. 
First prepare the motherboard by removing R166 (or R164 if Canadian version). This will remove any connection to the CLIO digital video processor and any pull-up resistors.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/IMG_2038_R166.jpg)

Then solder wires from your switch to the points indicated below. You can also solder this wire to the pad of R166. There are many options for GND and 5V on the board, these points were chosen for convenience assuming you are using a standalone switch (you can even use a custom pcb with a mini din connector and switch if combining with RGB mod, more on that later ;-) (The print on the encoder is orientated differently  in the next picture due to a newer encoder being installed in the same space for a different mod). For the sake of this guide 'INT' refers to the Interlace/ Progressive switching pin of the respective Video encoder.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/IMG_2311_pinout.jpg)

If you have the Canadian version, R165 will not be present and you will need to solder your 5V wire to the other pad as indicated. Or you can get 5V from another point.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/IMG_2311_pinout_alt.jpg)

Next either solder your wires to a simple SPDT switch.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/IMG_2056_cropped.jpg)

Or use a custom pcb which lines up with the original shell cut outs for the RF modulator and switch.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/IMG_2642(cropped).jpg)

### **Panasonic FZ-1 with VP536 encoder (US/ JP)**

All Japanese Panasonic FZ-1 and some US Panasonic FZ-1 contain the VP536 video encoder. This video encoder is the reverse of the BT9103 in a sense in that logical one on pin 52 switches it to progressive mode while logical zero switches it to interlace mode.
Once again remove R166. This breaks the connection with the CLIO and also any pull-up resistors (naughty R167).

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/VP536_remove.jpg)

Then solder wires from your switch to the points indicated below. The VP536 has weak internal pull down resistors which maintain a default 480i state if nothing is connected externally to pin 52. You could just wire pin 52 to a switch and 5V using 2 wires but I always like to use external wires in case the internal resistor fails.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/VP536_pinout.jpg)

### **Panasonic FZ-10 with VP536 encoder (US/ JP)**

The early Panasonic FZ-10 came with the VP536 encoder. Later releases came with the new Anvil combined chipset which didn't have 240p ability. This model had a common problem of not being able to boot in 240p mode. Users had to boot in 480i and switch back to 240p once booted.
One day I had a closer look and noticed that even though R166 was not soldered to the board, there was a trace running through the middle. 

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/FZ_10_R166.jpg)

By cutting the trace with a scalpel, the connection to pin 197 on the CLIO, and any other pull down resistors upstream, can be broken. This avoids the VP536 from being put into conflicting states and causing boot issues. 

Cut the trace in between the pads of R166. No need to go crazy, just cut deep enough to break the trace. Confirm with a multimeter to check for continuity between the pads.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/FZ_10_cut_arrow.jpg)

Then solder wires from your switch to the points indicated below. The VP536 has a weak internal pull down resistor which maintains a default 480i state if nothing is connected externally to pin 52. You could just wire pin 52 to a switch and 5V using 2 wires but I always like to use external wires in case the internal resistor fails. 5V and GND can be grabbed from numerous places on the board, I have just shown 2 options based on convenience.

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/FZ_10_pinout.jpg)



