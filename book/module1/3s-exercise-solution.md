# เฉลยแบบฝึกหัด: แคเริล

## โจทย์แบบฝึกหัด
### ข้อ 1
`collect_newspaper_karel.py` จงเขียนโปรแกรมสั่งให้แคเริลหยิบ beeper และเดินกลับมาที่เดิม โดยให้เขียนฟังก์ชันย่อยตามหลักการย่อยโจทย์ (decomposition) เพื่อทำให้โค้ดดูสะอาดตา อ่านง่ายเข้าใจง่ายขึ้น 
```python
def main():
    """
    แนวทางการคิดคือ แบ่งงานออกเป็นขาเดินไปเก็บ beeper และขาเดินกลับไปวาง beeper ที่จุดเริ่มต้น
    """
    go_collect()
    return_home()

# ฟังก์ชันย่อย
def go_collect():
    turn_right()
    move()
    turn_left()
    for i in range(3):
        move()
    pick_beeper()

def return_home():
    turn_around()
    for i in range(3):
        move()
    turn_right()
    move()
    put_beeper()

def turn_right():
    for i in range(3):
        turn_left()

def turn_around():
    for i in range(2):
        turn_left()
```

### ข้อ 2 
`corner_to_corner_karel.py`  จงเขียนโปรแกรมสั่งให้แคเริล วิ่งจากจุดเริ่มต้นที่มุมซ้ายล่างไปมุมขวาบน โดยที่เราไม่รู้ว่า world จะมีขนาดเท่าไร ให้ลองทดสอบกับ world หลายๆ แบบ
```python
def main():
    """
    แนวทางการคิด
    1. เดินไปเรื่อยๆ จนกว่าจะเจอทางตัน + หันซ้าย + เดินไปเรื่อยๆ จนกว่าจะเจอทางตัน
    2. ใช้ while front_is_clear เพื่อให้ karel เดินไปเรื่อยๆ จนกว่าจะเจอทางตัน
    """
    # 1. ซ้ายล่าง -> ขวาล่าง
    move_l()
    # 2. ซ้ายหัน
    turn_left()
    # 3. ขวาล่าง -> ขวาบน
    move_l()

# ฟังก์ชันย่อย
def move_l():
    # เดินหน้าจนกว่าจะเจอทางตัน
    while front_is_clear():
        move()
```

### ข้อ 3 
`four_corner_karel.py` จงเขียนโปรแกรมสั่งให้แคเริลวาง beeper ไปทั้งสี่มุม มุมละ 3 beeper โดยที่เราไม่รู้ว่า world จะมีขนาดเท่าไร ให้ลองทดสอบกับ world หลายๆ แบบ
```python
def main():
    """
    แนวทางการคิด
    1. รูปแบบการเดินคือ เดินไปจนสุดทาง + วาง beeper
    2. หันซ้ายเพื่อเดินแนวต่อไป
    3. เดินรอบกรอบสี่เหลี่ยม ใช้ for loop เพื่อวน 4 รอบ
    """
    for i in range(4):
        walk_to_wall_and_put_beeper()
        turn_left()

# ฟังก์ชันย่อย
def walk_to_wall_and_put_beeper():
    # เดินต่อไปถ้าข้างหน้ายัง clear
    while front_is_clear():
        move()
    # เมื่อหยุดเดินแล้วแล้ว วาง beeper
    put_beeper()
```

### ข้อ 4
`roomba_karel.py`  จงเขียนโปรแกรมสั่งให้แคเริลเก็บ beeper ที่กระจัดกระจายอยู่ทั้งห้อง โดยโปรแกรมจะต้องทำงานทั้ง `roomba_karel.w` และ `roomba_karel2.w`
```python
def main():
    """
    แนวทางการคิด
    1. หาวิธีเดินให้ได้ครบทุกช่องก่อน
    2. พอเดินได้ครบทุกช่องแล้ว ก็ค่อยเพิ่มการ pick beepers ไปในทุกช่องที่เดินผ่าน
    3. Done

    Trick:
    ก่อนขึ้นแถวถัดไปให้เดินกลับมาช่องเดิมก่อน
    จะช่วยให้เขียนเงื่อนไขการเปลี่ยนแถวได้ง่ายขึ้น
    เพราะจะอยู่ในสภาวะเดียวกันทุกครั้ง
    """
    # 1. เก็บแถวแรก
    clean_row()
    # 2. เดินกลับมาจุดเริ่มต้น
    come_back()
    # 3. ถ้าขวาว่าง เท่ากับยังมีแถวต่อไป ก็เปลี่ยนแถวแล้ว clean แถวใหม่วนไป
    while right_is_clear():
        # ขึ้นไปแถวใหม่
        turn_right()
        move()
        turn_right()
        # ทำเหมือนแถวแรกอีกครั้ง
        clean_row()
        come_back()

# ฟังก์ชันย่อย
def turn_right():
    turn_left()
    turn_left()
    turn_left()

def clean_beepers():
    # เก็บ beeper จนกว่าจะไม่เหลือ
    while beepers_present():
        pick_beeper()

def clean_row():
    # เก็บช่องแรก
    clean_beepers()
    # เดินไปเก็บช่องที่เหลือในแถว
    while front_is_clear():
        move()
        clean_beepers()

def come_back():
    # กลับหลังหัน
    turn_left()
    turn_left()
    # เดินไปจนสุด
    while front_is_clear():
        move()
```

### ข้อ 5
`alternate_beeper.py` จงเขียนโปรแกรมสั่งให้แคเริลวาง beeper แบบช่องเว้นช่องเฉพาะแถวล่าง โดยที่เราไม่รู้ว่า world จะมีขนาดเท่าไร ให้ลองทดสอบกับ world หลายๆ แบบ
```python
def main():
    """
    แนวทางการคิด
    1. รูปแบบการเดิน คือ เดิน-วาง-เดิน จึงใช้ while front_is_clear เพื่อทำ action รูปแบบเดิมไปเรื่อยๆ จนกว่าจะเจอทางตัน 
    2. แต่ while front_is_clear จะเช็กข้างหน้าก็ต่อเมื่อทำ action 3 อันครบในแต่ละรอบเท่านั้น หลังจากที่วาง beeper แล้วเดินก้าวต่อไป จึงจำเป็นต้องเช็กว่าข้างหน้า clear หรือไม่ จึงใช้ if front_is_clear
    """
    # เดินหน้าจนกว่าจะเจอทางตัน
    while front_is_clear():
        move() # เริ่มต้นด้วยการเดินหน้า
        put_beeper() # วาง beeper

        # ถ้าข้างหน้ายังว่างก็เดินหน้าต่อไป
        if front_is_clear():
            move()
```