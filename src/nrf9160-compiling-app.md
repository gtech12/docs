# Compiling an Application

## Prerequisites/SDK Setup

If you haven't already, make sure you've set up the SDK:

- [Mac OS](nrf9160-sdk-setup-mac.md)
- [Windows](nrf9160-sdk-setup-windows.md)
- [Linux](nrf9160-sdk-setup-linux.md)

**Side note** One of the engineers at Nordic configured a [Docker Image](https://github.com/coderbyheart/fw-nrfconnect-nrf-docker#using-prebuild-image-from-dockerhub) you can also use to build your code. I'll be adding a section on this when I get a chance to test it!

## Board Defintion Files

Currently the 1.2 and 1.3 branchs of the nRF Connect SDK does not have support for the nRF9160 Feather built in. You'll need to download and copy the appropriate board defintion files from the [downloads page.](nrf9160-downloads.md) If you're using the latest nRF SDK those defintions should be included.

To install, unzip the contents of the board defintions to `ncs/zephyr/boards/arm/` It should create a folder called `circuitdojo_feather_nrf9160`. Congrats your board files are installed! You should be able to use the `circuitdojo_feather_nrf9160ns` target for your Zephyr builds!

Here are the direct downloads:

- [board-defs-v1.3.x](files/board-definitions-ncs-v1.3.x.zip)
- [board-defs-v1.2.x](files/board-definitions-ncs-v1.2.x.zip)

**Note:** if you're using the v1.2.x branch of nRF Connect SDK, make sure you're using the v1.2.x definitions. Same for the v1.3.x definitions.

## Example
As long as you have all the requirements from the guide above, compiling for the nRF9160 Feather should be as simple as running the following:

```
west build -b circuitdojo_feather_nrf9160ns
```

If you would like to "clean" your project before building add the `-p` parameter.

```
west build -b circuitdojo_feather_nrf9160ns -p
```

The output assets are placed in the `build/zephyr` folder. If you're programming from scratch, you'll want the `merged.hex`. If you're using `newtmgr` then you'll want the `app_update.bin`. More info on different programming methods in the programming and debugging section using [newtmgr](nrf9160-programming-and-debugging.md#using-newtmgr) and [an external programmer](nrf9160-programming-and-debugging.md#programming-with-the-nrf5340-pdk).

For subsequent builds you don't need `-b circuitdojo_feather_nrf9160ns` **if you're not using the -p param**.

```
west build
```

`west` uses the last board that was indicated for the re-build.

Here's an example compile output from the [blinky sample](nrf9160-blinky-sample.md):

```
$ west build -b circuitdojo_feather_nrf9160ns
[0/1] Re-running CMake...
Including boilerplate (Zephyr base (cached)): /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/cmake/app/boilerplate.cmake
-- Application: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client
-- Zephyr version: 2.3.99 (/Users/jaredwolff/Git/nrf-connect/ncs/zephyr)
-- Found west: /usr/local/bin/west (found suitable version "0.7.2", minimum required is "0.7.1")
-- Board: circuitdojo_feather_nrf9160ns
-- Found dtc: /usr/local/bin/dtc (found suitable version "1.5.0", minimum required is "1.4.6")
-- Found toolchain: gnuarmemb (/Users/jaredwolff/gcc-arm-none-eabi-9-2019-q4-major)
-- Found BOARD.dts: /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/boards/arm/circuitdojo_feather_nrf9160/circuitdojo_feather_nrf9160ns.dts
circuitdojo_feather_nrf9160ns.dts.pre.tmp:358.32-362.5: Warning (simple_bus_reg): /soc/cryptocell-sw: missing or empty reg/ranges property
circuitdojo_feather_nrf9160ns.dts.pre.tmp:57.42-69.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@40000000/flash-controller@39000: duplicate unit-address (also used in node /soc/peripheral@40000000/kmu@39000)
circuitdojo_feather_nrf9160ns.dts.pre.tmp:306.19-312.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@40000000/clock@5000: duplicate unit-address (also used in node /soc/peripheral@40000000/power@5000)
-- Generated zephyr.dts: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/zephyr/zephyr.dts
-- Generated devicetree_unfixed.h: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/zephyr/include/generated/devicetree_unfixed.h
Parsing /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/Kconfig
Loaded configuration '/Users/jaredwolff/Git/nrf-connect/ncs/zephyr/boards/arm/circuitdojo_feather_nrf9160/circuitdojo_feather_nrf9160ns_defconfig'
Merged configuration '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/prj.conf'
Configuration saved to '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/zephyr/.config'
Kconfig header saved to '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/zephyr/include/generated/autoconf.h'
-- Cache files will be written to: /Users/jaredwolff/Library/Caches/zephyr
Changed board to secure circuitdojo_feather_nrf9160 (NOT NS)

=== child image spm -  begin ===
Including boilerplate (Zephyr base (cached)): /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/cmake/app/boilerplate.cmake
-- Application: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/spm
-- Zephyr version: 2.3.99 (/Users/jaredwolff/Git/nrf-connect/ncs/zephyr)
-- Found west: /usr/local/bin/west (found suitable version "0.7.2", minimum required is "0.7.1")
-- Board: circuitdojo_feather_nrf9160
-- Found dtc: /usr/local/bin/dtc (found suitable version "1.5.0", minimum required is "1.4.6")
-- Found toolchain: gnuarmemb (/Users/jaredwolff/gcc-arm-none-eabi-9-2019-q4-major)
-- Found BOARD.dts: /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/boards/arm/circuitdojo_feather_nrf9160/circuitdojo_feather_nrf9160.dts
circuitdojo_feather_nrf9160.dts.pre.tmp:57.42-69.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@50000000/flash-controller@39000: duplicate unit-address (also used in node /soc/peripheral@50000000/kmu@39000)
circuitdojo_feather_nrf9160.dts.pre.tmp:306.19-312.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@50000000/clock@5000: duplicate unit-address (also used in node /soc/peripheral@50000000/power@5000)
-- Generated zephyr.dts: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/spm/zephyr/zephyr.dts
-- Generated devicetree_unfixed.h: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/spm/zephyr/include/generated/devicetree_unfixed.h
Parsing /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/Kconfig
Loaded configuration '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/spm/zephyr/.config'
No change to configuration in '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/spm/zephyr/.config'
No change to Kconfig header in '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/spm/zephyr/include/generated/autoconf.h'
-- Cache files will be written to: /Users/jaredwolff/Library/Caches/zephyr
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/spm
=== child image spm -  end ===

Changed board to secure circuitdojo_feather_nrf9160 (NOT NS)

=== child image mcuboot -  begin ===
Including boilerplate (Zephyr base (cached)): /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/cmake/app/boilerplate.cmake
-- Application: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr
-- Zephyr version: 2.3.99 (/Users/jaredwolff/Git/nrf-connect/ncs/zephyr)
-- Found west: /usr/local/bin/west (found suitable version "0.7.2", minimum required is "0.7.1")
-- Board: circuitdojo_feather_nrf9160
-- Found dtc: /usr/local/bin/dtc (found suitable version "1.5.0", minimum required is "1.4.6")
-- Found toolchain: gnuarmemb (/Users/jaredwolff/gcc-arm-none-eabi-9-2019-q4-major)
-- Found BOARD.dts: /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/boards/arm/circuitdojo_feather_nrf9160/circuitdojo_feather_nrf9160.dts
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
circuitdojo_feather_nrf9160.dts.pre.tmp:57.42-69.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@50000000/flash-controller@39000: duplicate unit-address (also used in node /soc/peripheral@50000000/kmu@39000)
circuitdojo_feather_nrf9160.dts.pre.tmp:306.19-312.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@50000000/clock@5000: duplicate unit-address (also used in node /soc/peripheral@50000000/power@5000)
-- Generated zephyr.dts: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/mcuboot/zephyr/zephyr.dts
-- Generated devicetree_unfixed.h: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/mcuboot/zephyr/include/generated/devicetree_unfixed.h
Parsing /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/Kconfig
Loaded configuration '/Users/jaredwolff/Git/nrf-connect/ncs/zephyr/boards/arm/circuitdojo_feather_nrf9160/circuitdojo_feather_nrf9160_defconfig'
Merged configuration '/Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/prj.conf'
Merged configuration '/Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/boards/circuitdojo_feather_nrf9160.conf'
Configuration saved to '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/mcuboot/zephyr/.config'
Kconfig header saved to '/Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/mcuboot/zephyr/include/generated/autoconf.h'
-- Cache files will be written to: /Users/jaredwolff/Library/Caches/zephyr
MCUBoot bootloader key file: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/root-rsa-2048.pem
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build/mcuboot
=== child image mcuboot -  end ===

CMake Warning at /Users/jaredwolff/Git/nrf-connect/ncs/nrf/cmake/mcuboot.cmake:115 (message):


        ---------------------------------------------------------
        --- WARNING: Using default MCUBoot key, it should not ---
        --- be used for production.                           ---
        ---------------------------------------------------------


Call Stack (most recent call first):
  /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/zephyr/CMakeLists.txt:1 (include)


CMake Warning at /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/CMakeLists.txt:1379 (message):
  __ASSERT() statements are globally ENABLED


-- Configuring done
-- Generating done
-- Build files have been written to: /Users/jaredwolff/Git/nrf-connect/ncs/nrf/samples/nrf9160/at_client/build
[0/180] Performing build step for 'spm_subimage'
[151/155] Linking C executable zephyr/zephyr_prebuilt.elf
Memory region         Used Size  Region Size  %age Used
           FLASH:       32256 B        48 KB     65.62%
            SRAM:        5488 B        64 KB      8.37%
        IDT_LIST:          40 B         2 KB      1.95%
[155/155] Linking C executable zephyr/zephyr.elf
[2/176] Performing build step for 'mcuboot_subimage'
[248/253] Linking C executable zephyr/zephyr_prebuilt.elf
Memory region         Used Size  Region Size  %age Used
           FLASH:       42500 B        48 KB     86.47%
            SRAM:       26800 B        64 KB     40.89%
        IDT_LIST:          72 B         2 KB      3.52%
[253/253] Linking C executable zephyr/zephyr.elf
[163/176] Linking C executable zephyr/zephyr_prebuilt.elf
Memory region         Used Size  Region Size  %age Used
           FLASH:       76868 B     441856 B     17.40%
            SRAM:       36928 B       128 KB     28.17%
        IDT_LIST:         120 B         2 KB      5.86%
[174/174] Generating zephyr/merged.hex
MacBook-Pro:at_client jaredwolff$ newtmgr -c serial image upload build/zephyr/app_update.bin
MacBook-Pro:at_client jaredwolff$ cd ../../..
MacBook-Pro:nrf jaredwolff$ cd ..
MacBook-Pro:ncs jaredwolff$ cd zephyr/samples/basic/blinky
MacBook-Pro:blinky jaredwolff$ code prj.conf
MacBook-Pro:blinky jaredwolff$ west build -b circuitdojo_feather_nrf9160ns
[0/16] Performing build step for 'spm_subimage'
ninja: no work to do.
[1/9] Performing build step for 'mcuboot_subimage'
[0/1] Re-running CMake...
Including boilerplate (Zephyr base (cached)): /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/cmake/app/boilerplate.cmake
-- Application: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr
-- Zephyr version: 2.3.99 (/Users/jaredwolff/Git/nrf-connect/ncs/zephyr)
-- Found west: /usr/local/bin/west (found suitable version "0.7.2", minimum required is "0.7.1")
-- Board: circuitdojo_feather_nrf9160
-- Found dtc: /usr/local/bin/dtc (found suitable version "1.5.0", minimum required is "1.4.6")
-- Found toolchain: gnuarmemb (/Users/jaredwolff/gcc-arm-none-eabi-9-2019-q4-major)
-- Found BOARD.dts: /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/boards/arm/circuitdojo_feather_nrf9160/circuitdojo_feather_nrf9160.dts
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
-- Found devicetree overlay: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/dts.overlay
circuitdojo_feather_nrf9160.dts.pre.tmp:57.42-69.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@50000000/flash-controller@39000: duplicate unit-address (also used in node /soc/peripheral@50000000/kmu@39000)
circuitdojo_feather_nrf9160.dts.pre.tmp:306.19-312.3: Warning (unique_unit_address_if_enabled): /soc/peripheral@50000000/clock@5000: duplicate unit-address (also used in node /soc/peripheral@50000000/power@5000)
-- Generated zephyr.dts: /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/samples/basic/blinky/build/mcuboot/zephyr/zephyr.dts
-- Generated devicetree_unfixed.h: /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/samples/basic/blinky/build/mcuboot/zephyr/include/generated/devicetree_unfixed.h
Parsing /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/Kconfig
Loaded configuration '/Users/jaredwolff/Git/nrf-connect/ncs/zephyr/boards/arm/circuitdojo_feather_nrf9160/circuitdojo_feather_nrf9160_defconfig'
Merged configuration '/Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/prj.conf'
Merged configuration '/Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/boot/zephyr/boards/circuitdojo_feather_nrf9160.conf'
Configuration saved to '/Users/jaredwolff/Git/nrf-connect/ncs/zephyr/samples/basic/blinky/build/mcuboot/zephyr/.config'
Kconfig header saved to '/Users/jaredwolff/Git/nrf-connect/ncs/zephyr/samples/basic/blinky/build/mcuboot/zephyr/include/generated/autoconf.h'
-- Cache files will be written to: /Users/jaredwolff/Library/Caches/zephyr
MCUBoot bootloader key file: /Users/jaredwolff/Git/nrf-connect/ncs/bootloader/mcuboot/root-rsa-2048.pem
-- Configuring done
-- Generating done
-- Build files have been written to: /Users/jaredwolff/Git/nrf-connect/ncs/zephyr/samples/basic/blinky/build/mcuboot
[247/252] Linking C executable zephyr/zephyr_prebuilt.elf
Memory region         Used Size  Region Size  %age Used
           FLASH:       42528 B        48 KB     86.52%
            SRAM:       26800 B        64 KB     40.89%
        IDT_LIST:          72 B         2 KB      3.52%
[252/252] Linking C executable zephyr/zephyr.elf
[7/7] Generating zephyr/merged.hex
```

## Common errors and warnings

1. CMake complains about your MCUBoot key

   ```
   CMake Warning at /Users/jaredwolff/Git/nrf-connect/ncs/nrf/cmake/mcuboot.cmake:115 (message):


           ---------------------------------------------------------
           --- WARNING: Using default MCUBoot key, it should not ---
           --- be used for production.                           ---
           ---------------------------------------------------------
   ```

   The default nRF9160 Feather bootloader uses the default MCUBoot key. If you're working on a secure application, be sure to change this key. More information about this topic is [here.](#)

