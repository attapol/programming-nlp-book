# เฉลยโจทย์: การประยุกต์ใช้มเดลภาษาขนาดใหญ่

## 1. วิเคราะห์อารมณ์ผู้พูด

```python
import openai

def analyze_emotion(text):
    prompt = f"""บทสนทนา:
{text}

จงวิเคราะห์อารมณ์ของผู้พูดในข้อความข้างต้น และระบุว่าเป็นหนึ่งในประเภทต่อไปนี้:
'ดีใจ', 'เศร้า', 'โกรธ', 'แปลกใจ', หรือ 'อื่นๆ'
ตอบเพียงคำเดียวในบรรทัดเดียว เช่น: เศร้า
"""
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    return response.choices[0].message['content'].strip()
```

## 2. สรุปความ

```python
def convert_to_bullet_points(text, num_points):
    if num_points > 8:
        print("ห้ามระบุเกิน 8 ข้อ")
        return []

    prompt = f"""ข้อความ:
{text}

จงสรุปเนื้อหาจากข้อความข้างต้น โดยที่บทสรุปจะต้องมีลักษณะดังนี้
- เป็น bullet point ทั้งหมด {num_points} ข้อเท่านั้น
- ไม่ต้องมีสัญลักษณ์ใด ๆ นำหน้าบทสรุปแต่ละข้อ 
- แต่ละข้ออยู่คนละบรรทัด 
- ห้ามมีข้อความอื่น ๆ นอกเหนือจากบทสรุปติดมาด้วย
"""
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    return response.choices[0].message['content'].strip().split('\n')
```

## 3. ตรวจเรียงความ 
```python
import json

def grade_feedback_essay(essay):
    prompt = f"""เรียงความ:
{essay}

จากเรียงความข้างต้น ให้คืน output ในรูปแบบ JSON ดังนี้

grade: คะแนนของเรียงความนี้จาก 1 ถึง 5 โดยมีเกณฑ์ดังนี้:
- 1 = ต่ำกว่ามาตรฐานระดับมัธยมปลาย
- 3 = เทียบเท่าระดับมัธยมปลาย
- 5 = เทียบเท่าระดับคนวัยทำงาน

feedback: ข้อเสนอแนะในการพัฒนาการเขียนเรียงความ โดยต้องมีลักษณะดังนี้
- เป็นภาษาไทย 
- ยกส่วนของเรียงความที่ต้องการแก้ไขให้เด่นชัด
"""
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    return json.loads(response.choices[0].message['content'])
```


## 4. วิเคราะห์คำศัพท์
```python
import pandas as pd
from io import StringIO

def analyze_vocab(article, output_csv_path):
    prompt = f"""บทความภาษาอังกฤษ:
{article}

จงดึงคำศัพท์สำคัญจากบทความนำมาจัดอยู่ในรูปแบบของ csv ที่มีคอลัมน์ดังนี้
word: คำ
translation_th: คำแปลไทย 
difficulty: ระดับความยากของคำศัพท์ (ง่าย / ปานกลาง / ยาก) 
example: ดึงประโยคในบทความที่มีคำ ๆ นั้นอยู่ 

ห้ามนำเอาข้อความอย่างอื่นนอกเหนือจากข้อมูลใน csv ติดมาด้วย
"""
    response = openai.ChatCompletion.create(
        model="gpt-4",
        messages=[{"role": "user", "content": prompt}]
    )
    csv_text = response.choices[0].message['content']
    df = pd.read_csv(StringIO(csv_text))
    df.to_csv(output_csv_path, index=False)
    return df
```

