# 🎬 LINE Chatbot + MongoDB Vector Store (AI Movie Assistant)

---

## 🧩 **ภาพรวม (Overview)**

Workflow นี้ทำหน้าที่เป็น **LINE Chatbot อัจฉริยะ** ที่สามารถ:

- 💬 รับข้อความ, รูปภาพ หรือเสียงจากผู้ใช้ทาง LINE  
- 🧠 วิเคราะห์ข้อความด้วย AI (ผ่าน **OpenAI GPT-4o-mini**)  
- 🎞️ ค้นหาข้อมูลภาพยนตร์จาก **MongoDB Vector Store**  
- 🤖 ตอบกลับผู้ใช้บน LINE แบบอัตโนมัติ  
- 🌐 รองรับทั้งภาษาไทยและภาษาอังกฤษ  

---

## ⚙️ **สิ่งที่ผู้ใช้งานต้องตั้งค่า (Configuration Guide)**

### 1. 🔗 **LINE Webhook**

**Node:** `Webhook`  
**พารามิเตอร์:**  
- HTTP Method → `POST`  
- Path → `line-n8n-webhook`

**✅ สิ่งที่ต้องทำ:**
1. คัดลอก Webhook URL: https://<your-n8n-domain>/webhook/line-n8n-webhook
2. ไปที่ [LINE Developers Console → Messaging API](https://developers.line.biz/)  
3. วาง URL นี้ลงในช่อง **Webhook URL**  
4. กด **“Verify”** และ **“Enable Webhook”**

---

### 2. 🔑 **LINE Channel Access Token**

**Node:** `Get image`, `Get audio`, `reply message`

**✅ สิ่งที่ต้องทำ:**
1. เข้าสู่ **LINE Developers Console**  
2. ไปที่ **Messaging API → Channel access token (long-lived)**  
3. คัดลอก token มาแทนที่ในแต่ละ node:
"Authorization": "Bearer <YOUR_LINE_CHANNEL_ACCESS_TOKEN>"
---

### 3. 🧠 **Gemini หรือ AI ที่ต้องการ**
Node ที่ใช้:`Transcribe a recording`, `Analyze an image`, `Google Gemini Chat Model`

✅ สิ่งที่ต้องทำ:
สร้าง API Key
ไปที่เมนู Credentials ใน n8n
เพิ่ม credential: Google Gemini

ใน Node เลือก credential ที่ตั้งคต่าไว้และ model: gemini-2.5-flash

---
### 4. 🧩 **MongoDB Atlas Vector Store หรือ Vector database อื่นๆ**

ในทีนี้ใช้ MongoDB Atlas Vector Store <br> 
✅ สิ่งที่ต้องทำ: ตั้งค่า MongoDB Credentials ใน n8n (ไปที่ Credentials → MongoDB แล้วใส่ Connection String `mongodb+srv://rosarin456:1234@cluster0.pspzc1v.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0`) <br> 
Database: sample_mflix

---
### 5. 🗃️ Chat Memory (MongoDB Chat Memory หรืออื่นๆ)

Node: MongoDB Chat Memory <br> 
✅ สิ่งที่ต้องทำ: ตั้งค่า MongoDB Credentials ใน n8n (ไปที่ Credentials → MongoDB แล้วใส่ Connection String `mongodb+srv://rosarin456:1234@cluster0.pspzc1v.mongodb.net/?retryWrites=true&w=majority&appName=Cluster0`) <br> 
Database: n8n-rag

--- 
### 6. 🧩 **Azure AI หรือ embedding AI model ตัวอื่นๆ**
Node: Embeddings <br> 
เนื่องจาก sample data: sample_mflix มี embedding dimension 1536 จึงต้องเลือก model ที่แปลง embedding เป็น 1536d <br> 
ในทีนี้เลือกใช้ model text-embedding-ada-002

---

หมายเหตุ1: ภาพยนตร์ที่อยู่บนฐานข้อมูลส่วนมากเราบนภาพยนตร์เก่า

หมายเหตุ2: เนื่องจากฐานข้อมูลมีการ embedded ช้อมูลเกี่ยวกับพล็อตภาพยนตร์ ดังนั้น หากคุณสอบถามเกี่ยวกับ ชื่อนักแสดง ประเทศ หรือผู้กำกับ ข้อมูลอาจไม่ครบถ้วนหรืออาจคลาดเคลื่อนนะคะ

---
### Testing
เมื่อเชื่อมต่อเสร็จแล้วสามารถ Test ได้เลย โปรดตรวจสอบ webhook ที่ใช้ให้ถูกต้อง
<br>
หรืออีกทางหนึ่ง สามารถเทส workflow นี้ได้ที่ line @832gkadd น้อง chatbot พร้อมตอบคำถามเกี่ยวกับภาพยนตร์แล้ว !!
