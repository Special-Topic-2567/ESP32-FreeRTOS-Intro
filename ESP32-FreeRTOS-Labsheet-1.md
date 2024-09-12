# การทดลอง ESP32 FreeRTOS 
## เรื่อง การสร้าง Task เบื้องต้น

## ลำดับการทดลอง

### 1. สร้าง project ใหม่ใน ESP-IDF เพื่อทำงานกับ FreeRTOS

1.1 ชื่อ  `FreeRTOS_Task_1`

1.2 ไม่ต้องเลือก Template (ใช้เทมเพลตพื้นฐาน)

1.3 เมื่อสร้างแล้ว ให้แก้ไข Code ดังนี้

1. เพิ่ม include files

2. ลบ code ใน app_main() แล้วเพิ่มcode ตามรูปต่อไปนี้

![Alt text](./Pictures/Labs/FreeRTOS-Lab-Picture-03.PNG)


3. รันโปรแกรมและอธิบายผลที่ได้


![image](https://github.com/user-attachments/assets/138630a7-8ca2-4a60-8170-ed5f85a8ce79)

แสดงผลข้อความ "Hello My First Task (ตัวเลข)" โดยตัวเลขจะนับจำนวนข้อความข้างต้น


## [>> ต่อไป >>](./ESP32-FreeRTOS-Labsheet-2.md) 
