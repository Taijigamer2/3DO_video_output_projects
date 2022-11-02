# 3DO_video_output_projects
A collection of projects for enhancing the video output of the 3DO hardware.

These projects are a result of a continuing journey which started back in 2017. I was facinated by the 3DO when I read that it wasn't a specific console but a hardware
standard that could be used by different companies to design their own consoles. I was particularly interested in the obscure PC ISA card, the Creative Labs
3DO Blaster. Unfortunately this card was very rare and expensive so I decided to look at enhancing the video output of the 3DO consoles to get it as close as possible
to the VGA standard of the Creative Labs 3DO Blaster. 

The 3DO hardware standard was designed for 480i video output. Some models of 3DO were found to be able to be modified to output 240p video. This was dependent on the 
analogue video encoder on the motherboard. Only one video encoder (VP536) was known to support 240p at the time so I bought a Panasonic FZ-1 in the hope it contained 
the VP536. What I found was Panasonic FZ-1 released in Europe had a different encoder (BT9103). As there were no schematics or service manuals available for 3DO at the time, 
I started to research the BT9103 encoder and surrounding video processing circuitry. I was able to discover the pinout and subsequent 240p mode of the BT9103 along 
with pinouts and service manuals of other models of Panasonic 3DO which formed the basis of subsequent 3DO projects in this repository.

## Brief description of projects

**240p_video_mode_on_3DO**

- README.md
  - Instruction on correct modification of the 3DO hardware to output 240p video
  - Which models are able to support 240p
  
**3DO_RGB_V1.1 (discontinued)**

- 24bit digital RGB to analog RGB video encoder pcb
  - BU3616K based circuit
  - Outputs 700mV RGB
  - CSYNC or SYNC over Luma
  
**3DO_RGB_V1.2**

- 24bit digital RGB to analog RGB video encoder pcb
  - BU3616K based circuit
  - Outputs 700mV RGB
  - XOR combined HSYNC/ VSYNC to create CSYNC

**3DO_RGB_V2**

- 24bit digital RGB to analog RGB video encoder and Sync generator pcb
  - BT856 based circuit
  - Outputs 700mV RGB via 7374 video Amp (8 pin Mini Din pcb)
  - XOR combined HSYNC/ VSYNC to create CSYNC
  - SYNC generation to restore 240p in 3DO with BT9101 encoders

**8_PIN_Mini_Din_pcb**

- PCB to mount 8 pin mini din connector and 240p mode switch for RGB mods
  - Option for 7374 RGB amp or passive attenuation of RGB and SYNC signals
  - Solders to RF modulator footprint to reduce wires needed

**3DO_RGB_Native_Mod**

- README.md
  - Instruction on removing the native BT9103 encoder (compatible models only) and replacing with a BT856 encoder
  - supports native analog RGB output and 240p
