# Piano Robot Motherboard

STM32F446RET6-based motherboard for a piano-playing robot. This board serves as the central controller, interfacing with three daughter boards via board-to-board connectors:

- **Actuator control board** — drives the key-pressing mechanisms
- **Motor control board** — controls motors for positioning
- **Power board** — supplies regulated power to the system

## Key Design Decisions

### MCU — STM32F446RET6 (LQFP64)
- ARM Cortex-M4 with FPU, 180 MHz, 512 KB Flash, 128 KB SRAM
- Chosen for its timer peripherals (motor PWM), ADC channels, and USB OTG FS

### Power
- 3.3V supplied externally from the power board, or via USB through an AMS1117-3.3 LDO
- SPDT slide switch (CS12ANW03) selects between external and USB power — break-before-make to prevent supply conflicts
- Full decoupling per ST AN4488: 4x 100nF on VDD, 4.7uF bulk, 100nF + 1uF on VDDA, 4.7uF on VCAP1, 100nF on VBAT

### USB (Micro-B)
- USB OTG FS in device-only mode for CDC virtual COM port and DFU flashing
- ESD protection: USBLC6-2SC6 on D+/D-, ESDA7P60-1U1M on VBUS
- No VBUS sensing (PA9 used for motor PWM TIM1_CH2)

### Debug
- SWD 6-pin header: SWDIO, SWCLK, SWO, NRST, VDD_TARGET, GND
- Programmed via Nucleo-F401RE's onboard ST-LINK

### Peripherals
- HSE and LSE crystal oscillators
- HAL encoder interface
- Homing button
- LCD and SD card connectors
- Board-to-board connectors (SFH11-PBPC-D05-ST-BK) for daughter boards
- Status LED

## References
- [STM32F446RE Datasheet (DS10693)](https://www.st.com/resource/en/datasheet/stm32f446re.pdf)
- [AN4488 — Getting started with STM32F4 hardware development](https://www.st.com/resource/en/application_note/an4488.pdf)
- [AN4879 — USB hardware and PCB guidelines using STM32 MCUs](https://www.st.com/resource/en/application_note/an4879.pdf)

## Status
Work in progress — schematic capture in Altium Designer.
