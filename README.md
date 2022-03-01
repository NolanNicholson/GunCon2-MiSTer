# GunCon2-MiSTer
Resources for using the Namco GunCon 2 lightgun with the MiSTer FPGA

**NOTE!** This set of instructions has you install an experimental
Linux kernel and main executable on to your SD card.
Improper installation may put your installation in an unworkable state,
so I recommend using a fresh installation instead of your "main" one.
In any case, use at your own risk!

If you would prefer not to manually
replace important files on your MiSTer, support for the GunCon 2 will
eventually be included in the MiSTer's official main executable and Linux
kernel. The performance of the gun may be more reliable at that time as well.

Thank you for trying this driver, and for your patience while we work out any rough edges.


# Setup instructions

You will need:
- a Namco GunCon 2 (compatibles/clones should work)
- a standard-definition CRT TV
- a means of tapping your GunCon's RCA cable into your MiSTer's video
  sync signal (see step 4 below)

Optionally, for calibration, you will also need:
- an installed copy of the 240p Test Suite for the core you will run
- a keyboard with a working F10 key

1. ~~At the root of your SD card, back up your `MiSTer` executable
   (renaming it to leave it in the same directory is fine), then put
   the `MiSTer` executable in this folder in its place.~~ For now, simply
   run the downloader script on your MiSTer to keep its main executable
   up to date.

2. In the `/linux/` folder of your SD card, back up the `zImage_dtb` kernel
   image file (again, renaming it is fine) and add the `zImage_dtb` file
   from this folder.

3. Plug in the GunCon 2. The USB connector can be plugged
   into any of your data-capable USB ports (i.e., not the "POWER ONLY"
   one on the USB hub.) The yellow RCA connector needs to be connected
   to a composite sync signal. If you are using component video, you can tap
   into the Luma (green) cable. If you are using RGB, you need to be using
   composite sync, and the gun needs to be tapped into the composite sync
   signal. If you are using RGB with Sync on Green (SOG) enabled, the green
   line should also work.

You should now be able to use your GunCon 2 as a controller on the MiSTer.
The ideal calibration settings for the gun will vary for each display, and
for each core.


# Calibration instructions

To calibrate the gun for a particular core, follow these steps:

4. Open a core (e.g., SNES), and load the 240p Test Suite.

5. Use the 240p Test Suite's "White and RGB Screen" pattern to display
   a full white screen.

6. Open the MiSTer OSD and press F10 on a keyboard. A lightgun calibration
   menu should appear.

7. Using the menu, aim at the extreme edges of the screen, then press A
   on the left side of the gun to calibrate that edge. (Note: The menu
   will prompt you to press "Trigger"; press "A" instead.) Your goal is to
   get the most extreme numbers you can without the gun losing sight of the screen.

8. You should now be calibrated. To confirm, try enabling the core's
   lightgun crosshair (if it has one) and moving around the white screen.


# GunCon 2 Performance on MiSTer

Overall, the GunCon 2 is an accurate and precise lightgun with relatively little jitter.
It requires a certain level of screen brightness in order to detect the CRT beam; some
consoles' lightguns were designed for IR tracking or very tight CRT flash timing, which
gives the GunCon 2 some trouble.

- NES (Zapper): ~~**Good.** As of 2022-02-06, this driver has been modified to improve compatibility
  with NES Zapper games. There are some issues with hit detection on black screens, such as the
  Duck Hunt menu, but in-game performance has tested mostly solid. (As of this writing, you
  will require the updated MiSTer binary here in order to play NES games.)~~ NES Zapper is currently
  not working, pending submission of some code to the main MiSTer framework.

- Master System (Light Phaser): **Okay.** Works well for brighter games. Darker games, like
  certain sections of Shooting Gallery, have trouble.

- SNES (Super Scope, Justifier): **Good.** You may need to brighten your screen for some games, but most
  Super Scope games are already bright enough to work well. All SNES Justifier games have been
  thoroughly tested, except for Lethal Enforcers.

- Genesis (Menacer, Justifier): **Okay.** You may need to brighten your screen for some games.

- PSX: Basic GunCon emulation has been implemented, but the horizontal scale is not correct due
  to resource constraints. The MiSTer executable in this repo contains a patch that corrects any
  lightgun-type inputs being sent to the PSX.
  With this calibration, performance is good overall, though "shoot offscreen to reload" is not yet
  working correctly, and there are some detection issues when shooting at dark areas of the screen.
  The Konami Justifier is not supported.
  
  Note: The GunCon in the PSX core uses the following buttons from the standard gamepad:
  - Circle: maps to Trigger
  - Start: maps to A
  - Cross: maps to B
  
  So, map your GunCon 2's trigger to Circle, your A button to Start, and your B button to Cross.
  (For the other buttons, feel free to either map them as desired or skip them - they will be
  ignored when the core is emulating the GunCon 1.)

- Saturn (Stunner): **Core is still in development and does not yet have lightgun support.**


# Notes on using the GunCon 2, and on this driver/setup

- Like the Wiimote, this gun can report its coordinates as a mouse (with
  throttling applied) and as a raw joystick. It will work much better as
  a raw joystick. Hence, when setting up specific cores, choose the "Joy" options for aiming.

- The self-compiled kernel here works fine for the most part, but it may not work properly
  with some devices (for example, some WiFi dongles.) These issues should no longer exist
  once the next official kernel release incorporates GunCon 2 support. In the meantime, be sure
  to keep your official kernel image available, so that you can swap back to it if needed.

- If you accidentally severely miscalibrate the gun for a core, the core
  may crash or not start up. If this happens, or if you want to retry
  calibration for another reason, look for the gun calibration files in
  /config on your SD card, and delete them.

- The GunCon 2 is capable of reading a 480p screen, but this driver is
  not yet capable of that, so it functions only with standard-definition
  CRTs. NTSC and PAL should both be fine.


# Sinden Lightgun Support

If you have a Sinden Lightgun and are interested in using it on the MiSTer FPGA, this driver can
make that possible with the following additional hardware:

- Raspberry Pi 4
- Arduino Micro
- Open-Source Scan Converter (OSSC)

Follow the instructions at https://sindenlightgun.miraheze.org/wiki/OG_Console_Setup_Guide to set
your Sinden Lightgun up to emulate a GunCon 2 using the Raspberry Pi and Arduino. Use your MiSTer
to output over analog or direct video, and use the OSSC to apply a Sinden-compatible white border
to the screen.

Using the Sinden as an emulated GunCon 2 should give excellent performance on all
lightgun-compatible cores, without any of the tracking issues or brightness dependence of the
original GunCon 2, and without the need for a CRT.


# Credits

This GunCon 2 driver was originally created by beardypig with the assistance of Rubén Tomás and the RGB-Pi development team. You can find the main version of the driver at https://github.com/beardypig/guncon2 . Many thanks to them for developing an excellent driver, and for making it open-source and publicly available so that as many people as possible can enjoy some good CRT shooting.

Thanks to sonik_br, Freddo, wickerwaka, and alanswx for testing, technical advice, and encouragement.
