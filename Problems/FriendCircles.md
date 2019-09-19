# 547. Friend Circles
## 思路
简单的Union-Find题目，但这题比较简单，用DFS应该也可以做。
## 代码
```Java
class Solution {
    int[] rnk;
    int[] parent;
    public int findCircleNum(int[][] M) {
        int n = M.length;
        if(n == 0)return 0;
        rnk = new int[n];
        parent = new int[n];
        for(int i = 0; i < n; i ++){
            parent[i] = i;
            rnk[i] = 1;
        }
        for(int i = 0; i < n; i ++){
            for(int j = 0; j < i; j ++){
                if(M[i][j] == 1){
                    union(i, j);
                }
            }
        }
        Set<Integer> s = new HashSet<>();
        int count = 0;
        for(int i = 0; i < n; i ++){
            if(s.contains(find(i)))continue;
            else{
                s.add(find(i));
                count ++;
            }
        }
        return count;
    }
    
    public boolean union(int a, int b){
        int pa = find(a);
        int pb = find(b);
        if(pa != pb){
            if(rnk[pb] > rnk[pa]){
                parent[pa] = pb;
            }else if(rnk[pb] < rnk[pa]){
                parent[pb] = pa;
            }else{
                parent[pb] = pa;
                rnk[pa] ++;
            }
            return true;
        }else{
            return false;
        }
    }
    
    public int find(int a){
        if(parent[a] != a)return find(parent[a]);
        else return a;
    }
}
```