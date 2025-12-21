RTL SDR FM Player
===================

## Fork for modified [rtl-sdr](https://github.com/Mr-Precise/rtl-sdr)
SDR Stereo FM radio receiver for RTL dongles, with TimeShift and Recording.
TimeShift function can go back some minutes in time to listen it again.
Recording function to save WAV files.


Description
-----------
**RTL FM Player** is a small tool to listen FM stereo radio by using a compatible DVB-T dongle.
Is a console application that runs on Linux and Windows, all commands like changing stations and timeshifting is controlled by keyboard keys.
Outputs stereo audio to sondcard using SDL library.
Can record audio .wav file format.

The DVB-T dongle has to be based on the Realtek RTL2832U.
See http://sdr.osmocom.org/trac/wiki/rtl-sdr for more RTL SDR details.
You need to install a new driver to use this dongle.


Installation
------------

#### Windows:

- Download Zadig driver from [official zadig.akeo.ie](https://zadig.akeo.ie) site or my custom build [Zadig winusb driver installer](https://github.com/Mr-Precise/SDR-binary-builds-stuff/releases/download/windows/zadig-2025.2-msvc142-Win64.exe)

    1. Plug in the RTL-SDR.
    2. Run Zadig as administrator by right clicking it and choosing run as administrator.
    3. Go to Options -> List all devices and make sure it is checked.
    4. In the drop down box choose Bulk-In, Interface (Interface 0). This may also sometimes show up as something prefixed with “RTL28328U”. That choice is also valid.
    5. Make sure that WinUSB is selected as the target driver and click on Replace Driver.

- Download a compiled **RTL FM Player** here: [ >> Releases << ](https://github.com/Mr-Precise/rtl_fm_sdlplayer/releases)
- Optional. Compile it on Linux, or Windows using MinGW.


Usage
-----

On Linux, open a console and type `./rtl_fm_player`

On Windows, just double click `rtl_fm_player.exe`

Warning, may be loud!

Use keyboard to control frequency, tuner gain, timeshift, mute and recording.

You can also open Command Prompt and type parameters manually:
```
C:\>rtl_fm_player.exe -h
./rtl_fm_player -h
```


Common parameters
-------

    Show all available parameters
    rtl_fm_player -h

    Start and tune to frequency in Hz 
    (97.7Mhz)
    rtl_fm_player -f 97700000

    Tune to frequency and record audio to FileName.wav
    (Keyboard controls disabled)
    rtl_fm_player -f 97700000 FileName.wav


Performance
--------------
On modern PCs (x86, x64) mono and stereo decoding should be possible easily.


Limitations
--------------
Latency increase if SDL2 audio queue becomes larger. I clean the buffer when changing stations or Timeshifting.


Building
-------


### Compiling RTL FM Player sources on Linux:
`Tested on Debian 10 "buster"+ and ubuntu 20.04 "focal"+`


1. `sudo apt install cmake libusb-1.0-0-dev libsdl2-dev pkg-config make gcc`
2. Download sources `git clone --recursive https://github.com/Mr-Precise/rtl_fm_sdlplayer`
3. Create and enter build dir `cd rtl_fm_sdlplayer && mkdir build && cd build`
4. CMake configure:
    - `cmake .. -DDETACH_KERNEL_DRIVER=ON`
    - `cmake --build . --config Release`

### Compiling RTL FM Player sources on Windows or Cross-compiling on Linux:
Use MinGW/[msys](https://www.msys2.org/)/[LLVM Clang](https://github.com/mstorsjo/llvm-mingw)/[MXE](https://mxe.cc/) etc...  
libusb [libusb/releases](https://github.com/libusb/libusb/releases)  
Latest [CMake Build System](https://cmake.org/download/)  
SDL2 [libsdl-org/SDL/tree/SDL2](https://github.com/libsdl-org/SDL/tree/SDL2)

Credits
-------

- This project is based on RTL SDR FM Streamer by Albrecht Lohoefener

- Libusb. A cross-platform library that gives apps easy access to USB devices

- Simple DirectMedia Layer development library


Similar Projects
----------------
- RTL SDR FM Streamer
  - https://github.com/AlbrechtL/rtl_fm_streamer
- FM Radio receiver based upon RTL-SDR as pvr addon for KODI
  - http://esmasol.de/open-source/kodi-add-on-s/fm-radio-receiver/
  - https://github.com/xbmc/xbmc/pull/6174
  - https://github.com/AlwinEsch/pvr.rtl.radiofm
- rtl_fm
  - This tool is the base of rtl_fm_streamer
  - http://sdr.osmocom.org/trac/wiki/rtl-sdr
- sdr-j-fmreceiver
  - http://www.sdr-j.tk/index.html
- GPRX
  - http://gqrx.dk

