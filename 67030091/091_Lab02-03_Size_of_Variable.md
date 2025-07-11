1 คำถาม

1.1 int บน ESP32 ใช้กี่ไบต์?
4 ไบต์ 

1.2 จากผลลัพธ์ นักศึกษาสังเกตเห็นอะไรเมื่อค่าเกินขอบเขตของ int บน ESP32?
เมื่อค่าตัวแปร int เกินขอบเขตของมัน ไม่ว่าจะเกินค่าสูงสุด (Overflow) หรือต่ำกว่าค่าต่ำสุด (Underflow) ค่าของตัวแปรจะ "วนกลับ" (wrap around) ไปยังอีกฝั่งหนึ่งของช่วงขอบเขตที่เป็นไปได้ เหมือนกับมาตรวัดที่หมุนครบรอบแล้วกลับมาเริ่มต้นใหม่


2 คำถาม
float และ double บน ESP32 ใช้กี่ไบต์ตามลำดับ?
ขนาดของ float: 4 bytes
ขนาดของ double: 8 bytes

นักศึกษาสังเกตเห็นความแตกต่างของความแม่นยำระหว่าง float และ double อย่างไร? สถานการณ์ใดที่คุณควรเลือกใช้ double แทน float?
ความแตกต่างความแม่นยำ:
float (4 ไบต์): เก็บค่าทศนิยมได้น้อยกว่า (แม่นยำประมาณ 6-7 ตำแหน่ง) ทำให้มีโอกาสคลาดเคลื่อนสูงกว่าเมื่อต้องการความแม่นยำมาก ๆ (เช่น 3.14159265f แสดงผลเป็น 3.14159274)
double (8 ไบต์): เก็บค่าทศนิยมได้มากกว่าและแม่นยำกว่ามาก (ประมาณ 15-17 ตำแหน่ง) จึงมีความคลาดเคลื่อนน้อยมากหรือไม่คลาดเคลื่อนเลยสำหรับเลขทั่วไป (เช่น 3.141592653589793 แสดงผลตรงตามเดิม)

ควรใช้ double แทน float เมื่อ:
ความแม่นยำสำคัญมาก: เช่น การคำนวณทางวิทยาศาสตร์, วิศวกรรม, การเงิน, หรือการคำนวณที่ต้องสะสมค่ากันไปเรื่อยๆ ซึ่งข้อผิดพลาดเล็กน้อยอาจส่งผลใหญ่
หน่วยความจำไม่ใช่ปัญหา: เนื่องจาก double ใช้พื้นที่มากกว่า float สองเท่า


3 คำถาม
char ใช้กี่ไบต์? ค่าตัวเลข (ASCII value) มีความสัมพันธ์กับอักขระอย่างไร?
char ใช้ 1 ไบต์
ความสัมพันธ์กับ ASCII: char เก็บตัวอักษร แต่เบื้องหลังมันคือค่าตัวเลขตามรหัส ASCII เราสามารถแปลง char เป็น int เพื่อดูค่า ASCII หรือแปลงค่า int (ที่เป็นรหัส ASCII) กลับเป็น char เพื่อแสดงตัวอักษรได้


4 คำถาม
bool ใช้กี่ไบต์? true และ false ถูกแสดงผลเป็นค่าใดบน Serial Monitor?
ขนาดของ bool: 1 bytes
myBool = true ผลลัพธ์: 1
myBool = false ผลลัพธ์: 0

5 คำถาม 
ชนิดข้อมูลจำนวนเต็มแต่ละชนิด (long, long long, unsigned int, unsigned long, unsigned long long) ใช้กี่ไบต์บน ESP32?
ขนาดของ long: 4 bytes
ขนาดของ long long: 8 bytes
ขนาดของ unsigned int: 4 bytes
ขนาดของ unsigned long: 4 bytes
ขนาดของ unsigned long long: 8 bytes

บน ESP32, long มีขอบเขตเท่ากับ int หรือไม่? ชนิดข้อมูลใดที่คุณจะใช้หากต้องการเก็บค่าจำนวนเต็มบวกที่ใหญ่ที่สุด?
บน ESP32, long ทั้งคู่เป็น 4 ไบต์ หรือ 32-bit signed integer
หากต้องการเก็บค่าจำนวนเต็ม บวกที่ใหญ่ที่สุด บน ESP32 ใช้ unsigned long long


6 คำถาม 
byte ใช้กี่ไบต์? เมื่อ myByte ถูกกำหนดให้เป็น 256 ผลลัพธ์ที่ได้คืออะไร และเพราะเหตุใด?
byte ใช้ 1 ไบต์ และสามารถเก็บค่าได้ตั้งแต่ 0 ถึง 255 เท่านั้น เมื่อกำหนดให้เป็น 256 จะเกิด Overflow ทำให้ค่าวนกลับไปเป็น 0 


7 คำถาม
ทำไม 10 / 3.0 (เมื่อตัวหารเป็น float หรือ double) ถึงได้ผลลัพธ์เป็นทศนิยม แต่เมื่อตัวหารถูกแปลงเป็น int แล้วผลลัพธ์เป็นจำนวนเต็ม?
เมื่อหารด้วย float หรือ double (ทศนิยม):
คอมพิวเตอร์จะทำการหารแบบ ทศนิยม ผลลัพธ์จึงออกมาเป็นทศนิยมที่แม่นยำ เช่น 10/3.0 จะได้ 3.333...

เมื่อหารด้วย int (จำนวนเต็ม):
ถ้าทั้งตัวตั้งและตัวหารเป็น จำนวนเต็ม คอมพิวเตอร์จะทำการหารแบบ จำนวนเต็ม โดยจะตัดส่วนที่เป็นทศนิยมทิ้งไปทั้งหมด ไม่มีการปัดเศษขึ้นหรือลง เช่น 10/(int)3.0 จะกลายเป็น 10/3 ซึ่งได้ผลลัพธ์เป็น 3 (เพราะตัด 0.333... ทิ้งไป)


8 คำถาม
นักศึกษาจะใช้การทำ Type Casting ในสถานการณ์ใดบ้างในการเขียนโปรแกรม?
- แปลงค่าทศนิยมเป็นจำนวนเต็ม:
เมื่อต้องการใช้แค่ส่วนจำนวนเต็มของค่าทศนิยม เช่น จาก 25.79 ให้เหลือแค่ 25 (โค้ด: (int)temperatureCelsius). การทำแบบนี้จะตัดส่วนทศนิยมทิ้ง.

- ป้องกันการหารจำนวนเต็ม:
เมื่อต้องการให้ผลลัพธ์ของการหารเป็นทศนิยม แทนที่จะเป็นจำนวนเต็มที่ปัดเศษทิ้ง เช่น ถ้ามี int count = 7; และ int total = 20; ถ้าหาร count / total จะได้ 0 แต่ถ้าต้องการ 0.35 จะต้องทำ (float)count / total เพื่อให้การคำนวณเป็นแบบทศนิยม.

- แปลงตัวอักขระเป็นรหัสตัวเลข (ASCII):
เมื่อต้องการรู้ค่าตัวเลขที่เป็นตัวแทนของตัวอักษรนั้นๆ เช่น ตัวอักษร 'P' มีรหัส ASCII เป็น 80 (โค้ด: (int)letter).

- เมื่อฟังก์ชันหรือคำสั่งต้องการข้อมูลประเภทที่เฉพาะเจาะจง:
บางครั้งฟังก์ชันที่เราจะใช้ถูกออกแบบมาให้รับพารามิเตอร์เป็นประเภทข้อมูลหนึ่งๆ เท่านั้น แม้ว่าข้อมูลที่เรามีจะเป็นประเภทอื่นที่สามารถแปลงได้ ก็ต้องทำการ Type Casting ให้ตรงกับที่ฟังก์ชันต้องการเพื่อความถูกต้องของโปรแกรม.


