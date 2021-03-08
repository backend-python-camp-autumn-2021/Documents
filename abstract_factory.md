<div dir="rtl">

# الگوی طراحی کارخانه انتزاعی یا Abstract Factory 

الگوی طراحی کارخانه انتزاعی یا Abstract Factory جزو الگوهای طراحی سازنده (Creational) است که برای مدیریت
ساخت اشیا از کلاس ها توسعه داده شده است. این الگوی طراحی به شما اجازه می دهد که مجموعه ای از اشیا مرتبط را بدون 
نیاز به ساخت کلاس های جداگانه و متعدد ایجاد کنید.
کاربرد الگوی طراحی کارخانه انتزاعی تا حدودی مانند الگوی طراحی Factory است. این الگوی طراحی معمولا زمانی 
استفاده می شود که کاربر به صورت دقیق از نوع شی ای که می خواهد ایجاد کند اطلاع نداشته باشد
##چرا باید از الگوی طراحی Factory استفاده کنیم
تصور کنید که یکی از تولیدکنندگان محصولات اداری به منظور طراحی نرم افزاری به منظور فروش و مدیریت خط تولید 
محصولاتش به شما مراجعه می کند. در این نرم افزار محصولاتی از جمله انواع مبلمان، میز و... طراحی می شوند و سپس به 
فروش می رسند. در حالت پیش فرض نرم افزار شما باید به ازای هر محصول یک کلاس (Class) داشته باشد تا رفتار و وظایف 
مربوط به هر کدام از اشیا را برای خط تولید تعریف کند. از طرفی دیگر این محصولات معمولا با یکدیگر به فروش می رسند و 
مکمل یکدیگر هستند.
فرض کنید این کارخانه فقط شامل سه محصول میز، کاناپه و مبل است. پس کلاس های مورد نیاز در نرم افزار عبارتند از: مبل 
وکاناپه و میز. همچنین در این کارخانه محصولات در سه سبک ساده، هنری و مدرن طراحی و ایجاد می شوند. از آنجایی
که محصولات یک سبک معمولا با یکدیگر سفارش داده می شوند، باید آن ها به صورت خانواده ای از محصولات مرتبط در نظر گرفته شوند
بنابراین باید قابلیت افزودن محصولات یا سبک های جدید را در نرم افزار در نظر گرفت. زیرا اگر این امکان پیش بینی نشده
باشد در آینده باید کدهای موجود در نرم افزار تغییر یابند. زیرا فروشندگان محصولات معمولا خودشان لیست محصولات و 
کاتالوگ ها را به روز می کنند و منطقی نخواهد بود که هر بار که تغییری در محصولات ایجاد شود، کد اصلی نرم افزار نیاز به 
تغییر داشته باشد.
همچنین از طرفی دیگر باید در نرم افزار راهی برای فروش محصولات مرتبط با یکدیگر در نظر گرفته شود تا آن ها با سایر 
محصولات خریداری شده از یک نوع و سبک باشند. زیرا اگر محصولات ارسال شده به مشتری از لحاظ سبک متفاوت باشند، 
قطعا از آن ها ناراضی خواهد بود. فرض کنید که مشتری یک مبل، کاناپه و میز سفارش داده است و مبل از سبک ساده، کاناپه 
از سبک هنری و میز از سبک مدرن برای آن ارسال شوند. برای جلوگیری از چنین مشکلاتی در نرم افزارها، باید راه حلی در
نظر گرفت.
## راه حل الگوی طراحی کارخانه انتزاعی
راه حلی که الگوی کارخانه انتزاعی برای اینگونه مسائل پیشنهاد می دهد این است که یک Interface برای هر نوع محصول
صرف نظر از سبک های آن ایجاد شود. مثلا در این مثال باید سه Interface برای مبل، کاناپه و میز به صورت جداگانه 
تعریف شوند. سپس سبک های مختلف از این محصولات باید از این Interfaceها پیروی کنند. به عنوان مثال، تمام مبل ها با هر 
سبکی که دارند باید Interface مبل را پیاده سازی (implement) کنند؛ این روند به همین صورت باید برای محصولات دیگر انجام شود.
سپس باید در نرم افزار کارخانه ساخت محصولاتی را که از یک سبک هستند به صورت جداگانه تعریف شوند. برای این 
منظور نیاز به ایجاد یک Interface جدید خواهیم داشت که توابع و روش ساخت محصولات در آن تعریف می شوند. مثلا اگر 
نام کارخانه اصلی را کارخانه ساخت مبلمان در نظر گیریم، در این Interface توابع مربوط به ایجاد مبل، کاناپه و میز تعریف 
می شوند. همه این توابع باید یک محصول از نوع انتزاعی (Abstract) برگردانند. همچنین محصولاتی در این کارخانه ها تولید 
می شوند باید همگی محصولاتی باشند که به صورت Interface تعریف شده اند: مثلا مبل، کاناپه و میز.
برای هر سبک از محصولات، باید یک کلاس کارخانه ساخته شود که از Interface کارخانه ساخت مبلمان پیروی می کند. بر 
این اساس هر کارخانه یک کلاس است که از یک interface برای دریافت توابع پیروی می کند و محصولاتی از یک نوع 
خاص را بر می گرداند. به عنوان مثال، کارخانه ساخت مبلمان مدرن تنها می تواند مبل مدرن، کاناپه مدرن و میز مدرن ایجاد
کند
نرم افزار باید به گونه ای طراحی شده باشد که حتما کارخانه ها و محصولات از Interfaceها پیروی کنند. با این کار شما 
می توانید بدون اینکه نیازی به تغییر در کدهای اصلی نرم افزار داشته باشید، به راحتی در کارخانه و محصولات تغییر ایجاد 
کنید
</div>


### abstract_factory_

```

from __future__ import annotations
from abc import ABC, abstractmethod


class AbstractFactory(ABC):
    
    @abstractmethod
    def create_product_a(self):
        pass

    @abstractmethod
    def create_product_b(self):
        pass


class ConcreteFactory1(AbstractFactory):
   

    def create_product_a(self):
        return ConcreteProductA1()

    def create_product_b(self):
        return ConcreteProductB1()


class ConcreteFactory2(AbstractFactory):
   
    def create_product_a(self) :
        return ConcreteProductA2()

    def create_product_b(self) :
        return ConcreteProductB2()

# AbstractProductA
class AbstractProductA(ABC):
   

    @abstractmethod
    def useful_function_a(self) :
        pass


class ConcreteProductA1(AbstractProductA):
    def useful_function_a(self) :
        return "The result of the product A1."


class ConcreteProductA2(AbstractProductA):
    def useful_function_a(self) :
        return "The result of the product A2."

# AbstractProductB
class AbstractProductB(ABC):
   
    @abstractmethod
    def useful_function_b(self) :
       
        pass

    @abstractmethod
    def another_useful_function_b(self, collaborator: AbstractProductA) :
       
        pass



class ConcreteProductB1(AbstractProductB):
    def useful_function_b(self) :
        return "The result of the product B1."

    
    def another_useful_function_b(self, collaborator: AbstractProductA) :
        result = collaborator.useful_function_a()
        return f"The result of the B1 collaborating with the ({result})"


class ConcreteProductB2(AbstractProductB):
    def useful_function_b(self) -> str:
        return "The result of the product B2."

    def another_useful_function_b(self, collaborator: AbstractProductA):
       
        result = collaborator.useful_function_a()
        return f"The result of the B2 collaborating with the ({result})"


def client_code(factory: AbstractFactory) :
    
    product_a = factory.create_product_a()
    product_b = factory.create_product_b()

    print(f"{product_b.useful_function_b()}")
    print(f"{product_b.another_useful_function_b(product_a)}", end="")


if __name__ == "__main__":
   
    print("Client: Testing client code with the first factory type:")
    client_code(ConcreteFactory1())

    print("\n")

    print("Client: Testing the same client code with the second factory type:")
    client_code(ConcreteFactory2())
```


</div>
