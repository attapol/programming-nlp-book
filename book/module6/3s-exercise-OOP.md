# เฉลยโจทย์: Object-Oriented Programming

การเขียนโปรแกรมเชิงอ็อบเจกต์เป็นสิ่งที่เคยได้รับความนิยมอย่างสูงในอดีต ถึงแม้ว่าในปัจจุบันเราอาจไม่จำเป็นต้องใช้ก็ได้ แต่ว่าเราควรจะรู้วิธีการใช้พื้นฐาน อาจจะไม่ต้องใช้สิ่งสืบทอด  หากโค้ดดังกล่าวมีการใช้ OOP เราจะได้สามารถนำโค้ดของผู้อื่นมาประยุกต์ใช้ได้ แบบฝึกหัดนี้จะช่วยส่งเสริมความเข้าใจในเรื่องการใช้ OOP ซึ่งจำเป็นต่อการนำไปประยุกต์ใช้ในงานโปรแกรมมิ่งที่เกี่ยวข้องกับการสร้างคลาส (class)

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

จากโค้ดด้านล่างนี้ จงวิเคราะห์ว่าแต่ละบรรทัดจะแสดงผลลัพธ์อย่างไรบ้าง หรืออาจจะเกิดข้อผิดพลาด

```python
c1 = MyCounter(10) # "I am number 10"
c2 = MyCounter() # TypeError เนื่องจากคอนสตรัคเตอร์ (__init__) ต้องการอาร์กิวเมนต์ number
c3 = MyCounter(15) # "I am number 15"

print(c1.report) # ผลลัพธ์เป็นข้อมูลเกี่ยวกับอ็อบเจกต์ของเมธอดนั้น เนื่องจากไม่ได้เรียกใช้งานจริง (ไม่ได้ใส่วงเล็บหลังเมธอด)
print(c1.max_number) # '200'

c1.report() # "I am now number 10"
c3.report() # "I am now number 15"

c1.multiply(2, 5) # TypeError เนื่องจากเมธอด multiply() ต้องการอาร์กิวเมนต์เดียว
c3.multiply(4)
c1.report() # "I am now number 10"
c3.report() # "I am now number 60"

MyCounter.report() # TypeError เนื่องจากพยายามเรียกใช้เมธอด report ของคลาส MyCounter โดยตรง แต่ไม่มีการส่งอินสแตนซ์ (self) 

print (MyCounter.max_number) # '200'
print (c3.max_number) # '200'

c3.contacts.append(10)
MyCounter.append(15) # AttributeError เนื่องจากพยายามเรียกเมธอด append ของคลาส MyCounter โดยตรง จะเกิดข้อผิดพลาดเพราะ MyCounter ไม่มีเมธอด append
print(c3.contacts) # '[10]'
print(c1.contacts) # '[10]'
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

จากโค้ดด้านล่างนี้ จงวิเคราะห์ว่าแต่ละบรรทัดจะแสดงผลลัพธ์อย่างไรบ้าง หรืออาจจะเกิดข้อผิดพลาด
```python
my_lex = SentimentLexicon()
french_lex = SentimentLexicon(language='fr')
german_neg_lex = SentimentLexicon('de', 'negative') # "Found a weird polarity: de"

print(my_lex.polarity) # "positive"
print(french_lex.polarity) # "positive"
print(my_lex.add_word)  # ผลลัพธ์เป็นข้อมูลเกี่ยวกับอ็อบเจกต์ของเมธอดนั้น เนื่องจากไม่ได้เรียกใช้งานจริง (ไม่ได้ใส่วงเล็บหลังเมธอด)

my_lex.add_word('good')
my_lex.add_word('bon')
print(my_lex.vocab_size()) # '2'
print(french_lex.vocab_size()) # '0'
```

## ข้อ 3
สมมติว่าเรามีคลาสชื่อ `Library` และ `Book` ดังนี้
```python
class Library:
    def __init__(self):
        self.books = []

    def add_book(self, book):
        self.books.append(book)
        print(f"{book.title} added to the library.")

    def lend_book(self, book_title):
        for book in self.books:
            if book.title == book_title and book.available:
                book.available = False
                print(f"{book.title} lent from the library.")
                return
        print("Book not available for lending.")

    def collect_book(self, book_title):
        for book in self.books:
            if book.title == book_title and not book.available:
                self.books.append(book)
                book.available = True
                print(f"{book.title} collected back to the library.")
                return
        print("Book not found or already available in the library.")

    def report(self):
      if self.books:
          print("Books available in the library:")
          for book in self.books:
              print("-", book.title)
      else:
          print("No books available in the library.")

class Book:
    def __init__(self, title):
        self.title = title
        self.available = True
```

จากโค้ดด้านล่างนี้ จงวิเคราะห์ว่าแต่ละบรรทัดจะแสดงผลลัพธ์อย่างไรบ้าง หรืออาจจะเกิดข้อผิดพลาด
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
สมมติว่าเรามีคลาสชื่อ `BankAccount` ดังนี้
```python
class BankAccount:
        
    def __init__(self, account_number, initial_balance=0):
        self.account_number = account_number
        self.balance = initial_balance

    def deposit(self, amount):
        self.balance += amount

    def withdraw(self, amount):
        if amount <= self.balance:
            self.balance -= amount
            print("Withdrawal successful.")
        else:
            print("Insufficient funds. Withdrawal not allowed.")

    def get_balance(self):
        return self.balance
```

จากโค้ดด้านล่างนี้ จงวิเคราะห์ว่าแต่ละบรรทัดจะแสดงผลลัพธ์อย่างไรบ้าง หรืออาจจะเกิดข้อผิดพลาด
```python
account1 = BankAccount(12345, 500)
account1.deposit(200)
account1.withdraw(100) # "Withdrawal successful."
account1.withdraw(700) # "Insufficient funds. Withdrawal not allowed."

print("Current balance:", account1.get_balance()) # "Current balance: 600"
```

## ข้อ 5
สมมติว่าเรามีคลาสชื่อ `StudentRecord` ดังนี้
```python
class StudentRecord:
    def __init__(self, name, roll_number):
        self.name = name
        self.roll_number = roll_number
        self.courses = []

    def add_course(self, course):
        self.courses.append(course)
        print(f"Course '{course}' added to {self.name}'s record.")

    def drop_course(self, course):
        if course in self.courses:
            self.courses.remove(course)
            print(f"Course '{course}' dropped from {self.name}'s record.")
        else:
            print(f"Course '{course}' not found in {self.name}'s record.")

    def view_courses(self):
        if self.courses:
            print(f"Courses enrolled by {self.name}:")
            for course in self.courses:
                print("-", course)
        else:
            print(f"No courses enrolled by {self.name}.")

```

จากโค้ดด้านล่างนี้ จงวิเคราะห์ว่าแต่ละบรรทัดจะแสดงผลลัพธ์อย่างไรบ้าง หรืออาจจะเกิดข้อผิดพลาด
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
สมมติว่าเรามีคลาสชื่อ `SocialMediaProfile` ดังนี้
```python
class SocialMediaProfile:
    def __init__(self, username, bio='', followers=0):
        self.username = username
        self.bio = bio
        self.followers = followers
        self.posts = []
        self.mentioned_organizations = {}
 
    def add_post(self, post_content):
        self.posts.append(post_content)
        self.extract_and_track_organizations(post_content)
 
    def num_posts(self):
        return len(self.posts)
    
    def extract_and_track_organizations(self, text):
        organizations = ['XYZ Corp', 'ABC Company', 'Tech Inc']
        for org in organizations:
            if org.lower() in text.lower():
                self.mentioned_organizations[org] = self.mentioned_organizations.get(org, 0) + 1
    
    def get_mentioned_organizations(self):
        return self.mentioned_organizations
```

จากโค้ดด้านล่างนี้ จงวิเคราะห์ว่าแต่ละบรรทัดจะแสดงผลลัพธ์อย่างไรบ้าง หรืออาจจะเกิดข้อผิดพลาด
```python
profile1 = SocialMediaProfile('user1', bio='I love technology!', followers=1000)
profile2 = SocialMediaProfile('user2', bio='Foodie | Traveler', followers=500)

print(profile2.bio) # "Foodie | Traveler"
print(profile1.add_post) # ผลลัพธ์เป็นข้อมูลเกี่ยวกับอ็อบเจกต์ของเมธอดนั้น เนื่องจากไม่ได้เรียกใช้งานจริง (ไม่ได้ใส่วงเล็บหลังเมธอด)

profile1.add_post('Just got a new job at XYZ Corp!')
profile1.add_post('Excited to join the team at ABC Company!')

print(profile1.num_posts()) # '2'
print(profile2.num_posts()) # '0'

print(profile1.get_mentioned_organizations())# "{'XYZ Corp': 1, 'ABC Company': 1}"
```

