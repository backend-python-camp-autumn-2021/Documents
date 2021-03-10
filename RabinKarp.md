# Rabin-Karp Algorithm
<div dir="rtl">

## **فهرست** 
- [درخت حالت فضایی یا State Space Tree](https://www.programiz.com/dsa/backtracking-algorithm)
- [کد backtracking](https://www.programiz.com/dsa/backtracking-algorithm)
- [مثالی از backtracking](https://www.programiz.com/dsa/backtracking-algorithm)
- [برنامه های الگوریتم backtracking](https://www.programiz.com/dsa/backtracking-algorithm)
------

در این آموزش می آموزید که الگوریتم rabin-karp چیست. همچنین ، نمونه های مفیدی از الگوریتم rabin-karp را در پایتون خواهید یافت.

الگوریتم Rabin-Karp الگوریتمی است که برای جستجو / تطبیق الگوهای متن با استفاده از تابع هش استفاده می شود. برخلاف الگوریتم تطبیق رشته ساده و ساده ، در فاز اولیه از بین همه کاراکترها عبور نمی کند بلکه شخصیت هایی را که مطابقت ندارند فیلتر می کند و سپس مقایسه را انجام می دهد.

<div>

**تابع هش ابزاری برای ترسیم مقدار ورودی بزرگتر به مقدار خروجی کوچکتر است. این مقدار خروجی را مقدار هش می نامند.**

<div dir="rtl">


الگوریتم **Rabin-Karp** چگونه کار می کند؟

دنباله ای از کاراکترها گرفته می شوند و از نظر وجود رشته مورد نیاز بررسی می شوند. اگر این امکان یافت شود ، مطابقت شخصیت انجام می شود.

اجازه دهید الگوریتم را با مراحل زیر درک کنیم:
