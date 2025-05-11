# 🚇 Delhi Metro Route Simulator (Java)

This Java program simulates the **Delhi Metro Network** to compute:

* Shortest **distance** and **time**
* Route details with **interchanges**
* View the full metro **map** and **station list**

---

## 📁 Files

* `Graph_M.java`: Implements the graph and core algorithms.
* `Heap.java`: Implements a generic max-heap used in Dijkstra’s algorithm.

---

## ⚙️ Algorithms Used

| Feature                       | Algorithm                | Time Complexity            |
| ----------------------------- | ------------------------ | -------------------------- |
| Shortest Path (Distance/Time) | Dijkstra's Algorithm     | O((V + E) log V)           |
| All Possible Paths            | Depth-First Search (DFS) | O(2^V) worst case          |
| to find if Path exist         | Breadth-First Search (BFS) | O(V+E) worst case          |
| Priority Queue                | Min-Heap                 | O(log N) for insert/remove |

---

## 📘 Class: `Graph_M`

### Data Structures:

* **Graph Representation:** `HashMap<String, Vertex>`
* **Vertex:** Contains `HashMap<String, Integer>` for neighbors and edge weights

---

## 📚 Method List

| Method                                 | Description                                            |
| -------------------------------------- | ------------------------------------------------------ |
| `addVertex(String)`                    | Adds a station (vertex)                                |
| `removeVertex(String)`                 | Removes a station and its connections                  |
| `containsVertex(String)`               | Checks if station exists                               |
| `addEdge(String, String, int)`         | Connects two stations with a distance                  |
| `removeEdge(String, String)`           | Removes the edge between stations                      |
| `containsEdge(String, String)`         | Checks if two stations are directly connected          |
| `numVertex()`                          | Returns number of stations                             |
| `numEdges()`                           | Returns number of connections                          |
| `display_Map()`                        | Displays all connections in the map                    |
| `display_Stations()`                   | Lists all station names                                |
| `hasPath(String, String, HashMap)`     | Checks if a path exists between two stations using DFS |
| `Create_Metro_Map(Graph_M)`            | Initializes the graph with hardcoded station data      |
| `dijkstra(String, String, boolean)`    | 🔹 Finds shortest distance/time between two stations   |
| `Get_Minimum_Distance(String, String)` | 🔹 Gets shortest distance path using DFS               |
| `Get_Minimum_Time(String, String)`     | 🔹 Gets shortest time path using DFS                   |
| `get_Interchanges(String)`             | Extracts and counts interchanges from path             |
| `main(String[])`                       | User interface loop for CLI menu                       |

---

## 🧠 Detailed Explanations for Core Methods

---

### 🔹 `dijkstra(String src, String des, boolean nan)`

**Purpose:** Find the shortest distance or time between `src` and `des`.

#### Logic:

1. Initialize a min-cost map and heap (`Heap<DijkstraPair>`)
2. For all vertices:

   * Set cost = 0 for `src`, ∞ for others
3. While heap is not empty:

   * Remove pair with min cost
   * Update neighbors' cost if shorter path is found
   * Use `nan` flag:

     * `false`: use distance
     * `true`: use time = `120 + 40*distance` per edge

#### Time Complexity:

**O((V + E) log V)**

---

### 🔹 `Get_Minimum_Distance(String src, String dst)`

**Purpose:** Find the path with minimum total distance using DFS.

#### Logic:

1. Use a stack for DFS (`LinkedList<Pair>`)
2. Explore all paths
3. Track the path with the minimum distance
4. Return the full path and total distance

#### Time Complexity:

**O(2^V)** (Worst case for DFS)

---

### 🔹 `Get_Minimum_Time(String src, String dst)`

**Purpose:** Find the path with minimum total time using DFS.

#### Logic:

1. Like `Get_Minimum_Distance`, but track `min_time`
2. Time per edge = `120 + 40*distance`
3. Return path and total time (converted to minutes)

#### Time Complexity:

**O(2^V)**

---

### 🔹 `get_Interchanges(String path)`

**Purpose:** Parses a path string to identify and count line interchanges.

#### Logic:

1. Split path on `"  "`
2. Compare line codes (suffixes after `~`)
3. Count where lines change (i.e., interchange occurs)

#### Time Complexity:

**O(n)** where `n` = number of stations in path

---

## 🧪 Example

```java
Graph_M g = new Graph_M();
Graph_M.Create_Metro_Map(g);

String shortestDistance = g.Get_Minimum_Distance("Rajiv Chowk~BY", "AIIMS~Y");
String shortestTime = g.Get_Minimum_Time("Rajiv Chowk~BY", "AIIMS~Y");

int dist = g.dijkstra("Rajiv Chowk~BY", "AIIMS~Y", false);  // 7 km
int time = g.dijkstra("Rajiv Chowk~BY", "AIIMS~Y", true);   // 400 seconds ≈ 7 mins
```

---

## 📘 Class: `Heap<T>`

Custom max-heap used as a priority queue in Dijkstra’s algorithm.

| Method                   | Description                   | Time Complexity |
| ------------------------ | ----------------------------- | --------------- |
| `add(T item)`            | Adds to heap and heapifies    | O(log n)        |
| `remove()`               | Removes top element           | O(log n)        |
| `updatePriority(T item)` | Reheapify if priority changes | O(log n)        |
| `isEmpty()`              | Checks if heap is empty       | O(1)            |
| `get()`                  | Gets top item                 | O(1)            |

---

## 🏁 CLI Menu Features

* View all stations
* View full metro map
* minTime between two station
* Min distance between two station
* Get shortest path by distance or time
* View path breakdown with interchanges

---

## ✅ Example Output (CLI)

```
1. LIST ALL THE STATIONS
2. SHOW METRO MAP
3. SHORTEST DISTANCE
4. SHORTEST TIME
5. SHORTEST PATH (DISTANCE)
6. SHORTEST PATH (TIME)
7. EXIT

ENTER CHOICE: 3
ENTER SOURCE AND DESTINATION:
> AIIMS~Y
> IGI Airport~O
Shortest Distance = 24 KM
```
