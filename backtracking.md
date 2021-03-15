# Backtracking Algorithm
<div dir="rtl">

## **فهرست** 
- [درخت حالت فضایی یا State Space Tree]()
- [کد backtracking]()
- [مثالی از backtracking]()
- [برنامه های الگوریتم backtracking]()
------

در این آموزش می آموزیم که الگوریتم بازگشت به مرحله یا **backtracking** چیست. همچنین ، نمونه ای از رویکرد عقب نشینی را پیدا خواهید کرد.
الگوریتم **backtracking** یک الگوریتم حل مسئله است که از رویکرد **brute force** برای یافتن بازده مورد نظر استفاده می کند.
رویکرد **brute force** تمام راه حلهای ممکن را امتحان کرده و بهترین راه حلهای مورد نظر را انتخاب می کند.
اصطلاح **backtracking** یا پس گرد نشان می دهد که اگر راه حل فعلی مناسب نیست ، پس از آن عقب نشینی کرده و راه حل های دیگر را امتحان کنید. بنابراین ، بازگشت در این روش استفاده می شود.
این روش برای حل مسائلی استفاده می شود که چندین راه حل دارند. اگر یک راه حل بهینه می خواهید ، باید به دنبال برنامه نویسی پویا یا **dynamic programming** باشید.

پس گرد یا **backtracking** یک روش الگوریتمی برای حل مشکلات بصورت بازگشتی با تلاش برای ساختن یک راه حل به صورت تدریجی ، یک قطعه در هر بار ، از بین بردن راه حل هایی است که قادر به رفع محدودیت های مسئله در هر زمان نیستند (با توجه به زمان ، در اینجا ، زمان سپری شده تا رسیدن به هر سطح از درخت جستجو).
برای مثال ، مسئله حل سودوکو را در نظر بگیرید ، سعی می کنیم ارقام را یکی یکی پر کنیم. هر زمان که متوجه شدیم رقم فعلی نمی تواند به راه حلی منجر شود ، آن را حذف می کنیم (بک ترک) و رقم بعدی را امتحان می کنیم. این روش بهتر از رویکرد ساده لوحانه است (تولید همه ترکیبات احتمالی رقم و سپس آزمایش هر ترکیبی یک به یک) زیرا هر زمان که برگردد مجموعه ای از جایگشت ها را کاهش می دهد.

## State Space Tree
درخت حالت فضایی درختی است که نمایانگر تمام حالات ممکن (راه حل یا عدم حل) مسئله از ریشه به عنوان یک حالت اولیه تا برگ به عنوان یک حالت انتهایی است.

![state space tree](https://cdn.programiz.com/sites/tutorial2program/files/ba-state-space-tree.png)

### کد الگوریتم **backtracking**:

</div>

```python
Backtrack(x)
    if x is not a solution
        return false
    if x is a new solution
        add to list of solutions
    backtrack(expand x)

```
<div dir="rtl">


### مثالی از رویکرد **backtracking**:
مشکل: شما می خواهید همه روش های ممکن برای چیدمان 2 پسر و 1 دختر را در 3 نیمکت پیدا کنید. محدودیت: دختر نباید روی نیمکت وسط باشد.
راه حل: در کل 3 وجود دارد! = 6 احتمال. ما همه امکانات را امتحان خواهیم کرد و راه حل های ممکن را بدست خواهیم آورد. ما به طور بازگشتی همه احتمالات را امتحان می کنیم.
تمام احتمالات عبارت اند از:

![All possibilities](https://cdn.programiz.com/sites/tutorial2program/files/ba-possibilities.png)

#### درخت **state space** زیر راه حل های ممکن را نشان می دهد:

![state-state-tree-example](https://cdn.programiz.com/sites/tutorial2program/files/ba-state-state-tree-example.png)

#### **برنامه های الگوریتم **backtracking**:**
1. **برای یافتن تمام مسیرهای همیلتونی [Hamiltonian Paths](https://en.wikipedia.org/wiki/Hamiltonian_path_problem) موجود در یک نمودار** 
2. **برای حل مشکل [N Queen](https://en.wikipedia.org/wiki/Eight_queens_puzzle)**
3. **حل مسئله پیچ و خم یا [Maze solving](https://en.wikipedia.org/wiki/Maze_solving_algorithm)**
4. **مشکل تور شوالیه یا [The Knight's tour](https://en.wikipedia.org/wiki/Knight%27s_tour)** 












