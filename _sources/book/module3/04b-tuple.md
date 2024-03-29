
# ทูเปิล (tuple) 
ทูเปิล เป็นโครงสร้างข้อมูลที่เก็บข้อมูลเป็นลำดับคล้ายกับลิสต์ ลิสต์สามารถทำทุกอย่างที่ทูเปิลสามารถทำได้ การสร้างทูเปิลคล้ายคลึงกับการสร้างลิสต์แต่ว่าเราจะใช้วงเล็บ `()` แทนวงเล็บเหลี่ยม `[]` เช่น
```python
first_last_name = ('อรรถพล', 'ธำรงรัตนฤทธิ์')
```

ข้อแตกต่างคือ ทูเปิลเป็นโครงสร้างข้อมูลที่เปลี่ยนแปลงไม่ได้ (immutable) เมื่อเราสร้างทูเปิลขึ้นมาแล้ว ไม่สามารถเปลี่ยนแปลงสมาชิกที่อยู่ภายในได้ รวมถึงไม่สามารถเพิ่มสมาชิกเข้าไปได้ ทั้งหมดนี้ดูเหมือนจะเป็นข้อเสียของทูเปิล แต่ว่าการใช้ทูเปิลทำให้เกิดข้อผิดพลาดในโปรแกรมน้อยลง 
การใช้ทูเปิลเป็นการสื่อความหมายในโปรแกรมว่าแต่ละ index ของทูเปิลมีความหมายเจาะจง เช่น

- พิกัดบนแผนที่โลก อาจจะถูกเก็บในทูเปิดโดยที่ index 0 เป็น latitude และ index 1 เป็น longtitude อาจจะถูกเก็บในทูเปิล ดังนี้  `('13.7563° N', '100.5018°')`
- ชื่อนามสกุล อาจจะถูกเก็บในทูเปิลโดยที่ index 0 เป็นชื่อ index 1 เป็นนามสกุล ดังนี้ `('อรรถพล', 'ธำรงรัตนฤทธิ์')`
- สี มักจะถูกจัดเก็บเป็นค่าแดงเขียวน้ำเงิน (RGB) โดยที่ index 0 เป็นค่าของสีแดง index 1 เป็นค่าของสีเขียว index 2 เป็นค่าของสีน้ำเงิน ดังนี้ `(256, 256, 256)`

ในกรณีดังกล่าวทั้งหมดนี้เราไม่ควรจะเพิ่มสมาชิกเข้าไปในทูเปิลอีกแล้ว เพราะว่าพิกัดจะต้องมี 2 ตำแหน่งเท่านั้น ชื่อนามสกุลควรจะต้องถูกแทนด้วยทูเปิลแบบสองตำแหน่ง ค่าสีแบบ RGB ก็ต้องมีสีสามค่าเท่านั้น การเพิ่มสมาชิกเข้าไปทำให้สูญเสียความหมายของสิ่งที่ทูเปิลจะเก็บไว้

การเข้าถึงข้อมูลในทูเปิลใช้วิธีเดียวกับลิสต์ทุกประการ สามารถใช้ positive index และ negative index ได้เหมือนกันหมด 
```python
first_last_name = ('อรรถพล', 'ธำรงรัตนฤทธิ์')
first_name = first_last_name[0]
last_name = first_last_name[1]
print (first_name)
print (last_name)
```
เพื่อความสะดวกเรามักจะ*กระจาย*ค่าของทูเปิลใส่ตัวแปรหลาย ๆ ตัวพร้อม ๆ กัน เช่น 
```python
first_last_name = ('อรรถพล', 'ธำรงรัตนฤทธิ์')
first_name, last_name = first_last_name
print (first_name)
print (last_name)
```
การกระจายค่าที่จริงแล้วสามารถทำกับลิสต์ก็ได้ แต่ว่าไม่กรณีที่จะให้ใช้เนื่องจากเวลาเราเขียนโค้ดในการกระจายค่าเข้าสู่ตัวแปร เราจำเป็นต้องรู้ว่าลิสต์หรือทูเปิลนั้นมีจำนวนสมาชิกกี่ตัว ลิสต์เป็นโครงสร้างข้อมูลที่เราสามารถเปลี่ยนแปลงค่าข้างในได้ ทำให้เราไม่แน่ใจว่าข้อมูลในลิสต์มีอยู่กี่ตัว เมื่อเรามาถึงส่วนของโค้ดที่ต้องทำการกระจายข้อมูล แต่ว่าทูเปิลไม่มีปัญหานี้ เวลาเราสร้างทูเปิล เรามั่นใจได้เลยว่าค่าของทูเปิล และจำนวนสมาชิกของทูเปิลจะไม่เปลี่ยน 

ทูเปิลมี method `.count .index` เช่นเดียวกับลิสต์ และสามารถหั่นเป็นทูเปิลย่อยได้เหมือนกับลิสต์เช่นกัน แต่ว่ามักจะไม่ค่อยได้ใช้ประโยชน์ เพราะทูเปิลมีโครงสร้างตายตัว และข้อมูลที่อยู่ในแต่ละตำแหน่งเก็บข้อมูลคนละชนิดกันหมด 