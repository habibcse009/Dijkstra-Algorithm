# Dijkstra-Algorithm
### Dijkstra এর অ্যালগরিদম
Dijkstra এর অ্যালগরিদম আমাদের একটি গ্রাফের যেকোনো দুটি শীর্ষবিন্দুর মধ্যে সংক্ষিপ্ততম পথ খুঁজে পেতে দেয়।

এটি ন্যূনতম বিস্তৃত গাছ থেকে পৃথক কারণ দুটি শীর্ষবিন্দুর মধ্যে সবচেয়ে কম দূরত্ব গ্রাফের সমস্ত শীর্ষবিন্দু অন্তর্ভুক্ত নাও করতে পারে।
### How Dijkstra's Algorithm works
ডিজকস্ট্রার অ্যালগরিদম এই ভিত্তিতে কাজ করে যে যেকোনো উপপথ B -> D এর সংক্ষিপ্ততম পথ A -> D শীর্ষবিন্দু A এবং D এর মধ্যেও B এবং D এর মধ্যে সবচেয়ে ছোট পথ।
Djikstra এই বৈশিষ্ট্যটি বিপরীত দিকে ব্যবহার করেছে অর্থাৎ আমরা প্রারম্ভিক শীর্ষবিন্দু থেকে প্রতিটি শীর্ষবিন্দুর দূরত্বকে অতিমূল্যায়ন করি। তারপরে আমরা প্রতিটি নোড এবং এর প্রতিবেশীদের পরিদর্শন করি সেই প্রতিবেশীদের কাছে সংক্ষিপ্ততম উপপথ খুঁজে পেতে।

অ্যালগরিদম এই অর্থে একটি লোভী পদ্ধতি ব্যবহার করে যে আমরা পরবর্তী সেরা সমাধানটি খুঁজে পাই এই আশায় যে শেষ ফলাফলটি পুরো সমস্যার জন্য সর্বোত্তম সমাধান।
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
Enter the number of nodes:
3
Enter the Adjacency matrix:
Enter the weight of the path between nodes 1 and 1: 
2
Enter the weight of the path between nodes 1 and 2: 
3
Enter the weight of the path between nodes 1 and 3: 
5
Enter the weight of the path between nodes 2 and 1: 
4
Enter the weight of the path between nodes 2 and 2: 
3
Enter the weight of the path between nodes 2 and 3: 
4
Enter the weight of the path between nodes 3 and 1: 
3
Enter the weight of the path between nodes 3 and 2: 
2
Enter the weight of the path between nodes 3 and 3: 
1
Enter the source matrix:
3

Shortest path:
3->1,cost=3
3->2,cost=2

```
