# Dijkstra's Algorithm

Given a graph of a road network, where the weights of each edge represent the difficulty of traversing the road (smaller is better and represents a faster road), Dijkstra's algorithm basically starts by inspecting the fastest roads first. It does this using a priority queue.

Dijkstra's algorithm only works on directed graphs, and the edges cannot have negative values.

```mermaid

graph LR
	S---|7|A;
	S---|3|C;
	S---|2|B;
	A---|3|B;
	A---|4|D;
	B---|4|D;
	B---|1|H;
	D---|5|F;
	F---|3|H;
	H---|2|G;
	G---|2|E;
	E---|5|K;
	K---|4|I;
	K---|4|J;
	J---|6|I;
	J---|4|L;
	I---|4|L;
	L---|2|C;
```

```javascript
function Dijkstra(Graph, source):

  create vertex set Q

  for each vertex v in Graph:            
      dist[v] ← INFINITY                 
      prev[v] ← UNDEFINED                
      add v to Q                     
  dist[source] ← 0                       
 
  while Q is not empty:
      u ← vertex in Q with min dist[u]   
                                         
      remove u from Q
     
      // only v that are still in Q
      for each neighbor v of u:           
          alt ← dist[u] + length(u, v)
          if alt < dist[v]:              
              dist[v] ← alt
              prev[v] ← u

  return dist[], prev[]
```