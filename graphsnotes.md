<h1>Creating a Graph<h1>
<h3>Create a graph using arraylist of arraylist using
ArrayList<ArrayList<Integer>>adj</h3>

<h2>BfS - algorithm</h2>

<h2>Java</h2>
```

class Solution {
    // Function to return Breadth First Traversal of given graph.
    ArrayList<Integer> ans = new ArrayList<>();
    // boolean[] vis = new boolean[V]
    public ArrayList<Integer> bfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        // Code here
        boolean[] vis = new boolean[V];
        var list = new ArrayList<Integer>();
        
        bfs(0,list,vis,adj);
        
        
        return list;
    }
    private static void bfs(int node,ArrayList<Integer>list,boolean[]vis,ArrayList<ArrayList<Integer>> adj)
    {
        Queue<Integer> q = new LinkedList<>();
        q.add(node);
        vis[node] = true;
        
        while(!q.isEmpty())
        {
            int x = q.poll();
            list.add(x);
            
            for(Integer it : adj.get(x))
            {
                if(vis[it] == false)
                {
                    vis[it] = true;
                    q.offer(it);
                }
            }
        }
    }
}

```

<h1>python</h1>
```
from collections import deque
class Solution:
    
    #Function to return Breadth First Traversal of given graph.
    def bfsOfGraph(self, V, adj):
        # code here
        vis = [False]*V
        ans = []
        
        self.bfs(0,vis,ans,adj)
        
        return ans
        
        
        
    def bfs(self,node,vis,ans,adj):
        q = deque()
        vis[node] = True
        q.append(node)
        
        while len(q) != 0:
            curr = q.popleft()
            ans.append(curr)
            
            for i in adj[curr]:
                if vis[i] != True:
                    q.append(i)
                    vis[i] = True
                

```
#DFS-algorithm

##Java

```
class Solution {
    // Function to return a list containing the DFS traversal of the graph.
    public ArrayList<Integer> dfsOfGraph(int V, ArrayList<ArrayList<Integer>> adj) {
        var list = new ArrayList<Integer>();
        boolean[] vis = new boolean[V];
        for(int i = 0;i < V;i++)
        {
            if(!vis[i])
            {
                dfs(i,vis,list,adj);
            }
        }
        return list;
    }
    private static void dfs(int node,boolean[]vis,ArrayList<Integer>list,ArrayList<ArrayList<Integer>> adj)
    {
        vis[node] = true;
        list.add(node);
        
        for(Integer it : adj.get(node))
        {
            if(!vis[it])
            {
                dfs(it,vis,list,adj);
            }
        }
    }
}



```

##Python

```
class Solution:
    
    #Function to return a list containing the DFS traversal of the graph.
    def dfsOfGraph(self, V, adj):
        # code here
        list = []
        vis  = [False for x in range(V+1)]
        
        for i in range(0,V):
            if not vis[i]:
                self.dfs(i,vis,list,adj)
                
        return list
                
    def dfs(self,node,vis,list,adj):
            vis[node] = True
            list.append(node)
            
            for i in adj[node]:
               if vis[i] == False:
                   self.dfs(i,vis,list,adj)

```

<h1>Bipartite Graph</h1>

<h2>check using dfs</h2>

```
class Solution
{
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>>adj)
    {
        // Code here
        int[]color = new int[V];
        Arrays.fill(color,-1);
        
        for(int i = 0;i < V;i++)
        {
            if(color[i] == -1)
            {
                if(dfs(i,color,0,adj) == false) 
                {
                    return false;
                }
            }
        }
        
        return true;
        
    }
    
    private static boolean dfs(int node,int[]color,int c,ArrayList<ArrayList<Integer>>adj)
    {
       color[node] = c;
       
       for(Integer it : adj.get(node))
       {
           if(color[it] == -1)
           {
               color[it] = color[node] == 1 ? 0:1;
               if(dfs(it,color,color[it],adj) == false)return false;
           }
           else if(color[it] == color[node])
           {
               return false;
           }
       }
       
       return true;
    }
}

```

<h1>python</h1>

```
from collections import deque
class Solution:
	def isBipartite(self, V, adj):
		#code here
		color = [-1]*V
		
		for i in range(V):
		    if color[i] == -1:
		        if(self.bfs(i,color,adj)):
		            return True
		return False
		
	def bfs(self,node,color,adj):
	    q = deque()
	    q.append(node)
	    color[node] = 0
	    
	    while len(q) != 0:
	        curr = q.pop()
	        clr = color[curr]
	        
	        for i in adj[curr]:
	            if color[i] == -1:
	                color[i] = color[curr] ^ 1
	                q.append(i)
	            elif color[i] == color[curr]:
	                return False
	                
	    return True

```

<h1>using dfs</h1>

```
class Solution
{
    public boolean isBipartite(int V, ArrayList<ArrayList<Integer>>adj)
    {

        int[] color = new int[V];
        Arrays.fill(color, -1);

        Queue<Integer> q = new LinkedList<>();

        boolean is_Bipratite = true;

        for(int i = 0; i < V; i++)
        {
            if(color[i] == -1)
            {
                q.add(i);
                color[i] = 0;
                while(!q.isEmpty())
                {
                    int u = q.poll();
                    for(Integer v : adj.get(u))
                    {
                        if(color[v] == -1)
                        {
                            color[v] = color[u] ^ 1;
                            q.add(v);
                        }
                        else is_Bipratite = is_Bipratite & (color[u] != color[v]);
                    }

                }
            }
        }
        return is_Bipratite;
    }
};

```

<h1>python</h1>

```
from collections import deque
class Solution:
    def isBipartite(self, V, adj):
        is_bipartite = True
        q = deque()
        color = [-1 for i in range(V)]
        for i in range(V):
            if(color[i] == -1):
                q.append(i)
                color[i] = 0
                while(len(q)):
                    u = q.pop();
                    for v in adj[u]:
                        if(color[v] == -1):
                            color[v] = color[u] ^ 1
                            q.append(v)
                        else:
                            is_bipartite  = is_bipartite & (color[v] != color[u])
        return is_bipartite

```

<h1>cycle detection in undirected graph<h1>
<h2>using dfs</h2>

```

class Solution {
    Boolean isCyclicUtil(int v, Boolean visited[], int parent,
                         ArrayList<ArrayList<Integer>> adj) {
        // marking the current vertex as visited.
        visited[v] = true;
        Integer i;

        Iterator<Integer> it = adj.get(v).iterator();
        while (it.hasNext()) {
            i = it.next();

            // if an adjacent is not visited, then calling function
            // recursively for that adjacent vertex.
            if (!visited[i]) {
                if (isCyclicUtil(i, visited, v, adj)) return true;
            }

            // if an adjacent is visited and it is not a parent of current
            // vertex then there is a cycle and we return true.
            else if (i != parent)
                return true;
        }
        return false;
    }

    // Function to detect cycle in an undirected graph.
    public boolean isCycle(int V, ArrayList<ArrayList<Integer>> adj) {
        // using a boolean list to mark all the vertices as not visited.
        Boolean visited[] = new Boolean[V];
        for (int i = 0; i < V; i++) visited[i] = false;

        // iterating over all the vertices.
        for (int u = 0; u < V; u++) {
            // if vertex is not visited, we call the function to detect cycle.
            if (!visited[u])

                // if cycle is found, we return true.
                if (isCyclicUtil(u, visited, -1, adj)) return true;
        }

        return false;
    }
}

```
<h2>using bfs</h2>

```
class Pair{
    int num1;
    int num2;
    Pair(int _num1,int _num2)
    {
        this.num1 = _num1;
        this.num2 = _num2;
    }
}
class Solution {
    // Function to detect cycle in an undirected graph.
    public boolean isCycle(int V, ArrayList<ArrayList<Integer>> adj) {
        
        int[] vis = new int[V];
        
        for(int i = 0;i < V;i++)
        {
            if(vis[i] == 0)
            {
                vis[i] = 1;
                Queue<Pair> q = new LinkedList<>();
                q.offer(new Pair(i,-1));
                
                while(!q.isEmpty())
                {
                    int child = q.peek().num1;
                    int parent = q.peek().num2;
                    q.poll();
                    
                    for(Integer x : adj.get(child))
                    {
                        if(vis[x] == 0)
                        {
                            q.offer(new Pair(x,child));
                            vis[x] = 1;
                        }
                        else if(x != parent)
                        {
                            return true;
                        }
                    }
                    
                }
           }
        }
        
        return false;
    }
}

```

<h1>cycle detection in directed graph</h1>

<h2>using bfs</h2>

```
class Solution {
    // Function to detect cycle in a directed graph.
    
    public boolean isCyclic(int V, ArrayList<ArrayList<Integer>> adj) {
        
        int[] indegree = new int[V];
        for(int i = 0;i < V;i++)
        {
            for(Integer x : adj.get(i))
            {
                indegree[x]++;
            }
        }
        
        int count = 0;
        Queue<Integer> q = new LinkedList<>();
        for(int i = 0;i < V;i++)
        {
            if(indegree[i] == 0)
            {
                q.offer(i);
                count++;
            }
        }
        
        while(!q.isEmpty())
        {
            int curr = q.poll();
            for(Integer x : adj.get(curr))
            {
                indegree[x]--;
                if(indegree[x] == 0)
                {
                    q.offer(x);
                    count++;
                }
            }
        }
        
        return count == V ? false:true;
    }
}

```

<h2>using dfs</h2>

```
class Solution {
    boolean isCyclicUtil(int i, boolean[] visited, boolean[] recStack,
                         ArrayList<ArrayList<Integer>> adj) {

        // marking the current node as visited and part of recursion stack.
        if (recStack[i]) return true;

        if (visited[i]) return false;

        visited[i] = true;

        recStack[i] = true;
        List<Integer> children = adj.get(i);

        // calling function recursively for all the vertices
        // adjacent to this vertex.
        for (Integer c : children)
            if (isCyclicUtil(c, visited, recStack, adj)) return true;

        // removing the vertex from recursion stack.
        recStack[i] = false;

        return false;
    }

    // Function to detect cycle in a dire
    cted graph.
    public boolean isCyclic(int V, ArrayList<ArrayList<Integer>> adj) {
        // marking all vertices as not visited and not a part of recursion stack
        boolean[] visited = new boolean[V];
        boolean[] recStack = new boolean[V];

        // calling the recursive helper function to detect cycle in
        // different DFS trees.
        for (int i = 0; i < V; i++)
            if (isCyclicUtil(i, visited, recStack, adj)) return true;

        return false;
    }
}

```

<h1>Implementing  Dijkstra`s algorithm</h1>

```
class Node implements Comparable<Node>
{
    int v;
    int d;
    public Node(int v,int d)
    {
        this.v = v;
        this.d = d;
    }
    
    @Override
    public int compareTo(Node temp)
    {
        return this.d - temp.d;
    }
}

class Solution
{
    //Function to find the shortest distance of all the vertices
    //from the source vertex S.
    static int[] dijkstra(int V, ArrayList<ArrayList<ArrayList<Integer>>> adj, int S)
    {
        boolean[] vis = new boolean[V];
        int[]dis = new int[V];
        Arrays.fill(dis,Integer.MAX_VALUE);
        dis[S] = 0;
        PriorityQueue<Node>q = new PriorityQueue<>();
        q.offer(new Node(S,0));
        
        while(!q.isEmpty())
        {
            Node curr = q.poll();
            if(vis[curr.v])continue;
            
            vis[curr.v] = true;
            
            for(ArrayList<Integer> it : adj.get(curr.v))
            {
                int nb = it.get(0);
                int w = it.get(1);
                if(vis[nb] == false)
                {
                    if(w + curr.d < dis[nb])
                    {
                        dis[nb] = w + curr.d;
                        q.offer(new Node(nb,w + curr.d));
                    }
                }
            }
        }
        return dis;
        
    }
}

```




