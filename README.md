# แนวทางการทำงาน ESP32 simple cook book
## 1. ระบุตัวอย่างที่ใช้ ว่าเอามาจากตัวอย่างไหน
-  ### เลือกโปรเจค simple HTTPD server Example จาก show examples แล้วกด create
![image](https://github.com/user-attachments/assets/b3331fc0-e2cc-49d4-be81-9a23e63931c4)
## 2. ระบุว่า จะแก้ไขตรงไหนบ้าง เพื่ออะไร 
- ### 1.ไปที่ idf.py menuconfig ที่ example config ตั้งค่า WiFi SSID/password
![image](https://github.com/user-attachments/assets/129ddfdf-d474-44cc-b5ab-d25c09483d6b)
- ### 2. เพิ่มโค้ด 
```
//1 บรรทัด 25
#include "esp_adc/adc_cali.h"
#include "esp_adc/adc_cali_scheme.h"
#include "esp_adc/adc_oneshot.h"

//2 บรรทัด 51
char analogtxt[128];
int adc_raw;

//3 ตรง /* An HTTP GET handler */

    // อ่านค่าจาก ADC
    adc_oneshot_read(adc1_handle, ADC_CHANNEL_0, &adc_raw);
    // อัพเดท
    sprintf(analogtxt, "<H1> Voltage = %d </H1>", adc_raw);
    // ส่งข้อมูลไปยังผู้ใช้
    httpd_resp_send(req, analogtxt, HTTPD_RESP_USE_STRLEN);
    return ESP_OK;

```

## 3. แสดงขั้นตอนการทำ project
- ### หลังจากแก้ไขแล้วให้กด build จะได้ IP address ให้เอาไปกรอกใน google(ใช้เน็ตเดียวกับที่เขียนในบอร์ด ESP32)
![image](https://github.com/user-attachments/assets/db05fc7d-25df-4ac3-8e83-0162cb9f5fff)
## 4. แสดงผลการทำ project
- ### สามารถปรับค่าได้ที่ volume
![image](https://github.com/user-attachments/assets/6e939ea8-41e3-4584-b504-2f957f4a8fcf)
---
![image](https://github.com/user-attachments/assets/93388447-4a93-45a5-bc2f-f5c765154b57)
---
![image](https://github.com/user-attachments/assets/be3371eb-5927-40ec-9583-34cfa5525a04)

## 5. สรุปผลการทำ project 
โปรเจคนี้เป็นการใช้งาน HTTP Server เพื่อทดสอบการทำงานของ GET และ POST ตามโค้ดที่เขียนบน esp32

