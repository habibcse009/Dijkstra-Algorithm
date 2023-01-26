# Dijkstra-Algorithm

***
### A java code program that implements the Floyd-Warshall algorithm to find the shortest paths between all pairs of vertices in a weighted, directed graph

```
import java.util.*;

public class Dijkstra {

    public static final int infinity = 999;
    public static int flag[] = new int[10];

    public static void dij(int n, int v, int cost[][], int dist[]) {
        int i, u = 0, count, w, min;
        for (i = 1; i <= n; i++) {
            flag[i] = 0;
            dist[i] = cost[v][i];
        }

        count = 2;
        while (count <= n) {
            min = infinity;
            for (w = 1; w <= n; w++) {
                if (dist[w] < min && flag[w] == 0) {
                    min = dist[w];
                    u = w;
                }
            }
            flag[u] = 1;
            count++;
            for (w = 1; w <= n; w++) {
                if ((dist[u] + cost[u][w] < dist[w]) && flag[w] == 0) {
                    dist[w] = dist[u] + cost[u][w];
                }
            }
        }
    }

    public static void main(String[] args) {
        int n, v, i, j, cost[][] = new int[10][10], dist[] = new int[10];

        Scanner scan = new Scanner(System.in);

        System.out.println("Enter the number of nodes:");
        n = scan.nextInt();

        System.out.println("Enter the Adjacency matrix:");
        for (i = 1; i <= n; i++) {
            for (j = 1; j <= n; j++) {
                System.out.println("Enter the weight of the path between nodes " + i + " and " + j + ": ");
                cost[i][j] = scan.nextInt();
                if (cost[i][j] == 0) {
                    cost[i][j] = infinity;
                }
            }
        }

        System.out.println("Enter the source matrix:");
        v = scan.nextInt();
        dij(n, v, cost, dist);// call dij

        System.out.println("\nShortest path:");
        for (i = 1; i <= n; i++) {
            if (i != v) {
                System.out.println(v + "->" + i + ",cost=" + dist[i]);
            }
        }
        scan.close();
    }
}

```
#### Output: 
```

```
