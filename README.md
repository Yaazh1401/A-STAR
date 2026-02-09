<h1>ExpNo 4 : Implement A* search algorithm for a Graph</h1> 
<h3>Name:   Yaazhini S    </h3>
<h3>Register Number:   212224230308        </h3>
<H3>Aim:</H3>
<p>To ImplementA * Search algorithm for a Graph using Python 3.</p>
<H3>Algorithm:</H3>

``````
// A* Search Algorithm
1.  Initialize the open list
2.  Initialize the closed list
    put the starting node on the open 
    list (you can leave its f at zero)

3.  while the open list is not empty
    a) find the node with the least f on 
       the open list, call it "q"

    b) pop q off the open list
  
    c) generate q's 8 successors and set their 
       parents to q
   
    d) for each successor
        i) if successor is the goal, stop search
        
        ii) else, compute both g and h for successor
          successor.g = q.g + distance between 
                              successor and q
          successor.h = distance from goal to 
          successor (This can be done using many 
          ways, we will discuss three heuristics- 
          Manhattan, Diagonal and Euclidean 
          Heuristics)
          
          successor.f = successor.g + successor.h

        iii) if a node with the same position as 
            successor is in the OPEN list which has a 
           lower f than successor, skip this successor

        iV) if a node with the same position as 
            successor  is in the CLOSED list which has
            a lower f than successor, skip this successor
            otherwise, add  the node to the open list
     end (for loop)
  
    e) push q on the closed list
    end (while loop)

``````

<hr>
<h2>Sample Graph I</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/b1377c3f-011a-4c0f-a843-516842ae056a)

<hr>

## PROGRAM 
```
import heapq

def astar(graph, heuristics, start, goal):
    open_list = []
    heapq.heappush(open_list, (0, start))
    
    came_from = {}
    g_cost = {start: 0}
    closed_list = set()

    while open_list:
        f, current = heapq.heappop(open_list)

        if current == goal:
            path = []
            while current:
                path.append(current)
                current = came_from.get(current)
            return path[::-1]

        closed_list.add(current)

        for neighbor, cost in graph[current]:
            if neighbor in closed_list:
                continue

            tentative_g = g_cost[current] + cost

            if neighbor not in g_cost or tentative_g < g_cost[neighbor]:
                g_cost[neighbor] = tentative_g
                f_cost = tentative_g + heuristics[neighbor]
                heapq.heappush(open_list, (f_cost, neighbor))
                came_from[neighbor] = current

    return None

n, m = map(int, input().split())

graph = {}
for _ in range(m):
    u, v, w = input().split()
    w = int(w)
    graph.setdefault(u, []).append((v, w))
    graph.setdefault(v, []).append((u, w))

heuristics = {}
for _ in range(n):
    node, h = input().split()
    heuristics[node] = int(h)

start = 'A'
goal = min(heuristics, key=heuristics.get)

path = astar(graph, heuristics, start, goal)

print("Path found:", path)

```
<h2>Sample Input</h2>
<hr>
10 14 <br>
A B 6 <br>
A F 3 <br>
B D 2 <br>
B C 3 <br>
C D 1 <br>
C E 5 <br>
D E 8 <br>
E I 5 <br>
E J 5 <br>
F G 1 <br>
G I 3 <br>
I J 3 <br>
F H 7 <br>
I H 2 <br>
A 10 <br>
B 8 <br>
C 5 <br>
D 7 <br>
E 3 <br>
F 6 <br>
G 5 <br>
H 3 <br>
I 1 <br>
J 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
<img width="615" height="577" alt="image" src="https://github.com/user-attachments/assets/83d56e5a-629d-44c6-a8a4-a6d77b05555c" />


<hr>
<h2>Sample Graph II</h2>
<hr>

![image](https://github.com/natsaravanan/19AI405FUNDAMENTALSOFARTIFICIALINTELLIGENCE/assets/87870499/acbb09cb-ed39-48e5-a59b-2f8d61b978a3)


<hr>
<h2>Sample Input</h2>
<hr>
6 6 <br>
A B 2 <br>
B C 1 <br>
A E 3 <br>
B G 9 <br>
E D 6 <br>
D G 1 <br>
A 11 <br>
B 6 <br>
C 99 <br>
E 7 <br>
D 1 <br>
G 0 <br>
<hr>
<h2>Sample Output</h2>
<hr>
<img width="494" height="354" alt="image" src="https://github.com/user-attachments/assets/05a75a22-6b53-4d91-b327-f1a801c2d7f0" />

