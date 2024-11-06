# เฉลยโจทย์: การเขียนโปรแกรมเชิงอ็อบเจกต์ 

## ข้อ 1

```python
c1 = MyCounter(10) # "I am number 10"
c2 = MyCounter() # TypeError เนื่องจากตัวสร้าง (__init__) ต้องการอาร์กิวเมนต์ number
c3 = MyCounter(15) # "I am number 15"

print(c1.report) # ผลลัพธ์เป็นข้อมูลเกี่ยวกับอ็อบเจกต์ของเมท็อดนั้น เนื่องจากไม่ได้เรียกใช้งานจริง (ไม่ได้ใส่วงเล็บหลังเมท็อด)
print(c1.max_number) # '200'

c1.report() # "I am now number 10"
c3.report() # "I am now number 15"

c1.multiply(2, 5) # TypeError เนื่องจากเมท็อด multiply() ต้องการอาร์กิวเมนต์เดียว
c3.multiply(4)
c1.report() # "I am now number 10"
c3.report() # "I am now number 60"

MyCounter.report() # TypeError เนื่องจากพยายามเรียกใช้เมท็อด report ของคลาส MyCounter โดยตรง แต่ไม่มีการส่ง self 

print (MyCounter.max_number) # '200'
print (c3.max_number) # '200'

c3.contacts.append(10)
MyCounter.append(15) # AttributeError เนื่องจากพยายามเรียกเมท็อด append ของคลาส MyCounter โดยตรง จะเกิดข้อผิดพลาดเพราะ MyCounter ไม่มีเมท็อด append
print(c3.contacts) # '[10]'
print(c1.contacts) # '[10]'
```

## ข้อ 2

```python
my_lex = SentimentLexicon()
french_lex = SentimentLexicon(language='fr')
german_neg_lex = SentimentLexicon('de', 'negative') # "Found a weird polarity: de"

print(my_lex.polarity) # "positive"
print(french_lex.polarity) # "positive"
print(my_lex.add_word)  # ผลลัพธ์เป็นข้อมูลเกี่ยวกับอ็อบเจกต์ของเมท็อดนั้น เนื่องจากไม่ได้เรียกใช้งานจริง (ไม่ได้ใส่วงเล็บหลังเมท็อด)

my_lex.add_word('good')
my_lex.add_word('bon')
print(my_lex.vocab_size()) # '2'
print(french_lex.vocab_size()) # '0'
```

## ข้อ 3

```python
arts_library = Library()

book1 = Book("ภาษาศาสตร์เบื้องต้น")
book2 = Book("ปรัชญาทั่วไป")
arts_library.add_book(book1) # "ภาษาศาสตร์เบื้องต้น added to the library."
arts_library.add_book(book2) # "ปรัชญาทั่วไป added to the library."

arts_library.lend_book("ภาษาศาสตร์เบื้องต้น") # "ภาษาศาสตร์เบื้องต้น lent from the library."
arts_library.lend_book("ภาษาศาสตร์เบื้องต้น") # "Book not available for lending."
arts_library.collect_book("ภาษาศาสตร์เบื้องต้น") # "ภาษาศาสตร์เบื้องต้น collected back to the library."
arts_library.lend_book("Machine Learning Basics") # "Book not available for lending."

arts_library.report() 
# "Books available in the library:
# - ภาษาศาสตร์เบื้องต้น
# - ปรัชญาทั่วไป"
```

## ข้อ 4

```python
account1 = BankAccount(12345, 500)
account1.deposit(200)
account1.withdraw(100) # "Withdrawal successful."
account1.withdraw(700) # "Insufficient funds. Withdrawal not allowed."

print("Current balance:", account1.get_balance()) # "Current balance: 600"
```

## ข้อ 5
```python
student1 = StudentRecord("เอเรน", "S001")
student2 = StudentRecord("มิคาสะ", "S002")
student3 = StudentRecord("อามิน", "S003")


student1.add_course("NLP_SYSTEM") # "Course 'NLP_SYSTEM' added to เอเรน's record."
student2.add_course("USE_IN_DE_INF_WRK") # "Course 'USE_IN_DE_INF_WRK' added to มิคาสะ's record."

student1.view_courses() 
# "Courses enrolled by เอเรน:
# - NLP_SYSTEM"

student1.drop_course("NLP_SYSTEM") # "Course 'NLP_SYSTEM' dropped from เอเรน's record."
student1.drop_course("WEB_DES_DEV") # "Course 'WEB_DES_DEV' not found in เอเรน's record."


student1.view_courses() # "No courses enrolled by เอเรน."

student2.view_courses() 
# "Courses enrolled by มิคาสะ:
# - USE_IN_DE_INF_WRK"

student3.view_courses() # "No courses enrolled by อามิน."
```

## ข้อ 6

```python
profile1 = SocialMediaProfile('user1', bio='I love technology!', followers=1000)
profile2 = SocialMediaProfile('user2', bio='Foodie | Traveler', followers=500)

print(profile2.bio) # "Foodie | Traveler"
print(profile1.add_post) # ผลลัพธ์เป็นข้อมูลเกี่ยวกับอ็อบเจกต์ของเมท็อดนั้น เนื่องจากไม่ได้เรียกใช้งานจริง (ไม่ได้ใส่วงเล็บหลังเมท็อด)

profile1.add_post('Just got a new job at XYZ Corp!')
profile1.add_post('Excited to join the team at ABC Company!')

print(profile1.num_posts()) # '2'
print(profile2.num_posts()) # '0'

print(profile1.get_mentioned_organizations())# "{'XYZ Corp': 1, 'ABC Company': 1}"
```

