# HP141T LCD Upgrade

![Example Image](/IMG_3088.jpg)

This firmware is designed to run on an STM32F746G Discovery board to enable it to complement or replace the CRT of an HP141T spectrum analyzer.

A demo video with hardware connections and an overview of this codebase can be found on VK2SEB's YouTube channel here: <http://youtube.com/c/vk2seb>.  This build has been modified by G8GKQ to use the libraries availble in late 2019, and to add some additional features.

New features so far:

1.  The ability to deselect Normalisation mode.

## Prerequisites

This code was proved on Ubuntu Linux LTS 1804.03 "Minimal Installation" running in a VM.  More work may be required to get it to compile on other distros.

The packages required ("sudo apt-get install" each one) are:

     git (to clone the application software)
     gcc-arm-none-eabi (to compile the application software)
     make (to configure the compile)
     openocd (to enable the transfer from the PC to the STM32)
     gdb-multiarch (to control the transfer from the PC to the STM32)

Then download the zip of the STM32 cube F7 software suite (from https://www.st.com/en/embedded-software/stm32cubef7.html) and the zip of the STemWin library (from https://www.st.com/en/embedded-software/stemwin.html) to your home directory.  You can then move them to /opt and unzip them as root:

     sudo -i
     cp /home/<username>/en.* /opt/
     cd /opt
     unzip en.STM32Cube_FW_F7_V1.15.0.zip
     unzip en.stemwin.zip
     exit

You will need to modify the code above and also the "STM_LIBS" and/or the "STemWin_LIBS" in the makefile if you use different versions.

Then clone the code: 

     git clone https://github.com/davecrump/stm32_hp141_lcd

## Building the code

     cd stm32_hp141_lcd
     make

Will generate `out.elf` (this can be modified by changing `EXECUTABLE` in the makefile)

## Flashing / debugging

In one terminal:

     make debug_server

This will start the `openocd` server enabling gdb to communicate with the STM32F7 board.

In another terminal:

     make debug_gdb

This will load the `out.elf` you compiled, flash it to the board and break at `main`. Press enter, type `c` and hit enter to continue execution. Alternatively you can just disconnect the board and reconnect it.

