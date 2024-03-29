# Regular expression

Regular expression (เรียกกันย่อ ๆ ว่า regex อ่านว่า /regeks/ เร็กเก็กส์)  เป็นภาษาในการระบุเขียนจับแพทเทิร์นของตัวอักษรที่เราต้องการตรวจหา เพื่อที่จะได้ดึงหรือแก้ไขข้อมูลที่อยากได้โดยสะดวก ตัวอย่างเช่น 
- ตรวจหาเบอร์โทรศัพท์ซึ่งมีแพทเทิร์นว่า มีตัวเลขทั้งหมด 10 ตัวแต่ตัวแรกต้องเป็น 0 อีก 9 ตัวเป็นอะไรก็ได้ แต่ถ้าตัวเลขมีทั้งหมด 9 ตัว ตัวแรกไม่ต้องเป็น 0 ก็ได้ 
- ตรวจหาอีเมลของพนักงานทุกคนที่มาจากภาครัฐ ซึ่งมีแพทเทิร์นว่า ข้างหน้าเครื่องหมาย @ เป็นตัวภาษาอังกฤษหรือจุดหรือตัวเลขอะไรก็ได้ แต่ข้างหลังเครื่องหมาย @ ต้องเป็นชื่อองค์กรอะไรก็ได้แต่ต้องลงท้ายด้วย .go.th 
- ตรวจหาอักษรย่อขององค์กรที่เป็นภาษาไทย ซึ่งมีแพทเทิร์นว่า ต้องเป็นตัวอักษรไทย 2 - 4 ตัวและลงท้ายด้วย .
แพทเทิร์นเหล่านี้ยากที่จะอธิบายให้เป็นตัวอักษร regular expression เป็นภาษาสื่อกลางที่ช่วยให้เราอธิบายแพทเทิร์นที่เราต้องการให้ได้อย่างชัดเจน

Regex มีความสำคัญมากๆ ในการทำงานเกี่ยวกับการประมวลผลภาษาธรรมชาติ  เพราะทำให้เราสามารถดึงข้อมูลที่มีแพทเทิร์นเด่นชัดในภาษา (เช่น อีเมล์ เบอร์โทรศัพท์ ชื่อ ตัวย่อ) ออกมาจากข้อความที่เราต้องการประมวลผลได้สะดวก ความสำคัญของ regex อีกประการหนึ่งคือ การทำความสะอาดข้อมูล ข้อมูลภาษาที่เราได้รับมามักจะมีข้อความแปลกปลอมหลากหลายประเภทที่จำเป็นต้องกรองออกก่อน ตัวอย่างเช่น ข้อความที่ดาวน์โหลดมาจากทวิตเตอร์อาจจะมีข้อความที่เป็น hashtag หรือ mention ที่เราต้องการกรองออกไป หรือข้อความที่มีลิงก์ที่เราต้องการแปลงเป็นชื่อเว็บไซต์ หรือข้อความที่มีตัวอักษรพิเศษที่เราต้องการลบออกไป เป็นต้น

## สัญลักษณ์ที่ใช้ใน regular expression

Regular expression มีความพิเศษกว่าสตริงปกติ คือตีความหมายสัญลักษณ์พิเศษต่าง ๆ ที่ช่วยระบุแพทเทิร์นที่ซับซ้อนและยืดหยุ่นมาก  เช่น 
- `[a-z.]+@[a-z]+\.com` เป็น regex สำหรับแพทเทิร์นของ email address ที่ลงท้ายด้วย .com
- `\d\d\d-\d\d\d-\d\d\d\d` เป็น regex  สำหรับแพทเทิร์นของหมายถึงเลขโทรศัพท์ เช่น 123-123-1234

สัญลักษณ์ที่ใช้ใน regular expression มีอยู่ 5 ประเภทด้วยกัน คือ

###	ตัวอักษรปกติ (Literal character)
ตัวอักษรปกติคือตัวอักษรที่เราต้องการให้ regex แมทช์กับตัวอักษรนั้น ๆ ตัวอักษรปกติสามารถเป็นตัวอักษรอะไรก็ได้ แต่บางตัวอักษรจะมีความหมายพิเศษใน regular expression ทำให้เราต้องทำการหนี (escape) โดยการเพิ่ม \ เข้าไปข้างหน้า เพื่อบอกว่าเป็นตัวอักษรปกติ ไม่ใช่อักขระพิเศษ ตัวอักษรที่ต้องทำการหนี (escape) ได้แก่ `\` `+` `*` `?` `^` `$` `(` `)` `[` `]` `{` `}` `|` และ `.`

### อักขระพิเศษ (Metacharacter)

อักขระพิเศษเป็นหัวใจสำคัญของการเขียน regex เพื่อระบุแพทเทิร์น เพราะอักขระพิเศษใช้แทนกลุ่มของตัวอักษร อักขระพิเศษมีหลายตัว แต่ในบทนี้เราจะเรียนรู้เพียงอักขระพิเศษที่ใช้บ่อย ๆ ซึ่งเราควรจะจำให้ได้ทั้งหมด ดังนี้

| สัญลักษณ์ | แทนตัวอะไรบ้าง                        |
|--------|-------------------------------------|
| ^      | หน้าสุดของ string                     |
| $      | ท้ายสุดของ string                     |
| .      | ตัวอะไรก็ได้                           |
| \w     | (**w**ord) a-z A-Z 0-9 และ _  |
| \W     | อะไรก็ได้ที่ไม่ใช่ \w                     |
| \d     | (**d**igit) ตัวเลข 0-9              |
| \D     | อะไรก็ได้ที่ไม่ใช่ \d                     |
| \s     | (**s**pace) ช่องว่างรวมถึง \t (แท็บให้ขึ้นย่อหน้าใหม่) \n (new line บ่งบอกการขึ้นบรรทัดใหม่) และ \r (new line แบบของ Windows)   |
| \S     | อะไรก็ได้ที่ไม่ใช่ \s                     |
| \b     | ตัวแบ่งคำ (แบบภาษาอังกฤษ)              |

ข้อสังเกตอย่างหนึ่งเพื่อให้ช่วยจำได้ง่ายขึ้น คือ \w \d และ \s จะจับคู่กับเวอร์ชั่นที่เป็นตัวพิมพ์ใหญ่ซึ่งเป็นเวอร์ชั่นที่เป็นนิเสธของ \w \d และ \s ตามลำดับ เช่น \w หมายถึง a-z A-Z 0-9 และ _ แต่ \W เป็นนิเสธของ \w จึงแมทช์กับอะไรก็ได้ที่ไม่ใช่ a-z A-Z 0-9 และ _ ดังนั้น \W จะจับคู่กับตัวอักษรพิเศษ และช่องว่าง แต่ไม่จับคู่กับตัวอักษรทั่วไป เป็นต้น

#### ตัวอย่าง regex ที่ใช้อักขระพิเศษ 1
`\d\d\d-\d\d\d-\d\d\d\d` เป็น regex  สำหรับแพทเทิร์นของหมายเลขโทรศัพท์ เริ่มต้นด้วยตัวเลข (\d) 3 ตัว ตามด้วยเครื่องหมายขีดกลาง แล้วตามด้วยตัวเลข (\d) 3 ตัว ตามด้วยเครื่องหมายขีดกลาง แล้วตามด้วยตัวเลข (\d) 4 ตัว 

| สตริง | แมทช์กับ regex | คำอธิบาย |
|------|--------------|----------|
| 123-123-1234 |  ✔️ |             |
| 123-123-12345 | ❌ |  เพราะว่ามีตัวเลข 5 ตัว หลังขีดสุดท้าย |
| a23-123-1234 | ❌ |  เพราะว่า \d ตัวแรกไม่แมทช์กับ a |
| ๑๒๓-๑๒๓-๑๒๓๔ | ❌ |  เพราะว่า \d แมทช์กับเลขอารบิกเท่านั้น |

#### ตัวอย่าง regex ที่ใช้อักขระพิเศษ 2
`\w\.\w\.\w\.` เป็น regex สำหรับแพทเทิร์นของตัวย่อที่มีสามตัวอักษร แต่แต่ละตัวอักษรคั่นด้วยจุด เช่น `a.b.c.` `a.b.c.` `a.b.c.` เป็นต้น อย่าลืมว่าเราต้องทำการหนี `.` โดยการใช้ `\.` เพราะ `.` เป็นอักขระพิเศษ

| สตริง | แมทช์กับ regex | คำอธิบาย |
|------|--------------|----------|
| U.S.A. |  ✔️ |             |
| ABC | ❌ |  เพราะว่าไม่มีจุดคั่นตามที่ระบุในแพทเทิร์น |
| พ.ร.บ. | ❌ |  เพราะว่า \w ไม่แมทช์กับตัวอักษรไทย |

อักขระพิเศษถูกออกแบบมาตอนที่ชุดอักขระมีเพียงแค่ตัวลาตินและเครื่องวรรคตอนเท่านั้น เพราะฉะนั้นถึงแม้ว่า \w ถูกออกแบบมาเพื่อจับคู่กับตัวอักษรที่ประกอบขึ้นมาเป็นคำ แต่ว่าไม่ได้ครอบคลุมถึงสตริงไม่ได้ใช้ได้ตัวลาติน เช่น ภาษาไทย ภาษาจีน ภาษาเกาหลี ภาษาญี่ปุ่น  ซึ่งเราจะเรียนรู้วิธีการจับคู่กับสตริงที่ไม่ใช่ตัวลาตินในตัวอย่างต่อไป

### การจัดเซ็ตของตัวอักษร
อักขระพิเศษมีข้อจำกัด เพราะมีการจัดกลุ่มมาแน่นอนอยู่แล้ว เช่น ตัวเลข ตัวอักษรลาติน ช่องว่าง แต่ถ้าหากเราต้องการจัดกลุ่มตัวอักษรตามที่เราต้องการเอง เราสามารถทำได้โดยการใช้เครื่องหมายวงเล็บเหลี่ยม `[]` เพื่อจับกลุ่มตัวอักษร และ `|` เพื่อจัดกลุ่มแพทเทิร์น 

เครื่องหมาย `[]` ใช้ในการระบุว่าตัวอักษรใดบ้างที่จะแมทช์กับแพทเทิร์น เช่น `[abc]` แปลว่าตัวอักษร a หรือ b หรือ c แต่ถ้าหากเราต้องการให้แมทช์กับตัวอักษรที่ไม่ใช่ a หรือ b หรือ c เราสามารถใช้เครื่องหมาย `^` นำหน้าได้ เช่น `[^abc]` แปลว่าตัวอักษรอะไรก็ได้ที่ไม่ใช่ a หรือ b หรือ c สรุปได้ดังนี้

| สัญลักษณ์     | แทนตัวอะไรบ้าง       | ตัวอย่าง                         |
|------------|--------------------|--------------------------------|
| `[abc]`      | ตัวอักษรตัวหนึ่งใน set  | `b[aei]d` match bad bed bid     |
| `[^abc]`     | อะไรก็ได้ที่ไม่อยู่ใน set | `b[^aei]d` match bbd bcd bdd  |
| `aaa\|bb\|c` | aaa หรือ bb หรือ c   | `bea\|ook` match bea ook         |

เครื่องหมาย `-` ที่อยู่ใน `[]` ใช้สำหรับการไล่ตัวอักษร เช่น 
- `[a-z]` แปลว่าตัวอักษรที่อยู่ใน a ถึง z  
- `[0-9]` แปลว่าตัวอักษรที่อยู่ใน 0 ถึง 9 ซึ่งความหมายเหมือนกับ \d


| สัญลักษณ์     | แทนตัวอะไรบ้าง       | ตัวอย่าง                         |
|------------|--------------------|--------------------------------|
| `[a-z]`      | ไล่ตัวอักษรทำเป็น set  | `[b-d]ad` match bad cad dad      |
| `[^abc]`     | อะไรก็ได้ที่ไม่อยู่ใน set | `b[^aei]d` match bbd bcd bdd  |
| `aaa\|bb\|c` | aaa หรือ bb หรือ c   | `bea\|ook` match bea ook         |

### ตัวบอกปริมาณ (quantifier)

เราสามารถระบุปริมาณของตัวอักษรหรือกลุ่มของตัวอักษรโดยการใช้ตัวอักษรร่วมกับ quantifier

| quantifier | แปลว่า                            |
|------------|----------------------------------|
| +          | อย่างน้อยหนึ่งตัว (1 or more)         |
| *          | กี่ตัวก็ได้ หรือไม่มีสักตัวก็ได้ (0 or more) |
| ?          | 1 ตัว หรือไม่มีก็ได้ (0 or 1)          |
| {n}        | n ตัวเป๊ะๆ                         |
| {m,n}      | m - n ตัว                         |
| {n,}       | อย่างน้อย n ตัว                     |
| {,n}       | อย่างมาก n ตัว                     |

ตัวอย่าง

| regex | แปลว่า | ตัวอย่างที่แมทช์ |  
| ----- | ------ | --- | 
| \d+   | ตัวเลขอย่างน้อยหนึ่งตัว | 1113333 
| [ก-ฮ]{2} \d{4} | ตัวอักษรไทย 2 ตัว ตามด้วยตัวเลข 4 ตัว (เลขทะเบียนรถ) |  ตอ 6465 |

#### ตัวอย่าง regex ที่ใช้ตัวบอกปริมาณ 1
`\w+\.\w@chula\.ac\.th` เป็น regex สำหรับแพทเทิร์นของ email address ที่โดเมนคือ chula.ac.th 
- เริ่มต้นด้วยตัวอักษร (\w) หนึ่งตัวขึ้นไป
- ตามด้วยเครื่องหมายจุด ซึ่งเครื่องหมายจุดต้องมีการหนีโดยการใช้ backslash `\.` เพราะ `.` เป็นอักขระพิเศษ
- ตามด้วยตัวอักษร (\w) หนึ่งตัว
- ตามด้วยเครื่องหมาย @
- ตามด้วยคำว่า chula.ac.th ซึ่งเครื่องหมายจุดทั้งสองตัวต้องมีการหนีโดยการใช้ backslash `\.` เพราะ `.` เป็นอักขระพิเศษ 


| สตริง | แมทช์กับ regex | คำอธิบาย |
|------|--------------|----------|
| attapol.t@chula.ac.th |  ✔️ |             |
| 123-123-12345 | ❌ |  เพราะว่ามีตัวเลข 5 ตัว หลังขีดสุดท้าย |
| a23-123-1234 | ❌ |  เพราะว่า \d ตัวแรกไม่แมทช์กับ a |


### การอ้างอิงกลับ (backreference)
การอ้างอิงกลับ (backreference) คือการส่วนที่แมทช์ใน regex มาอ้างถึงอีกครั้ง เหมือนกับการระบุว่าแมทช์แพทเทิร์นเดียวกับที่แมทช์ไปแล้ว ซึ่งก่อนที่จะให้ regex อ้างถึงแพทเทิร์นก่อนหน้านี้ จะต้องมีการจับกลุ่มโดยการใช้วงเล็บ `()`  ในการจัดกลุ่มเพื่อที่จะอ้างถึงได้ในภายหลัง จากนั้นจึงมีการอ้างอิงกลับด้วยหมายเลขกลุ่ม `\1` เพื่ออ้างอิงกลับถึงจับกลุ่มด้วย `()` คู่แรก `\2`เพื่ออ้างอิงกลับถึงจับกลุ่มด้วย `()` คู่ที่สอง เช่น 
```
(\w+) \1 
```
แปลว่าแพทเทิร์นที่ขึ้นตัวด้วยตัวอักษรอย่างน้อยหนึ่งตัว ซึ่งให้เรียกว่ากลุ่มที่ 1 เนื่องจากเราใส่ไว้ในวงเล็บมน จากนั้นตามด้วยช่องว่างหนึ่งช่อง และตามด้วยแพทเทิร์นที่เราแมทช์ไปแล้วในกลุ่มที่หนึ่ง ซึ่งเราใช้ `\1` ในการอ้างถึงกลับ (backreference) ไปยังกลุ่มที่หนึ่ง  ดังนั้น regex นี้จะแมทช์กับสตริงที่มีคำที่ซ้ำกันอยู่ติดกัน เช่น
`hello hello` หรือ `bye bye` หรือ `hi hi` แต่ว่า `hello hi` ไม่แมทช์เพราะว่า `\1` จะต้องแมทช์กับสตริงที่แมทช์กับ regex ใน `()` แรก 

สมมติว่าเราต้องการแมทช์ข้อความที่มีแพทเทิร์น เช่น `มอร์นิ่งค่่ะ มอร์นิ่ง` `ดีค่่ะ ดี` `จบค่่ะ จบ` `แยกย้ายค่่ะ แยกย้าย` แต่ไม่แมทช์กับ `มอร์นิ่งค่่ะ ดี` `ดีค่่ะ จบ` `จบค่่ะ แยกย้าย` เราสามารถใช้ backreference ในการแก้ปัญหานี้ได้ดังนี้
```
^(\w+)ค่ะ \1$
```
คำอธิบาย
- `^` แปลว่าต้องขึ้นต้นด้วย
- `(\w+)` แปลว่าตัวอักษรอย่างน้อยหนึ่งตัว ซึ่งเราใส่ไว้ในวงเล็บเพื่อบ่งบอกว่าการจับกลุ่ม ทำให้สามารถ backreference กลับได้
- `ค่ะ ` เป็นสตริงปกติ
- `\1` แปลว่าอ้างถึงกลุ่มที่หนึ่ง ซึ่งกลุ่มก็คือสตริงที่ถูกแมทช์ด้วย `(\w+)` 

## Regular expression ในภาษาไพธอน
คำสั่งที่เกี่ยวกับ regular expression อยู่ในโมดูล `re` ของไพธอน คำสั่งที่จำเป็นต้องทราบสำหรับการใช้ regular expression มีอยู่ 5 คำสั่ง

| ฟังก์ชัน  | จุดประสงค์การใช้ | 
|--------|--------------|
| `re.match` | ตรวจสอบว่า regex match กับต้นสตริงหรือไม่ | 
| `re.search` | ตรวจสอบว่า regex match กับส่วนใดส่วนหนึ่งของสตริงหรือไม่ | 
| `re.findall` | หาส่วนที่ regex match ทั้งหมด
| `re.sub` | แทนที่ส่วนที่ regex match ด้วยสตริงอีกสตริงหนึ่ง 
| `re.split` | หั่นสตริงออกเป็นลิสต์ โดยใช้ regex เป็นตัวบ่งบอกส่วนที่ใช้หั่นสตริง 

ทั้ง 5 คำสั่งเป็นคำสั่งที่ต้องเราเขียน regex เพื่อระบุแพทเทิร์นที่เราต้องการหา ในภาษาไพธอนเรามักจะระบุ regex โดยการใช้สตริงดิบ หรืออาร์สตริง (raw string หรือ r string) อาร์สตริงมีวิธีการสร้างเหมือนกับสตริงทั่วไปเพียงแต่ว่าเราจะมีตัวอักษร `r` ก่อนเครื่องหมาย `'` หรือ `""` ที่เราใช้นำหน้าสตริงทั่วไป เช่น regex สำหรับหาหมายเลขโทรศัพท์ประเทศไทย 10 หลัก จะเขียนได้เป็น
```python
phone_regex = r'\d\d\d-\d\d\d-\d\d\d\d'
```
จริง ๆ แล้วเราจะใช้สตริงธรรมดาแทนก็ได้ แต่ว่ามีอักขระพิเศษบางสัญลักษณ์ที่สตริงธรรมดา และอาร์สตริงมีความหมายต่างกัน เช่น '\b' ในสตริงธรรมดาหมายถึง backspace แต่ในอาร์สตริงหมายถึงตัวแบ่งคำ ดังนั้นเราจึงควรใช้อาร์สตริงในการเขียน regex แทน

## re.match 
คำสั่งนี้ต้องการ regular expression ที่บ่งบอกแพทเทิร์น และสตริงที่ต้องการจะตรวจสอบ 
```python
import re
match = re.match(r'นาย([ก-์]+)พล ([ก-์]+)', 'นายณัฐพล โคกสูงเนิน')
if not match:
    print ('ชื่อไม่แมทช์กับแพทเทิร์นนี้')
```
คำสั่ง `re.match` จะรีเทิร์น match object กลับมาให้ถ้าหากแพทเทิร์นแมทช์กับสตริงที่ระบุไว้ ถ้าหากไม่เราจะได้ `None` คืนกลับมาแทน 

ถ้าหากเราต้องการทราบด้วยว่าแพทเทิร์นไป match ส่วนใดของสตริงบ้าง เราต้องใช้ match object ที่รีเทิร์นมา และใช้ method ที่ชื่อว่า `.group` ซึ่งจะรีเทิร์นสตริงที่แมทช์กับกลุ่มแพทเทิร์นที่ระบุไว้กลับมาให้ 
```python
import re
match = re.match(r'นาย([ก-์]+)พล ([ก-์]+)', 'นายณัฐพล โคกสูงเนิน')
if not match:
    print ('ชื่อไม่แมทช์กับแพทเทิร์นนี้')
else:
    print (match.group(0)) # นายณัฐพล โคกสูงเนิน
    print (match.group(1)) # ณัฐ
    print (match.group(2)) # โคกสูงเนิน
```
ข้อสังเกตแรกคือเราใช้ `()` ใน regex ข้างต้นเพื่อเป็นการจัดกลุ่มที่เราสามารถอ้างถึงได้ภายหลังด้วยคำสั่ง `.group` โดย group ที่ 0 จะอ้างถึงทั้งแพทเทิร์น ส่วน group ต่อ ๆ มาจะเรียงจากซ้ายไปขวา 

## re.search
คำสั่งคล้ายกับ `re.match` เกือบทุกประการ เพียงแต่ว่าจะคำสั่งนี้จะสแกนหาทั้งสตริง เพื่อหาว่าแพทเทิร์นไปแมทช์กับส่วนใดส่วนหนึ่งของสตริงหรือไม่ ไม่ได้จำกัดแค่ตัวอักษรแรกของสตริงเหมือนกับ `.match` 

```python
import re
match = re.match(r'นาย([ก-์]+)พล ([ก-์]+)', 'ได้เข้าพบนายณัฐพล โคกสูงเนิน') # None เพราะไม่มีแมทช์ตั้งแต่ต้นสตริง
match = re.search(r'นาย([ก-์]+)พล ([ก-์]+)', 'ได้เข้าพบนายณัฐพล โคกสูงเนิน') # match 
print (match.group(0)) # นายณัฐพล โคกสูงเนิน
print (match.group(1)) # ณัฐ
print (match.group(2)) # โคกสูงเนิน
```
match object ที่รีเทิร์นกลับมามีวิธีการใช้เช่นเดิม

## re.findall
คำสั่งนี้ใช้ในสถานการณ์ที่เราทราบว่าแพทเทิร์นที่เราระบุใน regex นั่นเกิดขึ้นซ้ำกันหลาย ๆ ครั้ง และเราต้องการดึงข้อความที่แมทช์กับ regex ทั้งหมดมาเก็บไว้ในลิสต์ ซึ่งต่างจาก `re.search` และ `re.match` ซึ่งจะให้ส่วนของสตริงที่แมทช์มาแค่ส่วนเดียวเท่านั้น

สมมติว่าเราต้องการหาคำที่ลงท้ายด้วย -s ทั้งหมด
```python
import re
pattern = r'\w+s'
sentence = 'James misses the stitches that Carlos fixes'
s_words = re.findall(pattern, sentence)
s_words # --> ['James', 'misses', 'stitches', 'Carlos', 'fixes']
```

สมมติว่าเราต้องการหาคำที่ลงที่เราเติม -es ต่อท้ายเพื่อเปลี่ยนคำนามภาษาอังกฤษให้เป็นพหูพจน์ หรือเปลี่ยนคำกริยาภาษาอังกฤษให้เป็นรูป present tense สำหรับประธานที่เป็นบุรุษที่สามเอกพจน์ กล่าวคือเราต้องการหาคำที่ลงท้ายด้วย -xes -ches -shes -zes -ses ในประโยค
` เท่านั้น เช่น
```python
import re
pattern = r'\w+(x|tch|sh|z|s)es'
sentence = 'James misses the stitches that Carlos fixes'
es_words = re.findall(pattern, sentence)
es_words # --> ['s', 'tch', 'x']
```
ถ้าหาก regex มีการใช้ `()` หนึ่งครั้ง เรารีเทิร์นมาเฉพาะส่วนที่อยู่ใน `() เท่านั้นซึ่งต่างจากตอนที่เราใช้ regex แบบไม่มี `()` ซึ่งจะสตริงที่แมทช์แบบเต็ม ๆ กลับมาให้

แต่ถ้าหาก regex มีการใช้ `()` มากกว่าหนึ่งครั้ง เรารีเทิร์นมาทุกกลุ่ม กลายเป็นลิสต์ขของทูเปิล เช่น
```python
import re
pattern = r'(\w+(x|tch|sh|z|s)es)'
sentence = 'James misses the stitches that Carlos fixes'
es_words = re.findall(pattern, sentence)
es_words # --> [('misses', 's'), ('stitches', 'tch'), ('fixes', 'x')]
```
ในทั้งสองตัวอย่างให้สังเกตว่าคำสั่งนี้จะคืนค่ามาเป็นลิสต์ของสตริง หรือลิสต์ของทูเปิล ไม่ได้คืนค่ามาเป็น match object เหมือนคำสั่ง `re.match` และ `re.search` 

## re.sub
คำสั่งนี้ย่อมาจากภาษาอังกฤษ **sub**stitute แปลว่าการแทนค่า คำสั่งนี้ไว้สำหรับการแทนที่ส่วนของสตริงที่แมทช์กับ regex ด้วยสตริงอื่น ๆ หรือสตริงว่างก็ได้ ซึ่งเป็นคำสั่งที่ใช้บ่อยในการประมวลผลข้อความ 
```
re.sub(regex ที่ต้องการแทนค่า (สตริง), สิ่งที่จะมาแทน (สตริง), สตริงที่ต้องทำการแมทช์และแทนค่า)
```

### ตัวอย่างการใช้งานเบื้องต้น
สมมติว่าเราต้องการแทนที่คำว่า "สวัสดี" ด้วยคำว่า "สวัสดีครับ" ในประโยค ในกรณีนี้เราไม่จำเป็นต้องใช้อักขระพิเศษของ regex เลย สามารถใช้สตริงเป็นแพทเทิร์นได้เลย 

```python
import re
text = 'สวัสดีทุกท่านที่มาร่วมงานในวันนี้'
text = re.sub(r'สวัสดี', 'สวัสดีครับ', text)
text # --> 'สวัสดีครับทุกท่านที่มาร่วมงานในวันนี้'
```

สมมติว่าเราต้องการแทนที่คำว่า "คะ" และ "ค่ะ" ด้วยคำว่า "ครับ" ในกรณีนี้เราจะใช้สัญลักษณ์ `|` ใน regex เพื่อบอกว่าเราต้องการแทนที่คำว่า "คะ" หรือ "ค่ะ" ด้วยคำว่า "ครับ"

```python
import re
text = 'สวัสดีค่ะ ชื่อนัทนะคะ ยินดีรับใช้ค่ะ'
text = re.sub(r'คะ|ค่ะ', 'ครับ', text)
text # --> 'สวัสดีครับ ชื่อนัทนะครับ ยินดีรับใช้ครับ'
```
### ตัวอย่างการใช้งานแบบมี backreference

สมมติว่าเราต้องการเปลี่ยนคำนามที่เป็นรูปพหูพจน์ทีเกิดจากการเติม -es ต่อท้ายคำ ให้กลายเป็นคำนามที่เป็นรูปเอกพจน์ ในกรณีนี้เราจะใช้สัญลักษณ์ `()` ใน regex เพื่อบอกว่าเราต้องการแทนที่ส่วนที่แมทช์กับ regex ด้วยสตริงอื่น ๆ ซึ่งสตริงนั้นจะเป็นส่วนที่อยู่ใน `()` ซึ่งเราสามารถอ้างถึงได้ด้วย `.group` ของ match object ที่รีเทิร์นกลับมาจาก `re.sub` ได้

```python
import re
text = 'James misses the stitches that Carlos fixes'
text = re.sub(r'(\w+)(x|tch|sh|z|s)es', r'\1\2', text)
text # --> 'James miss the stitch that Carlos fix'
```

## re.split
คำสั่งนี้ใช้ในการหั่นสตริงออกเป็นลิสต์ โดยใช้ regex เป็นตัวบ่งบอกส่วนที่ใช้หั่นสตริง คำสั่งนี้คล้ายคลึงกับสตริง method ที่ชื่อว่า `.split` แต่ว่า `re.split` มีความยืดหยุ่นกว่า เพราะว่า `str.split` ต้องระบุตัวแบ่ง (delimiter) เป็นสตริงไม่สามารถระบุเป็นแพทเทิร์นที่ซับซ้อนได้ `re.split` ใช้ regex ในการกำหนดตัวแบ่ง 

สมมติว่าเราต้องการหั่นสตริงด้านล่างออกเป็นลิสต์ โดยใช้เครื่องหมาย `,` หรือ `;` หรือช่องว่างเป็นตัวบ่งบอกส่วนที่ใช้หั่นสตริง ในกรณีนี้เราจะใช้ regex `[,;\s]+` ซึ่งหมายถึงเครื่องหมาย `,` หรือ `;` หรือช่องว่างหนึ่งช่องหรือมากกว่า ในการหั่นสตริงออกเป็นลิสต์ดังนี้
```python
import re
data = "Apples; Oranges, Bananas ;Grapes,Watermelons;Pineapples"
items = re.split(r'[,;\s]+', data)
items # --> ['Apples', 'Oranges', 'Bananas', 'Grapes', 'Watermelons', 'Pineapples']
```

## สรุป
ในบทนี้เราได้เรียนรู้เกี่ยวกับ regular expression ซึ่งเป็นเครื่องมือที่ใช้ในการกำหนดแพทเทิร์นในสตริง โดยใช้อักขระพิเศษต่าง ๆ เช่น  `^ $ . + * ? [ ] { } | ( ) \w \W \d \D \s \S \b` และได้เรียนรู้วิธีการใช้งาน quantifier ใน regular expression ซึ่งประกอบด้วยสัญลักษณ์ `+ * ? {n} {m,n} {n,} {,n}` และได้เรียนรู้วิธีการใช้งานการอ้างอิงกลับ (backreference) 

ภาษาไพธอนมีโมดูลในการทำงานกับ regular expression คำสั่งที่ใช้บ่อย ๆ ในการประมวลข้อมูล ได้แก่ `re.match` `re.search` `re.findall` `re.sub` `re.split` ซึ่งใช้ในการตรวจหาแพทเทิร์นตามที่กำหนดด้วย regular expression ในสถานการณ์ต่าง ๆ 