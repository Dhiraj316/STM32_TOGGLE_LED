# STM_TOGGLE_LED Project

This repository contains a complete LED blinking application developed for the STM32F407VETx microcontroller[cite: 1]. The project demonstrates basic GPIO configuration and hardware abstraction layer (HAL) usage within the STM32CubeIDE ecosystem[cite: 1].

## 🛠Development Environment
* **IDE:** STM32CubeIDE
* **Framework:** STM32 HAL (Hardware Abstraction Layer)
* **Target MCU:** STM32F407VETx

## Hardware & Programmer
* **Board:** STM32F407 Development Board (core logic is fully adaptable for Geehy/APM32 equivalent architectures).
* **Programmer:** ST-LINK V2 or compatible SWD programmer.
* **Wiring:** Connect `SWDIO`, `SWCLK`, `GND`, and `3.3V` securely between the programmer and the target board.

## Quick Start Guide

### 1. Project Creation
1. Launch STM32CubeIDE and navigate to **File > New > STM32 Project**.
2. In the MCU/MPU Selector, choose the **STM32F407VETx**
3. Name the project `LED_BLINKING` and click **Finish**

### 2. IOC Pin Configuration
1. Open the `.ioc` Device Configuration Tool.
2. Locate your onboard LED pin (e.g., `PA5`, `PD12`, or `PE5`).
3. Left-click the pin and select **GPIO_Output**.
4. Go to **System Core > SYS** and set **Debug** to **Serial Wire** (crucial for reprogramming).
5. Save (`Ctrl+S`) and click **Yes** to generate the initialization code[cite: 1].

### 3. Application Code
Open `Core/Src/main.c` and locate the `while (1)` loop inside `main()` Add the following toggle and delay logic:

HAL_GPIO_TogglePin(USER_LED_GPIO_Port, USER_LED_Pin);
HAL_Delay(500);

### 4. Build and Flash
Click the Build (Hammer) icon and verify the .elf binary is generated with zero errors.
Connect your ST-LINK and target board via USB.

Click the Run (Play) icon, leave the ST-LINK debug probe defaults, and click OK.

The onboard LED will begin blinking continuously.

### 5. Flashing via DFU Mode

If you do not have an ST-LINK programmer, you can flash the microcontroller using its built-in DFU (Device Firmware Upgrade) bootloader.
1. Enable .bin or .hex Generation in CubeIDE
Right-click the project in Project Explorer and select Properties.
Navigate to C/C++ Build > Settings > MCU Post build outputs.
Check Convert to Intel Hex file (-O ihex) or Convert to binary file (-O binary).
Click Apply and Close, then rebuild the project to generate the file in your Debug folder

2. Hardware Boot Configuration
Locate the BOOT0 pins or jumpers on your board.
Set BOOT0 to HIGH (connect to 3.3V).
Connect the board to your PC via USB and press the RESET button to enter DFU mode.
