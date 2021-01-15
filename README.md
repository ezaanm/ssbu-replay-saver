# SSBU Replay Saver
I love Smash Ultimate especially when I get a nutty clip and dunk my friends. The process to save clips as videos, however, makes me want to hop into the blast zone since we have to watch the entire game and start each match recordings individually.

This fork^5 modifies prior Switch proof of concept input emulators to automatically save clips using an Arduino Uno R3 (which I got on Amazon for $10) so you don't need to constantly start new recordings. Plug the Arduino in and rollout.

---

LUFA has been included as a git submodule, so clone the repo like this:

```
git clone --recursive git@github.com:ezaanm/ssbu-replay-saver.git
```

will put LUFA in the right directory.

### Setup Instructions For Arduino Uno R3
1. Cop an Arduino Uno R3 (You can use a Teensy as well but the Uno R3 is the cheapest one on Amazon. I actually got a knockoff: https://amzn.com/B01EWOE0UU)
2. Clone this repo like shown ^^^
3. We're gonna need to put that [Arduino Uno R3 in DFU mode](https://www.arduino.cc/en/Hacking/DFUProgramming8U2) and flash it with our own .hex code. If you're using a PC download the applications in the [link](https://www.arduino.cc/en/Hacking/DFUProgramming8U2), if you're using a Mac you can run the following ```brew``` commands below.
4. In Terminal ```cd``` into the ```ssbu-replay-saver``` repo you just cloned. 
5. Run: ```brew install dfu-programmer```
6. Run: ```brew tap osx-cross/avr```
7. Run: ```brew install avr-gcc```
8. Plug your Arduino into your computer, take a piece of wire or metal, and connect these two pins briefly using the wire. Don't worry you won't get thunder jolted. Your Arduino is now in DFU mode! ![image](https://www.arduino.cc/en/uploads/Hacking/Uno-front-DFU-reset.png)
9. Next run my script: ```bash installToArd``` to compile the code, erase the standard Arduino software, flash the Arduino with our Joystick.hex file, and save it.
10. Your Arduino is ready to roll!

#### Setup Instructions For Teensy
The process is a bit simpler for Teensy boys.

Go to the Teensy website and download/install the [Teensy Loader application](https://www.pjrc.com/teensy/loader.html). For Linux, follow their instructions for installing the [GCC Compiler and Tools](https://www.pjrc.com/teensy/gcc.html). For Windows, you will need the latest [AVR toolchain](http://www.atmel.com/tools/atmelavrtoolchainforwindows.aspx) from the Atmel site. See [this issue](https://github.com/LightningStalker/Splatmeme-Printer/issues/10) and [this thread](http://gbatemp.net/threads/how-to-use-shinyquagsires-splatoon-2-post-printer.479497/) on GBAtemp for more information. For Mac you can run the same brew instructions from the Arduino Uno R3 setup.

You'll need to edit the ```makefile``` setting ```MCU = atmega32u4``` for Teensy 2.0, or whatever version you have.  Open a terminal window in the ```ssbu-replay-saver``` directory, type make, and hit enter to compile. If all goes well, the printout in the terminal will let you know it finished the build! Follow the directions on flashing Joystick.hex onto your Teensy, which can be found page where you downloaded the Teensy Loader application.

### Run Instructions Once Your Arduino Has Been Setup And Flashed
Now that your Arduino is flashed with the program you can do the following steps to automate your replay saving whenever you need!

Take your Switch in handheld mode. Open the SSBU Game > Vault > Replays > Leave your cursor over the "Replay Data" Button. Plug your Arduino into the Switch using any sort of USB C to USB A Adapter and let it run! You'll note that it will start the recording of a replay, wait about 7 minutes (since that's the standard game time's max length), delete the replay, and continue on looping the inputs forever.

#### Thanks
Thanks to https://github.com/kidGodzilla/woff-grinder for his Final Fantasy XP grinder which I modified.

Thanks to https://github.com/bertrandom/snowball-thrower for the updated information which modifies the original script to throw snowballs in Zelda. This C Source is much easier to start from, and has a nice object interface for creating new command sequences.

Thanks to Shiny Quagsire for his [Splatoon post printer](https://github.com/shinyquagsire23/Switch-Fightstick) and progmem for his [original discovery](https://github.com/progmem/Switch-Fightstick).
