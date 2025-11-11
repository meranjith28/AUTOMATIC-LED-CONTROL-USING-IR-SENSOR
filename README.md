##  AIM
To design and implement a system using the **STM32 microcontroller** where an LED automatically turns ON or OFF based on the input from an **IR sensor**.

---

##  Components Required
- STM32 Nucleo or Discovery Board (e.g., **Nucleo-G071RB**)
- IR Sensor Module
- LED (5mm Green or any color)
- Jumper wires
- Breadboard

---

##  Theory
An **IR sensor** detects the presence of an object by emitting and receiving infrared light.

### IR Sensor Behavior
- When an **object is detected**, the IR sensor output goes **LOW (0V)**.
- When **no object is detected**, the output stays **HIGH (3.3V)**.

### Microcontroller Response
- If **IR output = LOW** → **LED ON**
- If **IR output = HIGH** → **LED OFF**
### **Procedure**

1. Open **STM32CubeIDE**.
   ![WhatsApp Image 2025-11-08 at 09 16 44_ff146180](https://github.com/user-attachments/assets/55544408-9fdd-4ab1-abe4-77323d8fd3a5)

2. Click **File → New STM32 Project**.
   ![WhatsApp Image 2025-11-08 at 09 17 26_a59e2d43](https://github.com/user-attachments/assets/cad527c5-aa6a-49c2-9e1d-6745df26ba8d)

![WhatsApp Image 2025-11-08 at 09 22 57_4cf419bf](https://github.com/user-attachments/assets/431f4cb6-9a74-466e-835c-cd98d02f4dcb)


3. Select the **target microcontroller** or board and click **Next**.
  
![WhatsApp Image 2025-11-08 at 20 23 18_3a962f49](https://github.com/user-attachments/assets/9b36ede0-60e5-46d8-b0f6-eab188bf4042)


4. Name the project.

![WhatsApp Image 2025-11-08 at 20 24 25_34610cb9](https://github.com/user-attachments/assets/296eb2e4-3480-47c2-aa7c-5f667e2e6157)

	
6. The corresponding `.ioc` file will be generated automatically.
  <img width="1919" height="1116" alt="image" src="https://github.com/user-attachments/assets/aa4a831a-a80c-48cb-8956-e09c8fe6de69" />

7. Configure the pins as **GPIO (Input/Output)**, **USART**, etc. as needed.
   ![WhatsApp Image 2025-11-08 at 20 31 07_a8c11ae9](https://github.com/user-attachments/assets/5a2fb5cd-6465-4d87-bb9d-2fa34f4c95e9)

![WhatsApp Image 2025-11-08 at 20 32 02_5ff93ab7](https://github.com/user-attachments/assets/916ce282-01cc-4b36-b077-f736f1057e4a)

8. Save the configuration (`Ctrl + S`) – the base C program will be generated automatically.
   <img width="1916" height="1119" alt="image" src="https://github.com/user-attachments/assets/03517739-0730-4e68-9141-e2bad357ad98" />

9. Edit the generated main program as required.
   <img width="1919" height="1116" alt="image" src="https://github.com/user-attachments/assets/df9460ad-23ea-43b0-9131-03655d8fed9c" />
<img width="1917" height="1142" alt="image" src="https://github.com/user-attachments/assets/0d9a90b2-0324-452e-aecf-a5bbdd3aa80d" />

10. Click **Project → Build All**.
   <img width="1872" height="1055" alt="image" src="https://github.com/user-attachments/assets/caf2fbc6-e8c0-42f5-9589-71c2344d73b6" />

11. Link the **HEX file** using the post-build process.
    <img width="1053" height="465" alt="image" src="https://github.com/user-attachments/assets/478187a0-0ee6-4c50-9cac-c3b5ee18521b" />

12. Click **Debug** and connect the **STM Nucleo Board**.
    <img width="1080" height="608" alt="image" src="https://github.com/user-attachments/assets/f72fff44-6073-4ae4-aa78-0da455df9af1" />

13. Click **Run** to execute the program.
    
---

### 💻 **Program**


```c
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
        GPIO_PinState ir = HAL_GPIO_ReadPin(GPIOA, GPIO_PIN_10); // IR OUT at PA10 (D2)

	      if (ir == GPIO_PIN_RESET)  // IR sensor HIGH = object detected
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_SET); // Turn ON LED
	      }
	      else
	      {
	          HAL_GPIO_WritePin(GPIOB, GPIO_PIN_3, GPIO_PIN_RESET); // Turn OFF LED
	      }

	      HAL_Delay(100);
    }
}
```
---
### OUTPUT
CASE 1: LED ON 

CASE 2: LED OFF

---
### RESULT

The experiment on IR Sensor-Based Automatic LED Control using STM32 was successfully carried out. The STM32 microcontroller accurately read the IR sensor output and controlled the LED based on object detection. When an object was detected, the LED glowed (ON) and when no object was present, the LED remained OFF. Thus, the objective of the experiment was achieved.




