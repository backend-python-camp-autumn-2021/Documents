<div dir="rtl">

# Sorting Algorithms

## فهرست 
- [الگوریتم مرتب سازی حبابی](https://github.com/zahrafarrokhi/Bubble_sort#readme)
- [الگوریتم مرتب سازی انتخابی](https://github.com/zahrafarrokhi/Bubble_sort#readme)
- [الگوریتم مرتب سازی درجی](https://github.com/zahrafarrokhi/Bubble_sort#readme)
- [الگوریتم مرتب سازی ادغامی](https://github.com/zahrafarrokhi/Bubble_sort#readme)
- [الگوریتم مرتب سازی سریع](https://github.com/zahrafarrokhi/Bubble_sort#readme)
- [الگوریتم مرتب سازی شمارشی](https://github.com/zahrafarrokhi/Bubble_sort#readme)




 </div
 
 
 

 
 <hr>
 
<div dir="rtl">

# الگوریتم مرتب سازی حبابی

در این آموزش ، نحوه عملکرد مرتب سازی حبابی را خواهید آموخت.

## مرتب سازی حبابی چگونه کار می کند؟
با شروع از شاخص اول ، عناصر اول و دوم را مقایسه کنید. اگر عنصر اول بزرگتر از عنصر دوم باشد ، آنها عوض می شوند.
اکنون ، عناصر دوم و سوم را مقایسه کنید. اگر مرتب نیستند آنها را عوض کنید.
روند فوق تا آخرین عنصر ادامه دارد.

</div>


### الگوریتم مرتب سازی حبابی

```

bubbleSort(array)
  for i <- 1 to indexOfLastUnsortedElement-1
    if leftElement > rightElement
      swap leftElement and rightElement
end bubbleSort
```

### الگوریتم مرتب سازی حبابی در پایتون
```
# Bubble sort in Python

def bubbleSort(array):
    
    # run loops two times: one for walking throught the array 
    # and the other for comparison
    for i in range(len(array)):
        for j in range(0, len(array) - i - 1):

            # To sort in descending order, change > to < in this line.
            if array[j] > array[j + 1]:
                
                # swap if greater is at the rear position
                (array[j], array[j + 1]) = (array[j + 1], array[j])


data = [-2, 45, 0, 11, -9]
bubbleSort(data)
print('Sorted Array in Asc ending Order:')
print(data)
```


<div dir="rtl">
 
 ### الگوریتم مرتب سازی حبابی بهینه شده


در کد بالا ، تمام مقایسه های ممکن حتی اگر آرایه مرتب شده باشد انجام می شود. زمان اجرا را افزایش می دهد.

کد را می توان با معرفی یک متغیر اضافی مبادله شده بهینه کرد. پس از هر بار تکرار ، اگر مبادله ای انجام نشود ، دیگر نیازی به انجام حلقه های بعدی نیست.

در چنین حالتی ، متغیر مبادله نادرست تنظیم می شود. بنابراین ، می توانیم از تکرارهای بعدی جلوگیری کنیم.

الگوریتم زیر برای مرتب سازی حباب بهینه شده است
</div>

###  الگوریتم حبابی  با استفاده ازمتغیر(swapped)
```
bubbleSort(array)
  swapped <- false
  for i <- 1 to indexOfLastUnsortedElement-1
    if leftElement > rightElement
      swap leftElement and rightElement
      swapped <- true
end bubbleSort
```

### الگوریتم مرتب سازی حبابی بهینه شده
```
# Bubble sort in Python

def bubbleSort(array):
    
    # Run loops two times: one for walking throught the array
    # and the other for comparison
    for i in range(len(array)):
        
        # swapped keeps track of swapping
        swapped = True
        for j in range(0, len(array) - i - 1):

            # To sort in descending order, change > to < in this line.
            if array[j] > array[j + 1]:

                # Swap if greater is at the rear position
                (array[j], array[j + 1]) = (array[j + 1], array[j])
                swapped = False
                
        # If there is not swapping in the last swap, then the array is already sorted.
        if swapped:
            break


data = [-2, 45, 0, 11, -9]
bubbleSort(data)
print('Sorted Array in Ascending Order:')
print(data)
```
<div dir="rtl">

###### پیچیدگی
مرتب سازی حباب یکی از ساده ترین الگوریتم های مرتب سازی است. دو حلقه در الگوریتم اجرا شده است
تعداد مقایسه
</div>

```

(n - 1) + (n - 2) + (n - 3) +.....+ 1 = n(n - 1) / 2

```
<div dir="rtl">
 
###### پیچیدگی: O (n2)

همچنین ، ما می توانیم پیچیدگی را به سادگی با مشاهده تعداد حلقه ها تجزیه و تحلیل کنیم. 2 حلقه وجود دارد بنابراین پیچیدگی n * n = n2 است

###### پیچیدگی بدترین حالت: O (n2)
اگر بخواهیم به ترتیب صعودی مرتب شویم و آرایه به ترتیب نزولی باشد ، بدترین حالت رخ می دهد.

###### پیچیدگی بهترین حالت: O (n)
اگر آرایه از قبل مرتب شده باشد ، دیگر نیازی به مرتب سازی نیست.

###### پیچیدگی حالت میانگین: O (n2)
زمانی اتفاق می افتد که عناصر آرایه به ترتیب بهم ریخته (نه صعودی و نه نزولی) باشند.

###### پیچیدگی فضا:O(1)
زیرا از یک  متغیر اضافی برای مبادله استفاده می شود.
###### پیچیدگی فضا در االگوریتم بهینه سازی شده :O(2)
متغیرswapp بر پیچیدگی افزوده
آن را O(2)می کند
</div>

<hr>


 
<div dir="rtl">

# الگوریتم مرتب سازی انتخابی

در این آموزش ، نحوه عملکرد مرتب سازی انتخابی را خواهید آموخت.

## مرتب سازی انتخابی چگونه کار می کند؟
1. اولین عنصر را حداقل(مینیمم) قرار دهید
2. مینیمم را با عنصر دوم مقایسه کنید. اگر عنصر دوم کوچکتر از مینیمم است ، عنصر دوم را به عنوان مینیمم اختصاص دهید.
مینیمم را با عنصر سوم مقایسه کنید. باز هم ، اگر عنصر سوم کوچکتر باشد ، مینیمم را به عنصر سوم اختصاص دهید
در غیر این صورت کاری انجام ندهید. این روند تا آخرین عنصر ادامه دارد.
3. بعد از هر بار تکرار ، مینیمم در جلوی لیست مرتب نشده قرار می گیرد.
4. برای هر تکرار ، ایندکس از اولین عنصر مرتب نشده شروع می شود 
مرحله 1 تا 3 تکرار می شود تا زمانی که همه عناصر در موقعیت صحیح خود قرار بگیرند.

</div>

### الگوریتم مرتب سازی انتخابی
```

selectionSort(array, size)
  repeat (size - 1) times
  set the first unsorted element as the minimum
  for each of the unsorted elements
    if element < currentMinimum
      set element as new minimum
  swap minimum with first unsorted position
end selectionSort
```

### الگوریتم مرتب سازی انتخابی در پایتون
```
# Selection sort in Python

def selectionSort(array, size):
   
    for step in range(size):
        min_idx = step

        for i in range(step + 1, size):
         
            # to sort in descending order, change > to < in this line
            # select the minimum element in each loop
            if array[i] < array[min_idx]:
                min_idx = i
         
        # put min at the correct position
        (array[step], array[min_idx]) = (array[min_idx], array[step])


data = [-2, 45, 0, 11, -9]
size = len(data)
selectionSort(data, size)
print('Sorted Array in Ascending Order:')
print(data)


```

<div dir="rtl">
 
###### پیچیدگی
 دو حلقه در الگوریتم اجرا شده است
تعداد مقایسه
</div>

```

(n - 1) + (n - 2) + (n - 3) +.....+ 1 = n(n - 1) / 2

```
<div dir="rtl">
 
###### پیچیدگی: O (n2)

همچنین ، ما می توانیم پیچیدگی را به سادگی با مشاهده تعداد حلقه ها تجزیه و تحلیل کنیم. 2 حلقه وجود دارد بنابراین پیچیدگی n * n = n2 است

###### پیچیدگی بدترین حالت: O (n2)
اگر بخواهیم به ترتیب صعودی مرتب شویم و آرایه به ترتیب نزولی باشد ، بدترین حالت رخ می دهد.

###### پیچیدگی بهترین حالت: O (n2)
وقتی آرایه مرتب شده باشد رخ می دهد

###### پیچیدگی حالت میانگین: O (n2)
زمانی اتفاق می افتد که عناصر آرایه به ترتیب بهم ریخته (نه صعودی و نه نزولی) باشند.

###### پیچیدگی فضا:O(1)
زیرا از یک  متغیر اضافی temp برای مبادله استفاده می شود.

#####  مرتب سازی انتخابی هنگامی استفاده میشود  :

- یک لیست کوچک مرتب می شود
- هزینه مبادله مهم نیست
- بررسی همه عناصر اجباری است
- هزینه نوشتن در یک حافظه مانند حافظه فلش مهم است (تعداد نوشتن / مبادله O (n) در مقایسه با O (n2) نوع حباب است)



</div>
<hr>

<div dir="rtl">

# الگوریتم مرتب سازی درجی 

در این آموزش ، نحوه عملکرد مرتب سازی درجی را خواهید آموخت.

## مرتب سازی درجی چگونه کار می کند؟
1. فرض می شود که اولین عنصر در آرایه مرتب شده است. عنصر دوم را بردارید و آن را جداگانه در کلید ذخیره کنید.
 مقایسه کلید با اولین عنصر. اگر اولین عنصر از کلید بزرگتر باشد ، کلید مقابل عنصر اول قرار می گیرد
2. اکنون ، دو عنصر اول مرتب شده اند
سومین عنصر را بردارید و آن را با عناصر سمت چپ آن مقایسه کنید. آن را درست در پشت عنصر کوچکتر از آن قرار دهید. اگر عنصری کوچکتر از آن نیست ، آن را در ابتدای آرایه قرار دهید.
3. به همین ترتیب ، هر عنصر مرتب نشده را در موقعیت صحیح خود قرار دهید.

</div>


### الگوریتم مرتب سازی درجی

```

insertionSort(array)
  mark first element as sorted
  for each unsorted element X
    'extract' the element X
    for j <- lastSortedIndex down to 0
      if current element j > X
        move sorted element to the right by 1
    break loop and insert X here
end insertionSort
```

### الگوریتم مرتب سازی درجی در پایتون
```
def insertionSort(array):

    for step in range(1, len(array)):
        key = array[step]
        j = step - 1
        
        # Compare key with each element on the left of it until an element smaller than it is found
        # For descending order, change key<array[j] to key>array[j].        
        while j >= 0 and key < array[j]:
            array[j + 1] = array[j]
            j = j - 1
        
        # Place key at after the element just smaller than it.
        array[j + 1] = key


data = [9, 5, 1, 4, 3]
insertionSort(data)
print('Sorted Array in Ascending Order:')
print(data)

```




<div dir="rtl">

###### پیچیدگی بدترین حالت: O (n2)
فرض کنید ، یک آرایه به ترتیب صعودی است و شما می خواهید آن را به ترتیب نزولی مرتب کنید. در این حالت ، بدترین حالت پیچیدگی رخ می دهد.
هر عنصر باید با هر یک از عناصر دیگر مقایسه شود بنابراین ، برای هر عنصر n ، (n-1) تعداد مقایسه انجام می شود.

بنابراین ، تعداد کل مقایسه ها = n * (n-1) n2
###### پیچیدگی بهترین حالت: O (n)
وقتی آرایه از قبل مرتب شده باشد ، حلقه خارجی برای n تعداد دفعات اجرا می شود در حالی که حلقه داخلی به هیچ وجه اجرا نمی شود. بنابراین ، فقط تعداد n مقایسه وجود دارد. بنابراین ، پیچیدگی خطی است.

###### پیچیدگی حالت میانگین: O (n2)
زمانی اتفاق می افتد که عناصر یک آرایه به ترتیب بهم ریخته (نه صعودی و نه نزولی) باشند.

###### پیچیدگی فضا:O(1)
زیرا از یک  متغیر اضافی برای مبادله استفاده می شود.
##### مرتب سازی درجی هنگامی استفاده می شود:
- آرایه تعداد کمی عنصر دارد
-  فقط چند عنصر برای مرتب سازی باقی مانده است



</div>
<hr>
<div dir="rtl">

# الگوریتم مرتب سازی ادغامی

در این آموزش ، نحوه عملکرد مرتب سازی ادغامی را خواهید آموخت.

## مرتب سازی ادغامی چگونه کار می کند؟
یکی از مشهورترین الگوریتم های مرتب سازی است که بر اساس اصل الگوریتم تقسیم و غلبه طراحی شده است.
با استفاده از تکنیک تقسیم و غلبه ، یک مسئله را به زیرمشکلات تقسیم می کنیم. 
وقتی راه حل برای هر زیرمشکل آماده شد ، ما نتایج حاصل از زیرمشکلات را برای حل مشکل اصلی "ترکیب" می کنیم.
فرض کنید ما باید یک آرایه  Aمرتب کنیم
یک مسئله فرعی می تواند یک زیر بخش از این آرایه را با شروع از شاخص p و پایان دادن به شاخص r ، به عنوان A [p..r] نشان دهد.

##### تقسیم
اگر q نقطه نیمه راه بین p و r باشد ، پس می توان زیر مجموعه A [p..r] را به دو آرایه A [p..q] و A [q + 1، r] تقسیم كرد.
######  غلبه
در مرحله تسخیر ، سعی می کنیم هم زیرآرایه های A [p..q] و هم A [q + 1، r] را مرتب کنیم. اگر هنوز به مورد اصلی نرسیده ایم ، دوباره هر دو زیرآرایه را تقسیم می کنیم و سعی می کنیم آنها را مرتب کنیم.
######  ترکیب
هنگامی که مرحله تسخیر به مرحله پایه می رسد و دو زیرآرایه مرتب شده A [p..q] و A [q + 1، r] برای آرایه A [p..r] بدست می آوریم ، با ایجاد یک آرایه مرتب شده A نتایج را ترکیب می کنیم [p..r] از دو زیرآرایه مرتب شده A [p..q] و A [q + 1، r].
</div>


### الگوریتم مرتب سازی ادغامی

```

MergeSort(A, p, r):
    if p > r 
        return
    q = (p+r)/2
    mergeSort(A, p, q)
    mergeSort(A, q+1, r)
    merge(A, p, q, r)
```

### الگوریتم مرتب سازی ادغامی در پایتون
```
# MergeSort in Python


def mergeSort(array):
    if len(array) > 1:

        #  r is the point where the array is divided into two subarrays
        r = len(array)//2
        L = array[:r]
        M = array[r:]

        # Sort the two halves
        mergeSort(L)
        mergeSort(M)

        i = j = k = 0

        # Until we reach either end of either L or M, pick larger among
        # elements L and M and place them in the correct position at A[p..r]
        while i < len(L) and j < len(M):
            if L[i] < M[j]:
                array[k] = L[i]
                i += 1
            else:
                array[k] = M[j]
                j += 1
            k += 1

        # When we run out of elements in either L or M,
        # pick up the remaining elements and put in A[p..r]
        while i < len(L):
            array[k] = L[i]
            i += 1
            k += 1

        while j < len(M):
            array[k] = M[j]
            j += 1
            k += 1


# Print the array
def printList(array):
    for i in range(len(array)):
        print(array[i], end=" ")
    print()


# Driver program
if __name__ == '__main__':
    array = [6, 5, 12, 10, 9, 1]

    mergeSort(array)

    print("Sorted array is: ")
    printList(array)
```


###### پیچیدگی بدترین حالت: O (n * log n)

###### پیچیدگی بهترین حالت: O (n * log n)

###### پیچیدگی حالت میانگین: O (n * log n)

###### پیچیدگی فضا:O(1)
پیچیدگی فضایی نوع ادغام O (n) است
###### برنامه های مرتب سازی ادغامی
- مشکل شمارش وارونگی
- مرتب سازی خارجی
- مرتب سازی خارجی

</div>

<hr>
<div dir="rtl">

# الگوریتم مرتب سازی سریع

در این آموزش ، نحوه عملکرد مرتب سازی سریع را خواهید آموخت.

## مرتب سازی سریع چگونه کار می کند؟
###### تقسیم
آرایه به قسمتهای فرعی تقسیم می شود که محور را به عنوان نقطه تقسیم می کند. عناصر کوچکتر از محور در سمت چپ محور و عناصر بزرگتر از محور در سمت راست قرار می گیرند.
###### غلبه
قسمتهای فرعی چپ و راست با انتخاب عناصر محوری برای آنها دوباره با استفاده از بخش تقسیم می شوند. این امر می تواند با انتقال مجدد قسمتهای فرعی به الگوریتم حاصل شود.
###### ترکیب
این مرحله نقش مهمی در مرحله quicksort ندارد. آرایه قبلاً در انتهای مرحله تسخیر مرتب شده است.

</div>


### الگوریتم مرتب سازی سریع

```

quickSort(array, leftmostIndex, rightmostIndex)
  if (leftmostIndex < rightmostIndex)
    pivotIndex <- partition(array,leftmostIndex, rightmostIndex)
    quickSort(array, leftmostIndex, pivotIndex)
    quickSort(array, pivotIndex + 1, rightmostIndex)

partition(array, leftmostIndex, rightmostIndex)
  set rightmostIndex as pivotIndex
  storeIndex <- leftmostIndex - 1
  for i <- leftmostIndex + 1 to rightmostIndex
  if element[i] < pivotElement
    swap element[i] and element[storeIndex]
    storeIndex++
  swap pivotElement and element[storeIndex+1]
return storeIndex + 1
```

### الگوریتم مرتب سازی سریع در پایتون
```
# Quick sort in Python


# Function to partition the array on the basis of pivot element
def partition(array, low, high):

    # Select the pivot element
    pivot = array[high]
    i = low - 1

    # Put the elements smaller than pivot on the left and greater 
    #than pivot on the right of pivot
    for j in range(low, high):
        if array[j] <= pivot:
            i = i + 1
            (array[i], array[j]) = (array[j], array[i])

    (array[i + 1], array[high]) = (array[high], array[i + 1])

    return i + 1


def quickSort(array, low, high):
    if low < high:

        # Select pivot position and put all the elements smaller 
        # than pivot on left and greater than pivot on right
        pi = partition(array, low, high)

        # Sort the elements on the left of pivot
        quickSort(array, low, pi - 1)

        # Sort the elements on the right of pivot
        quickSort(array, pi + 1, high)


data = [8, 7, 2, 1, 0, 9, 6]
size = len(data)
quickSort(data, 0, size - 1)
print('Sorted Array in Ascending Order:')
print(data)

```



###### پیچیدگی
مرتب سازی حباب یکی از ساده ترین الگوریتم های مرتب سازی است. دو حلقه در الگوریتم اجرا شده است
تعداد مقایسه
</div>

```

(n - 1) + (n - 2) + (n - 3) +.....+ 1 = n(n - 1) / 2

```
<div dir="rtl">
 

###### پیچیدگی بدترین حالت: [Big-O]: O (n2)
هنگامی رخ می دهد که عنصر محوری انتخاب شده بزرگترین یا کوچکترین عنصر باشد.
این شرایط منجر به حالتی می شود که عنصر محوری در انتهای انتهایی آرایه مرتب شده قرار داشته باشد. یک زیر آرایه همیشه خالی است و زیر آرایه دیگر شامل n - 1 عنصر است. بنابراین ، quicksort فقط در این زیر آرایه فراخوانی می شود.
با این حال ، الگوریتم مرتب سازی سریع عملکرد بهتری برای محورهای پراکنده دارد.

###### پیچیدگی بهترین حالت:[Big-omega]: O(n*log n)

زمانی اتفاق می افتد که عنصر محوری همیشه عنصر میانی یا نزدیک به عنصر میانی باشد.

###### پیچیدگی حالت میانگین: [Big-theta]: O(n*log n)

این اتفاق زمانی رخ می دهد که شرایط فوق رخ ندهد..

###### پیچیدگی فضا:O(log n).
###### Quicksort زمانی اجرا می شود
- زبان برنامه نویسی بازگشتی 
- پیچیدگی زمان مهم است
- پیچیدگی فضا مهم است


</div>
<hr>
<div dir="rtl">

# الگوریتم مرتب سازی شمارشی

در این آموزش ، نحوه عملکرد مرتب سازی شمارشی را خواهید آموخت.

## مرتب سازی شمارشی چگونه کار می کند؟
1. از آرایه داده شده بیشترین عنصر را پیدا کنید (بگذارید حداکثر باشد).
2. یک آرایه با طول حداکثر 1 را با تمام عناصر 0 شروع کنید. این آرایه برای ذخیره تعداد عناصر در آرایه استفاده می شود.
3. تعداد هر عنصر را در شاخص مربوطه در آرایه شمارش ذخیره کنید
4. جمع تجمعی عناصر آرایه شمارش را ذخیره کنید. این به قرار دادن عناصر در فهرست صحیح آرایه مرتب شده کمک می کند.
5. شاخص هر عنصر از آرایه اصلی را در آرایه شمارش پیدا کنید. این تعداد تجمعی را می دهد. عنصر را در شاخص محاسبه کنید.
6. پس از قرار دادن هر عنصر در موقعیت صحیح خود ، تعداد آن را یکی کاهش دهید.
</div>


### الگوریتم مرتب سازی شمارشی

```

countingSort(array, size)
  max <- find largest element in array
  initialize count array with all zeros
  for j <- 0 to size
    find the total count of each unique element and 
    store the count at jth index in count array
  for i <- 1 to max
    find the cumulative sum and store it in count array itself
  for j <- size down to 1
    restore the elements to array
    decrease count of each element restored by 1
```

### الگوریتم مرتب سازی شمارشی در پایتون
```
# Counting sort in Python programming


def countingSort(array):
    size = len(array)
    output = [0] * size

    # Initialize count array
    count = [0] * 10

    # Store the count of each elements in count array
    for i in range(0, size):
        count[array[i]] += 1

    # Store the cummulative count
    for i in range(1, 10):
        count[i] += count[i - 1]

    # Find the index of each element of the original array in count array
    # place the elements in output array
    i = size - 1
    while i >= 0:
        output[count[array[i]] - 1] = array[i]
        count[array[i]] -= 1
        i -= 1

    # Copy the sorted elements into original array
    for i in range(0, size):
        array[i] = output[i]


data = [4, 2, 2, 8, 3, 3, 1]
countingSort(data)
print("Sorted Array in Ascending Order: ")
print(data)

```


<div dir="rtl">
 

###### پیچیدگی بدترین حالت: O(n+k)

###### پیچیدگی بهترین حالت: O(n+k)

###### پیچیدگی حالت میانگین: O(n+k)

###### پیچیدگی فضا:O(max)
پیچیدگی فضایی شمارش مرتب سازی O (حداکثر) است. دامنه عناصر بیشتر ، پیچیدگی فضا بزرگتر است.

###### این مرتب سازی زمانی استفاده میشود
- عددهای صحیح کوچکتر با تعداد زیاد وجود دارد
- پیچیدگی خطی نیاز است.


</div>








