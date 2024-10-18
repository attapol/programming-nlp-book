# เฉลยโจทย์: ชนิดของโครงสร้างข้อมูล

## ข้อ 1 
```python
name_to_phone_list = \
{ ('Mark', 'Wahlberg') : ['111-222-3333', '444-555-6666'] ,
  ('Jane', 'Doe'): ['222-333-4444'],
  ('Jane', 'Eyre'): ['333-444-5555', '777-555-1111']
}

name_to_phone_list[('Jane', 'Eyre')] # คืนค่าลิสต์ของสตริง
name_to_phone_list[('Jane', 'Eyre')][1] # คืนค่าสตริง
for x in name_to_phone_list:
    print(x)  # x เป็นทูเปิล (สตริง, สตริง)
```

## ข้อ 2
```python
animal = [ {'dog':['ear','leg','tail','bark'],'cat':['eye','ear','tail']},
{'snake':['poison','tongue'],'frog':['hop','insect','rain']}]

animal[1] # คืนค่าดิกชันนารี (สตริง -> ลิสต์)
animal[0]['cat'] # คืนค่าลิสต์ของสตริง
animal[1]['frog'][1] # คืนค่าสตริง
for x in animal:
    print(x)  # x เป็นดิกชันนารี (สตริง -> ลิสต์)
```

## ข้อ 3
```python
news_dic = {
  "headers": {
    "Cache-Control": "public, max-age=300, must-revalidate"
  },
  "lastModified": "2020-07-06T11:01:00+07:00",
  "items": {
    "content": [
      {
        "news_id": 85089,
        "title": "ฮือฮา! ชาวบ้านแห่กราบไหว้ใบไม้สิบแฉก",
        "publishTime": "2020-08-11T12:50:00+07:00",
        "tags": [
          "ความเชื่อ",
          "ไสยศาสตร์",
          "เรื่องอัศจรรย์",
          "ข่าวฮิต"
        ],
        "url": "www.khaodee.com/85089"
      },
      {
        "news_id": 96686,
        "title": "กระทรวงศึกษาธิการชี้ ทำร้ายร่างกายนักเรียนมีความผิด",
        "publishTime": "2020-08-21T17:19:00+07:00",
        "tags": [
          "กระทรวงศึกษา",
          "กระทรวงศึกษิการ",
          "ความรุนแรงในโรงเรียน",
          "ทำร้ายร่างกาย"
        ],
        "url": "www.khaodee.com/96686"
      },
      {
        "news_id": 19286,
        "title": "โลกตะลึง! นาซ่าพบสิ่งมีชีวิตบนดวงจันทร์",
        "publishTime": "2020-08-05T19:41:00+07:00",
        "tags": [
          "นาซ่า",
          "มนุษย์ต่างดาว",
          "อวกาศ",
          "จักรวาล"
        ],
        "url": "www.khaodee.com/19286"
      }
    ]
  }
}


news_dic['items']['content'] # คืนค่าลิสต์ของดิกชันนารี
news_dic['items']['content'][1]['tags'] # คืนค่าลิสต์ของสตริง
for x in news_dic:
    print(x)  # x เป็นสตริง (คีย์ของดิกชันนารี)
```

## ข้อ 4

```python
student_lst = 
[({'student_id': 1710501115187,
   'name': 'Weiying',
   'class_attended': ['History', 'Math', 'Chinese']},
  ['A', 99.88, 'S']),
 ({'student_id': 1030102285053,
   'name': 'Lelouch',
   'class_attended': ['Japanese', 'Politics', 'Material Arts']},
  ['A', 100, 'U']),
 ({'student_id': 2584275888067,
   'name': 'Tunjiro',
   'class_attended': ['Japanese', 'Economics', 'Programming']},
  ['B+', 80, 'S']),
 ({'student_id': 4080802291786,
   'name': 'Somsak',
   'class_attended': ['Thai', 'Math', 'Science']},
  ['C+', 50, 'S'])]

for info, score in student_lst: 
   print(info, score)
```
1. `score` เป็นลิสต์ [สตริง, เลขจำนวนเต็ม, สตริง]
2. `info` เป็นดิกชันนารี
3. `student_lst[0][0]` เป็นดิกชันนารี


## ข้อ 5
```python
phoneme_pairs = 
[{'vowel': [{('i', 'e'): {'fnLoad': 0.0438, 'predictability': 0.93}},
            {('i', 'ɛ'): {'fnLoad': None, 'predictability': 0.89}},
            {('ɛ', 'e'): {'fnLoad': 0.0188, 'predictability': 0.995}}
            ]
 },
 {'consonant': [{('b', 'p'): {'fnLoad': 0.06, 'predictability': 0.763}},
                {('t', 'd'): {'fnLoad': 0.0588, 'predictability': 0.611}}
                ]
 }
]
```
1. `phoneme_pairs[0]['vowel']` คืนค่าลิสต์ของดิกชันนารี
2. `phoneme_pairs[0]['vowel'][1][("i", "ɛ")]["fnLoad"]` คืนค่า None


## ข้อ 6
```python
homework_info = 
{'AM001': {'name': ('Mr.', 'Robert', 'Kim'),
            'score': 15,
            'lateStatus': False,
            'subject': 'American History',
            'wordCount': 500},
 'AM002': {'name': ('Mr.', 'Francis', 'Owen'),
            'score': 20,
            'lateStatus': True,
            'subject': 'American History',
            'wordCount': 520},
 'LT001': {'name': ('Ms.', 'Rebecca', 'Lawrence'),
            'score': 20,
            'lateStatus': False,
            'subject': 'Literature',
            'wordCount': 348}
}
```
`homework_info["AM002"]['lateStatus']` คืนค่าบูลีน

## ข้อ 7
```python
required_langtech_course = {
    '2206323':{'subject_name':'INFO SYS HUMAN',
                'credit':3.0,
                'semester':1,
                'day':'Tuesday',
                'time':'13:00-16:00'
                },
    '2209261':{'subject_name':'BASIC PROG NLP',
                'credit':3.0,
                'semester':1,
                'day':'Friday',
                'time':'13:30-16:30'
                },
    '2209304':{'subject_name':'GRAM SYSTEM',
                'credit':3.0,
                'semester':1,
                'day':'Thursday',
                'time':'9:30-12:30'
                },
    '2209308':{'subject_name':'SOUND SYSTEM',
                'credit':3.0,
                'semester':1,
                'day':'Wednesday',
                'time':'13:00-16:00'
                },
    '2206385':{'subject_name':'DATA MGT HUMAN',
                'credit':3.0,
                'semester':2,
                'day':'Tuesday',
                'time':'13:00-16:00'
                },
    '2209305':{'subject_name':'MEANING LANG',
                'credit':3.0,
                'semester':2,
                'day':'Wednesday',
                'time':'9:30-12:30'
                },
    '2209372':{'subject_name':'INTRO COMPU LING',
                'credit':3.0,
                'semester':2,
                'day':'Thursday',
                'time':'9:30-12:30'
                },
    '2209368':{'subject_name':'LING ANALYS THAI',
                'credit':3.0,
                'semester':1,
                'day':'Thursday',
                'time':'9:30-12:30'
                },
    '2206366':{'subject_name':'STAT HUMAN RES',
                'credit':3.0,
                'semester':1,
                'day':'Thursday',
                'time':'13:00-16:00'
                }
}
```
1. `required_langtech_course['2209368']['time']` คืนค่าสตริง 
2. `required_langtech_course['2209368']` คืนค่าดิกชันนารี

## ข้อ 8 
```python
s = [['I am a student', 'You are also a student.'], 
      ['You are right', 'You are correct']]
s[1][0].split(' ') # คือ ลิสต์ของสตริง

t = [ (1120, {'status': 12, 'enc': '458df', 'contact': [230, 460, 125]}) ,
      (2506, {'status': 0, 'enc': 'cvirg', 'contact': [1120, 508]}) ,
      (508, {'status': 1, 'enc': '9kjb3', 'contact': [77, 2506]}) ]
for x in t:
	x[1] # คือ ดิกชันนารี

results = []
for i, y in t:
	for k in y.keys():
		k # คือ สตริง
	results.append(i)
results # คือ ลิสต์ของเลขจำนวนเต็ม
```