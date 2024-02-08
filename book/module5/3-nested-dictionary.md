# ดิกชันนารีที่เก็บโครงสร้างข้อมูลอื่นอยู่

Under construction
## ดิกชันนารีที่ key เป็นทูเปิล


```{figure} img/dict-tuple.jpeg
---
height: 100px
align: center
---
ภาพอธิบายโครงสร้างของดิกชันนารี
```

```python
friend_list = [ ('Mark', 'Wahlberg', '111-222-3333'),
  ('Jane', 'Doe', '222-333-4444'),
  ('Jane', 'Eyre', '333-444-5555')
]

friend_to_phone = { ('Mark', 'Wahlberg') : '111-222-3333',
  ('Jane', 'Doe'): '222-333-4444',
  ('Jane', 'Eyre'): '333-444-5555'
}
```

```python
def find_mark_from_list(friend_list):
query = ('Mark', 'Wahlberg')
for entry in friend_list:
	first, last, phone = entry
	first_last = (first, last)
	if query == first_last: 
		return phone
```

```python
def find_mark_from_dict(friend_to_phone):
    query = ('Mark', 'Wahlberg')
    return friend_to_phone[query]
```

Under construction

## ดิกชันนารีที่ value เป็นลิสต์

Under construction

## ดิกชันนารีที่ value เป็นดิกชันนารี

Under construction