```
Name : E. Varsha Sharon
Register Number: 212222100058
```
# EXPERIMENT-06-INTERRUPT-GENERATION-USING-PUSHBUTTON-AND-SIMULATING-THE-OUTPUT

### Aim:
To Interface a push button and generate an interrupt , simulate it using an led and simuate it on  proteus 

### Components required:
STM32 CUBE IDE, Proteus 8 simulator .

### Theory:

ARM v7 Core supports multiple great features for handling exceptions and interrupts. Which includes the Nested Vectored Interrupt Controller (NVIC).

Micro-Coded Architecture So that interrupt stacking, entry, and exit are done automatically in hardware. Which offloads this work overhead from the CPU
### Processor Mode
The processor mode can change when exceptions occur. And it can be in one of the following modes:
Thread Mode: Which is entered on reset.
Handler Mode: Which is entered on all other exceptions.
![image](https://github.com/vasanthkumarch/EXPERIMENT-06-INTERRUPT-GENERATION-USING-PUSHBUTTON-AND-SIMULATING-THE-OUTPUT-/assets/36288975/4f52f2d6-4cdb-4315-b2b2-b55dc1639c43)
The STM32 ARM microcontroller interrupts are generated in the following manner:

The system runs the ISR and then goes back to the main program. The NVIC and EXTI are configured. The Interrupt Service Routine (ISR) also known as the interrupt service routine handler is defined to enable the external interrupts.

Let us learn about the important features which are needed to configure external interrupts in STM32 microcontrollers

Interrupt Lines (EXTI0-EXTI15)
The STM32 ARM microcontroller features 23 event sources which are divided into two sections. The first section corresponds t external pins on each port which are P0-P15. The second section corresponds to RTC, ethernet, USB interrupts. Therefore, in the first section, we have 16 lines corresponding to line0 till line15. All of these map to a pin number.
The diagram below shows how the GPIO pins are connected to the 16 interrupt lines:

![image](https://github.com/vasanthkumarch/EXPERIMENT-06-INTERRUPT-GENERATION-USING-PUSHBUTTON-AND-SIMULATING-THE-OUTPUT-/assets/36288975/3e1ededb-144c-4103-a64e-9132b7e06e1b)

One important thing to note here is that same number pins are connected to line with the same number. All of these then join to form a single line. Additionally, we can not use two pins one one line at the same time. For example out of PA1, PB1, PC1, PD1, PE1, PF1 and PG1 you can only use a single pin out of all these. This is because they are all connected to the same line EXTI1. However you can use PA1 and PA2 at the same time as they are connected with different lines.

Now each of these lines EXTI0-EXTI15 can be used to trigger an interrupt on different modes of the signal : rising edge, falling edge or rising_falling edge.
## Procedure:
 1. click on STM 32 CUBE IDE, the following screen will appear 
 ![image](https://user-images.githubusercontent.com/36288975/226189166-ac10578c-c059-40e7-8b80-9f84f64bf088.png)

 2. click on FILE, click on new stm 32 project 
 ![image](https://user-images.githubusercontent.com/36288975/226189215-2d13ebfb-507f-44fc-b772-02232e97c0e3.png)
![image](https://user-images.githubusercontent.com/36288975/226189230-bf2d90dd-9695-4aaf-b2a6-6d66454e81fc.png)
3. select the target to be programmed  as shown below and click on next 

![image](https://user-images.githubusercontent.com/36288975/226189280-ed5dcf1d-dd8d-43ae-815d-491085f4863b.png)

4.select the program name 
![image](https://user-images.githubusercontent.com/36288975/226189316-09832a30-4d1a-4d4f-b8ad-2dc28f137711.png)


5. corresponding ioc file will be generated automatically 
![image](https://user-images.githubusercontent.com/36288975/226189378-3abbdee2-0df6-470f-a3cd-79c74e3d3ad8.png)

6.select the appropriate pins as gipo, in or out, USART or required options and configure 
![image](https://user-images.githubusercontent.com/36288975/226189403-f7179f1a-3eae-4637-826b-ab4ec35ba1e1.png)
![image](https://user-images.githubusercontent.com/36288975/226189425-2b2414ce-49b3-4b61-a260-c658cb2e4152.png)


7.click on cntrl+S , automaticall C program will be generated 
![image](https://user-images.githubusercontent.com/36288975/226189443-8b43451d-0b14-47e4-a20b-cc09c6ad8458.png)
![image](https://user-images.githubusercontent.com/36288975/226189450-85ffa969-2ffb-4788-81e5-72d60fdda0f1.png)
8. edit the program and as per required 
![image](https://user-images.githubusercontent.com/36288975/226189461-a573e62f-a109-4631-a250-a20925758fe0.png)

9. Select EXTI pin configuration and clock configuration 
![image](https://user-images.githubusercontent.com/36288975/226189554-3f7101ac-3f41-48fc-abc7-480bd6218dec.png)
10. once the project is bulild 
![image](https://user-images.githubusercontent.com/36288975/226189577-c61cc1eb-3990-4968-8aa6-aefffc766b70.png)

11. click on debug option 
![image](https://user-images.githubusercontent.com/36288975/226189625-37daa9a3-62e9-42b5-a5ce-2ac63345905b.png)


12.  Creating Proteus project and running the simulation
We are now at the last part of step by step guide on how to simulate STM32 project in Proteus.

13. Create a new Proteus project and place STM32F40xx i.e. the same MCU for which the project was created in STM32Cube IDE. 
14. After creation of the circuit as per requirement as shown below 

![image](https://user-images.githubusercontent.com/36288975/233856847-32bea88a-565f-4e01-9c7e-4f7ed546ddf6.png)

14. Double click on the the MCU part to open settings. Next to the Program File option, give full path to the Hex file generated using STM32Cube IDE. Then set the external crystal frequency to 8M (i.e. 8 MHz). Click OK to save the changes.
https://engineeringxpert.com/wp-content/uploads/2022/04/26.png

15. click on debug and simulate using simulation as shown below 

![image](https://user-images.githubusercontent.com/36288975/233856904-99eb708a-c907-4595-9025-c9dbd89b8879.png)


  

## STM 32 CUBE PROGRAM :
```
#include "main.h"

void SystemClock_Config(void);
static void MX_GPIO_Init(void);

int main(void)
{
  HAL_Init();
  SystemClock_Config();
  MX_GPIO_Init();
  while (1)
  {
    
  }

}
void HAL_GPIO_EXTI_Callback(uint16_t GPIO_Pin)
{
	if((GPIO_Pin == GPIO_PIN_9))
	{
		HAL_GPIO_TogglePin(GPIOA,GPIO_PIN_11);
	}
}


void SystemClock_Config(void)
{
  RCC_OscInitTypeDef RCC_OscInitStruct = {0};
  RCC_ClkInitTypeDef RCC_ClkInitStruct = {0};

 
  __HAL_RCC_PWR_CLK_ENABLE();
  __HAL_PWR_VOLTAGESCALING_CONFIG(PWR_REGULATOR_VOLTAGE_SCALE2);
  
  RCC_OscInitStruct.OscillatorType = RCC_OSCILLATORTYPE_HSE;
  RCC_OscInitStruct.HSEState = RCC_HSE_ON;
  RCC_OscInitStruct.PLL.PLLState = RCC_PLL_ON;
  RCC_OscInitStruct.PLL.PLLSource = RCC_PLLSOURCE_HSE;
  RCC_OscInitStruct.PLL.PLLM = 25;
  RCC_OscInitStruct.PLL.PLLN = 168;
  RCC_OscInitStruct.PLL.PLLP = RCC_PLLP_DIV2;
  RCC_OscInitStruct.PLL.PLLQ = 4;
  if (HAL_RCC_OscConfig(&RCC_OscInitStruct) != HAL_OK)
  {
    Error_Handler();
  }
  
 
  RCC_ClkInitStruct.ClockType = RCC_CLOCKTYPE_HCLK|RCC_CLOCKTYPE_SYSCLK
                              |RCC_CLOCKTYPE_PCLK1|RCC_CLOCKTYPE_PCLK2;
  RCC_ClkInitStruct.SYSCLKSource = RCC_SYSCLKSOURCE_PLLCLK;
  RCC_ClkInitStruct.AHBCLKDivider = RCC_SYSCLK_DIV1;
  RCC_ClkInitStruct.APB1CLKDivider = RCC_HCLK_DIV2;
  RCC_ClkInitStruct.APB2CLKDivider = RCC_HCLK_DIV1;

  if (HAL_RCC_ClockConfig(&RCC_ClkInitStruct, FLASH_LATENCY_2) != HAL_OK)
  {
    Error_Handler();
  }
}


static void MX_GPIO_Init(void)
{
  GPIO_InitTypeDef GPIO_InitStruct = {0};

  
  __HAL_RCC_GPIOH_CLK_ENABLE();
  __HAL_RCC_GPIOA_CLK_ENABLE();

 
  HAL_GPIO_WritePin(GPIOA, GPIO_PIN_11, GPIO_PIN_RESET);


  GPIO_InitStruct.Pin = GPIO_PIN_9;
  GPIO_InitStruct.Mode = GPIO_MODE_IT_RISING;
  GPIO_InitStruct.Pull = GPIO_PULLUP;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

  
  GPIO_InitStruct.Pin = GPIO_PIN_11;
  GPIO_InitStruct.Mode = GPIO_MODE_OUTPUT_PP;
  GPIO_InitStruct.Pull = GPIO_NOPULL;
  GPIO_InitStruct.Speed = GPIO_SPEED_FREQ_LOW;
  HAL_GPIO_Init(GPIOA, &GPIO_InitStruct);

  
  HAL_NVIC_SetPriority(EXTI9_5_IRQn, 0, 0);
  HAL_NVIC_EnableIRQ(EXTI9_5_IRQn);

}


void Error_Handler(void)
{
  
  __disable_irq();
  while (1)
  {
  }
 
}

#ifdef  USE_FULL_ASSERT

void assert_failed(uint8_t *file, uint32_t line)
{

}
#endif
```


## Output screen shots of proteus  :
 ### LED OFF
![off](https://github.com/varshasharon/EXPERIMENT-06-INTERRUPT-GENERATION-USING-PUSHBUTTON-AND-SIMULATING-THE-OUTPUT-/assets/98278161/9b47e528-1fb9-4995-8e05-18ec5def670e)

### LED ON

 ![on](https://github.com/varshasharon/EXPERIMENT-06-INTERRUPT-GENERATION-USING-PUSHBUTTON-AND-SIMULATING-THE-OUTPUT-/assets/98278161/06717d73-f54e-4208-b7ec-fe8b3823d7a8)

 ## CIRCUIT DIAGRAM (EXPORT THE GRAPHICS TO PDF AND ADD THE SCREEN SHOT HERE): 
 ![image](https://github.com/varshasharon/EXPERIMENT-06-INTERRUPT-GENERATION-USING-PUSHBUTTON-AND-SIMULATING-THE-OUTPUT-/assets/98278161/8093a6e9-ef26-43f9-bc8f-b398c29d8337)

 
## Result :
Interfacing a push button and interrupt genrateion is simulated using proteus 
