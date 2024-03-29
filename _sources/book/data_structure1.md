# โครงสร้างข้อมูล (Data Structure I)
โครงสร้างข้อมูล (Data Structure) เป็นสิ่งที่ใช้เก็บข้อมูล เพื่อให้เราสามารถจัดเก็บ ค้นหา และจัดการนำมาใช้ได้อย่างดี และเป็นสิ่งที่สำคัญมากที่นักเขียนโปรแกรมทุกคนควรเข้าใจเป็นอย่างดี โดยเฉพาะอย่างยิ่งผู้ที่สนใจทางด้านวิทยาการข้อมูล (data science) เพราะต้องทำการจัดเก็บ เคลื่อนย้าย และนำข้อมูลไปคำนวณค่าต่าง ๆ เป็นประจำ

 โครงสร้างข้อมูลมีอยู่หลากหลายแบบซึ่งในบทนี้เราจะเรียนรู้วิธีการใช้ลิสต์ (list) ดิกชันนารี (dictionary) ทูเปิล (tuple) เคาวน์เตอร์ (counter) และเซ็ต (set) ในการเก็บข้อมูล เวลาเลือกใช้โครงสร้างข้อมูล เราต้องคำนึงถึง 3 อย่าง

1. ความถูกต้อง กล่าวคือข้อมูลจะต้องไม่สูญหายหรือผิดเพี้ยนไปจากความตั้งใจของเรา เช่น โครงสร้างข้อมูลบางอย่างไม่เก็บข้อมูลที่ซ้ำไว้ หรือโครงสร้างข้อมูลบางอย่างไม่สนใจลำดับในการจัดเก็บข้อมูล
2. ความรวดเร็ว เนื่องจากโครงสร้างข้อมูลแต่ละอย่างมีวิธีการเก็บข้อมูลที่ต่างกัน ทำให้เวลาที่ใช้ในการค้นหาข้อมูลเพื่อดึงเอามาใช้นั้นต่างกันไปด้วย
3. ความสะดวก โครงสร้างข้อมูลมี method ที่ต่างกัน ทำให้งานบางอย่างทำได้สะดวกมากน้อยต่างกัน เช่น ลิสต์เท่านั้นที่รองรับการดึงข้อมูลออกมาตามลำดับตัวอักษรอย่างสะดวก ๆ ขั้นตอนน้อย หากเราจำเป็นต้องดึงข้อมูลในลักษณะนี้เราต้องเลือกใช้ลิสต์ในการเก็บข้อมูล

ในบทนี้และบทที่ 5 เราจะศึกษาวิธีการใช้โครงสร้างข้อมูลหลากหลายแบบ ซึ่งเราจำเป็นต้องทราบ
1. วิธีการสร้างโครงสร้างข้อมูล
2. วิธีการเพิ่มข้อมูลเข้าไปในโครงสร้าง
3. วิธีการแก้ไขข้อมูลที่อยู่ในโครงสร้าง
4. วิธีการดึงข้อมูลออกมาโดยการใช้ลูป
5. วิธีการดึงข้อมูลออกมาโดยการใช้ method ต่าง ๆ 
6. ข้อดี ข้อเสียของโครงสร้างข้อมูล


```{tableofcontents}
```
