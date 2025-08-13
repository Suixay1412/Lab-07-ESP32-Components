# Lab 7-1: Local Component Demo

## คำอธิบาย
การทดลองนี้แสดงการใช้งาน component ที่มีอยู่ในโฟลเดอร์ `components/Sensors/` ของ project

### สรุปคำสั่งที่ใช้ และผลลัพธ์ที่ได้

```c
จากตอนแรกที่ใช้คำสั่ง idf.py build ไป จะขึ้นเป็นError เพราะระบบ build ยังไม่รู้จัก components เลยเข้าไปแก้ไขที่ไฟล์ CMaakeLists.txt โดยเพิ่ม include($ENV{IDF_PATH}/tools/cmake/project.cmake) เพื่อให้ build รู้จัก components

ผลลัพธ์ทั้งหมดหลังเพิ่ม display

I (6699) SENSOR: 🔧 Sensor initialized from file: /project/components/Sensors/sensor.c, line: 12
I (6699) SENSOR: 📡 Sensor module ready for operation
I (6699) SENSOR: 📊 Reading sensor data from file: /project/components/Sensors/sensor.c, line: 18
I (6699) SENSOR: 🌡️  Temperature: 28.7°C
I (6719) SENSOR: 💧 Humidity: 77.9%
I (6719) SENSOR: ✅ Sensor status check from file: /project/components/Sensors/sensor.c, line: 30
I (6719) SENSOR: 📈 All sensors operating normally
I (6719) LAB7-1: ----------------------------
I (9719) SENSOR: 📊 Reading sensor data from file: /project/components/Sensors/sensor.c, line: 18
I (9719) SENSOR: 🌡️  Temperature: 26.4°C
I (9719) SENSOR: 💧 Humidity: 85.5%
I (9719) SENSOR: ✅ Sensor status check from file: /project/components/Sensors/sensor.c, line: 30
I (9719) SENSOR: 📈 All sensors operating normally
I (9719) LAB7-1: ----------------------------
I (12719) SENSOR: 📊 Reading sensor data from file: /project/components/Sensors/sensor.c, line: 18
I (12719) SENSOR: 🌡️  Temperature: 33.4°C
I (12719) SENSOR: 💧 Humidity: 91.7%
I (12719) SENSOR: ✅ Sensor status check from file: /project/components/Sensors/sensor.c, line: 30
I (12719) SENSOR: 📈 All sensors operating normally
I (12719) LAB7-1: ---------------------------- 
```

# Lab 7-2: Managed Component from GitHub URL Demo

## คำอธิบาย
การทดลองนี้แสดงการใช้งาน managed component จาก GitHub Repository
ใช้ `Sensors` component จาก https://github.com/APPLICATIONS-OF-MICROCONTROLLERS/Lab7_Components

## ผลลัพธ์ที่คาดหวัง
- แสดงข้อความการเริ่มต้น sensor จาก GitHub component
- แสดงข้อมูล temperature และ humidity ทุก 4 วินาที
- แสดงสถานะการทำงานของ sensor
- แสดงแหล่งที่มาของ component (GitHub Repository)

## ความแตกต่างจาก Lab 7-1
- Lab 7-1: ใช้ local component (ในเครื่อง)
- Lab 7-2: ใช้ managed component จาก GitHub URL

## การใช้งาน
1. เข้าไปในโฟลเดอร์ lab7-2_Managed_url_Component
2. รันคำสั่ง `idf.py build` (จะดาวน์โหลด component จาก GitHub อัตโนมัติ)
3. ทดสอบด้วย QEMU

ผลลัพธ์ให้ผลลักษณะเดียวกับ component แบบ local หรือไม่

มีลักษณะเดียวกับ component อันเดิมแค่มีเพิ่มเติมขึ้นมา

### ผลลัพธ์ที่ได้
```c
I (10536) LAB7-2: 📋 Reading #2 from GitHub Component
I (10536) SENSOR: 📊 Reading sensor data from file: ./managed_components/lab7_components/Sensors/sensor.c, line: 18
I (10536) SENSOR: 🌡️  Temperature: 32.8°C
I (10536) SENSOR: 💧 Humidity: 65.2%
I (10536) SENSOR: ✅ Sensor status check from file: ./managed_components/lab7_components/Sensors/sensor.c, line: 30
I (10536) SENSOR: 📈 All sensors operating normally
I (10536) LAB7-2: � Component Source: GitHub Repository
I (10536) LAB7-2: ==========================================
I (14536) LAB7-2: 📋 Reading #3 from GitHub Component
I (14536) SENSOR: 📊 Reading sensor data from file: ./managed_components/lab7_components/Sensors/sensor.c, line: 18
I (14536) SENSOR: 🌡️  Temperature: 29.6°C
I (14536) SENSOR: 💧 Humidity: 63.9%
I (14536) SENSOR: ✅ Sensor status check from file: ./managed_components/lab7_components/Sensors/sensor.c, line: 30
I (14536) SENSOR: 📈 All sensors operating normally
I (14536) LAB7-2: � Component Source: GitHub Repository
I (14536) LAB7-2: ==========================================
```

# Lab 7-3: Custom ESP32 Components (Sensor + Display)

## คำอธิบาย
การทดลองนี้แสดงการสร้าง component ใหม่ด้วยคำสั่ง `idf.py create-component`
สร้าง 2 components:
1. **Sensor Component** - อ่านค่า temperature, humidity และคำนวณ heat index
2. **Display Component** - แสดงผลข้อมูลในรูปแบบตาราง

## โครงสร้างโฟลเดอร์หลังใช้ create-component
lab7-3_esp32_Component/
├── CMakeLists.txt
├── components/
│   ├── sensor/
│   │   ├── CMakeLists.txt
│   │   ├── include/
│   │   │   └── sensor.h
│   │   └── sensor.c
│   └── display/
│       ├── CMakeLists.txt
│       ├── include/
│       │   └── display.h
│       └── display.c
├── main/
│   ├── CMakeLists.txt
│   └── lab7-3.c
├── build/
└── README.md

### ผลลัพธ์ที่ได้
```c
I (25750) LAB7-3: 📋 Reading #4
I (25750) DISPLAY: 🧹 Display cleared
I (25750) DISPLAY: 
I (25750) ENHANCED_SENSOR: 🌡️  Temperature: 35.10°C
I (25750) ENHANCED_SENSOR: 💧 Humidity: 64.20%
I (25750) LAB7-3: 🔥 Heat Index: 67.20
I (25750) DISPLAY: ┌─────────────────────────────────┐
I (25750) DISPLAY: │        SENSOR DATA DISPLAY      │
I (25750) DISPLAY: ├─────────────────────────────────┤
I (25750) DISPLAY: │ 🌡️  Temperature:  35.10°C      │
I (25750) DISPLAY: │ 💧 Humidity:     64.20%       │
I (25750) DISPLAY: │ 🔥 Heat Index:   67.20        │
I (25750) DISPLAY: └─────────────────────────────────┘
I (25750) DISPLAY: ┌─────────────────────────────────┐
I (25750) DISPLAY: │         SYSTEM STATUS           │
I (25750) DISPLAY: ├─────────────────────────────────┤
I (25760) DISPLAY: │ Status: ✅ Comfortable         │
I (25760) DISPLAY: └─────────────────────────────────┘
I (25760) LAB7-3: ==========================================
I (31760) LAB7-3: 📋 Reading #5
I (31760) DISPLAY: 🧹 Display cleared
I (31760) DISPLAY:
I (31760) ENHANCED_SENSOR: 🌡️  Temperature: 34.10°C
I (31760) ENHANCED_SENSOR: 💧 Humidity: 76.60%
I (31760) LAB7-3: 🔥 Heat Index: 72.40
I (31760) DISPLAY: ┌─────────────────────────────────┐
I (31760) DISPLAY: │        SENSOR DATA DISPLAY      │
I (31760) DISPLAY: ├─────────────────────────────────┤
I (31760) DISPLAY: │ 🌡️  Temperature:  34.10°C      │
I (31760) DISPLAY: │ 💧 Humidity:     76.60%       │
I (31760) DISPLAY: │ 🔥 Heat Index:   72.40        │
I (31760) DISPLAY: └─────────────────────────────────┘
I (31760) DISPLAY: ┌─────────────────────────────────┐
I (31760) DISPLAY: │         SYSTEM STATUS           │
I (31760) DISPLAY: ├─────────────────────────────────┤
I (31770) DISPLAY: │ Status: ✅ Comfortable         │
I (31770) DISPLAY: └─────────────────────────────────┘
I (31770) LAB7-3: ==========================================
```
