# Rabin Karp Algorithm
<div dir="rtl">

## **فهرست** 
- [الگوریتم Rabin-karp چگونه کار میکند؟](https://www.programiz.com/dsa/rabin-karp-algorithm)
- [الگوریتم Rabin-Karp در پایتون](https://www.programiz.com/dsa/rabin-karp-algorithm)
- [محدودیت های الگوریتم Rabin-Karp](https://www.programiz.com/dsa/rabin-karp-algorithm)
- [پیچیدگی الگوریتم Rabin-Karp](https://www.programiz.com/dsa/rabin-karp-algorithm)
- [برنامه های الگوریتم Rabin-Karp](https://www.programiz.com/dsa/rabin-karp-algorithm)
- [ویدیو آموزش الگوریتم Rabin-Karp](https://www.programiz.com/dsa/rabin-karp-algorithm)
------

در این آموزش می آموزید که الگوریتم **rabin-karp** چیست. همچنین ، نمونه های مفیدی از الگوریتم **rabin-karp** را در **پایتون** خواهید یافت.

الگوریتم **Rabin-Karp** الگوریتمی است که برای جستجو / تطبیق الگوهای متن با استفاده از تابع هش استفاده می شود. برخلاف الگوریتم تطبیق رشته ساده و ساده ، در فاز اولیه از بین همه کاراکترها عبور نمی کند بلکه شخصیت هایی را که مطابقت ندارند فیلتر می کند و سپس مقایسه را انجام می دهد.

* **تابع هش ابزاری برای ترسیم مقدار ورودی بزرگتر به مقدار خروجی کوچکتر است. این مقدار خروجی را مقدار هش می نامند**

## الگوریتم Rabin-Karp چگونه کار می کند؟

دنباله ای از کاراکترها گرفته می شوند و از نظر وجود رشته مورد نیاز بررسی می شوند. اگر این امکان یافت شود ، مطابقت شخصیت انجام می شود.

اجازه دهید الگوریتم را با مراحل زیر درک کنیم:

1. متن بگذارید:

![Text](https://cdn.programiz.com/sites/tutorial2program/files/rc-text.png)


و رشته ای که در متن بالا جستجو می شود این باشد:

![Pattern](https://cdn.programiz.com/sites/tutorial2program/files/rc-pattern.png)

2. بگذارید برای کاراکترهایی که در مسئله استفاده خواهیم کرد **مقدار عددی (v) / وزن** اختصاص دهیم. در اینجا ، ما فقط ده حروف اول را گرفته ایم (به عنوان مثال A تا J).

![Text Weights](https://cdn.programiz.com/sites/tutorial2program/files/rc-text-wieghts.png)

3. متر **m** طول الگو و **n** طول متن است. در اینجا ، **m = 10 و n = 3**.
بگذارید **d** تعداد کاراکترهای مجموعه ورودی باشد. در اینجا ، مجموعه ورودی {A، B، C، ...، J} را گرفته ایم. بنابراین ، **d = 10**. شما می توانید هر مقدار مناسبی را برای **d** فرض کنید.

4. اجازه دهید مقدار هش الگو را محاسبه کنیم:

![Hash value of text](https://cdn.programiz.com/sites/tutorial2program/files/rc-mod-pattern.png)

</div>

```python
hash value for pattern(p) = Σ(v * dm-1) mod 13 
                      = ((3 * 102) + (4 * 101) + (4 * 100)) mod 13 
                      = 344 mod 13 
                      = 6

```
<div dir="rtl">

در محاسبه بالا ، یک عدد اول (در اینجا ، 13) را به گونه ای انتخاب کنید که بتوانیم همه محاسبات را با حساب تک دقت انجام دهیم.

در زیر دلیل محاسبه مدول آورده شده است.
5. مقدار هش را برای پنجره متن با اندازه **m** محاسبه کنید.

</div>

```python
For the first window ABC,
hash value for text(t) = Σ(v * dn-1) mod 13 
                  = ((1 * 102) + (2 * 101) + (3 * 100)) mod 13 
                  = 123 mod 13  
                  = 6

```
<div dir="rtl">

6. مقدار هش الگو را با مقدار هش متن مقایسه کنید. اگر آنها مطابقت داشته باشند ، مطابقت شخصیت انجام می شود.
در مثال های بالا ، مقدار هش پنجره اول (به عنوان مثال **t**) با **p** مطابقت دارد ، به دنبال مطابقت کاراکتر بین ABC و CDD باشید. از آنجا که مطابقت ندارند ، به دنبال پنجره بعدی بروید.

7. ما مقدار هش پنجره بعدی را با کم کردن اصطلاح اول و اضافه کردن اصطلاح بعدی مانند تصویر زیر محاسبه می کنیم: 

</div>

```python
t = ((1 * 102) + ((2 * 101) + (3 * 100)) * 10 + (3 * 100)) mod 13 
  = 233 mod 13  
  = 12

```
<div dir="rtl">

به منظور بهینه سازی این فرآیند ، ما از مقدار هش قبلی به روش زیر استفاده می کنیم:

</div>

```python
t = ((d * (t - v[character to be removed] * h) + v[character to be added] ) mod 13  
  = ((10 * (6 - 1 * 9) + 3 )mod 13  
  = 12
Where, h = dm-1 = 103-1 = 100.

```
<div dir="rtl">

8. برای BCC ، t = 12 (6 ≠). بنابراین ، به پنجره بعدی بروید.
پس از چند جستجو ، متناسب با **CDA** پنجره را در متن دریافت خواهیم کرد. 

![Hash value of different windows](https://cdn.programiz.com/sites/tutorial2program/files/rc-mod-txt.png)

## الگوریتم

</div>

```python
n = t.length
m = p.length
h = dm-1 mod q
p = 0
t0 = 0
for i = 1 to m
    p = (dp + p[i]) mod q
    t0 = (dt0 + t[i]) mod q
for s = 0 to n - m
    if p = ts
        if p[1.....m] = t[s + 1..... s + m]
            print "pattern found at position" s
    If s < n-m
        ts + 1 = (d (ts - t[s + 1]h) + t[s + m + 1]) mod q
```
<div dir="rtl">

## الگوریتم **Rabin-Karp** در پایتون:

</div>

```python
# Rabin-Karp algorithm in python
d = 10

def search(pattern, text, q):
    m = len(pattern)
    n = len(text)
    p = 0
    t = 0
    h = 1
    i = 0
    j = 0

    for i in range(m-1):
        h = (h*d) % q

    # Calculate hash value for pattern and text
    for i in range(m):
        p = (d*p + ord(pattern[i])) % q
        t = (d*t + ord(text[i])) % q

    # Find the match
    for i in range(n-m+1):
        if p == t:
            for j in range(m):
                if text[i+j] != pattern[j]:
                    break

            j += 1
            if j == m:
                print("Pattern is found at position: " + str(i+1))

        if i < n-m:
            t = (d*(t-ord(text[i])*h) + ord(text[i+m])) % q

            if t < 0:
                t = t+q


text = "ABCCDDAEFG"
pattern = "CDD"
q = 13
search(pattern, text, q)
```
<div dir="rtl">

## **محدودیت های الگوریتم Rabin-Karp**

**ضربه جعلی یا Spurious Hit**

وقتی مقدار هش الگو با مقدار هش یک پنجره از متن مطابقت داشته باشد اما پنجره الگوی واقعی نباشد ، آن را ضربه جعلی می نامند.

ضربه جعلی میزان پیچیدگی زمان الگوریتم را افزایش می دهد. به منظور به حداقل رساندن ضربه جعلی ، ما از مدول استفاده می کنیم. ضربه جعلی را تا حد زیادی کاهش می دهد.

## پیچیدگی الگوریتم Rabin-Karp

متوسط و بهترین حالت پیچیدگی الگوریتم رابین-کارپ **O (m + n)** و بدترین حالت **O (mn)** است.

بدترین حالت در شرایطی رخ می دهد که تعداد بازدیدهای جعلی برای همه پنجره ها زیاد باشد.

## برنامه های الگوریتم Rabin-Karp

* برای تطبیق الگو
* برای جستجوی رشته در متن بزرگتر


## * ویدیو آموزش الگوریتم رابین−کارپ( Rabin-karp )

<a href="http://www.youtube.com/watch?feature=player_embedded&v=YOUTUBE_VIDEO_ID_HERE
" target="_blank"><img src="http://img.youtube.com/vi/YOUTUBE_VIDEO_ID_HERE/0.jpg" 
alt="Robin-Karp youtube video" width="440" height="380" border="20" /></a>
