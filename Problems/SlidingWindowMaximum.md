# 239 Sliding Window Maximum

## 思路

第二次做这个题结果还是做不出。参考了discussion里的使用deque的思路，使用deque存取index,每次移动时看下队列头部的index是否已经超出范围然后决定是否删除，同时比较窗口右端的元素a[i]与当前队列尾部的数字，删除尾部所有比a[i]小的数字，因为a[i]永远是窗口中比前面更好的选择。因此队列中的元素就是从大到小维护排列的，每次只需从队列头部peek即可。

## 代码

```Java
class Solution{
    public int[] maxSlidingWindow(int[] a, int k) {		
		if (a == null || k <= 0) {
			return new int[0];
		}
		int n = a.length;
		int[] r = new int[n-k+1];
		int ri = 0;
		// store index
		Deque<Integer> q = new ArrayDeque<>();
		for (int i = 0; i < a.length; i++) {
			// remove numbers out of range k
			while (!q.isEmpty() && q.peek() < i - k + 1) {
				q.poll();
			}
			// remove smaller numbers in k range as they are useless
			while (!q.isEmpty() && a[q.peekLast()] < a[i]) {
				q.pollLast();
			}
			// q contains index... r contains content
			q.offer(i);
			if (i >= k - 1) {
				r[ri++] = a[q.peek()];
			}
		}
		return r;
	}
}
```