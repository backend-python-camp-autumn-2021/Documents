<div dir="rtl">



 </div
 
 
 

 
 <hr>
 
<div dir="rtl">

# الگوریتم تقسیم و غلبه

در این آموزش ، خواهیم آموخت الگوریتم تقسیم و غلبه چگونه کار میکند.همچنین رویکرد الگوریتم تقسیم و غلبه را با سایر رویکرد های حل مسئله مقایسه خواهیم کرد.



## الگوریتم تقسیم و غلبه چگونه کار میکند؟
الگوریتم **تقسیم و غلبه** مسئله را به این صورت حل میکند:
1. **تقسیم:** مسئله را به زیر مسئله تبدیل می کند.
2. **غلبه:**‌ زیر مسئله ها را حل میکند.
3. **ترکیب:** آنها را با هم ترکیب میکند تا به جواب خواسته شده برسد.

به عنوان مثال میخواهیم مرتب سازی ادغامی را با استفاده از الگوریتم تقسیم و غلبه حل کنیم.

1. آرایه زیر را در نظر بگیرید:

![Array for merge sort](https://cdn.programiz.com/sites/tutorial2program/files/divide-and-conquer-0.png)

2. آرایه را به دو قسمت تقسیم میکنیم:

![Divide the array into two subparts](https://cdn.programiz.com/sites/tutorial2program/files/divide-and-conquer-1.png)

آنقدر به تقسیم آرایه ادامه میدهیم تا به المنت های تکی برسیم.

![Divide the array into smaller subparts](https://cdn.programiz.com/sites/tutorial2program/files/divide-and-conquer-2.png)


3. حال به ترکیب المنت های تکی به صورت مرتب شده میپردازیم.در این مرحله **تقسیم** و **غلبه** به صورت همزمان انجام میشوند.

![Combine the subparts](https://cdn.programiz.com/sites/tutorial2program/files/divide-and-conquer-3.png)

</div>


<div dir="rtl">

# پیچیدگی زمانی
پیچیدگی زمانی الگوریتم تقسیم و غلبه از طریق قضیه اصلی (Master Theorem) محاسبه میشود.



</div>

```
T(n) = aT(n/b) + f(n),
where,
n = size of input
a = number of subproblems in the recursion
n/b = size of each subproblem. All subproblems are assumed to have the same size.
f(n) = cost of the work done outside the recursive call, which includes the cost of dividing the problem and cost of merging the solutions

```
<div dir="rtl">

به عنوان مثال پیچیدگی زمانی مسئله بازگشتی را بررسی میکنیم.
برای مرتب سازی ادغامی معادله به صورت زیر نوشته میشود:

</div>

```
T(n) = aT(n/b) + f(n)
     = 2T(n/2) + O(n)
Where, 
a = 2 (each time, a problem is divided into 2 subproblems)
n/b = n/2 (size of each sub problem is half of the input)
f(n) = time taken to divide the problem and merging the subproblems
T(n/2) = O(n log n) (To understand this, please refer to the master theorem.)

Now, T(n) = 2T(n log n) + O(n)
          ≈ O(n log n)

```
<div dir="rtl">


# مقایسه الگوریتم های تقسیم و غلبه و داینامیک

تقسیم و غلبه مسئله را به زیر مسئله تقسیم میکند.این زیر مسائل به صورت بازگشتی حل میشوند. جواب هر مسئله برای استفاده های بعدی نگهداری نمیشود در صورتی که در الگوریتم داینامیک جواب هر زیر مسئله برای استفاده های بعدی ذخیره میشود.

از تقسیم و غلبه زمانی استفاده کنید که جواب زیر مسئله های یکسان چندین بار محاسبه نمیشوند.از الگوریتم داینامیک زمانی استفاده کنید که زیر مسائل چندین بار در ادامه الگوریتم استفاده خواهند شد. 

برای درک بهتر این موضوع سری فیبوناچی را در نظر بگیرید.


## رویکرد تقسیم و غلبه


</div>

```
fib(n)
    If n < 2, return 1
    Else , return f(n - 1) + f(n -2)
    
```
<div dir="rtl">

## رویکرد داینامیک

</div>

```
mem = []
fib(n)
    If n in mem: return mem[n] 
    else,     
        If n < 2, f = 1
        else , f = f(n - 1) + f(n -2)
        mem[n] = f
        return f
    
```
<div dir="rtl">

در رویکرد داینامیک mem جواب هر زیر مسئله را ذخیره میکند.

# مزیت استفاده از الگوریتم تقسیم و غلبه

- پیچیدگی برای ضرب دو ماتریس با استفاده از متد ساده (naive methode), O(n<sup>3</sup>) می باشد در صورتی که با رویکرد تقسیم و غلبه (در ضرب ماتریس استراسن) پیچیدگی به O(n<sup>2.8074</sup>) کاهش می یابد. همچنین این رویکرد مسائل دیگر مانند برج هانوی را ساده تر میکند.

- این رویکرد برای سیستم های چند پردازشی نیز مناسب است. 

- مصرف فضای ذخیره سازی را نیز کاهش میدهد.
