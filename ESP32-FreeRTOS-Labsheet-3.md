# การทดลอง ESP32 FreeRTOS 
##  ฟังก์ชัน xTaskCreatePinnedToCore()

1. แก่ไข Code จากโปรแกรมที่แล้ว โดยการเพิ่ม task เข้าไปอีก 1 task (ดู comment ใน code)



```c
#include <stdio.h>
#include <stdbool.h>
#include <unistd.h>

#include "freertos/FreeRTOS.h"
#include "freertos/task.h"

TaskHandle_t MyFirstTaskHandle = NULL;
// 1. เพิ่ม MySeconeTaskHandle
TaskHandle_t MySeconeTaskHandle = NULL;

void My_First_Task(void * arg)
{
	uint16_t i = 0;
	while(1)
	{
		printf("Hello My First Task %d\n",i);
		vTaskDelay(1000/portTICK_PERIOD_MS);
		i++;
	}
}

// 2. เพิ่ม task function
void My_Second_Task(void * arg)
{
	uint16_t i = 0;
	while(1)
	{
		printf("Hello My Second Task %d\n",i);
		vTaskDelay(1000/portTICK_PERIOD_MS);
		i++;
	}
}


void app_main(void)
{
	xTaskCreate(My_First_Task, "Fitst_Task", 4096, NULL, 10, &MyFirstTaskHandle);
	// 3. สร้างและเรียกใช้ task
	xTaskCreate(My_Second_Task, "Second_Task", 4096, NULL, 10, &MySeconeTaskHandle);
}
```

2. รันและบันทึกผลจากโปรแกรมข้างบน
![ภาพ](https://github.com/user-attachments/assets/b2889a9e-be70-4b16-814c-677335920830)
![ภาพ](https://github.com/user-attachments/assets/8808180c-0751-4660-a2fa-29a59620e235)

3.  แก้ไข code ในส่วนของการสร้าง task 2 (ตามหมายเหตุหมายเลข 3) เป็นดังนี้

```c
void app_main(void)
{
	xTaskCreate(My_First_Task, "Fitst_Task", 4096, NULL, 10, &MyFirstTaskHandle);
	// สร้างและเรียกใช้ task ด้วยฟังก์ชัน xTaskCreatePinnedToCore
	xTaskCreatePinnedToCore(My_Second_Task, "Second_Task", 4096, NULL, 10, &MySeconeTaskHandle, 1);
}
```

4. รันและบันทึกผลจากโปรแกรมข้างบน ได้ผลเหมือนหรือต่างกันอย่างไร
![ภาพ](https://github.com/user-attachments/assets/97751964-c737-4b4f-a09b-2161733441ee)

ได้ผลเหมือนกัน 

สรุป
การใช้ xTaskCreatePinnedToCore() ช่วยให้ควบคุมการทำงานของ Task บน Core ใด Core หนึ่งได้ ในขณะที่ xTaskCreate() จะปล่อยให้ระบบเลือก Core ที่เหมาะสมที่สุดสำหรับ Task นั้น ๆ โดยอัตโนมัติ
ในการทดลองนี้ ผลลัพธ์ที่แสดงออกมาใน Serial Monitor แทบจะไม่ต่างกัน แต่อาจมีผลต่อประสิทธิภาพการทำงานของโปรแกรมในกรณีที่ระบบมีการจัดการ Task จำนวนมาก
## [>> ต่อไป >>](./ESP32-FreeRTOS-Labsheet-4.md) 
