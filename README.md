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

- Download Zadig driver https://zadig.akeo.ie/.

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

Use keyboard to control frequency, timeshift, mute and recording.

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
`Tested on Debian 10 "buster" and ubuntu 20.04 "focal"`


1. sudo `apt-get install cmake`
2. sudo `apt-get install libusb-1.0-0-dev`
3. sudo `apt-get install libsdl2-dev`
4. Download sources `git clone --recursive https://github.com/Mr-Precise/rtl_fm_sdlplayer`
5. Create and enter build dir `cd rtl_fm_sdlplayer && mkdir build && cd build`
6. CMake configure:
    - `cmake .. -DDETACH_KERNEL_DRIVER=ON`
    - `make`


## Obsolete (soon new README)

### Compiling RTL FM Player sources using MinGW32 on Windows: (target 32 bit)
`MinGW32 manual installation. You can install to any directory name without spaces in root drive, (eg: C:\MinGW32-RTL, D:\MinGWTemp). In this example we install to C:\MinGW32`

1. Download latest **mingw-w64** toolchain targeting architecture **i686**, **win32** threads, **dwarf** exception
    - https://sourceforge.net/projects/mingw-w64/files/
    - tested: [i686-8.1.0-release-win32-dwarf-rt_v6-rev0.7z](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win32/Personal%20Builds/mingw-builds/8.1.0/threads-win32/dwarf/i686-8.1.0-release-win32-dwarf-rt_v6-rev0.7z/downloadd)
2. Extract the **mingw-w64** toolchain 7zip file to root directory, keeping the structure:
    ```
    C:\mingw32\
              \bin
              \etc
              ...
    ```
3. Download **CMake** Windows win32-x86 Zip file (not the installer)
    - https://cmake.org/download/ 
    - tested: [cmake-3.17.1-win32-x86.zip](https://github.com/Kitware/CMake/releases/download/v3.17.1/cmake-3.17.1-win32-x86.zip)
4. Extract **CMake** Zip file inside `C:\MinGW32\CMake` directory, keeping the structure:
    ```
    C:\mingw32\cmake\
              \cmake\bin
              \cmake\doc
              \cmake\man
              \cmake\share
    ```
5. Download **SDL2** Development Libraries for MinGW
    - https://www.libsdl.org/download-2.0.php
    - tested: [SDL2-devel-2.0.12-mingw.tar.gz](https://www.libsdl.org/release/SDL2-devel-2.0.12-mingw.tar.gz)
6. Extract **SDL2** zip file `i686-w64-mingw32\lib\libSDL2.dll.a` to `c:\mingw64\i686-w64-mingw32\lib\`
7. Extract **SDL2** zip directory `i686-w64-mingw32\include\SDL2` to `c:\mingw64\i686-w64-mingw32\include\SDL2`
    ```
    check the directory structure:
    C:\mingw32\i686-w64-mingw32\include\SDL2\
                                            \SDL.h
    ```
8. Download **libusb-1.0** 7zip file
    - https://sourceforge.net/projects/libusb/files/libusb-1.0/
    - tested: [libusb-1.0.23.7z](https://sourceforge.net/projects/libusb/files/libusb-1.0/libusb-1.0.23/libusb-1.0.23.7z/download)
9. Extract **libusb-1.0** Zip `\MinGW32\dll\libusb-1.0.dll.a` to `c:\mingw32\i686-w64-mingw32\lib\`
10. Extract **libusb-1.0** Zip `\include\libusb-1.0\libusb.h` to `c:\mingw32\i686-w64-mingw32\include\`
11. Extract this project source to any subdirectory below `c:\mingw32\`
12. Enter subdirectory `c:\mingw32\[projectsourcedirectory]\build\mingw32`
13. Run:
    - `1st-cmake.bat`
    - `2nd-make.bat`
14. If sucessfull, compiled `rtl_fm_player.exe` will be on `[projectsourcedirectory]\build\mingw32\src` directory.
    - Copy **SDL2** zip file `\i686-w64-mingw32\bin\SDL2.dll` to `src`
    - Copy **libusb-1.0** 7zip file `\MinGW32\dll\libusb-1.0.dll` to `src`


### Compiling RTL FM Player sources using MinGW64 on Windows: (target 64 bit)
`MinGW64 manual installation. You can install to any directory name without spaces in root drive, (eg: C:\MinGW64-RTL, D:\MinGWTemp). In this example we install to C:\MinGW64`

1. Download latest **mingw-w64** toolchain targeting architecture **x86_64**, **win32** threads, **seh** exception
    - https://sourceforge.net/projects/mingw-w64/files/
    - tested: [x86_64-8.1.0-release-win32-seh-rt_v6-rev0.7z](https://sourceforge.net/projects/mingw-w64/files/Toolchains%20targetting%20Win64/Personal%20Builds/mingw-builds/8.1.0/threads-win32/seh/x86_64-8.1.0-release-win32-seh-rt_v6-rev0.7z/download)
2. Extract the **mingw-w64** toolchain 7zip file to root directory, keeping the structure:
    ```
    C:\mingw64\
              \bin
              \etc
              ...
    ```
3. Download **CMake** Windows win64-x64 Zip file (not the installer)
    - https://cmake.org/download/ 
    - tested: [cmake-3.17.1-win64-x64.zip](https://github.com/Kitware/CMake/releases/download/v3.17.1/cmake-3.17.1-win64-x64.zip)
4. Extract **CMake** Zip file inside `C:\MinGW64\CMake` directory, keeping the structure:
    ```
    C:\mingw64\cmake\
              \cmake\bin
              \cmake\doc
              \cmake\man
              \cmake\share
    ```
5. Download **SDL2** Development Libraries for MinGW
    - https://www.libsdl.org/download-2.0.php
    - tested: [SDL2-devel-2.0.12-mingw.tar.gz](https://www.libsdl.org/release/SDL2-devel-2.0.12-mingw.tar.gz)
6. Extract **SDL2** zip file `x86_64-w64-mingw32\lib\libSDL2.dll.a` to `c:\mingw64\x86_64-w64-mingw32\lib\`
7. Extract **SDL2** zip directory `x86_64-w64-mingw32\include\SDL2` to `c:\mingw64\x86_64-w64-mingw32\include\SDL2`
    ```
    check the directory structure:
    C:\mingw64\x86_64-w64-mingw32\include\SDL2\
                                              \SDL.h
    ```
8. Download **libusb-1.0** 7zip file
    - https://sourceforge.net/projects/libusb/files/libusb-1.0/
    - tested: [libusb-1.0.23.7z](https://sourceforge.net/projects/libusb/files/libusb-1.0/libusb-1.0.23/libusb-1.0.23.7z/download)
9. Extract **libusb-1.0** Zip `MinGW64\dll\libusb-1.0.dll.a` to `c:\mingw64\x86_64-w64-mingw32\lib\`
10. Extract **libusb-1.0** Zip `include\libusb-1.0\libusb.h` to `c:\mingw64\x86_64-w64-mingw32\include\`
11. Extract this project source to any subdirectory below `c:\mingw64\`
12. Enter subdirectory `c:\mingw64\[projectsourcedirectory]\build\mingw64`
13. Run:
    - `1st-cmake.bat`
    - `2nd-make.bat`
14. If sucessfull, compiled `rtl_fm_player.exe` will be on `[projectsourcedirectory]\build\mingw64\src` subdirectory.
    - Copy **SDL2** zip file `\x86_64-w64-mingw32\bin\SDL2.dll` to `src`
    - Copy **libusb-1.0** 7zip file `\MinGW64\dll\libusb-1.0.dll` to `src`


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

