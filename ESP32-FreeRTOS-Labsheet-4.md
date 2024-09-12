# การทดลอง ESP32 FreeRTOS 
##  ฟังก์ชัน vTaskDelete()

1. แก่ไข Code จากโปรแกรมที่แล้ว โดยการเพิ่ม task เข้าไปอีก 1 task

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
			vTaskDelete(MySecondTaskHandle);
			printf("Second Task deleted\n");
		}
	}
}

...
```

จากโปรแกรมด้านบน เมื่อมีการนับจน i == 5 จะทำให้เงื่อนไขในประโยค if เป็นจริง

คำสั่ง `vTaskDelete(MySecondTaskHandle);` จะลบ `MySecondTaskHandle` ออกจาก list ของ task ที่จะทำงาน


4. รันและบันทึกผลจากโปรแกรมข้างบน วิเคราะห์ผลที่ได้ว่าเป็นอย่างไร
ผลลัพธ์ : แสดงผล ดังนี้
Hello My First Task 1
Hello My Second Task 1
Hello My First Task 2
Hello My Second Task 2
Hello My First Task 3
Hello My Second Task 3
Hello My First Task 4
Hello My Second Task 4
Second Task deleted
จากนั้นแสดงผลแค่ค่า
Hello My First Task +1 ไปเรื่อยๆ

![image](https://github.com/user-attachments/assets/2246d08b-2ed1-46b1-a5c9-18a58c3692ef)


![image](https://github.com/user-attachments/assets/a7315a1f-c025-4d42-9d64-7b7d83c24213)



## [>> ต่อไป >>](./ESP32-FreeRTOS-Labsheet-5.md) 
