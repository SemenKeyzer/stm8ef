# STM8L151K4 Base Image

This folder contains support for STM8L Medium Density devices like [STM8L151K4](https://www.st.com/resource/en/datasheet/stm8l151r6.pdf).

STM8L151K4 stands for "Medium density" devices with 2K RAM, 1K EEPROM and up to 32K Flash ROM as described in [RM0031](https://www.st.com/resource/en/reference_manual/cd00218714-stm8l050j3-stm8l051f3-stm8l052c6-stm8l052r8-mcus-and-stm8l151l152-stm8l162-stm8al31-stm8al3l-lines-stmicroelectronics.pdf) (or "32 Kbyte die" as described in [UM0470](https://www.st.com/content/ccc/resource/technical/document/user_manual/ca/89/41/4e/72/31/49/f4/CD00173911.pdf/files/CD00173911.pdf/jcr:content/translations/en.CD00173911.pdf)), all of which should work with the STM8L151K4 binary in the Releases section (likely it's also usable for Automotive Grade STM8L Medium Density devices).


"Medium+" or "High Density" devices described in RM0031 (e.g. STM8L052R8) have, besides more peripherals, 4K RAM and require different RAM settings in `target.inc`. If you have e.g. a NUCLEO-8L152R8 you may want to try the following settings:

```
;       STM8L152R8 device and memory layout configuration

        TARGET = STM8L152R8

        RAMEND =        0x0FFF  ; "RAMEND" system (return) stack, growing down
        EEPROMBASE =    0x1000  ; "EESTART" EEPROM start address
        EEPROMEND =     0x17FF  ; "EEEND" 2K EEPROM
        FLASHEND =      0xFFFF  ; 32K Forth + 32K far memory

        FORTHRAM =      0x0030  ; Start of RAM controlled by Forth
        UPPLOC  =       0x0060  ; UPP (user/system area) location for 4K RAM
        CTOPLOC =       0x0080  ; CTOP (user dictionary) location for 4K RAM
        SPPLOC  =       0x0f50  ; SPP (data stack top), TIB start
        RPPLOC  =       RAMEND  ; RPP (return stack top)
```

The default USART for the Forth console is USART1. That can be changed by setting `USE_USART2 = 1` or `USE_USART3 = 1` in `globconf.inc`. Peripheral register addresses are likely the same and constants imported from `\res MCU: STM8L151` should work.  Of course, we'd be happy to hear from you if it works (or help fixing it if it doesn't).

Low Density devices described in RM0031 (e.g. STM8L051), RM0013 (e.g. STM8L101) or RM0312 (STM8TL5xxx) use different peripheral register addresses and have a different memory layout. These require a different binary.

The code in this folder also contains [STM8L-Discovery_board support code](https://github.com/TG9541/stm8ef/tree/master/STM8L-DISCOVERY) by @plumbum but it has to be enabled manually in `globconf.inc`.
