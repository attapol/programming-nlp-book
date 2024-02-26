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

จากโค้ดข้างล่างนี้ให้ลองคิดว่า แต่ละบรรทัดจะ print อะไรออกมาบ้าง หรือว่ามันจะเกิด error แทน
```python
arts_library = Library()

book1 = Book("ภาษาศาสตร์เบื้องต้น")
book2 = Book("ปรัชญาทั่วไป")
arts_library.add_book(book1)
arts_library.add_book(book2)

arts_library.lend_book("ภาษาศาสตร์เบื้องต้น")
arts_library.lend_book("ภาษาศาสตร์เบื้องต้น")
arts_library.collect_book("ภาษาศาสตร์เบื้องต้น")
arts_library.lend_book("Machine Learning Basics")
arts_library.report()
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

จากโค้ดข้างล่างนี้ให้ลองคิดว่า แต่ละบรรทัดจะ print อะไรออกมาบ้าง หรือว่ามันจะเกิด error แทน
```python
account1 = BankAccount(12345, 500)
account1.deposit(200)
account1.withdraw(100)
account1.withdraw(700)

print("Current balance:", account1.get_balance())
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

จากโค้ดข้างล่างนี้ให้ลองคิดว่า แต่ละบรรทัดจะ print อะไรออกมาบ้าง หรือว่ามันจะเกิด error แทน
```python
student1 = StudentRecord("เอเรน", "S001")
student2 = StudentRecord("มิคาสะ", "S002")
student3 = StudentRecord("อามิน", "S003")


student1.add_course("NLP_SYSTEM")
student2.add_course("USE_IN_DE_INF_WRK")

student1.view_courses()

student1.drop_course("NLP_SYSTEM")
student1.drop_course("WEB_DES_DEV")


student1.view_courses()
student2.view_courses()
student3.view_courses()
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

จากโค้ดข้างล่างนี้ให้ลองคิดว่า แต่ละบรรทัดจะ print อะไรออกมาบ้าง หรือว่ามันจะเกิด error แทน
```python
profile1 = SocialMediaProfile('user1', bio='I love technology!', followers=1000)
profile2 = SocialMediaProfile('user2', bio='Foodie | Traveler', followers=500)

print(profile2.bio)
print(profile1.add_post)

profile1.add_post('Just got a new job at XYZ Corp!')
profile1.add_post('Excited to join the team at ABC Company!')

print(profile1.num_posts())
print(profile2.num_posts())

print(profile1.get_mentioned_organizations())
```

