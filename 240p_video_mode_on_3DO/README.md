# **240p mode on the 3DO**

The 3DO is an interesting piece of hardware. Originally designed to output a standard definition video signal at 480i NTSC or 576i PAL. A while ago it was discovered that the 3DO could be modded to output its video signal in progressive mode at 240p NTSC or 288P PAL. For more detailed information on how the 3DO handles 240p check here https://3dodev.com/documentation/hardware/opera/240p_mode.
This method was originally documented here https://www.retrorgb.com/3do240p.html (original thread here https://assemblergames.org/viewtopic.php?t=816) but some 3DO models had trouble booting in 240p so users had to switch back from 480i after booting the console. This guide hopes to gather all the information I have found through my research and illustrate how to correctly modify a 3DO console to produce 240p video output. It will also hopefully dispel some of the misconceptions around it.

## **Background**

A while ago, before we had publicly available hardware docs on the different 3DO hardware, I decided to try and see if any other models besides 3DO containing the VP536 encoder could be switched into 240p mode. I discovered that the Panasonic FZ-1E (PAL) and FZ-1 released in Canada containing the Brooktree BT9103 encoder could also handle 240p. Upon further investigation I found that the 3DO VDP (CLIO) had a pin for controlling interlace/ progressive mode on the analogue video encoder. 

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/IMG_2038_Interlace.jpg)

I figured that this pin could be pulling the interlace/ progressive control pin high or low and conflicting with the 240p mod in some consoles, causing erratic behaviour. By removing R166, a 0 ohm bridging resistor, this would in theory stop the CLIO from interfering with the 240p switching. It turned out after further investigation that the CLIO Pin 197 is inactive. It is unclear if 3DO ever planned to utilise this feature. There is, however a weak pull up resistor (R167) which holds the line at 5V so removing R166 is recommended in all Panasonic consoles when performing the 240p mod. In Canadian 3DO it may be necessary to remove R164 instead.
There are two approaches to this mod. The first option is to lift the interlace switching pin altogether and wire your switch. This way there is no chance of any unwanted states on this pin. The disadvantage to this is the PLCC package pins can be tricky to lift which also increases the risk of damage to the console and soldering directly to the chip increases the risk of bridging pins. The second option is to remove a resistor and solder to empty pads. This removes the risk of damage to the encoder and looks more eloquent. 

![](https://github.com/Taijigamer2/3DO_video_output_projects/blob/main/240p_video_mode_on_3DO/Images/BT9103_240p_crop.png)

### **Panasonic FZ-1 with BT9103 Encoder (PAL/ CAN)**
