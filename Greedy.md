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
<div dir="rtl">

## <span style="color:Green">Dijkstra's Algorithm</span>
الگوریتم دایجسترا به ما این امکان را میدهد که بتوانیم کوتاه ترین مسیر بین دو راس را پیدا کنیم<br>

فرض می‌شود که یک گراف به همراه یک راس مبدا داده شده و هدف پیدا کردن کوتاه‌ترین مسیر به همه راس‌های موجود در گراف مذکور است. الگوریتم دایجسترا شباهت زیادی به «الگوریتم پریم» (Prim’s Algorithm) برای «درخت پوشای کمینه» (Minimum Spanning Tree) دارد. در الگوریتم دایجسترا نیز درخت کوتاه‌ترین مسیر با استفاده از مبدا داده شده به عنوان ریشه، ساخته می‌شود. در هر مرحله از الگوریتم، راسی پیدا می‌شود که در مجموعه دیگر (مجموعه راس‌های در نظر گرفته نشده) قرار دارد و دارای کمترین فاصله از ریشه است. در ادامه، گام‌های مورد استفاده در الگوریتم دایجسترا به منظور یافتن کوتاه‌ترین مسیر از یک راس مبدا مجرد به دیگر راس‌ها در گراف داده شده به صورت مشروح بیان شده‌اند.


1. ساخت مجموعه sptSet (مجموعه درخت کوتاه‌ترین مسیر | Shortest Path Tree Set) که به دنبال راس‌های قرار گرفته در درخت کوتاه‌ترین مسیر می‌گردد؛ یعنی، راسی که حداقل فاصله آن از مبدا محاسبه و نهایی شده است. به طور مقدماتی، این مجموعه خالی است.
2. تخصیص یک مقدار فاصله به همه راس‌ها در گراف ورودی. مقداردهی اولیه همه مقادیر فاصله‌ها به عنوان INFINITE. تخصیص مقدار فاصله صفر به راس مبدا که موجب می‌شود این راس در ابتدا انتخاب شود.
3. تا هنگامی که sptSet شامل همه راس‌ها نشده است، اقدامات زیر انجام می‌شود:
	1. راس u انتخاب می‌شود که در sptSet نیست و دارای حداقل مقدار فاصله است.
	2. u در sptSet قرار می‌گیرد.
	3. مقدار فاصله از همه راس‌های مجاور u به روز رسانی می‌شود. برای به روز رسانی مقادیر فاصله، در همه راس‌های مجاور تکرار انجام می‌شود. برای هر راس مجاور v، اگر مجموع فاصله u (از کد منبع) و وزن یال u-v کمتر از مقدار فاصله v باشد، مقدار فاصله از v به روز رسانی می‌شود.
</div>

### Dijkstra Code In Python

```
# source shortest path algorithm. The program is  
# for adjacency matrix representation of the graph 
  
# Library for INT_MAX 
import sys 
  
class Graph(): 
  
    def __init__(self, vertices): 
        self.V = vertices 
        self.graph = [[0 for column in range(vertices)]  
                      for row in range(vertices)] 
  
    def printSolution(self, dist): 
        print "Vertex tDistance from Source"
        for node in range(self.V): 
            print node,"t",dist[node] 
  
    # A utility function to find the vertex with  
    # minimum distance value, from the set of vertices  
    # not yet included in shortest path tree 
    def minDistance(self, dist, sptSet): 
  
        # Initilaize minimum distance for next node 
        min = sys.maxint 
  
        # Search not nearest vertex not in the  
        # shortest path tree 
        for v in range(self.V): 
            if dist[v] < min and sptSet[v] == False: 
                min = dist[v] 
                min_index = v 
  
        return min_index 
  
    # Funtion that implements Dijkstras single source  
    # shortest path algorithm for a graph represented  
    # using adjacency matrix representation 
    def dijkstra(self, src): 
  
        dist = [sys.maxint] * self.V 
        dist[src] = 0
        sptSet = [False] * self.V 
  
        for cout in range(self.V): 
  
            # Pick the minimum distance vertex from  
            # the set of vertices not yet processed.  
            # u is always equal to src in first iteration 
            u = self.minDistance(dist, sptSet) 
  
            # Put the minimum distance vertex in the  
            # shotest path tree 
            sptSet[u] = True
  
            # Update dist value of the adjacent vertices  
            # of the picked vertex only if the current  
            # distance is greater than new distance and 
            # the vertex in not in the shotest path tree 
            for v in range(self.V): 
                if self.graph[u][v] > 0 and sptSet[v] == False and 
                   dist[v] > dist[u] + self.graph[u][v]: 
                        dist[v] = dist[u] + self.graph[u][v] 
  
        self.printSolution(dist) 
  
# Driver program 
g  = Graph(9) 
g.graph = [[0, 4, 0, 0, 0, 0, 0, 8, 0], 
           [4, 0, 8, 0, 0, 0, 0, 11, 0], 
           [0, 8, 0, 7, 0, 4, 0, 0, 2], 
           [0, 0, 7, 0, 9, 14, 0, 0, 0], 
           [0, 0, 0, 9, 0, 10, 0, 0, 0], 
           [0, 0, 4, 14, 10, 0, 2, 0, 0], 
           [0, 0, 0, 0, 0, 2, 0, 1, 6], 
           [8, 11, 0, 0, 0, 0, 1, 0, 7], 
           [0, 0, 2, 0, 0, 0, 6, 7, 0] 
          ]; 
  
g.dijkstra(0)
```

<div dir="rtl">

### الگوریتم درخت پوشا

##### الگوریتم کراسکال الگوریتمی برای یافتن یک زیرگراف فراگیر همبند با کمترین وزن در یک گراف وزن‌دار است (در یک گراف وزن دار، به هر یال وزنی نسبت داده شده‌است). همچنین این الگوریتم برای یافتن کوچکترین درخت فراگیر در یک گراف وزن دار استفاده می‌شود


درخت پوشا زیرمجموعه‌ای از گراف G است که همه رئوس آن با کمترین مقدار یال‌های ممکن پوشش یافته است. از این رو یک درخت پوشا دور ندارد و هیچ رأس ناهمبندی در آن دیده نمی‌شود.

بر اساس تعریف فوق می‌توانیم نتیجه بگیریم که هر گراف کاملاً همبند و غیر جهت‌دار G دست‌کم یک درخت پوشا دارد. یک گراف ناهمبند؛ هیچ درخت پوشایی ندارد، چون امکان پوشش همه رئوس آن میسر نیست.

#### مشخصات کلی درخت پوشا

اینک که دانستیم یک گراف می‌تواند بیش از یک درخت پوشا داشته باشد. در ادامه چند مورد از مشخصات درخت پوشای همبند با درخت G را بررسی می‌کنیم:

- یک گراف همبند G می‌تواند بیش از یک درخت پوشا داشته باشد.
- همه درخت‌های پوشای گراف G تعداد یکسانی از یال‌ها و رئوس را دارند.
- درخت پوشا هیچ دوری ندارد.
- با حذف یک یال از درخت پوشا، به گراف غیر همبند تبدیل می‌شود، یعنی درخت پوشا دارای کمینه اتصال‌های ممکن است.
- افزودن یک یال به درخت پوشا موجب ایجاد یک مدار یا طوقه می‌شود، یعنی درخت پوشا در حالت بیشینه غیر دوری (maximally acyclic) است.

#### کاربرد درخت پوشا

درخت پوشا اساساً برای یافتن کوتاه‌ترین مسیر بین همه گره‌ها در یک گراف مورد استفاده قرار می‌گیرد. کاربردهای رایج درخت‌های پوشا به صورت زیر هستند:

- برنامه‌ریزی شبکه تأسیسات شهری
- پروتکل مسیریابی شبکه رایانه‌ای
- تحلیل خوشه

با مثال کوچکی کاربردهای درخت پوشا را بررسی می‌کنیم. شبکه یک شهر را به صورت یک گراف بزرگ تصور کنید. اینک می‌خواهیم خطوط تلفن را به روشی توزیع کنیم که با کمترین مقدار سیم بتوان همه گره‌های شهر را به شبکه وصل کرد. این همان جایی است که درخت پوشا وارد عمل می‌شود.

## Kruskal algorithm

##### الگوریتم کراسکال الگوریتمی برای یافتن یک زیرگراف فراگیر همبند با کمترین وزن در یک گراف وزن‌دار است (در یک گراف وزن دار، به هر یال وزنی نسبت داده شده‌است). همچنین این الگوریتم برای یافتن کوچکترین درخت فراگیر در یک گراف وزن دار استفاده می‌شود

الگوریتم کروسکال برای یافتن درخت پوشای با کمترین هزینه از رویکرد حریصانه بهره می‌گیرد. این الگوریتم با گراف به صورت یک جنگل برخورد می‌کند که در آن هر گره یک درخت منفرد محسوب می‌شود. یک درخت زمانی به درخت دیگر وصل می‌شود اگر و فقط اگر در میان همه گزینه‌های موجود، کمترین هزینه را داشته باشد و مشخصات درخت پوشای کمینه (MST) را نیز نقض نکند.

### Kruskal Code In Python
```
# Kruskal's algorithm in Python


class Graph:
    def __init__(self, vertices):
        self.V = vertices
        self.graph = []

    def add_edge(self, u, v, w):
        self.graph.append([u, v, w])

    # Search function

    def find(self, parent, i):
        if parent[i] == i:
            return i
        return self.find(parent, parent[i])

    def apply_union(self, parent, rank, x, y):
        xroot = self.find(parent, x)
        yroot = self.find(parent, y)
        if rank[xroot] < rank[yroot]:
            parent[xroot] = yroot
        elif rank[xroot] > rank[yroot]:
            parent[yroot] = xroot
        else:
            parent[yroot] = xroot
            rank[xroot] += 1

    #  Applying Kruskal algorithm
    def kruskal_algo(self):
        result = []
        i, e = 0, 0
        self.graph = sorted(self.graph, key=lambda item: item[2])
        parent = []
        rank = []
        for node in range(self.V):
            parent.append(node)
            rank.append(0)
        while e < self.V - 1:
            u, v, w = self.graph[i]
            i = i + 1
            x = self.find(parent, u)
            y = self.find(parent, v)
            if x != y:
                e = e + 1
                result.append([u, v, w])
                self.apply_union(parent, rank, x, y)
        for u, v, weight in result:
            print("%d - %d: %d" % (u, v, weight))


g = Graph(6)
g.add_edge(0, 1, 4)
g.add_edge(0, 2, 4)
g.add_edge(1, 2, 2)
g.add_edge(1, 0, 4)
g.add_edge(2, 0, 4)
g.add_edge(2, 1, 2)
g.add_edge(2, 3, 3)
g.add_edge(2, 5, 2)
g.add_edge(2, 4, 4)
g.add_edge(3, 2, 3)
g.add_edge(3, 4, 3)
g.add_edge(4, 2, 4)
g.add_edge(4, 3, 3)
g.add_edge(5, 2, 2)
g.add_edge(5, 4, 3)
g.kruskal_algo()
```

## Prim's Algorithm

الگوریتم پریم برای یافتن درخت پوشای با کمترین هزینه (همانند الگوریتم کروسکال که در بخش قبل بررسی کردیم) از رویکرد حریصانه بهره می‌گیرد. الگوریتم پریم شباهت‌هایی با الگوریتم‌های «کوتاه‌ترین مسیر، اول» (shortest path first) دارد.

الگوریتم پریم در تضاد با الگوریتم کروسکال است، چون با گره‌ها به عنوان یک درخت منفرد برخورد می‌کند و به افزودن گره‌ها به یک درخت پوشا از گراف مفروض ادامه می‌دهد.

#### Prim's Code in Python


```

INF = 9999999
# number of vertices in graph
V = 5
# create a 2d array of size 5x5
# for adjacency matrix to represent graph
G = [[0, 9, 75, 0, 0],
     [9, 0, 95, 19, 42],
     [75, 95, 0, 51, 66],
     [0, 19, 51, 0, 31],
     [0, 42, 66, 31, 0]]
# create a array to track selected vertex
# selected will become true otherwise false
selected = [0, 0, 0, 0, 0]
# set number of edge to 0
no_edge = 0
# the number of egde in minimum spanning tree will be
# always less than(V - 1), where V is number of vertices in
# graph
# choose 0th vertex and make it true
selected[0] = True
# print for edge and weight
print("Edge : Weight\n")
while (no_edge < V - 1):
    # For every vertex in the set S, find the all adjacent vertices
    #, calculate the distance from the vertex selected at step 1.
    # if the vertex is already in the set S, discard it otherwise
    # choose another vertex nearest to selected vertex  at step 1.
    minimum = INF
    x = 0
    y = 0
    for i in range(V):
        if selected[i]:
            for j in range(V):
                if ((not selected[j]) and G[i][j]):  
                    # not in selected and there is an edge
                    if minimum > G[i][j]:
                        minimum = G[i][j]
                        x = i
                        y = j
    print(str(x) + "-" + str(y) + ":" + str(G[x][y]))
    selected[y] = True
    no_edge += 1
```

</div>


<span style="color:blue">
</span>
