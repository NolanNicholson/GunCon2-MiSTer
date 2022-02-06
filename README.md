# GunCon2-MiSTer
Resources for using the Namco GunCon 2 lightgun with the MiSTer FPGA

NOTE! This set of instructions has you install an experimental
Linux kernel and main executable on to your SD card.
Improper installation may put your installation in an unworkable state,
so I recommend using a fresh installation instead of your "main" one.
In any case, use at your own risk!

# Setup instructions

You will need:
- a Namco GunCon 2 (compatibles/clones should work but haven't been tested)
- a standard-definition CRT TV
- a means of tapping your GunCon's RCA cable into your MiSTer's video
  sync signal (see step 4 below)

Optionally, for calibration, you will also need:
- an installed copy of the 240p Test Suite for the core you will run
- a keyboard with a working F10 key

1. If you previously installed an external kernel module for the GunCon 2
   (in the form of a .ko) file, start up your MiSTer, open the shell,
   log in, and execute the following command:

   modprobe -r guncon2

   You can then remove the guncon2.ko file from your MiSTer.

2. At the root of your SD card, back up your "MiSTer" executable
   (renaming it to leave it in the same directory is fine), then put in
   the MiSTer executable in this folder.

3. In the /linux/ folder of your SD card, back up the "zImage\_dtb" kernel
   image file (again, renaming it is fine) and add the zImage\_dtb file
   from this folder.

4. Plug in the GunCon 2. The USB connector is normal and can be plugged
   into any of your data-capable USB ports (i.e., not the "POWER ONLY"
   one on the USB hub.) The yellow RCA connector needs to be connected
   to a composite sync signal. If you are using Component, you can tap
   into the Luma (green) cable. If you are using RGB, you need to be using
   composite sync, and the gun needs to be tapped into the composite sync
   signal. If you are using RGB with Sync on Green (SOG) enabled, the green
   line should also work.


You should now be able to use your GunCon 2 as a controller on the MiSTer!
The ideal calibration settings for the gun will vary for each display, and
for each core.

To calibrate the gun for a particular core, follow these steps:

5. Open a core (e.g., SNES), and load the 240p Test Suite.

6. Use the 240p Test Suite's "White and RGB Screen" pattern to display
   a full white screen.

7. Open the MiSTer OSD and press F10 on a keyboard. A lightgun calibration
   menu should appear.

8. Using the menu, aim at the extreme edges of the screen, then press A
   on the left side of the gun to calibrate that edge. (Note! When the
   calibration menu says "Trigger", it means "A". For most guns, the
   "trigger" is A, but the GunCon's side button is literally
   labelled A, so...)

   Your goal is to get the most extreme numbers you can without the gun
   losing sight of the screen.

9. You should now be calibrated. To confirm, try enabling the core's
   lightgun crosshair (if it has one) and moving around the white screen.


# Notes on the GunCon 2, and on this driver/setup

- As of 2022-02-06, this driver has been modified to improve compatibility
  with NES Zapper games. The way it does this is a tad hacky, and may
  affect compatibility with "shoot outside screen to reload"-type games.
  
- Like the Wiimote, this gun can report its coordinates as a mouse (with
  throttling applied) and as a raw joystick. It will work much better as
  a raw joystick.

- The PSX core does NOT support light gun games at the time of this
  writing. Please do not hassle anyone about this!

- This self-compiled kernel works fine for the most part, but it breaks
  compatibility with my Edimax WiFi dongle. You may experience similar
  random compatibility issues while using this kernel. These issues
  should no longer exist once the GunCon 2 driver is part of the
  official kernel release.

- The way this gun works requires a bright screen. Games with a dark
  (or red) screen, such as some Sega Genesis games, may function poorly
  unless you crank up your screen brightness.

- If you accidentally severely miscalibrate the gun for a core, the core
  may crash or not start up. If this happens, or if you want to retry
  calibration for another reason, look for the gun calibration files in
  /config on your SD card, and delete them.

- The GunCon 2 is capable of reading a 480p screen, but this driver is
  not yet capable of that, so it functions only with standard-definition
  CRTs. NTSC and PAL should both be fine.

- MiSTer's built-in calibration works by reading the extreme edges of
  the screen, which may be a bit troublesome depending on your overscan
  settings. It may be possible to manually correct the gun calibration
  file, but this hasn't been tried yet.
  
- If you have any questions or feedback, feel free to reach out to
  @Nolbin on the MiSTer discord. Thank you for trying this driver, and
  for your patience while we work out the rough edges.
