# การประมวลผลภาษาธรรมชาติขั้นพื้นฐาน
Under construction

## การใช้ไลบรารี
เรามักจะใช้ไลบรารีที่เปิดให้ใช้ฟรี และใช้คำสั่งบน terminal `pip install ชื่อไลบรารี` เพื่อติดตั้งลงบนเครื่อง เราควรตรวจสอบว่าเราติดตั้งถูก environment หรือไม่ ถ้าหากใช้บน Colab เราจะต้องติดตั้งไลบรารีที่ต้องการใช้ทุกครั้งที่เปิด Colab ขึ้นมาใช้งาน
```{margin} คำศัพท์
ไลบรารี (library) คือ โค้ดที่สามารถรวมกันเป็นกลุ่มก้อนเพื่อนำมาใช้งานร่วมกัน มักจะพูดถึงโค้ดที่คนอื่นเขียนเอาไว้ให้และเราสามารถดาวน์โหลดลงมาใช้ได้เลย 
```

## Default argument
Default argument เป็น argument ที่เรามีค่า default ให้อยู่แล้วจะใส่เองหรือไม่ใส่เองก็ได้ 

```python
def calc_volume(width, length, height=10):
    return width * length * height

calc_volume(5, 3, 2)
calc_volume(5, 3)
calc_volume(length=3, width=5, height=2)

calc_volume(5)                       # ไม่ได้ เพราะใส่ไม่พอ length ไม่รู้ค่าอะไร
calc_volume(5, 3, height=2)          # จะผสมก็ได้ แต่ต้องใช้ keyword arg หลังสุด
calc_volume(length=2, 5, 10)         # ไม่ได้
calc_volume(length=2, width=5, 10)   # ไม่ได้
```

default argument ใช้กันบ่อยมาก ๆ เวลาใช้ไลบรารีต่าง ๆ
เนื่องจากไลบรารีที่เราใช้ มักจะมีฟังก์ชันที่ต้องใช้ argument เยอะ ๆ 
ข้อดี คือเราสามารถปรับวิธีการใช้งาน function นั้นได้เยอะ
ข้อเสีย คือกว่าจะใช้ได้ต้องเอาค่า argument มาใส่ให้ครบซึ่งทำให้ใช้งานไม่สะดวก และบางทีก็ลืมว่าต้องใส่อะไรบ้าง ลำดับอะไรมาก่อนมาหลัง

วิธีแก้คือใช้ default argument คือใส่ค่า default ไปให้ก่อนเลย แล้วถ้าอยากปรับอะไรก็แก้โดยการใช้ keyword argument ระบุไปเลยว่าอยากจะแก้ค่า argument ตัวไหน โดยไม่ต้องสนใจลำดับที่เรียงอยู่บนฟังก์ชัน

### ตัวอย่างที่ 1
เวลาเราเรียกใช้ split เรามักจะไม่ใช้ argument อะไรเลย เพราะว่า default มันกำหนดมาให้แล้วแต่ว่าจะปรับเป็นอย่างอื่นก็ได้ ดังนี้

- `sep` เราระบุได้ว่าจะใช้อะไรเป็นตัวคั่นกลางในการ split
- `maxsplit` เรากำหนดได้ด้วยว่าจะให้มัน split ได้มากที่สุดกี่ครั้ง

จาก documentation ของ method นี้เราเห็นว่า `maxsplit=-1`  คือมีค่า default เป็น -1 เราจึงไม่จำเป็นต้องตั้งค่าเวลาเรียกใช้ method นี้

```
str.split(sep=None, maxsplit=-1)

Return a list of the words in the string, using sep as the delimiter string. If maxsplit is given, at most maxsplit splits are done (thus, the list will have at most maxsplit+1 elements). If maxsplit is not specified or -1, then there is no limit on the number of splits (all possible splits are made).

If sep is given, consecutive delimiters are not grouped together and are deemed to delimit empty strings (for example, '1,,2'.split(',') returns ['1', '', '2']). The sep argument may consist of multiple characters (for example, '1<>2<>3'.split('<>') returns ['1', '2', '3']). Splitting an empty string with a specified separator returns [''].

If sep is not specified or is None, a different splitting algorithm is applied: runs of consecutive whitespace are regarded as a single separator, and the result will contain no empty strings at the start or end if the string has leading or trailing whitespace. Consequently, splitting an empty string or a string consisting of just whitespace with a None separator returns [].

For example, ' 1  2   3  '.split() returns ['1', '2', '3'], and '  1  2   3  '.split(None, 1) returns ['1', '2   3  '].
```

### ตัวอย่างที่ 2
library nltk มี documentation บอกว่าให้ใช้ฟังก์ชันนี้ในการตัดข้อความให้เป็น list ของประโยค
```
nltk.tokenize.sent_tokenize(text, language='english')

Return a sentence-tokenized copy of text, using NLTK’s recommended sentence tokenizer (currently PunktSentenceTokenizer for the specified language).

Parameters
text – text to split into sentences
language – the model name in the Punkt corpus
```
เราไม่จำเป็นต้องระบุว่ากำลังตัดประโยคภาษาอะไร เพราะว่า default argument ระบุมาแล้วว่าเป็นภาษาอังกฤษ แต่ว่าเราสามารถเปลี่ยนค่านี้ได้

```python
import nltk

nltk.tokenize.sent_tokenize("The U.S. have dots. Mr. Robert met Dr. Evil in the lab.")  

nltk.tokenize.sent_tokenize("The U.S. have dots. Mr. Robert met Dr. Evil in the lab.", language='en')

nltk.tokenize.sent_tokenize("The U.S. have dots. Mr. Robert met Dr. Evil in the lab.", language='fr')

nltk.tokenize.sent_tokenize() # ไม่ได้ เพราะว่าไม่ได้ระบุ required argument
```
