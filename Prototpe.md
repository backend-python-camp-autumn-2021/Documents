# Prototype

<div dir="rtl">
الگوی طراحی پروتوتایپ یا Prototype یکی از الگوی‌های طراحی سازنده است که به منظور جلوگیری از ساخت یک شی جدید استفاده می‌شود


این الگوی طراحی راهکاری برای ایجاد یک شی جدید به واسطه کپی کردن آن از اشیا موجود دیگر ارائه می‌دهد. با استفاده از این تکنیک بدون اینکه وابستگی میان شی جدید و کلاسی که از آن ساخته شده است ایجاد شود، می‌توان اشیا جدیدی در نرم افزار تولید کرد. همچنین در مواردی که مواقع نیاز به ایجاد تغییرات در اشیا جدید وجود دارد تا بتوانیم اشیایی از یک نوع و با پارامترهایی متفاوت ایجاد کنیم.

مثلا تصور کنید بخواهید از یک شی ماشین چندین کپی ایجاد کنید با این تفاوت که هر کدام رنگی متفاوت داشته باشد. با استفاده از الگوی طراحی پروتوتایپ دیگر نیاز نیست که هر بار یک شی جدید از کلاس ایجاد کنید و سپس پارامترهای آن را مشخص کنید. زیرا شما می‌توانید از کلاس ماشین یک شی ایجاد کنید و سپس از آن به تعدادی که نیاز دارید کپی (Clone) تولید کنید.

## چرا باید از الگوی طراحی Prototype استفاده کنیم

تصور کنید که تصمیم گرفته اید یک هواپیما بر اساس نمونه خارجی آن بسازید. برای بومی ساز این هواپیما تنها راهی که پیش روی شما خواهد بود این است که دقیقا از پارامترها و ویژگی‌های ساختاری نمونه خارجی آن آگاه باشید. اما از آنجایی که تکنولوژی هایی مربوط به ساخت هواپیماها انحصاری هستند و به راحتی در اختیار دیگر شرکت‌ها قرار نمی‌گیرند، این امر برای شما امکان پذیر نخواهد بود. اما تصور کنید که یک ماشین کپی سه بعدی غول پیکر برای شبیه سازی اشیا داشته باشید. با این کار می‌توانید هواپیما خارجی به آن دستگاه وارد کرده و هواپیما شبیه سازی خود را دریافت کنید. این ماشین شبیه ساز کاری شبیه الگوی طراحی پروتوتایپ انجام می‌دهد.

بنابراین اگر بخواهید از شی ای موجود در نرم افزار دقیقا یک کپی ایجاد کنید. ابتدا باید یک شی جدید از کلاس مورد نظر ایجاد کنید. سپس باید تمام پارامترها و ویژگی‌های شی اصلی را دریافت کرده و بر روی جسم جدید اعمال کنید. اما این روش همیشه به درستی عمل نخواهد کرد زیرا بعضی از پارامترها و ویژگی‌های یک شی ممکن است به صورت خصوصی یا Private تعریف شده باشند. در این صورت دیگر امکان دسترسی به آن‌ها از خارج از کلاس امکان پذیر نخواهد بود.


بنابراین یکی از مشکلات کپی کردن اشیا در برنامه نویسی به صورت مستقیم، عدم دسترسی به برخی از پارامترهای خصوصی است. پس کپی کردن یک شی خارج از کلاسش همیشه امکان پذیر نخواهد بود. از طرفی دیگر به دلیل اینکه شما اشیای کپی شده را بر پایه کلاس‌های شی مبدا ایجاد می‌کنید، اشیای جدید به این کلاس‌ها وابسته می‌شوند و این کار باعث ایجاد وابستگی‌های زیاد در بین کلاس‌ها خواهد شد.

#### به اشیایی که کلاس‌های آن‌ها از قابلیت کپی شدن پشتیبانی کنند یک نمونه اولیه یا Prototype نامیده می‌شوند.

## راه حل الگوی طراحی پروتوتایپ
1. در الگوی طراحی نمونه اولیه یک Interface مشترک برای تمام اشیایی که باید کپی شوند در نظر گرفته می‌شود
>  این Interface به شما اجازه می‌دهد که یک شی را بدون نیاز به دوباره نویسی کدها در کلاس شی، کپی کنید.

2.معمولا، چنین Interface شامل تنها یک تابع به اسم Clone (کپی) هستند. پس با پیروی کلاس‌های مربوط به اشیا از این Interface دیگر نیازی به نوشتن توابع اضافه و یا استفاده از ایجاد مجدد یک شی نخواهیم داشت. برای این کار فقط کافی است تابع Clone را در کلاس‌ها پیاده سازی کنیم.

> پیاده سازی تابع Clone در همه کلاس‌ها بسیار شبیه به هم است. این تابع وظیفه دارد تا یک شی از کلاس فعلی ایجاد کند و سپس تمام مقادیر پارامترهای آن را به شی جدید منتقل می‌کند. همچنین مزیت دیگری که این الگوی طراحی در اختیار شما می‌گذارد این است که حتی می‌توانید پارامترهای Private را کپی کنید. زیرا اکثر زبان‌های برنامه نویسی اجازه می‌دهند که اشیاء به فیلدهای خصوصی از اشیاء دیگر که متعلق به یک کلاس هستند دسترسی پیدا کنند.

3. حتی میتوانبم یک registery store  تعریف کنیم که تعدادی از ابجکت ها را به تنظیمات پیش قرض داخل خود دارد ومطابق با وروردی و درخواست مشتری و یا کاربر ان آبجکت مد نظرش را به او خواهیم داد

بنابراین اگر بخواهیم روش کار این الگو را جمع بندی کنیم باید گفت که شما در ابتدا باید مجموعه ای از اشیا را ایجاد کنید که به شیوه‌های مختلف پیکربندی شده اند. سپس در هر زمانی که به یک شی با یکی از پیکربندی‌های تنظیم شده نیاز داشته باشید، کافی است یک نمونه اولیه را بر اساس آن ایجاد کنید و دیگر نیازی به ساخت یک شی جدید از ابتدا نخواهید داشت.

## کاربردهای الگوی طراحی Prototype

به کارگیری الگوی طراحی پروتوتایپ در طراحی نرم افزارها، باعث کاهش میزان کدنویسی خواهد شد. مزیت اصلی این دیزاین پترن افزایش سرعت کپی کردن یک شی از شی‌های است. زیرا این عمل خیلی سریع‌تر از ساخت اشیا می‌باشد. در عملیات کپی کردن اشیا تابع سازنده آن‌ها (Constructor) دیگر اجرا نخواهد شد. الگوی طراحی سازنده در موارد زیر کاربرد خواهد داشت:

- برای کاهش تعداد کلاس‌های فرزند (Subclass) استفاده می‌شود. همچنین با این روش می‌توان اشیا ساخته شده را متناسب با نیازهای مختلف پیکربندی کرد.
- به منظور جلوگیری از ایجاد وابستگی میان شی کپی شده به کلاس مورد نظر استفاده می‌شود.
- زمانی که بخواهیم از یک کلاس با پارامترهای Private زیاد شی ایجاد کنیم.

</div>

#### Simple Code in Python

```
import copy


class Prototype:
    def clone(self):
        return copy.deepcopy(self)

if __name__ == "__main__":
    prototype = Prototype()
    prototype_copy = prototype.clone()
    print(prototype_copy)

```

#### another one but more comlicated

```

import copy


class SelfReferencingEntity:
    def __init__(self):
        self.parent = None

    def set_parent(self, parent):
        self.parent = parent


class SomeComponent:
    """
    Python provides its own interface of Prototype via `copy.copy` and
    `copy.deepcopy` functions. And any class that wants to implement custom
    implementations have to override `__copy__` and `__deepcopy__` member
    functions.
    """

    def __init__(self, some_int, some_list_of_objects, some_circular_ref):
        self.some_int = some_int
        self.some_list_of_objects = some_list_of_objects
        self.some_circular_ref = some_circular_ref

    def __copy__(self):
        """
        Create a shallow copy. This method will be called whenever someone calls
        `copy.copy` with this object and the returned value is returned as the
        new shallow copy.
        """

        # First, let's create copies of the nested objects.
        some_list_of_objects = copy.copy(self.some_list_of_objects)
        some_circular_ref = copy.copy(self.some_circular_ref)

        # Then, let's clone the object itself, using the prepared clones of the
        # nested objects.
        new = self.__class__(
            self.some_int, some_list_of_objects, some_circular_ref
        )
        new.__dict__.update(self.__dict__)

        return new

    def __deepcopy__(self, memo={}):
        """
        Create a deep copy. This method will be called whenever someone calls
        `copy.deepcopy` with this object and the returned value is returned as
        the new deep copy.

        What is the use of the argument `memo`? Memo is the dictionary that is
        used by the `deepcopy` library to prevent infinite recursive copies in
        instances of circular references. Pass it to all the `deepcopy` calls
        you make in the `__deepcopy__` implementation to prevent infinite
        recursions.
        """

        # First, let's create copies of the nested objects.
        some_list_of_objects = copy.deepcopy(self.some_list_of_objects, memo)
        some_circular_ref = copy.deepcopy(self.some_circular_ref, memo)

        # Then, let's clone the object itself, using the prepared clones of the
        # nested objects.
        new = self.__class__(
            self.some_int, some_list_of_objects, some_circular_ref
        )
        new.__dict__ = copy.deepcopy(self.__dict__, memo)

        return new


if __name__ == "__main__":

    list_of_objects = [1, {1, 2, 3}, [1, 2, 3]]
    circular_ref = SelfReferencingEntity()
    component = SomeComponent(23, list_of_objects, circular_ref)
    circular_ref.set_parent(component)

    shallow_copied_component = copy.copy(component)

    # Let's change the list in shallow_copied_component and see if it changes in
    # component.
    shallow_copied_component.some_list_of_objects.append("another object")
    if component.some_list_of_objects[-1] == "another object":
        print(
            "Adding elements to `shallow_copied_component`'s "
            "some_list_of_objects adds it to `component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Adding elements to `shallow_copied_component`'s "
            "some_list_of_objects doesn't add it to `component`'s "
            "some_list_of_objects."
        )

    # Let's change the set in the list of objects.
    component.some_list_of_objects[1].add(4)
    if 4 in shallow_copied_component.some_list_of_objects[1]:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "changes that object in `shallow_copied_component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "doesn't change that object in `shallow_copied_component`'s "
            "some_list_of_objects."
        )

    deep_copied_component = copy.deepcopy(component)

    # Let's change the list in deep_copied_component and see if it changes in
    # component.
    deep_copied_component.some_list_of_objects.append("one more object")
    if component.some_list_of_objects[-1] == "one more object":
        print(
            "Adding elements to `deep_copied_component`'s "
            "some_list_of_objects adds it to `component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Adding elements to `deep_copied_component`'s "
            "some_list_of_objects doesn't add it to `component`'s "
            "some_list_of_objects."
        )

    # Let's change the set in the list of objects.
    component.some_list_of_objects[1].add(10)
    if 10 in deep_copied_component.some_list_of_objects[1]:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "changes that object in `deep_copied_component`'s "
            "some_list_of_objects."
        )
    else:
        print(
            "Changing objects in the `component`'s some_list_of_objects "
            "doesn't change that object in `deep_copied_component`'s "
            "some_list_of_objects."
        )

    print(
        f"id(deep_copied_component.some_circular_ref.parent): "
        f"{id(deep_copied_component.some_circular_ref.parent)}"
    )
    print(
        f"id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent): "
        f"{id(deep_copied_component.some_circular_ref.parent.some_circular_ref.parent)}"
    )
    print(
        "^^ This shows that deepcopied objects contain same reference, they "
        "are not cloned repeatedly."
    )

```






