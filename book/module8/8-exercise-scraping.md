# แบบฝึกหัดการขูดข้อมูลด้วย `BeautifulSoup`

## Warm-up: Scraping using regex
เราสามารถใช้ requests ในการดาวน์โหลดหน้าเว็บลงมา แล้วใช้ regex ตรวจหาได้เลย
https://math.sc.chula.ac.th/en/people/
https://www.arts.chula.ac.th/~english/people/

## Scrape บทความจากเว็บ
สมมติว่าเราต้องการขูดข้อมูลข่าวเศรษฐกิจจาก thestandard.co
หน้า article ตัว text อยู่ภายใน tag อะไร class อะไร id อะไร
https://thestandard.co/metaverse-and-investment-opportunities/
คลิกขวาบนจุดที่ต้องการของ web page แล้วกด Inspect Elements แล้วไล่หาว่าตัว text อยู่ตรง tag ไหน 
เขียนโค้ด run beautifulsoup สำหรับการขูด text ออกจาก article
หาหน้ารวม link ซึ่งควรจะมี url (a tag) ที่ลิงค์ไปที่ article เยอะ ๆ 
หา a tag ที่ลิงค์ไปที่ article จากหน้า main แต่ว่าต้องระวังเลือกแต่ลิงค์ทีต้องการเท่านั้น 
หาหน้ารวมลิงค์หลายๆ หน้า เพื่อให้ได้ข้อมูลเยอะ ๆ ให้สังเกตว่ามี pattern อะไรที่เห็นเด่นชัดมั้ย เช่น

https://thestandard.co/category/wealth/

https://thestandard.co/category/wealth/wealth-opinion/

https://thestandard.co/category/wealth/wealth-opinion/page/2/

https://thestandard.co/category/wealth/wealth-opinion/page/15/

https://thestandard.co/category/news/

https://thestandard.co/category/news/lgbtq/

รัน for loop ขูดเอา text ออกมาตามต้องการ

	for link_page in link_pages: 
		url_links  = scrape_url_links_from_page(link_page)
		for url_link in url_links:
			scrape_and_write(url_link)


## Beautifulsoup 
`Beautifulsoup` ขูดได้เฉพาะ static page เท่านั้น dynamic page ไม่ค่อยดีเช่น https://thestandard.co/pop/fashion/
### Mission 1:
ขูดข่าวจาก thestandard.co 5 page แรก ให้เลือกมาแค่ข่าวประเภทเดียว

Tech
Sport
Business
Science
Politics
Environment
LGBT
On this day
China
World
Thailand


### Mission 2:
ขูดข้อมูลจาก Dek-D จำนวน 20 กระทู้ ให้เลือกมาแค่บอร์ดเดียว

มีสาระ+รีวิว
บันเทิง
ปัญหาวัยรุ่น
NUGIRL
เด็ก TCAS
รร.+ติวเตอร์
เรียนต่อนอก
นักเขียน
แจ้งปัญหา
