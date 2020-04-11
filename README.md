RTL SDR FM Player
===================
Turns your Realtek RTL2832 based DVB dongle into a stereo FM radio receiver.
TimeShift function can go back some minutes in time to listen it again.
Recording function to write audio file.
Runs on Windows console only.

Description
-----------
RTL SDR FM Player is a small tool to listen FM stereo radio by using a DVB-T dongle.
Outputs stereo audio directly to any Windows sond card.

The DVB-T dongle has to be based on the Realtek RTL2832U.
See [http://sdr.osmocom.org/trac/wiki/rtl-sdr](http://sdr.osmocom.org/trac/wiki/rtl-sdr) for more RTL SDR details.

Usage
-----

    Double click rtl_fm_player.exe to open console.
    Use keyboard to control frequency, timeshift, mute and recording.

    You can also open Command Prompt and type parameters manually:
    C:\>rtl_fm_player.exe -h

Common parameters
-------

    Show all available parameters
    C:\>rtl_fm_player.exe -h

    Start and tune to frequency in Hz 
    (97.7Mhz)
    C:\>rtl_fm_player.exe -f 97700000

    Tune to frequency and record audio to FileName.mp3
    (Keyboard controls disabled)
    C:\>rtl_fm_player.exe -f 97700000 FileName.mp3


Performance
--------------
On modern PCs (x86, x64) mono and stereo decoding should be possible easily.

Limitations
--------------
Only runs on Windows because it uses "LibZPlay" for sound output.


Building
-------
Install MinGW on default location (\MinGW) with packages "mingw32-base" and "mingw32-pthreads-w32".

Install CMake on \MinGW\CMake

Download [http://sourceforge.net/projects/libzplay/files/2.02/libzplay-2.02-sdk.7z/download]libZPlay-2.02-SDK and extract (7zip file)\libzplay-2.02-sdk\C++\libzplay.a to \MinGW\lib
         (7zip file)\libzplay-2.02-sdk\libzplay.dll will be requered when runing rtl_fm_streamer.exe

Download this tweaked libzplay.h and copy to \MinGW\include

Download [https://sourceforge.net/projects/libusb/files/libusb-1.0/libusb-1.0.23/libusb-1.0.23.7z/download]libusb-1.0.23.7z, extract (7zip file)\MinGW32\dll\libusb-1.0.dll.a to \MinGW\lib and extract (7zip file)\include\libusb-1.0\libusb.h to \MinGW\include
         (7zip file)\MinGW32\dll\libusb-1.0.dll will be requered when runing rtl_fm_streamer.exe


Credits
-------
This project is based on RTL SDR FM Streamer by Albrecht Lohoefener


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

