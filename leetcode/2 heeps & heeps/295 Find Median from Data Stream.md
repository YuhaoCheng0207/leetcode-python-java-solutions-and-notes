### 思路

* 求数据流中的中位数，最简单的方法是排序后求中间的数。

* 其中findMedian()函数的时间复杂度O(nlogn)，空间复杂度O(n)

* 更好一点的方法是用插入排序，因为插入排序天然的对逐一添加的元素友好，可以将元素插入已经排好顺序的数据里，用二分查找就能找到该插入的位置，时间复杂度为O(logn)，但还需要移动插入后右边剩余的元素，时间为O(n)，因此整体为O(n)
* 最好的方法是，不进行没必要的排序。因为只要求数据的中位数，因此其他位置不用管。而堆非常适用于只找最值，而其它元素无需排序，这样就可以以 O(log N) 的复杂度每次都从堆中取出最值。因此我们用堆实现这道题。


#### 堆
* 用两个堆，一个最大堆存数据中小的那一半，一个最小堆存数据中大的一半，这样就能通过O(1)的时间复杂度取出两边（或者一边）的最值，求出中位数
* 我们设定最大堆的元素等于最小堆（总数为偶数），或者比最小堆大1（总数为奇数）
* 每次让数据先过一下最大堆，再过一下最小堆，这样最大堆的堆顶肯定放到了最小堆，如果总数为奇数，则最小堆返回给最大堆堆顶，否则不返回。
* 所以每次只需要**O(logn)**即可整理出新添加元素在哪个堆里，并且保持了堆的结构。

```java

class MedianFinder {
    private PriorityQueue<Integer> minQueue;
    private PriorityQueue<Integer> maxQueue;
    private int count;
    /** initialize your data structure here. */
    public MedianFinder() {
        minQueue = new PriorityQueue<>();
        maxQueue = new PriorityQueue<>((a, b) -> b - a);
        count = 0;
        
    }
    
    public void addNum(int num) {
        count += 1;
        maxQueue.add(num);
        minQueue.add(maxQueue.poll());
        if( count % 2 == 1){
            maxQueue.add(minQueue.poll());
        }
    }
    
    public double findMedian() {
        if (count % 2 == 1){
            return (double) maxQueue.peek();
        }
        else{
            return (double) (maxQueue.peek() + minQueue.peek())/2;
        }
    }
}
/**
 * Your MedianFinder object will be instantiated and called as such:
 * MedianFinder obj = new MedianFinder();
 * obj.addNum(num);
 * double param_2 = obj.findMedian();
 */


```