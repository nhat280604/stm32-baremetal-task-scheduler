# STM32 Simple Task Scheduler

A bare-metal implementation of a simple task scheduler on **STM32** microcontrollers.  
This project demonstrates how to build a cooperative, round-robin style scheduler that mimics the behavior of a minimal RTOS (without using FreeRTOS or any external OS).

---

## Features

- Implements a **basic task scheduler** using PendSV and SysTick exceptions.  
- Supports multiple tasks with independent stacks.  
- Provides **task delay** functionality (blocking with tick counter).  
- Simple **LED driver** to visualize task execution.  
- Exception handlers for **HardFault**, **MemManage**, **BusFault**, and **UsageFault**.  

---

## Project Structure
├── final_sh.elf # Compiled firmware
├── final.map # Linker map file
├── led.c / led.h # LED driver functions
├── led_log # Log output for LED module
├── main.c / main.h # Core scheduler & task implementations
├── main_log # Log output for main module
├── Makefile # Build script
├── stm32_ls.ld # Linker script
├── stm32_startup.c # Startup code and vector table
├── syscalls.c # Semihosting support for printf

## How It Works

- **SysTick timer** generates system ticks at a configured frequency.  
- **Tasks** are stored in a `TCB_t` structure containing PSP, state, and handler.  
- **Context switching** is handled by **PendSV_Handler** (saving/restoring registers R4–R11).  
- **Idle task** runs when no other task is ready.  
- Tasks demonstrate different blinking patterns on the on-board LEDs.  

---

## Requirements

- **STM32CubeIDE** or **ARM GCC toolchain** (`arm-none-eabi-gcc`)  
- A supported **STM32 board** (tested on STM32F4 series, but portable to others)  
- OpenOCD / ST-LINK for flashing and debugging  

---

## Demo

Task1: Blinks green LED every 1s

Task2: Blinks orange LED every 500ms

Task3: Blinks blue LED every 250ms

Task4: Blinks red LED every 125ms

Idle task: Runs when no other task is active
