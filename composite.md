# Composite Design Pattern
<div dir="rtl">

## **فهرست** 
- [ساختار(uml) composite](https://refactoring.guru/design-patterns/composite/python/example)
- [نحوه اجرا](https://refactoring.guru/design-patterns/composite/python/example)
- [مزایا و معایب](https://refactoring.guru/design-patterns/composite/python/example)
- [روابط با الگوهای دیگر](https://refactoring.guru/design-patterns/composite/python/example)
- [استفاده از الگو در پایتون](https://refactoring.guru/design-patterns/composite/python/example)
- [مثال از composite در پایتون](https://refactoring.guru/design-patterns/composite/python/example)
------

## هدف یا intent 
**کامپوزیت** یک الگوی طراحی ساختاری است که به شما امکان می دهد اشیا را در ساختارهای درختی ترکیب کنید و سپس با این ساختارها کار کنید گویی که اشیا individual جداگانه هستند.

![intent object tree](https://refactoring.guru/images/patterns/content/composite/composite.png)
                            به composite درخت شی نیز گفته میشود

## مشکل :(
استفاده از الگوی ترکیبی فقط زمانی منطقی است که مدل اصلی برنامه شما بتواند به عنوان یک درخت نشان داده شود.
به عنوان مثال ، تصور کنید که دو نوع شی دارید: محصولات و جعبه ها. یک جعبه می تواند شامل چندین محصول و همچنین تعدادی جعبه کوچکتر باشد. این جعبه های کوچک همچنین می توانند برخی از محصولات یا حتی جعبه های کوچکتر و غیره را در خود جای دهند.
بگویید تصمیم دارید یک سیستم سفارش دهی ایجاد کنید که از این کلاس ها استفاده کند. سفارشات می توانند حاوی محصولات ساده و بدون بسته بندی و همچنین جعبه های پر از محصولات ... و جعبه های دیگر باشند. قیمت کل چنین سفارشی را چگونه تعیین می کنید؟

![complex order](https://refactoring.guru/images/patterns/diagrams/composite/problem-en.png) 
###### یک سفارش ممکن است شامل محصولات مختلف ، بسته بندی شده در جعبه ها باشد که در جعبه های بزرگتر و غیره بسته بندی می شوند. کل ساختار مانند یک درخت وارونه به نظر می رسد.


می توانید روش مستقیم را امتحان کنید: همه جعبه ها را باز کنید ، تمام محصولات را مرور کنید و سپس کل را محاسبه کنید. این در دنیای واقعی قابل انجام است. اما در یک برنامه ، به سادگی اجرای یک حلقه نیست. پیش از این باید از کلاسهای محصولات و جعبه هایی که طی می کنید ، سطح لانه سازی جعبه ها و سایر جزئیات تند و زننده مطلع شوید. همه اینها رویکرد مستقیم را بیش از حد ناجور یا حتی غیرممکن می کند.

## راه حل :)

الگوی ترکیبی پیشنهاد می کند که شما با محصولات و جعبه ها از طریق یک رابط مشترک کار می کنید که روشی را برای محاسبه قیمت کل اعلام می کند.

این روش چگونه کار می کند؟ برای یک محصول ، به راحتی قیمت محصول را پس می دهد. برای یک جعبه ، باید از هر مورد جعبه بیشتر استفاده کند ، قیمت آن را بپرسید و سپس مبلغی را برای این جعبه بازگردانید. اگر یکی از این موارد جعبه کوچکتری بود ، آن جعبه نیز شروع به مرور مطالب و موارد دیگر می کرد ، تا زمانی که قیمت تمام اجزای داخلی محاسبه شود. یک جعبه حتی می تواند هزینه اضافی مانند هزینه بسته بندی را به قیمت نهایی اضافه کند.

![composit comic](https://refactoring.guru/images/patterns/content/composite/composite-comic-1-en.png) 
###### الگوی ترکیبی به شما امکان می دهد رفتاری را به صورت بازگشتی روی تمام اجزای یک درخت جسم اجرا کنید.
                          
بزرگترین مزیت این روش این است که شما نیازی به مراقبت از کلاسهای بتنی اشیا that که درخت را تشکیل می دهند نیست. نیازی نیست که بدانید یک شی یک محصول ساده است یا یک جعبه پیچیده. از طریق رابط مشترک می توانید با همه آنها یکسان رفتار کنید. هنگامی که شما یک روش را فرا می خوانید ، اشیا themselves خود درخواست را از درخت عبور می دهند.

## قیاس در دنیای واقعی

![real analogy](https://refactoring.guru/images/patterns/diagrams/composite/live-example.png) 

ارتش اکثر کشورها به عنوان سلسله مراتب ساختار یافته است. ارتش متشکل از چند لشکر است. یک لشکر مجموعه ای از تیپ ها است و یک تیپ متشکل از جوخه ها است که می تواند به جوخه تقسیم شود. سرانجام ، یک جوخه گروه کوچکی از سربازان واقعی است. دستورات در بالای سلسله مراتب داده می شوند و به هر سطح منتقل می شوند تا زمانی که هر سربازی بداند چه کاری باید انجام شود.

## ساختار(uml)

![structure uml](https://refactoring.guru/images/patterns/diagrams/composite/structure-en.png)

1. رابط **کامپوننت** عملیاتی را توصیف می کند که برای عناصر ساده و پیچیده درخت مشترک هستند.

2. **برگ** یک عنصر اساسی درخت است که عناصر فرعی ندارد.

     معمولاً اجزای برگ بیشتر کارهای واقعی را انجام می دهند ، زیرا آنها کسی را ندارند که کار را به آنها واگذار کنند.

3. **کانتینر** (با نام مستعار مرکب) عنصری است که دارای عناصر فرعی است: برگها یا ظروف دیگر. یک کانتینر کلاسهای بتونی فرزندانش را نمی داند. این فقط با رابط م componentلفه با تمام عناصر فرعی کار می کند.

     با دریافت یک درخواست ، یک کانتینر کار را به عناصر فرعی خود تفویض می کند ، نتایج متوسط را پردازش می کند و نتیجه نهایی را به مشتری برمی گرداند.

4. **مشتری** از طریق رابط component با تمام عناصر کار می کند. در نتیجه ، مشتری می تواند با هر دو عنصر ساده یا پیچیده درخت به همان شیوه کار کند.

## شبه کد

![Pseudocode](https://refactoring.guru/images/patterns/diagrams/composite/example.png)

در این مثال ، الگوی **Composite** به شما امکان می دهد انباشت اشکال هندسی را در یک ویرایشگر گرافیکی پیاده سازی کنید.
کلاس **CompoundGraphic** ظرفی است که می تواند شامل هر تعداد زیر شکل ، از جمله سایر اشکال مرکب باشد. یک شکل مرکب همان روش های یک شکل ساده را دارد. با این حال ، یک شکل مرکب به جای انجام کاری به تنهایی ، درخواست را به صورت بازگشتی به همه فرزندانش منتقل می کند و نتیجه را "خلاصه" می کند.
کد مشتری با همه اشکال از طریق یک رابط واحد مشترک در همه کلاس های شکل کار می کند. بنابراین مشتری نمی داند که آیا با یک شکل ساده کار می کند یا یک ترکیب. مشتری می تواند با ساختارهای بسیار پیچیده اشیا work کار کند بدون اینکه با کلاسهای بتونی تشکیل شده باشد.

## قابل اجرا بودن

**هنگامی که مجبورید یک ساختار شی مانند درخت را پیاده سازی کنید ، از الگوی Composite استفاده کنید.**

الگوی ترکیبی دو نوع عنصر اساسی را برای شما فراهم می کند که دارای یک رابط مشترک هستند: برگ های ساده و ظروف پیچیده. یک ظرف را می توان از هر دو برگ و سایر ظروف تشکیل داد. با این کار می توانید ساختار جسم بازگشتی تودرتو را که شبیه درخت است ، بسازید.

**وقتی می خواهید کد مشتری با عناصر ساده و پیچیده به طور یکنواخت رفتار کند از این الگو استفاده کنید.**

همه عناصر تعریف شده توسط الگوی کامپوزیت از یک رابط مشترک استفاده می کنند. با استفاده از این رابط ، مشتری نگران کلاس بتنی اشیایی نیست که با آنها کار می کند.

## نحوه اجرا

1. اطمینان حاصل کنید که مدل اصلی برنامه شما می تواند به عنوان یک ساختار درختی نشان داده شود. سعی کنید آن را به عناصر و ظروف ساده تقسیم کنید. به یاد داشته باشید که ظروف باید بتوانند حاوی عناصر ساده و ظروف دیگر باشند.

2. برای نمایش عناصر ساده کلاس برگ ایجاد کنید. یک برنامه ممکن است چندین کلاس برگ مختلف داشته باشد.

3. یک کلاس کانتینر برای نمایش عناصر پیچیده ایجاد کنید. در این کلاس ، یک قسمت آرایه برای ذخیره منابع به عناصر فرعی ارائه دهید.
 
4. در آخر ، روش های افزودن و حذف عناصر کودک را در ظرف تعریف کنید.

## مزایا و معایب

:)  شما می توانید با ساختارهای پیچیده درخت راحت تر کار کنید: از چند شکلی و بازگشت به نفع خود استفاده کنید.
:)  اصل باز / بسته شما می توانید بدون شکستن کد موجود ، که اکنون با درخت شی کار می کند ، انواع جدیدی از عناصر را به برنامه وارد کنید.
:(  تهیه یک رابط مشترک برای کلاسهایی که کارایی آنها بسیار زیاد است ممکن است دشوار باشد. در برخی از سناریوها ، باید بیش از حد کلی رابط component را ایجاد کنید ، و درک آن دشوارتر شود.

## روابط با الگوهای دیگر

* هنگام ایجاد درختان پیچیده **Composite** می توانید از **Builder** استفاده کنید زیرا می توانید مراحل ساخت آن را به صورت بازگشتی برنامه ریزی کنید.
* زنجیره مسئولیت اغلب همراه با کامپوزیت استفاده می شود. در این حالت ، وقتی یک جز **component** برگ درخواستی دریافت می کند ، ممکن است آن را از طریق زنجیره تمام اجزای اصلی تا ریشه درخت جسم عبور دهد.

* برای عبور از درختان مرکب می توانید از تکرارکننده ها استفاده کنید.

* می توانید از **Visitor** برای اجرای عملیاتی روی کل درخت **Composite** استفاده کنید.

* شما می توانید گره های برگ مشترک درخت **Composite** را به صورت **Flyweights** پیاده سازی کنید تا کمی **RAM** را ذخیره کنید.

* **کامپوزیت** و **دکوراتور** نمودارهای ساختاری مشابه دارند زیرا هر دو برای سازماندهی تعداد باز از اشیا on به ترکیب بازگشتی متکی هستند.

یک دکوراتور مانند یک کامپوزیت است اما فقط یک جز child کودک دارد. تفاوت قابل توجه دیگری نیز وجود دارد: Decorator مسئولیت های اضافی را به شی wra بسته بندی شده اضافه می کند ، در حالی که Composite فقط نتایج کودکان خود را "خلاصه" می کند.
با این حال ، الگوها همچنین می توانند همکاری کنند: شما می توانید از Decorator برای گسترش رفتار یک شی خاص در درخت مرکب استفاده کنید.
* طراحی هایی که از **Composite** و **Decorator** استفاده زیادی می کنند ، اغلب می توانند از استفاده از **Prototype** بهره مند شوند. استفاده از الگو به شما امکان می دهد ساختارهای پیچیده را به جای ساخت مجدد از ابتدا ، شبیه سازی کنید. 

# کامپوزیت یا مرکب(مخلوط) در پایتون

## کامپوزیت یک الگوی طراحی ساختاری است که اجازه می دهد اشیا را در یک ساختار درخت مانند ترکیب کرده و با آن کار کنیم ، مثل اینکه یک شی واحد باشد.

کامپوزیت به یک راه حل کاملاً محبوب برای بیشترین مشکلاتی که نیاز به ساختن یک ساختار درختی دارند تبدیل شد. ویژگی عالی کامپوزیت توانایی اجرای روشها بصورت بازگشتی بر روی کل ساختار درخت و جمع بندی نتایج است.

## استفاده از الگو در پایتون

**مثالهای قابل استفاده:** الگوی **Composite** در کد پایتون بسیار رایج است. این اغلب برای نشان دادن سلسله مراتب از اجزای رابط کاربر یا کدی که با نمودار کار می کند استفاده می شود.

**شناسایی:** اگر شما یک درخت شی دارید ، و هر یک از اشیا of یک درخت بخشی از همان سلسله مراتب کلاس است ، به احتمال زیاد این یک ترکیب است. اگر روشهای این کلاسها کار را به اشیا child اصلی درخت اختصاص داده و آن را از طریق کلاس پایه / رابط سلسله مراتب انجام دهید ، این قطعاً یک ترکیب است.
مثال مفهومی

این مثال ساختار الگوی طراحی کامپوزیت را نشان می دهد. این پاسخ به این سوالات متمرکز است:

* از چه کلاسهایی تشکیل شده است؟
* این کلاس ها چه نقشی دارند؟
* از چه روشی عناصر الگو با هم مرتبط هستند؟

</div>

```python
from __future__ import annotations
from abc import ABC, abstractmethod
from typing import List


class Component(ABC):
    """
    The base Component class declares common operations for both simple and
    complex objects of a composition.
    """

    @property
    def parent(self) -> Component:
        return self._parent

    @parent.setter
    def parent(self, parent: Component):
        """
        Optionally, the base Component can declare an interface for setting and
        accessing a parent of the component in a tree structure. It can also
        provide some default implementation for these methods.
        """

        self._parent = parent

    """
    In some cases, it would be beneficial to define the child-management
    operations right in the base Component class. This way, you won't need to
    expose any concrete component classes to the client code, even during the
    object tree assembly. The downside is that these methods will be empty for
    the leaf-level components.
    """

    def add(self, component: Component) -> None:
        pass

    def remove(self, component: Component) -> None:
        pass

    def is_composite(self) -> bool:
        """
        You can provide a method that lets the client code figure out whether a
        component can bear children.
        """

        return False

    @abstractmethod
    def operation(self) -> str:
        """
        The base Component may implement some default behavior or leave it to
        concrete classes (by declaring the method containing the behavior as
        "abstract").
        """

        pass


class Leaf(Component):
    """
    The Leaf class represents the end objects of a composition. A leaf can't
    have any children.

    Usually, it's the Leaf objects that do the actual work, whereas Composite
    objects only delegate to their sub-components.
    """

    def operation(self) -> str:
        return "Leaf"


class Composite(Component):
    """
    The Composite class represents the complex components that may have
    children. Usually, the Composite objects delegate the actual work to their
    children and then "sum-up" the result.
    """

    def __init__(self) -> None:
        self._children: List[Component] = []

    """
    A composite object can add or remove other components (both simple or
    complex) to or from its child list.
    """

    def add(self, component: Component) -> None:
        self._children.append(component)
        component.parent = self

    def remove(self, component: Component) -> None:
        self._children.remove(component)
        component.parent = None

    def is_composite(self) -> bool:
        return True

    def operation(self) -> str:
        """
        The Composite executes its primary logic in a particular way. It
        traverses recursively through all its children, collecting and summing
        their results. Since the composite's children pass these calls to their
        children and so forth, the whole object tree is traversed as a result.
        """

        results = []
        for child in self._children:
            results.append(child.operation())
        return f"Branch({'+'.join(results)})"


def client_code(component: Component) -> None:
    """
    The client code works with all of the components via the base interface.
    """

    print(f"RESULT: {component.operation()}", end="")


def client_code2(component1: Component, component2: Component) -> None:
    """
    Thanks to the fact that the child-management operations are declared in the
    base Component class, the client code can work with any component, simple or
    complex, without depending on their concrete classes.
    """

    if component1.is_composite():
        component1.add(component2)

    print(f"RESULT: {component1.operation()}", end="")


if __name__ == "__main__":
    # This way the client code can support the simple leaf components...
    simple = Leaf()
    print("Client: I've got a simple component:")
    client_code(simple)
    print("\n")

    # ...as well as the complex composites.
    tree = Composite()

    branch1 = Composite()
    branch1.add(Leaf())
    branch1.add(Leaf())

    branch2 = Composite()
    branch2.add(Leaf())

    tree.add(branch1)
    tree.add(branch2)

    print("Client: Now I've got a composite tree:")
    client_code(tree)
    print("\n")

    print("Client: I don't need to check the components classes even when managing the tree:")
    client_code2(tree, simple)

```

**Output: Execution result**

</div>

```
Client: I've got a simple component:
RESULT: Leaf

Client: Now I've got a composite tree:
RESULT: Branch(Branch(Leaf+Leaf)+Branch(Leaf))

Client: I don't need to check the components classes even when managing the tree:
RESULT: Branch(Branch(Leaf+Leaf)+Branch(Leaf)+Leaf)

```


