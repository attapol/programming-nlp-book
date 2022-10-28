# โจทย์: Object-Oriented Programming

Object-oriented programming เป็นสิ่งที่เคยนิยมรุ่งเรืองในอดีตมาก ๆ ซึ่งจริงๆ เราก็ไม่จำเป็นต้องใช้ก็ได้ แต่ว่าเราควรจะรู้วิธีการใช้พื้นฐาน (คืออาจจะไม่ต้องใช้ Inheritance) เพื่อที่เราจะได้นำโค้ดของคนอื่นมาใช้ได้ ถ้าโค้ดเหล่านั้นมีการใช้ OOP แบบฝึกหัดนี้จะช่วยส่งเสริมความเข้าใจเรื่องการใช้ OOP ซึ่งจำเป็นต่อการ implement class

## ข้อ 1

สมมติว่าเรามีคลาสชื่อ `MyCounter` ดังนี้
```python
class MyCounter:
       max_number = 200
       contacts = []
 
   def __init__(self, number):
       self.number = number
       print ("I am number " + str(self.number))
 
   def report(self):
       print ("I am now number " + str(self.number))
 
   def multiply(self, factor):
       self.number = self.number * factor
```

จากโค้ดข้างล่างนี้ให้ลองคิดว่า แต่ละบรรทัดจะ print อะไรออกมาบ้าง หรือว่ามันจะเกิด error แทน

```python
c1 = MyCounter(10)
c2 = MyCounter()
c3 = MyCounter(15)

print(c1.report)
print(c1.max_number)

c1.report()
c3.report()

c1.multiply(2, 5)
c3.multiply(4)
c1.report()
c3.report()

MyCounter.report()
print (MyCounter.max_number)
print (c3.max_number)

c3.contacts.append(10)
MyCounter.append(15)
print(c3.contacts)
print(c1.contacts)
```

## ข้อ 2
สมมติว่าเรามีคลาสชื่อ `SentimentLexicon` ดังนี้
```python
class SentimentLexicon:
        
   def __init__(self, polarity='positive', language='en'):
       self.language = language
       self.words = []
       if polarity in ['positive', 'negative', 'neutral']:
           self.polarity = polarity
       else:
           print('Found a weird polarity: {}'.format(polarity))
 
   def add_word(self, word):
       self.words.append(word)
 
   def vocab_size(self):
       return len(self.words)
```

จากโค้ดข้างล่างนี้ให้ลองคิดว่า แต่ละบรรทัดจะ print อะไรออกมาบ้าง หรือว่ามันจะเกิด error แทน
```python
my_lex = SentimentLexicon()
french_lex = SentimentLexicon(language='fr')
german_neg_lex = SentimentLexicon('de', 'negative')

print(my_lex.polarity)
print(french_lex.polarity)
print(my_lex.add_word)

my_lex.add_word('good')
my_lex.add_word('bon')
print(my_lex.vocab_size())
print(french_lex.vocab_size())
```
