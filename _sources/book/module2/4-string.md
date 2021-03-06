# สตริง
สตริง เป็นประเภทของข้อมูลที่ใช้สำหรับเก็บข้อมูลที่เป็นรูปแบบตัวหนังสือหรืออักขระ (character) อื่น ๆ 

## การสร้างสตริง

วิธีการสร้างสตริงโดยการพิมพ์ข้อความเข้าไปในตัวโค้ดโดยตรง เรียกว่าการสร้าง string literal ซึ่งต่างจากการสร้างสตริงขึ้นมาโดยกาเรียนฟังก์ชันอื่น ๆ 

การสร้าง string literal มีอยู่อย่างน้อย 3 วิธี

1. คร่อมข้อความด้วย single quote 
```python
first_sentence = 'I dreamed a dream in times gone by'
```
การใช้ single quote สะดวกดีเพราะว่าไม่ต้องกดปุ่ม shift และดูสะอาดตา แต่ว่าจะเปิดปัญหาเมื่อข้อความที่เราเก็บมี `'` อยู่ข้างในอยู่แล้ว เช่น
```
>>> climax_sentence = 'So different from this hell I'm living'
  File "<stdin>", line 1
    climax_sentence = 'So different from this hell I'm living'
                                                     ^
SyntaxError: invalid syntax
```
```{margin} คำศัพท์
หนีสตริง (escaping a string) คือการใช้เครื่องหมายอื่นในการบอกให้เครื่องรู้ว่าเครื่องหมายที่ตามมาให้ถือว่าเป็นข้อความอย่างหนึ่ง ไม่มีความพิเศษอื่นใด 
```
ซึ่งผิดไวยากรณ์เพราะ interpreter นึกว่า `'` ใน `I'm` ใช้ทำหน้าที่บอกจุดสิ้นสุดของสตริง เราจำเป็นต้องใช้การหนี (escape) โดยการใช้เครื่องหมาย `\` เพื่อบอกกับเครื่องว่า `'` ที่ตามหลังมาให้ถือว่าเป็นสตริง ไม่ใช่เครื่องหมาย quote เช่น
```
>>> climax_sentence = 'So different from this hell I\'m living'
>>> print(climax_sentence)
So different from this hell I'm living
```

2. คร่อมข้อความด้วย double quote เช่น
```
>>> climax_sentence = "So different from this hell I'm living"
>>> print(climax_sentence)
So different from this hell I'm living
```
จะสังเกตได้ว่าเราไม่ต้องหนี `'` เพราะเราใช้ `"` ในการสร้างสตริงแทน

แต่ก็ยังเกิดปัญหาคล้าย ๆ กันได้ถ้าเราใช้ `"` ในการคร่อมข้อความเพื่อสร้างสตริง และข้อความของเรามี `"` อยู่ในนั้น ทำให้เครื่องสับสน
```
>>> news_opening = "The spokesman reported "The company is in a great position." after being pressed many times"
File "<stdin>", line 1
news_opening = "The spokesman reported "The company is in a great position." after being pressed many times"

SyntaxError: invalid syntax
```
เราต้องทำการหนี `"` โดยการใช้ backslash `\` เช่นเคย
```python
news_opening = "The spokesman reported \"The company is in a great position.\" after being pressed many times"
```
3. คร่อมข้อความด้วย triple quote 

การสร้างสตริงด้วยวิธีนี้เป็นวิธีเดียวที่จะสร้าง string literal ที่มีหลาย ๆ บรรทัดอยู่ โดยตัวคั่นบรรทัดนั้นเครื่องจะจัดเก็บอยู่ในตัวอักขระพิเศษ `\n` เช่น 

```
>>> juliet_speech = """O Romeo, Romeo, wherefore art thou Romeo?
... Deny thy father and refuse thy name."""
>>> juliet_speech
'O Romeo, Romeo, wherefore art thou Romeo?\nDeny thy father and refuse thy name.'
>>> print(juliet_speech)
O Romeo, Romeo, wherefore art thou Romeo?
Deny thy father and refuse thy name.
```


## การหั่นสตริง (String splicing)
เราสามารถหั่นสตริงตั้งต้นออกมาอีกสตริงหนึ่ง เพื่อตัดเอาส่วนของข้อความที่เราอยากได้ เช่น 
- นายสมชาย --> สมชาย (ตัดคำนำหน้าชื่อออก)
- http://www.chula.ac.th --> www.chula.ac.th (ตัด http:// ทิ้งเพื่อให้ได้ชื่อเว็บไซต์ที่สั้นลง)
- @terutherford --> terutherford (เอามาแต่ชื่ออินสตาแกรมไม่เอา @)
- #ไอจีล่ม --> ไอจีล่ม (ตัดเอาแฮชแท็กออกไป)


ภาษาไพธอนมีคำสั่งในการหั่นสตริงมากมาย

### ดึงออกมาเพียงตัวอักขระเดียว

```{image} img/char-index.png
:height: 100px
:align: center
```
```{margin} คำศัพท์
index เลขชี้ตำแหน่ง
```
เราใช้ operator `[]` ครอบตำแหน่งที่ต้องการจะดึงตัวอักษรออกมา (index) แต่จะนับเริ่มจากศูนย์ เพราะฉะนั้น `string[a]` return ตัวอักขระจากช่องที่ index `a` ตามที่เห็นดังภาพข้างบน 

ภาษาไพธอนมีการดึงตัวอักขระโดยนับจากข้างหลังได้ด้วยโดยตัวอักขระสุดท้ายของสตริงจะเริ่มที่ -1 เพราะฉะนั้น `string[-a]` return ตัวอักขระจากช่องที่ index `-a` ซึ่งเราเรียกว่าการใช้เลข index ติดลบ (negative indexing)

ตัวอย่าง สมมติว่าเราได้รัน `s = 'นายสมชาย'` 
| คำสั่ง 			  | output |
| -------			|--------|
| `s[1]`			| `'า'`	 |
| `s[-3]`			| `'ช'`	 |
| `s[3]`			| `'ส'`	 |
| `s[-5]`			| `'ส'`	 |

```{margin} 
`IndexError` คือ error ที่เกิดจากการที่ใช้เลข index ที่ไม่อยู่ในช่วงที่เหมาะสม 
```
ถ้าหากเรารัน `s[9]` หรือ `s[-10]` เราได้ข้อความบอก error ดังนี้
```
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
IndexError: string index out of range
```
เครื่องบอกว่า index ไม่ได้อยู่ในช่วงที่เหมาะสม เพราะจากสตริงที่เราสร้าง เราสามาเลือก index ตั้งแต่ 0-7 และ -1 ถึง -8


### ดึงสตริงย่อย (substring)
```{margin} คำศัพท์
สตริงย่อย (substring) คือ สตริงที่เป็นส่วนหนึ่งของสตริงอีกสตริงหนึ่งที่ยาวกว่า
```
การหั่นสตริง หรือการดึง substring ออกมาจากสตริง สามารถทำได้โดยการใช้ operator `[]` เช่นเคยแต่ว่าต้องระบุตำแหน่งที่ต้องการตัด substring ออกมา `[ตำแหน่งที่เริ่ม:ตำแหน่งที่จบ]` เช่น สมมติว่าเราต้องการดึง substring จากสตริง `s` ที่เก็บข้อความอยู่ดังนี้

```{image} img/substring-index.png
:height: 100px
:align: center
```
การดึง substring ให้นึกถึงว่าตัวเลข index ชี้ไปที่ร่องระหว่างตัวอักขระสองตัว เช่น index 3 อยู่ระหว่าง `'ย'` และ `'ส'` หรือ index -2 อยู่ระหว่าง `'ช'` และ `'ย'`

ตัวอย่าง สมมติว่าเราได้รัน `s = 'นายสมชาย'` 
| คำสั่ง 		  | output | คำอธิบาย |
| -----			|--------|---------| 
| `s[0:3]`		| `'นาย'`	  |											
| `s[5:7]`		| `'ชา'`	  |
| `s[-3:-1]`	| `'ชา'`	  |
| `s[:3]`		| `'นาย'`   | ถ้าจุดเริ่มต้นเป็น 0 สามารถละออกไปได้
| `s[:-2]`		| `'นายสมช'`| negative indexing
| `s[3:]`		| `'สมชาย'` | `[index:]` แปลว่าตัดจาก index ไปจนสุดสตริง
| `s[-4:]`		| `'สมชาย'` | negative indexing

ไพธอนให้ความอะลุ่มอล่วยกับการใช้ index ในการดึง substring เวลาเราใส่ index ที่ผิดลงไปโดยไม่ได้ตั้งใจ interpreter จะไม่โยน `IndexError` ให้เราแต่ให้ output ที่เราไม่ได้คาดคิดมา ทำให้โปรแกรมเกิดข้อผิดพลาดเวลานำผลไปใช้ต่อกับคำสั่งอื่น ๆ 

| คำสั่ง 		  | output | คำอธิบาย |
| -----			|--------|---------| 
| `s[-3:-1]`	| `'ชา'`	  |
| `s[-3:0]`		| `''`		| เหมือนว่าเราควรจะได้ `'ชาย'` แต่ว่าไม่ได้ เพราะ 0 ชี้ไปที่ตำแหน่งที่มาก่อน -3  ไพธอนจะตีผลเป็นสตริงเปล่า 
| `s[5:2]`		| `''`		| 2 ชี้ไปที่ตำแหน่งที่มาก่อน 5  
| `s[5:10000]`	| `'ชาย'`		| ควรจะได้ error แต่ว่าไพธอนปล่อยไปถึงแม้ index จะเกิน
| `s[-100:-1]`	| `'นายสมชา'`	| ควรจะได้ error แต่ว่าไพธอนปล่อยไปถึงแม้ index จะเกิน

## String operator และ built-in function
นอกเหนือจาก operator `[]` แล้วสตริงยังมี operator ที่ใช้ได้อยู่อีก 4 ตัว 

| Operator  		| ความหมาย 				  | ตัวอย่าง |
| --------  		| ---------				  | -------|
| + 				| ต่อสตริง (concatenate)	| `'aa' + 'bb'` --> `'aabb'`| 
| * 				| ซ้ำสตริง      			| `'abc' * 23` --> `abcabcabc`| 
| `in`	    		| เช็คว่ามีสตริงหนึ่งเป็นสตริงย่อยอีกสตริงหนึ่งหรือไม่ | `'a' in 'girl'` --> `False` |
|					|						   |   `'i' in 'girl'` --> `True`
| `not in`			| นิเสธของ `in`			  |   `'a' not in 'girl'` --> `True`
| ==				| เท่ากันเป๊ะหรือไม่			| `'girl' == 'girl` --> `True` |
|					|							| `'girl' == 'Girl` --> `False`
| `len(s)`			| return ความยาวสตริง		| `len('girl')` --> 4 


## `for` loop บนสตริง
```{margin} คำศัพท์
iterate คือ การไล่ดึงข้อมูลมาทีละตัว เพื่อนำมาประมวลผลด้วยคำสั่งอื่น ๆ 
```
สตริง คือการนำอักขระหลาย ๆ ตัวมาต่อกันเป็นสายเดียว ในบางครั้งเราต้องการนำอักขระออกมาประมวลผลทีละตัว เช่น เราอยากนับว่าในสตริงมีตัวเลขทั้งหมดกี่ตัว มีอักษรภาษาอังกฤษทั้งหมดกี่ตัว หรือมีสระกี่ตัว เราต้องจะต้องเริ่มจากการดึงตัวอักษรออกมาทีละตัว (iterate) ออกมาตรวจสอบและนับ 

การ iterate ไปบนสตริงเราจะใช้ `for` ในการดึงตัวอักษรดังนี้
```python
s = 'abcdefg'
for alph in s:	# alph เป็นตัวแปรเก็บแทนตัวอักขระแต่ละตัว ในแต่ละรอบลูป
	print(alph)	# แสดงผลค่าของ alph
```
Output
```
a
b
c
d
e
f
g
```

อีกวิธีคือ iterate ลงไปบน index ของสตริงและดึงตัวอักขระโดยใช้ `[]` 
```python
s = 'abcdefg'
for i in range(len(s)):	# i เป็นตัวแปรเก็บ index จาก 0 ถึง len(s) ในแต่ละรอบลูป
	print(s[i])			# แสดงผลค่าของอักขระที่ index i 
```

## String method

```{margin} คำศัพท์
*object* มีหน้าที่เก็บข้อมูล นอกจากนั้นยังมี *method* ต่างๆ ที่ช่วยนำข้อมูลที่เก็บอยู่มาใช้ให้ได้สะดวกขึ้น
```
สตริงจัดเป็น object ประเภทแรกที่เราจะเรียนรู้วิธีการใช้ในภาษาไพธอน object เป็นสิ่งที่ไว้เก็บข้อมูลที่เป็นตัวหนังสือต่าง ๆ แต่ว่านอกจากนั้นแล้ว object มีสิ่งที่เรียกว่า method ติดตัวมาด้วย ซึ่งก็คือฟังก์ชันที่นำเอาข้อมูลที่ object ที่เรียก method นั้นขึ้นมาใช้ ในการเรียกใช้ method เราจำเป็นต้องรู้ว่า
1. object ชนิดนั้นมี method ชื่ออะไรบ้าง
2. method ที่จะใข้นั้น input คืออะไร
3. method ที่จะใช้นั้น return output อะไร และเป็นไทป์อะไร

คำสั่งในการใช้คือ `object.ชื่อmethod(parameter)` ตัวอย่าง เช่น 
```
name = 'james'
name.is_upper()
```
ตัวแปร `name` เก็บสตริง `'james'` ไว้โดยการสร้าง string literal แบบใช้ single quote จากนั้นสตริงนั้นเรียก method `is_upper` ซึ่งไม่ต้องการพารามิเตอร์ และ return บูลีนที่บ่งบอกว่าสตริงที่เก็บอยู่นั้นเป็นตัวลาตินตัวพิมพ์ใหญ่หรือไม่ 

สตริงในภาษาไพธอนมี method เยอะมาก ๆ ไม่มีโปรแกรมเมอร์ไหนพยายามจำทั้ง จะจำได้เฉพาะ method ที่ใช้หน้างานบ่อย ๆ ถ้าหากจำไม่ได้สามารถเสิร์ชหาออนไลน์ได้ และโปรแกรมเมอร์เปิดหากันเป็นปกติ แต่เพื่อความสะดวกคล่องตัวในการเขียนโปรแกรมที่เกี่ยวกับการประมวลผลข้อมูลที่เป็นข้อความ เราควรจะต้องรู้จัก method ของสตริงดังนี้


### `.lower()` และ `.upper()`
````{sidebar} ตัวอย่าง
```python
s = 'James'
s.lower() #--> 'james'
s.upper() #--> 'JAMES'
```
````
`string.lower()` return สตริงที่มีตัวอักษรเหมือนกันแต่เป็นตัวเล็กทั้งหมด

`string.upper()`return สตริงที่มีตัวอักษรเหมือนกันแต่เป็นตัวใหญ่ทั้งหมด

*ข้อควรระวัง* ทั้งสอง method เมื่อเราเรียกใช้แล้วจะ return สตริงชุดใหม่มาให้ แยกต่างหากจากตัวสตริงเดิม ซึ่งจะมีค่าข้อความเดิมอยู่ไม่เปลี่ยนแปล

คำสั่งเหล่านี้มีประโยชน์เวลาเราอยากเปรียบเทียบข้อความสองข้อความว่าเหมือนกันหรือไม่โดยไม่สนใจว่าเป็นตัวเล็กตัวใหญ่ (case-insensitive) 

### `.is_lower()` และ `.is_upper()`
````{sidebar} ตัวอย่าง
```python
s = 'NASA'
s.is_lower() #--> False
s.is_upper() #--> True

s2 = 'Casa'
s2.is_lower() #--> False เพราะไม่ใช่ตัวเล็กหมด
s2.is_upper() #--> False เพราะไม่ใช่ตัวใหญ่หมด
s2[0].is_upper() #--> True ตัวอักษรตัวแรกเป็นตัวใหญ่
```
````
`string.is_lower()` return `True` ถ้าทุกอักขระเป็นตัวเล็กทั้งหมด

`string.is_upper()` return `True` ถ้าทุกอักขระเป็นตัวใหญ่ทั้งหมด

