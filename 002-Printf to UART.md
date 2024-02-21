# Printf to UART
Printf to UART is as straightforward as it sounds. It gives us to capability to
use printf within STM, to print to the serial monitor. 

>[!WARNING]
> Additional steps, not outlined here, need to be taken to print floating point
> numbers.

## Main.c
Two snippets need to be included in main.c.

```c
/* USER CODE BEGIN Includes */
#include <stdio.h>
/* USER CODE END Includes */
```

```c
/* USER CODE BEGIN PFP */
#ifdef __GNUC__
#define PUTCHAR_PROTOTYPE int __io_putchar(int ch)
#else
#define PUTCHAR_PROTOTYPE int fputc(int ch, FILE *f)
#endif

PUTCHAR_PROTOTYPE
{
  HAL_UART_Transmit(&huart2, (uint8_t *)&ch, 1, HAL_MAX_DELAY);
  return ch;
}
/* USER CODE END PFP */
```

## IOC
The pins that are connected to the ST-Link RX and TX have to be used. In this
case the options were LPUART1 and UART2 (not shown in the image). In the example
I chose for UART2. 

![Schematic](img\002-Schematic.png)

### Mode and configuration
![Mode](img\002-Mode.png)

### Parameter Settings
![Parameters](img\002-Parameters.png)

The baudrate can be adjusted to preference. The rest may be left at default.