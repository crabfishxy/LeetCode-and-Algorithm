# 算法和常用数据结构

## Heap
删除元素：将最后的元素放到根然后进行下沉

插入元素：将元素放到最后然后进行上浮

构造二叉堆：时间复杂度O(N)(证明)，对一半的元素进行下沉操作

## Trie
代码摘自算法第四版，实际上可以不用递归
```Java
public class TrieST<Value>{
    private static int R = 256;
    private Node root;

    private static class Node{
        private Object val;
        private Node[] next = new Node[R];
    }

    public Value get(String key){
        Node x = get(root, key, 0);
        if(x == null) return null;
        return (Value) x.val;
    }

    private Node get(Node x, String key, int d){
        if(x == null) return null;
        if(d == key.length()) return x;
        char c = key.charAt(d);
        return get(x.next[c], key, d+1);
    }

    public void put(String key, Value val){
        root = put(root, key, val, 0);
    }

    private Node put(Node x, String key, Value val, int d){
        if(x == null) x = new Node();
        if(d == key.length()){
            x.val = val;
            return x;
        }
        char c = key.charAt(d);
        x.next[c] = put(x.next[c], key, val, d+1);
        return x;
    }
}
```

## Union-find
用了路径压缩
```Python

class DSU(object):

   def __init__(self):
       self.par = range(1001)  # modify to list(range(1001)) for python 3.0 and above!!!
       self.rnk = [0] * 1001

   def find(self, x):
       if self.par[x] != x:
           self.par[x] = self.find(self.par[x])
       return self.par[x]

   def union(self, x, y):
       xr, yr = self.find(x), self.find(y)
       if xr == yr:
           return False
       elif self.rnk[xr] < self.rnk[yr]:
           self.par[xr] = yr
       elif self.rnk[xr] > self.rnk[yr]:
           self.par[yr] = xr
       else:
           self.par[yr] = xr
           self.rnk[xr] += 1
       return True

```