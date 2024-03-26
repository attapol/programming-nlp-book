# การใช้ไลบรารีเพื่อประมวลผลภาษาธรรมชาติ

การประมวลผลภาษาธรรมชาติ (NLP) ในปัจจุบันมักจะใช้ไลบรารีของภาษาไพธอน เนื่องจากภาษาไพธอนมีไลบรารีที่หลากหลายและมีประสิทธิภาพสูงสำหรับการทำงานด้าน NLP ไลบรารีในที่นี้หมายถึงชุดของโมดูลหรือฟังก์ชันที่ถูกจัดเก็บและจัดระเบียบไว้เพื่อใช้งานร่วมกัน ซึ่งช่วยให้นักพัฒนาสามารถเรียกใช้ฟังก์ชันที่ต้องการได้อย่างง่ายดายโดยไม่ต้องเขียนโค้ดเหล่านั้นจากต้น ทำให้ประหยัดเวลาและลดความซับซ้อนในการพัฒนาโปรแกรม

ไลบรารีให้ความสะดวกในหลายด้าน เช่น การเข้าถึงฟังก์ชันที่ซับซ้อนได้ง่าย การลดระยะเวลาในการพัฒนาโปรแกรม และการใช้งานโค้ดที่ได้รับการทดสอบแล้วจากชุมชนผู้พัฒนา ซึ่งช่วยลดความเสี่ยงในการเกิดบั๊กและปัญหาความปลอดภัย

ในบทนี้ จะกล่าวถึงวิธีการติดตั้งไลบรารีลงในเครื่องผ่านเครื่องมือการจัดการแพ็คเกจ เช่น pip ซึ่งเป็นเครื่องมือมาตรฐานของภาษาไพธอนในการติดตั้งและจัดการไลบรารี จากนั้นจะอธิบายวิธีการใช้งานไลบรารีเหล่านั้นในโปรแกรมไพธอน เพื่อให้ผู้อ่านสามารถนำไปประยุกต์ใช้ในโปรเจกต์ NLP ของตนเองได้ นอกจากนี้ยังจะแนะนำไลบรารีที่ใช้บ่อยในการทำงานด้าน NLP ขั้นพื้นฐาน เช่น NLTK, spaCy, และ pythainlp ซึ่งแต่ละไลบรารีมีคุณสมบัติเฉพาะตัวที่เหมาะสมกับงาน NLP ต่างๆ ตั้งแต่การแยกคำ การแท็กชนิดของคำ ไปจนถึงการสร้างแบบจำลองภาษาที่ซับซ้อน

```{margin} คำศัพท์
ไลบรารี (library) หรือ แพ็กเกจ (package) คือ โค้ดที่สามารถรวมกันเป็นกลุ่มก้อนที่เราสามารถดาวน์โหลดมาใช้ได้เลย 
```

## การติดตั้งไลบรารี
ไลบรารีของภาษาไพธอนถูกจัดเก็บในที่เก็บรวมชื่อว่า PyPI (Python Package Index) ซึ่งเป็นระบบที่เก็บไลบรารีและโมดูลของภาษาไพธอนที่พัฒนาและแชร์โดยชุมชนผู้พัฒนาทั่วโลก การติดตั้งไลบรารีผ่านเครื่องมือจัดการแพ็คเกจเช่น pip หรือ conda จะมีการสื่อสารกับที่เก็บรวมนี้เพื่อดาวน์โหลดและติดตั้งแพ็คเกจที่ต้องการลงในระบบของผู้ใช้ ในกระบวนการนี้ อาจมีขั้นตอนหลังบ้านที่รวมถึงการตรวจสอบการขึ้นต่อกันของไลบรารี (dependencies) 

ไลบรารีที่พบใน PyPI มักจะเป็นแบบโอเพนซอร์ส (open-source) หมายความว่าโค้ดของไลบรารีเหล่านี้เปิดเผยให้สาธารณะสามารถเข้าถึง ใช้งาน แก้ไข และแชร์ต่อได้ เป็นส่วนหนึ่งของวัฒนธรรมการพัฒนาซอฟต์แวร์แบบร่วมมือ ซึ่งส่งเสริมการเรียนรู้ร่วมกันและการนำไปใช้ประโยชน์อย่างกว้างขวาง การเป็นโอเพนซอร์สทำให้ไลบรารีเหล่านี้ได้รับการตรวจสอบ ทดสอบ และพัฒนาอย่างต่อเนื่องจากชุมชนผู้ใช้และผู้พัฒนาทั่วโลก นอกจากนี้ยังช่วยเพิ่มความโปร่งใสและความน่าเชื่อถือของไลบรารีเนื่องจากผู้ใช้สามารถตรวจสอบและทำความเข้าใจการทำงานภายในของไลบรารีเหล่านั้นได้ โอเพนซอร์สยังเป็นแรงบันดาลใจและเป็นฐานสำหรับนวัตกรรมใหม่ๆ เนื่องจากผู้พัฒนาสามารถนำโค้ดที่มีอยู่มาปรับปรุงหรือรวมเข้ากับโปรเจกต์ของตนเองได้โดยไม่ต้องสร้างขึ้นจากศูนย์ เพิ่มความเร็วในการพัฒนาและลดต้นทุนในการวิเคราะห์ข้อมูล หรือสร้างซอฟต์แวร์ใหม่ ๆ

สภาพแวดล้อม (environment) ในบริบทของการพัฒนาซอฟต์แวร์ หมายถึง สภาพแวดล้อมการทำงานที่เราได้ติดตั้งโปรแกรมต่าง ๆ เอาไว้ที่เราจะใช้ในการรันโปรแกรมต่าง ๆ สำหรับในกรณีทั่ว ๆ ไปเรามักจะมีสภาพแวดล้อมเดียว และติดตั้งซอฟต์แวร์ทั้งหมดลงไปในสภาพแวดล้อมเดียวกัน แต่การแยกสภาพแวดล้อมเป็นสิ่งจำเป็นเมื่อทำงานกับโปรเจกต์หลายๆ โปรเจกต์ที่อาจต้องการเวอร์ชันของไลบรารีที่แตกต่างกัน ถ้าเราติดตั้งไพธอนผ่าน miniconda หรือ anaconda จะมีการแยกสภาพแวดล้อมออกมาต่างหากให้อยู่แล้ว และติดตั้ง python interpreter และไลบรารีอื่น ๆ ลงไปในสภาพแวดล้อมนั้น ซึ่งมักจะถูกตั้งชื่อไว้ว่า base หากเราติดตั้งไลบรารีไว้ในสภาพแวดล้อม base แต่ว่าไปใช้ python interpreter ที่อยู่อีกในสภาพแวดล้อมหนึ่ง เราจะไม่สามารถใช้ไลบรารีนั้นได้ เพราะว่าอยู่คนละสภาพแวดล้อมกัน 

```{margin} คำศัพท์
สภาพแวดล้อม (environment) คือ ระบบที่เก็บโปรแกรมและไลบรารีที่เราติดตั้งไว้ เพื่อใช้เป็นบริบทในการรันโปรแกรม 
```

### ติดตั้งไลบรารีโดยใช้ `pip`

`pip install` เป็นคำสั่งในเทอร์มินัลหรือคอมมานด์ไลน์ (ไม่ใช่คำสั่งภาษาไพธอน) ที่ใช้สำหรับการติดตั้งแพ็คเกจจาก PyPI โดยตรง คำสั่งนี้เป็นวิธีที่ง่ายที่สุดในการเพิ่มไลบรารีเข้าไปในสภาพแวดล้อมการพัฒนาภาษาไพธอนของคุณ เช่น `pip install pythainlp` จะดำเนินการดาวน์โหลดและติดตั้งไลบรารี pythainlp เราสามารถตรวจสอบว่าไลบรารีถูกติดตั้งแล้วหรือไม่โดยใช้คำสั่ง `pip list` ซึ่งจะแสดงรายการแพ็คเกจทั้งหมดที่ติดตั้งอยู่ในสภาพแวดล้อมนั้น

ถ้าหากใช้ไพธอนผ่าน jupyter notebook หรือ Google Colab ให้ใช้เครื่องหมาย `!` เพื่อบ่งบอกว่าเราจะใช้คำสั่งในระบบคอมมานด์ไลน์ ตามด้วย `pip install ชื่อไลบรารี` ถ้าหากใช้ผ่านเทอร์มินัล เช่น โปรแกรม Terminal ของแม็ค หรือ โปรแกรม Anaconda Prompt ของวินโดว์ ก็สามารถพิมพ์ `pip install ชื่อไลบรารี` ได้เลย ในทั้งสองกรณีเราจะได้ output ดังตัวอย่างข้างล่าง 
```
Collecting pythainlp
  Downloading pythainlp-5.0.1-py3-none-any.whl (17.9 MB)
     ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━ 17.9/17.9 MB 30.9 MB/s eta 0:00:00
Requirement already satisfied: requests>=2.22.0 in /usr/local/lib/python3.10/dist-packages (from pythainlp) (2.31.0)
Requirement already satisfied: charset-normalizer<4,>=2 in /usr/local/lib/python3.10/dist-packages (from requests>=2.22.0->pythainlp) (3.3.2)
Requirement already satisfied: idna<4,>=2.5 in /usr/local/lib/python3.10/dist-packages (from requests>=2.22.0->pythainlp) (3.6)
Requirement already satisfied: urllib3<3,>=1.21.1 in /usr/local/lib/python3.10/dist-packages (from requests>=2.22.0->pythainlp) (2.0.7)
Requirement already satisfied: certifi>=2017.4.17 in /usr/local/lib/python3.10/dist-packages (from requests>=2.22.0->pythainlp) (2024.2.2)
Installing collected packages: pythainlp
Successfully installed pythainlp-5.0.1
```
คำสั่งนี้จะเริ่มจากการดาวน์โหลดโค้ดของไลบรารี pythainlp และอ่านว่าจะต้องติดตั้งไลบรารีอะไรอื่นก่อนหรือไม่ เพราะว่าไลบรารี pythainlp อาจจะพึ่งพิงไลบรารีอื่น ๆ อีก เราเรียกว่าไลบรารีเหล่านี้ว่า dependencies ในตัวอย่างข้างบนไลบรารี pythainlp พึ่งพาไลบรารีชื่อว่า requests charset-normalizer idna urllib3 certifi เวอร์ชันตามที่ pythainlp เวอร์ชันนี้กำหนดไว้ หลังจากนั้นจึงติดตั้ง pythainlp ลงสภาพแวดล้อมที่เรารันคำสั่ง `pip install` 
 เมื่อเสร็จสิ้นแล้วจะแสดงข้อความว่า `Successfully installed pythainlp-5.0.1` หมายความว่าไลบรารี pythainlp เวอร์ชั่น 5.0.1 ได้ถูกติดตั้งเรียบร้อยแล้ว และเมื่อติดตั้งเสร็จแล้ว ไม่จำเป็นต้องติดตั้งอีกครั้งเมื่อต้องการเรียกใช้ เพราะว่าโค้ดทั้งหมดของไลบรารีนี้ได้ติดตั้งอยู่ในสภาพแวดล้อมนี้ที่อยู่ในเครื่องของเราแล้ว 

 เราสามารถลองรันคำสั่ง `import pythainlp` เพื่อทดสอบอีกครั้งได้ ถ้าหากไม่มีข้อผิดพลาดขึ้น แสดงว่าไลบรารี pythainlp ถูกติดตั้งเรียบร้อยแล้ว แต่ถ้าหากโปรแกรมแจ้งขึ้นมาว่า `ModuleNotFoundError: No module named 'pythainlp'` หมายความว่าไลบรารี pythainlp ไม่ได้ถูกติดตั้ง หรือติดตั้งไม่สำเร็จ

คำสั่ง `pip list` เป็นคำสั่งในระบบจัดการแพ็คเกจที่ใช้สำหรับแสดงรายการของแพ็คเกจที่ได้ติดตั้งไว้ในสภาพแวดล้อมการพัฒนา ณ ขณะนั้น เราสามารถใช้คำสั่งนี้เพื่อตรวจสอบแพ็คเกจต่างๆ ที่ได้รับการติดตั้งแล้ว เวอร์ชันของแพ็คเกจ รวมทั้งเพื่อยืนยันว่าแพ็คเกจที่ต้องการใช้งานได้ถูกติดตั้งเรียบร้อยหรือไม่ การใช้งานคำสั่งนี้ทำได้โดยพิมพ์ `pip list ชื่อไลบรารี` และกด Enter จากนั้นระบบจะแสดงรายชื่อแพ็คเกจที่ติดตั้งอยู่พร้อมกับเวอร์ชันของแต่ละแพ็คเกจออกมา

### ติดตั้งไลบรารีโดยใช้ `conda`

`conda install`  เป็นอีกหนึ่ง
คำสั่งในเทอร์มินัลหรือคอมมานด์ไลน์ ซึ่งใช้ในการติดตั้งไลบรารีผ่านเครื่องมือจัดการไลบรารี คำสั่ง `conda` เป็นส่วนหนึ่งของ Anaconda และ Miniconda เพราะฉะนั้นถ้าเราไม่ได้ติดตั้งภาษาไพธอนผ่าน Anaconda หรือ Miniconda เราจะไม่มีคำสั่ง `conda` เช่น หากเราใช้งานไพธอนผ่าน Google Colab เราก็จะไม่มีคำสั่ง `conda` เพราะว่า Google Colab สร้างสภาพแวดล้อมในการเขียนโค้ดเป็นของมันเอง และไม่ได้ติดตั้งโปรแกรมผ่าน Anaconda คำสั่ง `conda` มีประโยชน์ในการจัดการสภาพแวดล้อมการพัฒนาและไลบรารีสำหรับภาษาไพธอน คำสั่งนี้มีวิธีการใช้งานที่คล้ายกับ `pip` แต่มีคุณสมบัติเพิ่มเติม เช่น สามารถสร้างและจัดการสภาพแวดล้อมการพัฒนาแยกต่างหากได้ การตรวจสอบว่าการติดตั้งด้วย `conda install` เสร็จสมบูรณ์แล้วหรือไม่สามารถทำได้โดยใช้คำสั่ง `conda list` ซึ่งจะแสดงรายการแพ็คเกจที่ติดตั้งในสภาพแวดล้อม Conda นั้นๆ


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