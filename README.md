# STM32 RTOS GPIO Control Example

This repository contains an example project demonstrating the use of FreeRTOS with STM32 microcontrollers for multitasking. The program controls three LEDs (red, green, and blue) connected to GPIO pins and uses tasks for LED toggling. It ensures proper synchronization between tasks using critical sections.

---

## Features

- **RTOS Integration:** Utilizes FreeRTOS for task scheduling.
- **Critical Section Management:** Ensures safe access to shared resources using `taskENTER_CRITICAL` and `taskEXIT_CRITICAL`.
- **GPIO Control:** Manages three LEDs connected to GPIO pins (red, green, and blue).
- **Custom Delay Implementation:** Includes a millisecond delay function using the Data Watchpoint and Trace (DWT) unit.
- **Task Management:**
  - Red LED task toggles with a 100ms delay.
  - Green LED task toggles with a 500ms delay.
  - Blue LED indicates shared resource access.

---

## Hardware Requirements

- STM32 microcontroller (tested on STM32F4 series).
- LEDs connected to GPIO pins (red, green, and blue).
- STM32 development environment (STM32CubeIDE or similar).

---

## Software Configuration

1. **Dependencies:**
   - STM32 HAL library.
   - FreeRTOS (included in STM32CubeMX generated code).
   - `dwt_stm32_delay` library for millisecond-level delays.

2. **System Clock:**
   - Configured to use HSI at default settings.
   - System Clock frequency: 16 MHz.

3. **Pin Assignments:**
   - Red LED: `GPIOB, merah_Pin`
   - Green LED: `GPIOB, hijau_Pin`
   - Blue LED: `GPIOB, biru_Pin`

---

## File Structure

```
├── Core
│   ├── Inc
│   │   ├── main.h           # Header file for main.c
│   │   ├── cmsis_os.h       # RTOS wrapper header
│   ├── Src
│       ├── main.c           # Main program body
│       ├── freertos.c       # FreeRTOS-related code
│       ├── dwt_stm32_delay.c # DWT delay implementation
```

---

## How It Works

1. **Main Function:**
   - Initializes the HAL, system clock, and GPIO pins.
   - Configures and starts FreeRTOS scheduler.

2. **Tasks:**
   - `defaultTask`: Placeholder task (does nothing significant).
   - `redtask`: Toggles the red LED every 100ms while accessing shared resources.
   - `greentask`: Toggles the green LED every 500ms while accessing shared resources.

3. **Critical Section:**
   - Shared access to the blue LED is synchronized using `taskENTER_CRITICAL` and `taskEXIT_CRITICAL`.

4. **Custom Millisecond Delay:**
   - Uses the DWT unit to achieve precise millisecond delays.

---

## Usage

1. Clone the repository and open it in STM32CubeIDE.
2. Build and flash the project onto your STM32 microcontroller.
3. Observe the LED behavior:
   - Red LED blinks faster (100ms intervals).
   - Green LED blinks slower (500ms intervals).
   - Blue LED lights up briefly when a task accesses shared resources.

---

## Customization

- Modify the task priorities in `main.c` to adjust the behavior.
- Adjust delay timings in `StartTask02` and `StartTask03` for different blink patterns.
- Add additional tasks as needed for other peripherals.
