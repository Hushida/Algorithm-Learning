图分为有向图和无向图。图的存储方式分为邻接表和邻接矩阵。  
无向图的实现如下
```
public class Graph {
    private int v; //顶点的个数
    private LinkedList<Integer> adj[]; //邻接表
    
    public Graph(int v) {
        this.v = v;
        adj = new LinkedList[v];
        for(int i = 0; i < v; ++i) {
            adj[i] = new LinkedList<>();
        }
    }
    
    public void addEdge(int s, int t) {
        adj[s].add(t);
        adj[t].add(s);
    }
}
```
