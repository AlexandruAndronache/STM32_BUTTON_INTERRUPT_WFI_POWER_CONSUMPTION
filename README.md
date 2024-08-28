# STM32_BUTTON_INTERRUPT_WFI_POWER_CONSUMPTION
 Low Power mode for STM32F44xx

**Overview**

This repository contains a demonstration of the sleep mode functionality on an STM32F44xx microcontroller. The project showcases how to put the microcontroller into a low-power sleep mode and wake it up using an external button press. Upon waking, the microcontroller sends a message via UART to a connected terminal. The minor but very useful instructions reduced the power consumption from 25 mA to 6.4 mA. This was possible by using: 
SleepOnExit feature, 
__WFI (Wait for Interrupt - The processor sleeps between Interrupts), 
  GPIO_Analog_Config() which sets the unused pins into Analog mode, 
 __HAL_RCC_USART2_CLK_SLEEP_DISABLE()  __HAL_RCC_GPIOA_CLK_SLEEP_DISABLE();

**Features**

Low-Power Sleep Mode: The microcontroller enters a low-power sleep mode to conserve energy.
External Interrupt Wake-Up: The microcontroller wakes up from sleep mode when an external button is pressed.
UART Communication: Upon waking, a message is transmitted via UART to notify that the button was pressed.

**Project Structure**

├── Core
│   ├── Inc
│   │   └── main.h             # Main header file
│   └── Src
│       └── main.c             # Main source file
├── Drivers
│   └── STM32F4xx_HAL_Driver   # HAL driver files
└── README.md                  # This file

**Code Explanation**

 The code initializes the system clock, GPIO, and UART peripherals. The microcontroller is then configured to enter sleep mode using the __WFI() (Wait For Interrupt) instruction within the infinite loop.
 When the button is pressed, an external interrupt triggers the microcontroller to wake up from sleep mode. The HAL_GPIO_EXTI_Callback function handles this interrupt, setting a flag that causes the main loop to send a "Button pressed!" message via UART.

**Key Functions**

 HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin): This function is called when the external interrupt occurs (i.e., button press). It sets a flag to indicate the button was pressed.
 __WFI(): The instruction that puts the microcontroller into sleep mode.
 
**Power Consumption Optimization**

To further reduce power consumption, unused GPIO pins are configured in analog mode by the GPIO_Analog_Config() function. This minimizes leakage currents and helps achieve lower power consumption in sleep mode.
