# Greedy
<div dir="rtl">
اگر بخواهیم الگوریتم حریصانه را در یک جمله ساده تعریف کنیم بسیار شبیه به رفتار یک دم حریص است,  به این دلیل که دوتا اتفاق درشان میوفته:<br>

 - ######  تابعی روی انتخاب های ممکن تعریف میکند وهمیشه در هر انتخاب, تصمیمی که بیشترین ارزش تابع را دارد میگیرد
 - ######  در تصمیم خود تجدید نظر نمیکند

> این الگوریتم نه تنها ممکن است در برخی از مشکل ها بهترین راه حل نباشد,  بلکه میتواند باعث یک فاجعه به تمام معنا شود

الگوریتم حریصانه یک راه حل TopDown است  و مزایای این الگوریتم عبارتنداز:<br>

- 	توضیح دادنش بسیار ساده است
- 	در بعضی مسائل میتواند نتیجه بهتری ارایه دهد
	-  ##### البته فقط بعضی



 حالا سعی میکنیم با انجام چند تا مسئله ببینیم که این الگوریتم به چه شکل است
 
 ### <span style="color:orange"> Fractional knapsack</span>

برای راحت تر کردن صورت مسئله, مسئله را به این شکل مطرح میکنیم<br>
فرض میکنیم که دزدی وارد فروشگاهی میشود برای دزدی.این دزد یک کوله پشتی دارد که ظرفیت مشخصی دارد و در فروشگاه اجناسی با قیمت و وزن های متفاوتی وجود دارد و ما بایستی برای این که بتوانیم بهترین حالتی را که میتوان کوله پشتی را پر کرد و بیشترین ارزش را نیز داشته باشد, اگوریتمی طراحی کنیم.
<BR>
</div>
<div dir="rtl">

>  **نکته**:درمسئله Fractional knapsack ما میتوانیم تکه ای از جنس را نیز برداریم<br>
 
**حرفه ای ترین** راه حلی که میتوان برای حل این مسئله پیدا کرد این است که از روش حریصانه استفاده کنیم.ایده اصلی این است که چگالی(در این مسئله میتوانیم از کلمه **ارزش** نیز استفاده کنیم)تمام ایتم ها را بدست بیاوریم و به ترتیب انهارا وارد کوله پشتی کنیم و وقتی که به یک ایتم با وزن بیشتر از ظرفیت کوله رسیدیم, میتوانیم تا آن حجمی از ان را برداریم که کوله پشتی پر شود
</div>

#### <span style="color:purple">Fractional Knapsack Code In Python</span>

```

arr = [(2,12),(5,8),(4,16),(2,12)]   # (weight, value)
W = 3

def fractional_knapsack(arr, W):
    density = []
    knapsack = []

    value_in_knapsack = 0

    for elm in arr:
    	# calculating the cost of items
        cost = elm[1]/elm[0]
        density.append((cost,elm))
	
    # sorting them in reverse
    density.sort(key= lambda x: x[0], reverse=True)
    
    for elm in density:
        if elm[1][0] = W:
        	# if there is a space for taking the whole item
            knapsack.append((elm[1] , "fraction: 1"))
            W -= elm[1][0]
            value_in_knapsack += elm[1][1]
        else:
        	# if there is not enough space for the whole item
            # fractioning the item and full the knapsack
            fraction = W/elm[1][0]
            knapsack.append((elm[1] , f"fraction: {fraction}"))
            value_in_knapsack += (elm[1][1] * fraction)
            break
    
    return knapsack, value_in_knapsack
```
<div dir="rtl">

## <span style="color:Green">Ford-Fulkerson</span>

حالا به سراغ الگوریتم Ford-Fulkerson میرویم که از روش حریصانه برای حساب کردن مسیری با بیشترین جریان ممکن در شبگه و یا نمودار استفاده میکند<br>

برای بهتر متوجه شدن این اگوریتم میتوانیم یک شبکه ای از لوله ها را تصور کنیم که هر کدام ظرفیتی دارند و ما میخواهیم بیشترین حجم مایعی که از مبدا, به مقصد میرسد را به دست بیاوریم.

![image](https://cdn.programiz.com/sites/tutorial2program/files/flow-network.png)

اصطلاحاتی که برای حل این مسئله نیاز داریم عبارتنداز:

1. **مسیر افزایش** : این مسیر باقیمانده در شبکه را نشان میدهد
2. **مسیر طی شده** : این مسیر طی شده را نشان میدهد
3. **ظرفیت باقیمانده**: این ظرفیت جریان اب را مساوی حداکثر حجم لوله ای قرار میدهد که کمترین حجم را در مسیر طی شده دارد

روشی که برای حل این تمرین داریم به اینصورت است:<br>
1. جریان را در همه لبه ها صفر در نظر میگیریم
2. اگر مسیری بین مبدا و مقصد وجود دارد, این مسیر طی شده را به مسیر طی شده اضافه میکنیم
3. ظرفیت باقیمانده را به روز رسانی کن
</div>

### <span style="color:purple">Ford-Fulkerson Code In Python</span>

```
from collections import defaultdict


class Graph:

    def __init__(self, graph):
        self.graph = graph
        self.ROW = len(graph)


    # Using BFS as a searching algorithm 
    def searching_algo_BFS(self, s, t, parent):

        visited = [False] * (self.ROW)
        queue = []

        queue.append(s)
        visited[s] = True

        while queue:

            u = queue.pop(0)

            for ind, val in enumerate(self.graph[u]):
                if visited[ind] == False and val > 0:
                    queue.append(ind)
                    visited[ind] = True
                    parent[ind] = u

        return True if visited[t] else False

    # Applying fordfulkerson algorithm
    def ford_fulkerson(self, source, sink):
        parent = [-1] * (self.ROW)
        max_flow = 0

        while self.searching_algo_BFS(source, sink, parent):

            path_flow = float("Inf")
            s = sink
            while(s != source):
                path_flow = min(path_flow, self.graph[parent[s]][s])
                s = parent[s]

            # Adding the path flows
            max_flow += path_flow

            # Updating the residual values of edges
            v = sink
            while(v != source):
                u = parent[v]
                self.graph[u][v] -= path_flow
                self.graph[v][u] += path_flow
                v = parent[v]

        return max_flow


graph = [[0, 8, 0, 0, 3, 0],
         [0, 0, 9, 0, 0, 0],
         [0, 0, 0, 0, 7, 2],
         [0, 0, 0, 0, 0, 5],
         [0, 0, 7, 4, 0, 0],
         [0, 0, 0, 0, 0, 0]]

g = Graph(graph)

source = 0
sink = 5

print("Max Flow: %d " % g.ford_fulkerson(source, sink))
```

## <span style="color:Green">Dijkstra's Algorithm</span>
الگوریتم دایجسترا به ما این امکان را میدهد که بتوانیم کوتاه ترین مسیر بین دو راس را پیدا کنیم<br>



</div>






<span style="color:blue">
</span>
