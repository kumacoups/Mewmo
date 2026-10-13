# Mewmo (PWA)

แพลนเนอร์ไฟล์เดียว ใช้ได้ออฟไลน์ ติดตั้งเป็นแอปบนหน้าจอหลักได้

## ไฟล์ในโฟลเดอร์
- `index.html` ตัวแอปทั้งหมด (HTML/CSS/JS ไฟล์เดียว)
- `manifest.webmanifest` ชื่อแอป สี ไอคอน และทางลัด (โน้ต / Habit / ปฏิทิน)
- `sw.js` service worker ทำให้เปิดแอปได้เมื่อออฟไลน์
- `icons/` ไอคอนแอป (192, 512, maskable, apple-touch, favicon)
- `_headers` ตั้งค่าแคชสำหรับ Netlify / Cloudflare Pages
- `vercel.json` ตั้งค่าแคชสำหรับ Vercel

## วิธี deploy
อัปโหลดทั้งโฟลเดอร์ขึ้นโฮสต์แบบ static ที่เป็น HTTPS (จำเป็นสำหรับการติดตั้งและออฟไลน์)
- Netlify / Cloudflare Pages: ลากโฟลเดอร์นี้ไปวางได้เลย
- Vercel: ดูหัวข้อ Deploy บน Vercel ด้านล่าง
- GitHub Pages: ใส่ไฟล์ทั้งหมดใน branch ที่เปิด Pages ใช้ได้ทั้งที่ราก (`/`) และโฟลเดอร์ย่อย (`/mewmo/`) เพราะใช้ path แบบสัมพัทธ์

## วิธีติดตั้งบนมือถือ
- iPhone (Safari): ปุ่มแชร์ > เพิ่มไปยังหน้าจอโฮม
- Android (Chrome): เมนู 3 จุด > ติดตั้งแอป หรือ เพิ่มไปยังหน้าจอหลัก

## ข้อมูลอยู่ที่ไหน
เก็บในเบราว์เซอร์ของเครื่องที่ใช้ (localStorage และ IndexedDB) ผูกกับโดเมนที่ deploy
ย้ายเครื่องหรือเปลี่ยนโดเมนข้อมูลไม่ตามไป ให้ใช้ปุ่มบันทึก > ส่งออกไฟล์สำรอง แล้วนำเข้าที่เครื่องใหม่

## อัปเดตเวอร์ชัน
เมื่อแก้ `index.html` ให้เปลี่ยนค่า `V` บรรทัดแรกของ `sw.js` (เช่น `mewmo-2`) เพื่อให้เครื่องที่ติดตั้งไว้ดึงไฟล์ใหม่

## Deploy บน Vercel
### วิธีที่ 1: ใช้ CLI (เร็วที่สุด)
1. ติดตั้ง Node.js แล้วรัน `npm i -g vercel`
2. เข้าโฟลเดอร์ `pwa` แล้วรัน `vercel login`
3. รัน `vercel` ตอบคำถามดังนี้ Set up and deploy: Y / Link to existing project: N / Project name: mewmo / Directory: `./` / Override settings: N
4. รัน `vercel --prod` จะได้ลิงก์จริง เช่น `https://mewmo.vercel.app`
### วิธีที่ 2: ผ่าน GitHub
1. สร้าง repo แล้วอัปโหลดไฟล์ในโฟลเดอร์ `pwa` ไว้ที่รากของ repo
2. ที่ vercel.com เลือก Add New > Project > Import repo นั้น
3. Framework Preset: Other / Build Command: ปล่อยว่าง / Output Directory: ปล่อยว่าง แล้วกด Deploy
4. ครั้งต่อไปที่ push ขึ้น branch หลัก Vercel จะ deploy ให้เอง

### ข้อควรระวัง
- ใช้ลิงก์ production เดียวเท่านั้น (เช่น `mewmo.vercel.app` หรือโดเมนของคุณ) เพราะข้อมูลผูกกับโดเมน ลิงก์ preview ของแต่ละครั้งที่ deploy เป็นคนละโดเมนและข้อมูลจะไม่ตามไป
- ถ้าจะใช้โดเมนของตัวเอง ให้ตั้งที่ Settings > Domains ก่อนเริ่มใช้งานจริง
- ลิงก์ preview อาจต้องล็อกอินก่อนเปิด (Deployment Protection) ส่วนลิงก์ production เปิดได้ปกติ
- อัปเดตแอป: แก้ `index.html` แล้วเปลี่ยนค่า `V` ใน `sw.js` จากนั้นรัน `vercel --prod` อีกครั้ง
