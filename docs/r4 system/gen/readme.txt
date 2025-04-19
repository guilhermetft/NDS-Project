*******GAMES NEED TO BE RENAMED TO .gen IF THEY ARE IN .bin FORMAT*************

*********************************************
              jEnesisDS 0.7.4
                                   2008/07/13
*********************************************


-------------------
1. About jEnesisDS |
-------------------

"jEnesisDS" is a Sega MegaDrive/Genesis Emulator for the Nintendo DS.
It started as a port of my Java Genesis/32X emulator jEnesis. By now, the code has been 
completely rewritten and most parts are written in ARM assembler.

You have to play a bit with the settings to make some games boot or work better.
Some games work faster with "H-INT emulation", others need it to work at all.
Very few games will just boot, if checksum autofixing is disabled (Dynamite Heady, Thunder Force IV).


Changelog:
********
v0.7.4 * 
********
  - Changed scheduling of M68000 and Z80.
  - Some changes in M68000 internal memory handlers.
  - YM2612 FM core mostly rewritten in ASM.
  - Some bugs in FM core fixed (Operator 1 was sometimes not considered in certain cases).
  - Fixed reset bug for FM core resulting in unstable sound for every game loaded except the 1st one.
  - Raised sample rate for FM emulation from 16KHz to 28KHz (28, because a few games can't do 32KHz)
  - Sound is completely mixed in hardware now, meaning every FM channel, PSG and DAC have their own DS sound channels.


********
v0.7   * 
********
  - Fixed bug in Z80 core, preventing some games from having sound (Wonderboy, etc.).
  - Fixed bug in 68000 optimization, that could make some games hang (Bonanza Brothers, etc.).
  - Changed sound handling and doubled sample rate for PCM sound, resulting in slightly better sound quality.
  - HW renderer partially rewritten, many glitches should be gone, some are still there (and will probably not be easy to fix ever)
  - Sprite rendering completely rewritten in ASM. Should be faster and fix most of the sprite issues.
  - Implemented mid frame palette updates (water effects in Sonic games, Castlevania, etc.). Note, that this just works, if a game is constantly fast enough, so slowdowns can still cause colors to flicker).
  - Many little optimizations in memory handling and the CPU cores. Should reduce slowdowns.
  - Added option for sprite masking (Landstalker etc.). It is not 100% emulated, just faked to be enough for most games using it (disable it, if sprites are missing, that should be there).
  - Added option to change between 3- and 6-Button pad (just works, if the option is applied BEFORE loading a game). When 6-Button pad is disabled, L+R can be used to move the visible screen area, X to center it.
  - Added sound state to the savestates, so that the correct tracks should play now when a state is loaded. Savestates are still not 100% reliable and loading old states can potentially cause problems.


********
v0.6   * 
********
  - Custom Z80 ASM core implemented.
  - Custom YM2612 and PSG emulation, running on the ARM7. So there is sound now ;)
  - Many parts rewritten. Speed without Z80 core should be quite a bit faster for most games.
  - Idle-loop detection completely rewritten. Shouldn't break any games anymore. Therefore the option to
    disable it was taken out.
  - Some changes to HW renderer. Some glitches should be gone, others were probably introduced. Will be 
    rewritten for the next version.
  - Tweaked H-Int auto detection, so less games should need the "ON" option to boot now.
  - Mode-Button added (L+R+Start)


********
v0.5   * 
********
  - Implemented save-states (touch slot icons to load/save)
  - Extended SRAM compatibility. Story of Thor and Phantasy Star IV should work now.

  - Extended "force update" of HW renderer. Fixes Sonic3 intro, Sonic Bonus stage and probably others.
  - Fixed sprites showing garbage if more than 64 sprites were displayed.
    (Comix Zone, Outrun, Sonic, well most games i guess).
  - Partial rewrite of sprite handling in the HW renderer.
    Less slowdowns when a lot of sprites are displayed.
  - Implemented better VSync. Fixes temporary speedups after slowdowns.
  - Implemented vertical scaling option into HW renderer (horizontal is NOT possible, dont ask!).
    Aspect ratio will be incorrect, but makes games more enjoyable (at least in my opinion).
  - Implemented screen positioning in HW renderer (touch screen to pause, then use [D-Pad] to scroll.
    Push [A] for faster scrolling)

  - Rewrote DS interrupt system for HW renderer. Probably less slowdowns, surely safer.

  - Added "Fake Z80" option. The faking code can mess up some games (Ghouls n' Ghosts, Aladdin, 
    Cool Spot 2, and others), so it can be turned off now.
    Interestingly enough, if it is turned off, real Z80 emulation will be executed, BUT just under
    certain circumstances, to keep games working and not to slow things down.
    As with other options, some games might depend on a certain setting to boot 
    (Gaiares just boots when this option is set to "off").


********
v0.4a   * Updated Release
********
  - Recompiled with current cpu core. v0.4 was "accidentially" compiled with an older version.
    This should raise compatibility quite a bit.
  - Separated HW and SW renderer versions.
  - Activated "Force Update" Option in the HW renderer version. If enabled, the chances of tile 
    corruptions are minimized - it can lead to massive slowdowns though, if a game updates more than 
    1024 unique tiles per frame (Turrican intro, Comix Zone intro).
    You can also temporarily change this option for a one-time update, if the tiles are corrupted
    (i.e Viewpoint).

********
v0.4   * Initial Preview Release
********
  - Custom ARM asm Motorola68000 CPU core
  - Hardware and Software renderer (this release defaults to the HW renderer and the SW
    renderer can not yet been choosen through the settings.
  - VDP emulation with all DMA modes
  - Horizontal & Vertical Interrupts
  - Support for PAL/NTSC and all country codes (all games will run at 60Hz though)
  - .smd, .bin & .gen support
  - partial SRAM save/load support (doesnt work for all games yet)
  - Line based renderer
  - Scroll Layers A+B & Window rendering with priorities (horizontal Windows arenot emulated in the
    HW renderer yet)



--------------
2. How to use |
--------------

If you downloaded this, you probably know how to use an emulator. It
should be self-explanatory ;)

jEnesisDS uses DLDI for accessing your cards filesystem, so you have to patch the file
with the appropriate DLDI patch found here:
http://chishm.drunkencoders.com/DLDI/

There is no way to edit the key settings yet, so here is the layout:

6-Button Mode:
PAD1:
A=	 [Y]
B=	 [B]
C=	 [A]
X=	 [X]
Y=	 [L]
Z=       [R]
START=	 [START]
MODE =	 [START+L+R]
L,R,D,U= directional keys

3-Button Mode:
PAD1:
A=	 [Y]
B=	 [B]
C=	 [A]
L,R,D,U= directional keys
START=	 [START]

[X]: Center screen
[L]: Move screen area left
[R]: Move screen area right
(Note: screen area can just be moved, if the game has a horizontal resolution of 320 pixels)


[SELECT]: Enter File Browser (Also accessible by the cartridge icon)

Touch the Joypad icon to enter Setting ingame.
Touch save-slot icons to load/save states (2 slots available)
Touch screen to pause. While in pause mode, use the D-Pad for 
screen positioning in the HW renderer version.



----------------
3. Thanks go to |
----------------

-Exophase, St phane Dallongeville ,Charles McDonald, SiLeNt_Ni
-Anyone else who supported this project in one or another way


-------------------------------
4. Licence and Acknowledgement |
-------------------------------

jEnesisDS is a released under no special kind of licence, it is completely free, the sources
are closed and it is provided as is, without any kind of guarantees or support.
Use it at your own risk.
jEnesisDS is developed by me, Stephan Dittrich and i hold the copyright to it. Dont modify it, 
dont sell it, dont do anything illegal with it, or distribute it without this document.
If you want to host jEnesisDS on your website, do so, if you provide the original archive including
this document, as found on my website www.workingdesign.de.

jEnesisDS was entirely written by me, without using any existing sources

-----------
5. Contact |
-----------

If you want to leave a comment about jEnesisDS, do it here:

dittiman@gmx.net

or visit my website: www.workingdesign.de

Anyway, hope you enjoy it...


