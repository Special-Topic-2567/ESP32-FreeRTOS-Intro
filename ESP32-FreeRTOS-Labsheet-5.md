# การทดลอง ESP32 FreeRTOS 
##  ฟังก์ชัน vTaskSuspend() และ vTaskResume()

จากการทดลองที่แล้ว `vTaskDelete(MySecondTaskHandle);` จะลบ `MySecondTaskHandle` ออกจาก task  list และไม่สามารถเรียกกลับมาได้ใหม่ เรามีวิธีการที่จะหยุดและรันต่อ โดยใช้คำสั่ง `vTaskSuspend()` และ `vTaskResume()`

1. แก่ไข Code จากโปรแกรมที่แล้ว โดยการเพิ่ม task เข้าไปอีก 1 task (ดู comment ใน code)

```c
...

void My_First_Task(void * arg)
{
	uint16_t i = 0;
	while(1)
	{
		printf("Hello My First Task %d\n",i);
		vTaskDelay(1000/portTICK_PERIOD_MS);
		i++;

		if(i == 5)
		{
			vTaskSuspend(MySecondTaskHandle);
			printf("Second Task suspended\n");
		}

		if(i == 10)
		{
			vTaskResume(MySecondTaskHandle);
			printf("Second Task Resumed\n");
		}

		if(i == 15)
		{
			vTaskDelete(MySecondTaskHandle);
			printf("Second Task deleted\n");
		}

		if(i == 20)
		{
			printf("MyFirstTaskHandle will suspend itself\n");
			vTaskSuspend(NULL);
		}
	}
}
...
```
โดยปกติเราจะใส่ชื่อ task handle เป็นอาร์กิวเมนต์สำหรับฟังก์ชัน `vTaskDelete()`, `vTaskSuspend()` และ `vTaskResume()`  แต่การใส่อาร์กิวเมนต์เป็น `NULL` เช่น  `vTaskSuspend(NULL);` จะหมายถึงการกระทำกับ task ผู้ออกคำสั่งเอง 

4. รันและบันทึกผลจากโปรแกรมข้างบน วิเคราะห์ผลที่ได้ว่าเป็นอย่างไร
ผลลัพท์ : เมื่อ i == 5 Task ที่อ้างอิงโดย MySecondTaskHandle จะถูกระงับ (หยุดทำงานชั่วคราว)
เมื่อ i == 10 Task กลับมาทำงานใหม่
เมื่อ i == 15 Task แสดงผล MySecondTaskHandle จะถูกลบ Task นั้นจะไม่สามารถกลับมาทำงานได้อีก
เมื่อ i == 20 Task My_First_Task จะหยุดการทำงาน แสดงผล MyFirstTaskHandle will suspend itself

![image](https://github.com/user-attachments/assets/9ed9e4a3-9d4d-47f9-83fd-9630b6c95434)



![image](https://github.com/user-attachments/assets/3a3c93b9-6e04-4963-ae52-170a4e477fd6)



![image](https://github.com/user-attachments/assets/56f1e8e7-0615-4112-aa2d-56b529e9bc23)



![image](https://github.com/user-attachments/assets/dca61105-e426-423d-95a4-88d45961439f)




## [>> ต่อไป >>](./ESP32-FreeRTOS-Labsheet-6.md) 
