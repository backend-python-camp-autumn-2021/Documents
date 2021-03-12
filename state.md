<div dir="rtl">



 </div
 
 
 

 
 <hr>
 
<div dir="rtl">

# State

حالات یک الگوی طراحی رفتاری ست که به شی اجازه میدهد هر زمان وضعیت داخلی اش تغییر کرد ,رفتار خود را تغییر دهد. این رخداد زمانی اتفاق می افتد که شی کلاس خود را تغییر دهد.

![first pic](https://refactoring.guru/images/patterns/content/state/state-en.png)

## مشکل :pensive:
این الگوی طراحی به **ماشین حالات متناهی (Finite-State Machine)** بسیار شباهت دارد.

![first pic](https://refactoring.guru/images/patterns/diagrams/state/problem1.png)


ایده این است که,در هر زمان خاص,حالات متناهی وجود دارد که برنامه میتواند درآن حالات وجود داشته باشد. در هر state منحصز به فرد,برنامه رفتار مختلفی از خود نشان میدهد,و برنامه میتواند از یک حالت به حالت دیگر مدام درحال تغییر باشد. اگرچه,وابسته به حالت کنونی برنامه میتواند به حالت جدبد تغییر کند یا نکند.این قوانین تغییرپذیری که transmitions خوانده میشوند,متناهی و از پیش تعیین شده نیز هستند.

همچنین میتوانید این رویکرد را در مورد اشیا نیز در نظر بگیرید.برای مثال کلاس document را در نظر بگیرید,document میتواند در یکی از این حالات باشد: draft,moderation,published. متد publish در حالات مختلف متفاوت عمل میکند:

1. در حالت draft,داکیومنت را به مود moderate می برد.
2. در حالت moderation,داکیومنت را به صورت public در می آورد ولی به شرطی که یوزر admin باشد.
3. در حالت published, هیچ کاری انجام نمی شود.

![first pic](https://refactoring.guru/images/patterns/diagrams/state/problem2-en.png)



ماشین های حالات معمولا با جملات شرطی متعددی پیاده سازی میشوند که رفتار مناسب را با توجه به حالاتی که آبجکت درآن وجود دارد انتخاب می کنند. معمولا این "state" ,تنها مجموعه ای از وقادیر مختلف آبجکت هاست. حتی اگر تا به حال در مورد ماشین حالات متناهی نشنیده اید,احتمالا حد اقل یک بار یک state پیاده سازی کرده اید.کد زیر برایتان آسنا نیست؟

</div>

```
class Document is
    field state: string
    // ...
    method publish() is
        switch (state)
            "draft":
                state = "moderation"
                break
            "moderation":
                if (currentUser.role == 'admin')
                    state = "published"
                break
            "published":
                // Do nothing.
                break
    // ...

```
<div dir="rtl">

هر چه بیشتر به کلاس Document حالات بیشتر اضافه کنیم ,بزرگ ترین ضعف ماشین حالات شرطی بیشتر نمایان میشود. بیشتر متد ها در برگیرنده جملات شرطی هستند که رفتار مناسب را در بسته به وضعیت کنونی ماشین حالت انتخاب می کنند.نگهداری کد های اینچنینی بسیار دشوار است چراکه هر گونه تغییر در لاجیک ممکن است نیازمند تغییر در شرایط state در هر متد باشد.

این مشکل با بزرگ شدن پروژه بیشتر میشود.تقریبا غیر ممکن است که تمام stateهای ممکن را در زمان طراحی پیش بینی کرد. بنابراین,ماشین حالات ضعیفی که با مجموعه شرایط محدود ساخته مشود,به مرور زمان میتواند بسیار به هم ریخته شود.

# راه حل :smiley:

الگوی state پیشنهاد میکند که کلاس جدید برای تمام حالات ممکن یک آبجکت بسازد و تمام stateهای خاص را در این کلاس کلاس ها استخراج کند.

به جای اینکه تمام رفتار ها به تنهایی پیاده سازی شوند,آبجکت اصلی,یا همان context,رفرنسی برای هر آبجکت حالات نگهداری میکند که نشان دهنده ی حالات کنونی اش می باشد و نماینده تمام حالات مربوط به آن شی است.

![pic2](https://refactoring.guru/images/patterns/diagrams/state/solution-en.png)

# شبیه سازی دنیای واقعی :blue_car:
دکمه ها و سوئیچها روی گوشی موبایلتان با توجه به state کنونی کارهای مختلفی انجام میدهند.
- وقتی گوشی قفل نشده باشد,کلیک روی دکمه ها باعث میشود کارهای مختلفی انحام شود.
- وقتی گوشی قفل شده باشد دکمه ها باعث میشوند که صفحه قفل شود.
- وقتی شارژ گوشی موبایل کم شده باشد,هر دکمه باعث میشود که صفحه شارژ نمایان شود.

#ساختار 

![pic3](https://refactoring.guru/images/patterns/diagrams/state/structure-en-indexed.png)

1. کلاس Context رفرنس یکی از اشیای concrete state را در خود ذخیره میکند و این رفرنس را به تمام حالات خاص اختصاص می دهد.

2. اینترفیس State حالات خاص متدها را اعلان میکند.این متدها باید برای تمام concrete state ها معنی دهند چراکه نباید بعضی از state ها متدهای بلااستفاده داشته باشند.

3. کلاس Concrete State پیاده سازی مربوط به خودش را برای هر حالت خاص متدها ایجاد میکند. برای جلوگیری از چندگانه نشدن کدها در state های مختلف باید از کلاس های abstract استفاده کنیم که رفتارهای مشابه را encapsulate کند.

4. هم context و هم concrete state میتوانند state یعد را تنظیم کنند و انتقال حالت اصلی را به وسیله جابه جایی حالت شی لینک شده به context انجام دهند.

# سودوکد

در این مثال الگوی state بر اساس آهنگی که در حال پخش است مدیا پلیر را کنترل میکند.

![pic3](https://refactoring.guru/images/patterns/diagrams/state/example.png)


</div>

```
// The AudioPlayer class acts as a context. It also maintains a
// reference to an instance of one of the state classes that
// represents the current state of the audio player.
class AudioPlayer is
    field state: State
    field UI, volume, playlist, currentSong

    constructor AudioPlayer() is
        this.state = new ReadyState(this)

        // Context delegates handling user input to a state
        // object. Naturally, the outcome depends on what state
        // is currently active, since each state can handle the
        // input differently.
        UI = new UserInterface()
        UI.lockButton.onClick(this.clickLock)
        UI.playButton.onClick(this.clickPlay)
        UI.nextButton.onClick(this.clickNext)
        UI.prevButton.onClick(this.clickPrevious)

    // Other objects must be able to switch the audio player's
    // active state.
    method changeState(state: State) is
        this.state = state

    // UI methods delegate execution to the active state.
    method clickLock() is
        state.clickLock()
    method clickPlay() is
        state.clickPlay()
    method clickNext() is
        state.clickNext()
    method clickPrevious() is
        state.clickPrevious()

    // A state may call some service methods on the context.
    method startPlayback() is
        // ...
    method stopPlayback() is
        // ...
    method nextSong() is
        // ...
    method previousSong() is
        // ...
    method fastForward(time) is
        // ...
    method rewind(time) is
        // ...


// The base state class declares methods that all concrete
// states should implement and also provides a backreference to
// the context object associated with the state. States can use
// the backreference to transition the context to another state.
abstract class State is
    protected field player: AudioPlayer

    // Context passes itself through the state constructor. This
    // may help a state fetch some useful context data if it's
    // needed.
    constructor State(player) is
        this.player = player

    abstract method clickLock()
    abstract method clickPlay()
    abstract method clickNext()
    abstract method clickPrevious()


// Concrete states implement various behaviors associated with a
// state of the context.
class LockedState extends State is

    // When you unlock a locked player, it may assume one of two
    // states.
    method clickLock() is
        if (player.playing)
            player.changeState(new PlayingState(player))
        else
            player.changeState(new ReadyState(player))

    method clickPlay() is
        // Locked, so do nothing.

    method clickNext() is
        // Locked, so do nothing.

    method clickPrevious() is
        // Locked, so do nothing.


// They can also trigger state transitions in the context.
class ReadyState extends State is
    method clickLock() is
        player.changeState(new LockedState(player))

    method clickPlay() is
        player.startPlayback()
        player.changeState(new PlayingState(player))

    method clickNext() is
        player.nextSong()

    method clickPrevious() is
        player.previousSong()


class PlayingState extends State is
    method clickLock() is
        player.changeState(new LockedState(player))

    method clickPlay() is
        player.stopPlayback()
        player.changeState(new ReadyState(player))

    method clickNext() is
        if (event.doubleclick)
            player.nextSong()
        else
            player.fastForward(5)

    method clickPrevious() is
        if (event.doubleclick)
            player.previous()
        else
            player.rewind(5)

```
<div dir="rtl">



