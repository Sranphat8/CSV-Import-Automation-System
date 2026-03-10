# CSV Import Automation System 🚀

ระบบอัตโนมัติสำหรับนำเข้าข้อมูลจากไฟล์ CSV เข้าสู่ฐานข้อมูล PostgreSQL โดยใช้ **n8n** และจัดการ Environment ด้วย **Docker Compose**

## 🛠️ Tech Stack
* **n8n**: Workflow automation tool
* **PostgreSQL**: ฐานข้อมูลหลักสำหรับเก็บข้อมูลที่นำเข้า
* **Docker & Docker Compose**: สำหรับจัดการ Container

## 📂 โครงสร้างโปรเจกต์
```text
.
├── data/                  # โฟลเดอร์สำหรับวางไฟล์ CSV/XLSX เพื่อให้ n8n ดึงไปใช้งาน
├── docker-compose.yml     # ไฟล์ตั้งค่า Services (n8n + Postgres)
├── .env.example           # ไฟล์ตัวอย่าง Environment variables
└── .gitignore             # ป้องกันการอัพโหลดไฟล์ความลับขึ้น Git

**🚀 วิธีการใช้งาน (Getting Started)**
**  1. เตรียมไฟล์ Environment**
  ก๊อปปี้ไฟล์ .env.example และเปลี่ยนชื่อเป็น .env จากนั้นกรอกข้อมูลรหัสผ่านตามต้องการ:
  cp .env.example .env

** 2. เริ่มการทำงานของระบบ**
  ใช้ Docker Compose เพื่อดึง Image และรันระบบขึ้นมา:
  docker-compose up -d

**  3. การเข้าใช้งาน**

  n8n: เข้าไปที่ http://localhost:5679
  PostgreSQL: เข้าใช้งานผ่านพอร์ต (หรือตามที่คุณตั้งค่าไว้)

 ** ⚙️ การตั้งค่าที่สำคัญ**
  N8N_ENCRYPTION_KEY: ถูกกำหนดไว้ในไฟล์ .env เพื่อป้องกันข้อมูล Credentials ใน Workflow สูญหายหรือถูกถอดรหัส
  
  Volumes:
  
  ข้อมูลฐานข้อมูลจะถูกเก็บไว้ที่ postgres_csv_import_data
  
  ข้อมูล n8n จะถูกเก็บไว้ที่ n8n_csv_import_data
  
  ไฟล์ CSV ในโฟลเดอร์ ./data จะถูก Map เข้าไปที่ /home/node/.n8n-files ใน Container
  
 ** ⚠️ ข้อควรระวัง**
  ห้ามอัพโหลดไฟล์ .env ขึ้น Git โดยเด็ดขาด เนื่องจากเก็บรหัสผ่านฐานข้อมูลและ Encryption Key ของระบบไว้
  
  หากมีการเปลี่ยนรหัสผ่านใน .env หลังจากเริ่มรันระบบไปแล้ว อย่าลืมสั่ง docker-compose down และ up ใหม่อีกครั้ง
  
