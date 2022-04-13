# การทำใช้โมดูล relays กับ esp01 บน Homeassistant ผ่านส่วนเสริม esphome
อุปกรณ์ที่จำเป็น 
 
* รีเลย์ 5V DC 220V AC (แนะนำ 3.3V DC หากหาได้เพราะตัว esp01 และ 8266 บางตัวรับ 5V ไม่ได้) ในที่นี้ใช้รีเลย์ 5V
* สวิชชิ่งแปลงไฟลงจาก 220V AC to 5V DC
* CH340 usb to seriel สำหรับการแฟลช esp01
* esp01 (01 จะต่างกับ 01s ตรงที่ตัว 01s จะไม่มี led สถานะสีแดงมีแต่สีฟ้า) แต่ทั้งสองตัวมีขา GPIO ตำแหน่งเหมือนกัน และตัว 01s มี ram มากกว่า
* ขั้วหลอดไฟ
* หลอดไฟ
* สายจั๊มบอร์ด male to male 1 สาย สั้น ๆ (หรือสายไฟอะไรก็ได้ ที่มีปลายเปลือยสองด้าน)

------

Homeassistant ต้องติดตั้ง add-on ดังนี้
* ESPHOME
* Fileeditor
* NodeRed (หากต้องการใช้งานกับ Siri)

![image](https://user-images.githubusercontent.com/101375207/163098717-1f83a194-99b2-4bfd-a39d-445f272f41e0.png)
![image](https://user-images.githubusercontent.com/101375207/163098848-7da23f1a-0441-48bd-80ba-c8b3dfda3d02.png)
![image](https://user-images.githubusercontent.com/101375207/163098792-27c0b284-e0d7-49ef-a1ff-672542abe587.png)

------
### การตั้งค่า esp01 ใน ESPHome
*** หากไม่เคยตั้งค่าไวไฟ ESPHome ให้ไปตั้งค่าก่อน ตามคลิปนี้ ( https://www.youtube.com/watch?v=iufph4dF3YU )
- นำ esp01 เสียบลงที่โมดูล CH340 แล้วนำไปเสียบกับพอร์ต usb ที่คอมพิวเตอร์เครื่องที่รัน Homeassistant os อยู่   
จากนั้นให้ทำการ add new device ในหน้าต่างของ esphome กด continue การตั้งชื่อ device จะตั้งว่าอะไรก็ได้ (ในที่นี้จะใช้ esp01 เป็นชื่อ)
- Select your device type ให้เลือกเป็น esp8266 (เพราะ esp01 คือตัว 8266 ที่ไม่มีการเพิ่ม PIN I/O)
- จากนั้นให้กด Install โดยเลือกตัวเลือก "Plug into computer running ESPHome Dashboard"
- ตัว ESPHOME จะ compile โค้ดสำเร็จรูปและติดตั้งลงบนบอร์ด esp01 และแสดง log ตามภาพ                                                 
โดยเมื่อ compile เสร็จจะแสดงใน log ว่าพยายามติดต่อกับตัวบอร์ด esp01 หลังจากบรรทัดที่โชว์ดังภาพ



![image](https://user-images.githubusercontent.com/101375207/163100853-af8a2ff6-b2ee-43b9-a507-4fa27004a9f9.png)



- ให้นำสายจั๊ม หรือสายไฟที่เตรียมไว้ จิ้มไปที่ขา Gnd (Ground) และปลายอีกข้างแตะที่ GPIO0 เพื่อเข้าสู่ flash mode สำหรับตัว esp01                             
** หากไม่ได้ให้ทำเช่นเดิมแต่ ให้แตะที่ GPIO0 ก่อนและลากไปแตะที่ขา RST (Reset) (แตะ 3 ขาพร้อมกัน) (มันขึ้นบนจอให้ reset via pin ผมทำแบบนี้ได้ผล)


![image](https://user-images.githubusercontent.com/101375207/163102306-b5dcd938-4403-44e9-931c-b700fcb57a52.png)


- เมื่อสำเร็จจะขึ้นดังนี้


* ![image](https://user-images.githubusercontent.com/101375207/163101841-ecd19ae7-9478-4857-917b-bd3a3e42e5af.png)



------

### รูปการต่อวงจร แบบคร่าว ๆ
