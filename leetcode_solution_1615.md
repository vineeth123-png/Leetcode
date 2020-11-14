# 1615. Maximal Network Rank

## Approach : Using adjacency matrix and vector for degree of a vertex (Accepted)

Generally, when we need to store information about edges in a graph, we use an adjacency list, not an adjacency matrix, as it takes more space.  
Here, as the number of nodes are less than or equal to 100, we use an adjacency matrix so that finding whether two nodes are connected or not can be retrieved in O(1) time and we don’t use much memory.

The algorithm is as follows:

```
Create an adjacency matrix from the given roads vector.
Now, calculate the degree of each node using the above information.
Now, for every pair of nodes possible, calculate the network rank.
Return the maximum of them.
```
Now, lets calculate the rank for the pair shown in the question’s example 1.

The degree of node 0 is 2 and the degree of node 1 is 3.
Hence, the network rank for the pair [0,1] is 4, since we can’t count the edge [0,1] twice.  
Here’s the code in C++:

```
class Solution {
    int adj_list[100][100];
    int edge_count[100];
public:
    int maximalNetworkRank(int n, vector<vector<int>>& roads) {
        for(auto it: roads){
            adj_list[it[0]][it[1]] = 1;
            adj_list[it[1]][it[0]] = 1;
            edge_count[it[0]]++;
            edge_count[it[1]]++;
        }
        int m_num = 0;
        for(int i = 0; i<n; i++){
            for(int j = i+1; j<n; j++){
                int num = edge_count[i] + edge_count[j];
                if(adj_list[i][j]) num--;
                m_num = max(m_num, num);
            }
        }
        return m_num;
    }
};

```

Time complexity : O(N^2)  

Space complexity : O(1), since every time we ask for a 100*100 sized 2d int array and a 100 sized int array.
