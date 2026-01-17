# Complete DSA Study Guide with Java Solutions

## Table of Contents
1. [Arrays & Strings](#arrays--strings)
2. [Linked Lists](#linked-lists)
3. [Stacks](#stacks)
4. [Queues](#queues)
5. [Trees](#trees)
6. [Graphs](#graphs)
7. [Dynamic Programming](#dynamic-programming)
8. [Advanced Topics](#advanced-topics)

---

# 1. ARRAYS & STRINGS

## 📚 Basic Terminology

### Arrays
- **Static Array**: Fixed size, contiguous memory
- **Dynamic Array**: Resizable (ArrayList in Java)
- **Subarray**: Contiguous sequence of elements
- **Subsequence**: Non-contiguous sequence maintaining order
- **In-place**: Modifying array without extra space

### Strings
- **Immutable**: String objects cannot be changed (use StringBuilder for mutations)
- **Substring**: Contiguous sequence of characters
- **Palindrome**: Reads same forward and backward
- **Anagram**: Same characters, different arrangement

## 🔧 Major Algorithms with Java Code

### 1. Two Pointers

**When to use**: Sorted arrays, palindromes, pair finding

```java
// Two Sum II - Sorted Array
class TwoPointers {
    public int[] twoSum(int[] numbers, int target) {
        int left = 0, right = numbers.length - 1;
        
        while (left < right) {
            int sum = numbers[left] + numbers[right];
            if (sum == target) {
                return new int[]{left + 1, right + 1}; // 1-indexed
            } else if (sum < target) {
                left++;
            } else {
                right--;
            }
        }
        return new int[]{-1, -1};
    }
    
    // Valid Palindrome
    public boolean isPalindrome(String s) {
        int left = 0, right = s.length() - 1;
        
        while (left < right) {
            while (left < right && !Character.isLetterOrDigit(s.charAt(left))) {
                left++;
            }
            while (left < right && !Character.isLetterOrDigit(s.charAt(right))) {
                right--;
            }
            
            if (Character.toLowerCase(s.charAt(left)) != 
                Character.toLowerCase(s.charAt(right))) {
                return false;
            }
            left++;
            right--;
        }
        return true;
    }
}
```

### 2. Sliding Window

**When to use**: Substrings, subarrays, fixed/variable window size

```java
class SlidingWindow {
    // Maximum Sum Subarray of Size K (Fixed Window)
    public int maxSumSubarray(int[] arr, int k) {
        int windowSum = 0, maxSum = 0;
        
        // First window
        for (int i = 0; i < k; i++) {
            windowSum += arr[i];
        }
        maxSum = windowSum;
        
        // Slide the window
        for (int i = k; i < arr.length; i++) {
            windowSum = windowSum - arr[i - k] + arr[i];
            maxSum = Math.max(maxSum, windowSum);
        }
        return maxSum;
    }
    
    // Longest Substring Without Repeating Characters (Variable Window)
    public int lengthOfLongestSubstring(String s) {
        Map<Character, Integer> map = new HashMap<>();
        int maxLen = 0, left = 0;
        
        for (int right = 0; right < s.length(); right++) {
            char c = s.charAt(right);
            if (map.containsKey(c)) {
                left = Math.max(left, map.get(c) + 1);
            }
            map.put(c, right);
            maxLen = Math.max(maxLen, right - left + 1);
        }
        return maxLen;
    }
}
```

### 3. Prefix Sum

**When to use**: Range sum queries, subarray sums

```java
class PrefixSum {
    // Range Sum Query - Immutable
    private int[] prefix;
    
    public PrefixSum(int[] nums) {
        prefix = new int[nums.length + 1];
        for (int i = 0; i < nums.length; i++) {
            prefix[i + 1] = prefix[i] + nums[i];
        }
    }
    
    public int rangeSum(int left, int right) {
        return prefix[right + 1] - prefix[left];
    }
    
    // Subarray Sum Equals K
    public int subarraySum(int[] nums, int k) {
        Map<Integer, Integer> map = new HashMap<>();
        map.put(0, 1);
        int sum = 0, count = 0;
        
        for (int num : nums) {
            sum += num;
            if (map.containsKey(sum - k)) {
                count += map.get(sum - k);
            }
            map.put(sum, map.getOrDefault(sum, 0) + 1);
        }
        return count;
    }
}
```

### 4. Binary Search

**When to use**: Sorted arrays, search space reduction

```java
class BinarySearch {
    // Standard Binary Search
    public int binarySearch(int[] arr, int target) {
        int left = 0, right = arr.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (arr[mid] == target) {
                return mid;
            } else if (arr[mid] < target) {
                left = mid + 1;
            } else {
                right = mid - 1;
            }
        }
        return -1;
    }
    
    // Search in Rotated Sorted Array
    public int searchRotated(int[] nums, int target) {
        int left = 0, right = nums.length - 1;
        
        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (nums[mid] == target) return mid;
            
            // Left half is sorted
            if (nums[left] <= nums[mid]) {
                if (target >= nums[left] && target < nums[mid]) {
                    right = mid - 1;
                } else {
                    left = mid + 1;
                }
            } 
            // Right half is sorted
            else {
                if (target > nums[mid] && target <= nums[right]) {
                    left = mid + 1;
                } else {
                    right = mid - 1;
                }
            }
        }
        return -1;
    }
}
```

## 📝 LeetCode Problems

### Two Pointers
1. [Two Sum II](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/) - Easy
2. [Three Sum](https://leetcode.com/problems/3sum/) - Medium
3. [Container With Most Water](https://leetcode.com/problems/container-with-most-water/) - Medium
4. [Valid Palindrome](https://leetcode.com/problems/valid-palindrome/) - Easy
5. [Remove Duplicates from Sorted Array](https://leetcode.com/problems/remove-duplicates-from-sorted-array/) - Easy
6. [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) - Hard

### Sliding Window
1. [Longest Substring Without Repeating Characters](https://leetcode.com/problems/longest-substring-without-repeating-characters/) - Medium
2. [Minimum Window Substring](https://leetcode.com/problems/minimum-window-substring/) - Hard
3. [Longest Repeating Character Replacement](https://leetcode.com/problems/longest-repeating-character-replacement/) - Medium
4. [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) - Hard
5. [Minimum Size Subarray Sum](https://leetcode.com/problems/minimum-size-subarray-sum/) - Medium

### Hash Maps/Sets
1. [Two Sum](https://leetcode.com/problems/two-sum/) - Easy
2. [Group Anagrams](https://leetcode.com/problems/group-anagrams/) - Medium
3. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
4. [Longest Consecutive Sequence](https://leetcode.com/problems/longest-consecutive-sequence/) - Medium
5. [Contains Duplicate](https://leetcode.com/problems/contains-duplicate/) - Easy

### Prefix Sum
1. [Range Sum Query - Immutable](https://leetcode.com/problems/range-sum-query-immutable/) - Easy
2. [Subarray Sum Equals K](https://leetcode.com/problems/subarray-sum-equals-k/) - Medium
3. [Product of Array Except Self](https://leetcode.com/problems/product-of-array-except-self/) - Medium
4. [Find Pivot Index](https://leetcode.com/problems/find-pivot-index/) - Easy

---

# 2. LINKED LISTS

## 📚 Basic Terminology

- **Singly Linked List**: Each node has data and next pointer
- **Doubly Linked List**: Each node has data, next and prev pointers
- **Circular Linked List**: Last node points back to first node
- **Head**: First node in the list
- **Tail**: Last node in the list
- **Node**: Basic unit containing data and pointer(s)

## 🔧 Major Algorithms with Java Code

### 1. Node Definition

```java
// Singly Linked List Node
class ListNode {
    int val;
    ListNode next;
    ListNode(int val) { this.val = val; }
    ListNode(int val, ListNode next) { this.val = val; this.next = next; }
}

// Doubly Linked List Node
class DoublyListNode {
    int val;
    DoublyListNode prev;
    DoublyListNode next;
    DoublyListNode(int val) { this.val = val; }
}
```

### 2. Fast & Slow Pointers (Floyd's Cycle Detection)

**When to use**: Cycle detection, middle node, nth node

```java
class FastSlowPointers {
    // Detect Cycle
    public boolean hasCycle(ListNode head) {
        if (head == null) return false;
        
        ListNode slow = head, fast = head;
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) return true;
        }
        return false;
    }
    
    // Find Middle Node
    public ListNode findMiddle(ListNode head) {
        ListNode slow = head, fast = head;
        
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
        }
        return slow;
    }
    
    // Find Cycle Start
    public ListNode detectCycle(ListNode head) {
        ListNode slow = head, fast = head;
        
        // Detect cycle
        while (fast != null && fast.next != null) {
            slow = slow.next;
            fast = fast.next.next;
            if (slow == fast) break;
        }
        
        if (fast == null || fast.next == null) return null;
        
        // Find start of cycle
        slow = head;
        while (slow != fast) {
            slow = slow.next;
            fast = fast.next;
        }
        return slow;
    }
}
```

### 3. Linked List Reversal

**When to use**: Reversing lists, partial reversals

```java
class LinkedListReversal {
    // Reverse Entire List
    public ListNode reverseList(ListNode head) {
        ListNode prev = null, curr = head;
        
        while (curr != null) {
            ListNode next = curr.next;
            curr.next = prev;
            prev = curr;
            curr = next;
        }
        return prev;
    }
    
    // Reverse Between Positions
    public ListNode reverseBetween(ListNode head, int left, int right) {
        if (head == null) return null;
        
        ListNode dummy = new ListNode(0);
        dummy.next = head;
        ListNode prev = dummy;
        
        // Move to position before left
        for (int i = 0; i < left - 1; i++) {
            prev = prev.next;
        }
        
        // Reverse from left to right
        ListNode curr = prev.next;
        for (int i = 0; i < right - left; i++) {
            ListNode next = curr.next;
            curr.next = next.next;
            next.next = prev.next;
            prev.next = next;
        }
        
        return dummy.next;
    }
}
```

### 4. Merge and Sort

**When to use**: Merging sorted lists, sorting

```java
class MergeSort {
    // Merge Two Sorted Lists
    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        
        while (l1 != null && l2 != null) {
            if (l1.val < l2.val) {
                curr.next = l1;
                l1 = l1.next;
            } else {
                curr.next = l2;
                l2 = l2.next;
            }
            curr = curr.next;
        }
        
        curr.next = (l1 != null) ? l1 : l2;
        return dummy.next;
    }
    
    // Merge K Sorted Lists (Using Min Heap)
    public ListNode mergeKLists(ListNode[] lists) {
        PriorityQueue<ListNode> pq = new PriorityQueue<>((a, b) -> a.val - b.val);
        
        for (ListNode list : lists) {
            if (list != null) pq.offer(list);
        }
        
        ListNode dummy = new ListNode(0);
        ListNode curr = dummy;
        
        while (!pq.isEmpty()) {
            ListNode node = pq.poll();
            curr.next = node;
            curr = curr.next;
            if (node.next != null) {
                pq.offer(node.next);
            }
        }
        
        return dummy.next;
    }
}
```

## 📝 LeetCode Problems

### Fast & Slow Pointers
1. [Linked List Cycle](https://leetcode.com/problems/linked-list-cycle/) - Easy
2. [Linked List Cycle II](https://leetcode.com/problems/linked-list-cycle-ii/) - Medium
3. [Middle of the Linked List](https://leetcode.com/problems/middle-of-the-linked-list/) - Easy
4. [Happy Number](https://leetcode.com/problems/happy-number/) - Easy
5. [Palindrome Linked List](https://leetcode.com/problems/palindrome-linked-list/) - Easy

### Linked List Reversal
1. [Reverse Linked List](https://leetcode.com/problems/reverse-linked-list/) - Easy
2. [Reverse Linked List II](https://leetcode.com/problems/reverse-linked-list-ii/) - Medium
3. [Reverse Nodes in k-Group](https://leetcode.com/problems/reverse-nodes-in-k-group/) - Hard
4. [Swap Nodes in Pairs](https://leetcode.com/problems/swap-nodes-in-pairs/) - Medium
5. [Reorder List](https://leetcode.com/problems/reorder-list/) - Medium

### Two Pointers (Linked List)
1. [Merge Two Sorted Lists](https://leetcode.com/problems/merge-two-sorted-lists/) - Easy
2. [Intersection of Two Linked Lists](https://leetcode.com/problems/intersection-of-two-linked-lists/) - Easy
3. [Remove Nth Node From End](https://leetcode.com/problems/remove-nth-node-from-end-of-list/) - Medium
4. [Sort List](https://leetcode.com/problems/sort-list/) - Medium

---

# 3. STACKS

## 📚 Basic Terminology

- **Stack**: LIFO (Last In First Out) data structure
- **Push**: Add element to top
- **Pop**: Remove element from top
- **Peek/Top**: View top element without removing
- **Monotonic Stack**: Stack maintaining increasing/decreasing order
- **Stack Overflow**: When stack exceeds capacity
- **Stack Underflow**: Pop from empty stack

## 🔧 Major Algorithms with Java Code

### 1. Stack Implementation

```java
// Array-based Stack
class ArrayStack {
    private int[] arr;
    private int top;
    private int capacity;
    
    public ArrayStack(int size) {
        arr = new int[size];
        capacity = size;
        top = -1;
    }
    
    public void push(int x) {
        if (top == capacity - 1) {
            throw new RuntimeException("Stack Overflow");
        }
        arr[++top] = x;
    }
    
    public int pop() {
        if (isEmpty()) {
            throw new RuntimeException("Stack Underflow");
        }
        return arr[top--];
    }
    
    public int peek() {
        if (isEmpty()) {
            throw new RuntimeException("Stack is empty");
        }
        return arr[top];
    }
    
    public boolean isEmpty() {
        return top == -1;
    }
}

// Linked List-based Stack
class LinkedStack {
    private class Node {
        int data;
        Node next;
        Node(int data) { this.data = data; }
    }
    
    private Node top;
    
    public void push(int x) {
        Node newNode = new Node(x);
        newNode.next = top;
        top = newNode;
    }
    
    public int pop() {
        if (isEmpty()) {
            throw new RuntimeException("Stack Underflow");
        }
        int data = top.data;
        top = top.next;
        return data;
    }
    
    public int peek() {
        if (isEmpty()) {
            throw new RuntimeException("Stack is empty");
        }
        return top.data;
    }
    
    public boolean isEmpty() {
        return top == null;
    }
}
```

### 2. Stack for Matching/Parsing

**When to use**: Parentheses, expressions, parsing

```java
class StackMatching {
    // Valid Parentheses
    public boolean isValid(String s) {
        Stack<Character> stack = new Stack<>();
        Map<Character, Character> pairs = new HashMap<>();
        pairs.put(')', '(');
        pairs.put('}', '{');
        pairs.put(']', '[');
        
        for (char c : s.toCharArray()) {
            if (pairs.containsValue(c)) {
                stack.push(c);
            } else if (pairs.containsKey(c)) {
                if (stack.isEmpty() || stack.pop() != pairs.get(c)) {
                    return false;
                }
            }
        }
        return stack.isEmpty();
    }
    
    // Min Stack
    class MinStack {
        private Stack<Integer> stack;
        private Stack<Integer> minStack;
        
        public MinStack() {
            stack = new Stack<>();
            minStack = new Stack<>();
        }
        
        public void push(int val) {
            stack.push(val);
            if (minStack.isEmpty() || val <= minStack.peek()) {
                minStack.push(val);
            }
        }
        
        public void pop() {
            int val = stack.pop();
            if (val == minStack.peek()) {
                minStack.pop();
            }
        }
        
        public int top() {
            return stack.peek();
        }
        
        public int getMin() {
            return minStack.peek();
        }
    }
}
```

### 3. Monotonic Stack

**When to use**: Next greater/smaller element problems

```java
class MonotonicStack {
    // Next Greater Element
    public int[] nextGreaterElement(int[] nums) {
        int n = nums.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>();
        
        // Traverse from right to left
        for (int i = n - 1; i >= 0; i--) {
            // Pop smaller elements
            while (!stack.isEmpty() && stack.peek() <= nums[i]) {
                stack.pop();
            }
            
            result[i] = stack.isEmpty() ? -1 : stack.peek();
            stack.push(nums[i]);
        }
        
        return result;
    }
    
    // Daily Temperatures
    public int[] dailyTemperatures(int[] temperatures) {
        int n = temperatures.length;
        int[] result = new int[n];
        Stack<Integer> stack = new Stack<>(); // stores indices
        
        for (int i = 0; i < n; i++) {
            while (!stack.isEmpty() && temperatures[i] > temperatures[stack.peek()]) {
                int prevIndex = stack.pop();
                result[prevIndex] = i - prevIndex;
            }
            stack.push(i);
        }
        
        return result;
    }
    
    // Largest Rectangle in Histogram
    public int largestRectangleArea(int[] heights) {
        Stack<Integer> stack = new Stack<>();
        int maxArea = 0;
        int n = heights.length;
        
        for (int i = 0; i <= n; i++) {
            int h = (i == n) ? 0 : heights[i];
            
            while (!stack.isEmpty() && h < heights[stack.peek()]) {
                int height = heights[stack.pop()];
                int width = stack.isEmpty() ? i : i - stack.peek() - 1;
                maxArea = Math.max(maxArea, height * width);
            }
            stack.push(i);
        }
        
        return maxArea;
    }
}
```

## 📝 LeetCode Problems

### Stack (Matching/Parsing)
1. [Valid Parentheses](https://leetcode.com/problems/valid-parentheses/) - Easy
2. [Min Stack](https://leetcode.com/problems/min-stack/) - Medium
3. [Evaluate Reverse Polish Notation](https://leetcode.com/problems/evaluate-reverse-polish-notation/) - Medium
4. [Basic Calculator](https://leetcode.com/problems/basic-calculator/) - Hard
5. [Decode String](https://leetcode.com/problems/decode-string/) - Medium

### Monotonic Stack
1. [Next Greater Element I](https://leetcode.com/problems/next-greater-element-i/) - Easy
2. [Next Greater Element II](https://leetcode.com/problems/next-greater-element-ii/) - Medium
3. [Daily Temperatures](https://leetcode.com/problems/daily-temperatures/) - Medium
4. [Largest Rectangle in Histogram](https://leetcode.com/problems/largest-rectangle-in-histogram/) - Hard
5. [Trapping Rain Water](https://leetcode.com/problems/trapping-rain-water/) - Hard

---

# 4. QUEUES

## 📚 Basic Terminology

- **Queue**: FIFO (First In First Out) data structure
- **Enqueue**: Add element to rear/back
- **Dequeue**: Remove element from front
- **Circular Queue**: Last position connected to first
- **Priority Queue**: Elements ordered by priority (heap)
- **Deque**: Double-ended queue (add/remove from both ends)
- **Monotonic Queue**: Queue maintaining increasing/decreasing order

## 🔧 Major Algorithms with Java Code

### 1. Queue Implementation

```java
// Array-based Circular Queue
class CircularQueue {
    private int[] arr;
    private int front, rear, size, capacity;
    
    public CircularQueue(int k) {
        arr = new int[k];
        capacity = k;
        front = 0;
        rear = -1;
        size = 0;
    }
    
    public boolean enqueue(int value) {
        if (isFull()) return false;
        rear = (rear + 1) % capacity;
        arr[rear] = value;
        size++;
        return true;
    }
    
    public boolean dequeue() {
        if (isEmpty()) return false;
        front = (front + 1) % capacity;
        size--;
        return true;
    }
    
    public int front() {
        return isEmpty() ? -1 : arr[front];
    }
    
    public int rear() {
        return isEmpty() ? -1 : arr[rear];
    }
    
    public boolean isEmpty() {
        return size == 0;
    }
    
    public boolean isFull() {
        return size == capacity;
    }
}

// Linked List-based Queue
class LinkedQueue {
    private class Node {
        int data;
        Node next;
        Node(int data) { this.data = data; }
    }
    
    private Node front, rear;
    
    public void enqueue(int x) {
        Node newNode = new Node(x);
        if (rear == null) {
            front = rear = newNode;
            return;
        }
        rear.next = newNode;
        rear = newNode;
    }
    
    public int dequeue() {
        if (isEmpty()) {
            throw new RuntimeException("Queue is empty");
        }
        int data = front.data;
        front = front.next;
        if (front == null) rear = null;
        return data;
    }
    
    public boolean isEmpty() {
        return front == null;
    }
}
```

### 2. Deque (Double-Ended Queue)

```java
class DequeOperations {
    // Deque using ArrayList
    class MyDeque {
        private List<Integer> list;
        
        public MyDeque() {
            list = new ArrayList<>();
        }
        
        public void addFront(int x) {
            list.add(0, x);
        }
        
        public void addRear(int x) {
            list.add(x);
        }
        
        public int removeFront() {
            if (list.isEmpty()) throw new RuntimeException("Deque is empty");
            return list.remove(0);
        }
        
        public int removeRear() {
            if (list.isEmpty()) throw new RuntimeException("Deque is empty");
            return list.remove(list.size() - 1);
        }
        
        public int getFront() {
            if (list.isEmpty()) throw new RuntimeException("Deque is empty");
            return list.get(0);
        }
        
        public int getRear() {
            if (list.isEmpty()) throw new RuntimeException("Deque is empty");
            return list.get(list.size() - 1);
        }
    }
}
```

### 3. Monotonic Queue/Deque

**When to use**: Sliding window min/max

```java
class MonotonicQueue {
    // Sliding Window Maximum
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums == null || nums.length == 0) return new int[0];
        
        int n = nums.length;
        int[] result = new int[n - k + 1];
        Deque<Integer> deque = new LinkedList<>(); // stores indices
        
        for (int i = 0; i < n; i++) {
            // Remove elements outside current window
            while (!deque.isEmpty() && deque.peekFirst() < i - k + 1) {
                deque.pollFirst();
            }
            
            // Remove smaller elements from rear
            while (!deque.isEmpty() && nums[deque.peekLast()] < nums[i]) {
                deque.pollLast();
            }
            
            deque.offerLast(i);
            
            // Add to result when window is formed
            if (i >= k - 1) {
                result[i - k + 1] = nums[deque.peekFirst()];
            }
        }
        
        return result;
    }
}
```

### 4. Priority Queue (Heap)

```java
class PriorityQueueOperations {
    // Kth Largest Element
    public int findKthLargest(int[] nums, int k) {
        PriorityQueue<Integer> pq = new PriorityQueue<>(); // min heap
        
        for (int num : nums) {
            pq.offer(num);
            if (pq.size() > k) {
                pq.poll();
            }
        }
        
        return pq.peek();
    }
    
    // Top K Frequent Elements
    public int[] topKFrequent(int[] nums, int k) {
        Map<Integer, Integer> freq = new HashMap<>();
        for (int num : nums) {
            freq.put(num, freq.getOrDefault(num, 0) + 1);
        }
        
        PriorityQueue<Integer> pq = new PriorityQueue<>(
            (a, b) -> freq.get(a) - freq.get(b)
        );
        
        for (int num : freq.keySet()) {
            pq.offer(num);
            if (pq.size() > k) {
                pq.poll();
            }
        }
        
        int[] result = new int[k];
        for (int i = k - 1; i >= 0; i--) {
            result[i] = pq.poll();
        }
        return result;
    }
}
```

## 📝 LeetCode Problems

### Queue Implementation
1. [Design Circular Queue](https://leetcode.com/problems/design-circular-queue/) - Medium
2. [Implement Queue using Stacks](https://leetcode.com/problems/implement-queue-using-stacks/) - Easy
3. [Implement Stack using Queues](https://leetcode.com/problems/implement-stack-using-queues/) - Easy

### Monotonic Queue/Deque
1. [Sliding Window Maximum](https://leetcode.com/problems/sliding-window-maximum/) - Hard
2. [Shortest Subarray with Sum at Least K](https://leetcode.com/problems/shortest-subarray-with-sum-at-least-k/) - Hard
3. [Jump Game VI](https://leetcode.com/problems/jump-game-vi/) - Medium

### Priority Queue
1. [Kth Largest Element in an Array](https://leetcode.com/problems/kth-largest-element-in-an-array/) - Medium
2. [Top K Frequent Elements](https://leetcode.com/problems/top-k-frequent-elements/) - Medium
3. [Merge K Sorted Lists](https://leetcode.com/problems/merge-k-sorted-lists/) - Hard
4. [Find Median from Data Stream](https://leetcode.com/problems/find-median-from-data-stream/) - Hard
5. [Task Scheduler](https://leetcode.com/problems/task-scheduler/) - Medium

---

# 5. TREES

## 📚 Basic Terminology

### Tree Types
- **Binary Tree**: Each node has at most 2 children
- **Binary Search Tree (BST)**: Left < Root < Right
- **Balanced Tree**: Height difference ≤ 1 (AVL, Red-Black)
- **Complete Binary Tree**: All levels filled except possibly last
- **Full Binary Tree**: Every node has 0 or 2 children
- **Perfect Binary Tree**: All internal nodes have 2 children, all leaves at same level
- **N-ary Tree**: Each node can have N children

### Tree Terminology
- **Root**: Top node with no parent
- **Leaf**: Node with no children
- **Height**: Longest path from node to leaf
- **Depth**: Distance from root to node
- **Level**: Nodes at same depth
- **Subtree**: Tree formed by node and its descendants

### Traversal Types
- **Inorder (LNR)**: Left → Node → Right (sorted order for BST)
- **Preorder (NLR)**: Node → Left → Right (copy tree)
- **Postorder (LRN)**: Left → Right → Node (delete tree)
- **Level Order (BFS)**: Level by level traversal

## 🔧 Major Algorithms with Java Code

### 1. Tree Node Definition

```java
// Binary Tree Node
class TreeNode {
    int val;
    TreeNode left;
    TreeNode right;
    TreeNode(int val) { this.val = val; }
    TreeNode(int val, TreeNode left, TreeNode right) {
        this.val = val;
        this.left = left;
        this.right = right;
    }
}

// N-ary Tree Node
class Node {
    int val;
    List<Node> children;
    Node(int val) {
        this.val = val;
        children = new ArrayList<>();
    }
}
```

### 2. Tree Traversals

```java
class TreeTraversals {
    // Inorder Traversal (Iterative)
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        Stack<TreeNode> stack = new Stack<>();
        TreeNode curr = root;
        
        while (curr != null || !stack.isEmpty()) {
            while (curr != null) {
                stack.push(curr);
                curr = curr.left;
            }
            curr = stack.pop();
            result.add(curr.val);
            curr = curr.right;
        }
        return result;
    }
    
    // Preorder Traversal (Iterative)
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(node.val);
            
            if (node.right != null) stack.push(node.right);
            if (node.left != null) stack.push(node.left);
        }
        return result;
    }
    
    // Postorder Traversal (Iterative)
    public List<Integer> postorderTraversal(TreeNode root) {
        List<Integer> result = new ArrayList<>();
        if (root == null) return result;
        
        Stack<TreeNode> stack = new Stack<>();
        stack.push(root);
        
        while (!stack.isEmpty()) {
            TreeNode node = stack.pop();
            result.add(0, node.val); // Add to front
            
            if (node.left != null) stack.push(node.left);
            if (node.right != null) stack.push(node.right);
        }
        return result;
    }
    
    // Level Order Traversal (BFS)
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> result = new ArrayList<>();
        if (root == null) return result;
        
        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        
        while (!queue.isEmpty()) {
            int levelSize = queue.size();
            List<Integer> level = new ArrayList<>();
            
            for (int i = 0; i < levelSize; i++) {
                TreeNode node = queue.poll();
                level.add(node.val);
                
                if (node.left != null) queue.offer(node.left);
                if (node.right != null) queue.offer(node.right);
            }
            result.add(level);
        }
        return result;
    }
}
```

### 3. Tree DFS (Recursion)

**When to use**: Path problems, tree properties

```java
class TreeDFS {
    // Maximum Depth
    public int maxDepth(TreeNode root) {
        if (root == null) return 0;
        return 1 + Math.max(maxDepth(root.left), maxDepth(root.right));
    }
    
    // Diameter of Binary Tree
    private int diameter = 0;
    
    public int diameterOfBinaryTree(TreeNode root) {
        height(root);
        return diameter;
    }
    
    private int height(TreeNode node) {
        if (node == null) return 0;
        
        int left = height(node.left);
        int right = height(node.right);
        
        diameter = Math.max(diameter, left + right);
        return 1 + Math.max(left, right);
    }
    
    // Balanced Binary Tree
    public boolean isBalanced(TreeNode root) {
        return checkHeight(root) != -1;
    }
    
    private int checkHeight(TreeNode node) {
        if (node == null) return 0;
        
        int left = checkHeight(node.left);
        if (left == -1) return -1;
        
        int right = checkHeight(node.right);
        if (right == -1) return -1;
        
        if (Math.abs(left - right) > 1) return -1;
        return 1 + Math.max(left, right);
    }
    
    // Path Sum
    public boolean hasPathSum(TreeNode root, int targetSum) {
        if (root == null) return false;
        
        if (root.left == null && root.right == null) {
            return targetSum == root.val;
        }
        
        return hasPathSum(root.left, targetSum - root.val) ||
               hasPathSum(root.right, targetSum - root.val);
    }
    
    // Binary Tree Maximum Path Sum
    private int maxSum = Integer.MIN_VALUE;
    
    public int maxPathSum(TreeNode root) {
        maxGain(root);
        return maxSum;
    }
    
    private int maxGain(TreeNode node) {
        if (node == null) return 0;
        
        int leftGain = Math.max(maxGain(node.left), 0);
        int rightGain = Math.max(maxGain(node.right), 0);
        
        int currentPath = node.val + leftGain + rightGain;
        maxSum = Math.max(maxSum, currentPath);
        
        return node.val + Math.max(leftGain, rightGain);
    }
}
```

### 4. Binary Search Tree Operations

```java
class BSTOperations {
    // Search in BST
    public TreeNode searchBST(TreeNode root, int val) {
        if (root == null || root.val == val) return root;
        
        if (val < root.val) {
            return searchBST(root.left, val);
        } else {
            return searchBST(root.right, val);
        }
    }
    
    // Insert into BST
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        
        if (val < root.val) {
            root.left = insertIntoBST(root.left, val);
        } else {
            root.right = insertIntoBST(root.right, val);
        }
        return root;
    }
    
    // Delete from BST
    public TreeNode deleteNode(TreeNode root, int key) {
        if (root == null) return null;
        
        if (key < root.val) {
            root.left = deleteNode(root.left, key);
        } else if (key > root.val) {
            root.right = deleteNode(root.right, key);
        } else {
            // Node to be deleted found
            if (root.left == null) return root.right;
            if (root.right == null) return root.left;
            
            // Node has two children
            TreeNode minNode = findMin(root.right);
            root.val = minNode.val;
            root.right = deleteNode(root.right, minNode.val);
        }
        return root;
    }
    
    private TreeNode findMin(TreeNode node) {
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }
    
    // Validate BST
    public boolean isValidBST(TreeNode root) {
        return validate(root, null, null);
    }
    
    private boolean validate(TreeNode node, Integer min, Integer max) {
        if (node == null) return true;
        
        if ((min != null && node.val <= min) || 
            (max != null && node.val >= max)) {
            return false;
        }
        
        return validate(node.left, min, node.val) && 
               validate(node.right, node.val, max);
    }
    
    // Lowest Common Ancestor in BST
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (p.val < root.val && q.val < root.val) {
            return lowestCommonAncestor(root.left, p, q);
        } else if (p.val > root.val && q.val > root.val) {
            return lowestCommonAncestor(root.right, p, q);
        } else {
            return root;
        }
    }
}
```

### 5. Tree Construction

```java
class TreeConstruction {
    // Construct from Preorder and Inorder
    private int preIndex = 0;
    private Map<Integer, Integer> inorderMap;
    
    public TreeNode buildTree(int[] preorder, int[] inorder) {
        inorderMap = new HashMap<>();
        for (int i = 0; i < inorder.length; i++) {
            inorderMap.put(inorder[i], i);
        }
        return build(preorder, 0, inorder.length - 1);
    }
    
    private TreeNode build(int[] preorder, int left, int right) {
        if (left > right) return null;
        
        int rootVal = preorder[preIndex++];
        TreeNode root = new TreeNode(rootVal);
        
        int mid = inorderMap.get(rootVal);
        root.left = build(preorder, left, mid - 1);
        root.right = build(preorder, mid + 1, right);
        
        return root;
    }
    
    // Serialize and Deserialize Binary Tree
    public String serialize(TreeNode root) {
        StringBuilder sb = new StringBuilder();
        serializeHelper(root, sb);
        return sb.toString();
    }
    
    private void serializeHelper(TreeNode node, StringBuilder sb) {
        if (node == null) {
            sb.append("null,");
            return;
        }
        sb.append(node.val).append(",");
        serializeHelper(node.left, sb);
        serializeHelper(node.right, sb);
    }
    
    public TreeNode deserialize(String data) {
        Queue<String> queue = new LinkedList<>(Arrays.asList(data.split(",")));
        return deserializeHelper(queue);
    }
    
    private TreeNode deserializeHelper(Queue<String> queue) {
        String val = queue.poll();
        if (val.equals("null")) return null;
        
        TreeNode node = new TreeNode(Integer.parseInt(val));
        node.left = deserializeHelper(queue);
        node.right = deserializeHelper(queue);
        return node;
    }
}
```

## 📝 LeetCode Problems

### Tree Traversals
1. [Binary Tree Inorder Traversal](https://leetcode.com/problems/binary-tree-inorder-traversal/) - Easy
2. [Binary Tree Level Order Traversal](https://leetcode.com/problems/binary-tree-level-order-traversal/) - Medium
3. [Binary Tree Zigzag Level Order Traversal](https://leetcode.com/problems/binary-tree-zigzag-level-order-traversal/) - Medium
4. [Binary Tree Right Side View](https://leetcode.com/problems/binary-tree-right-side-view/) - Medium

### Tree DFS
1. [Maximum Depth of Binary Tree](https://leetcode.com/problems/maximum-depth-of-binary-tree/) - Easy
2. [Diameter of Binary Tree](https://leetcode.com/problems/diameter-of-binary-tree/) - Easy
3. [Balanced Binary Tree](https://leetcode.com/problems/balanced-binary-tree/) - Easy
4. [Path Sum](https://leetcode.com/problems/path-sum/) - Easy
5. [Binary Tree Maximum Path Sum](https://leetcode.com/problems/binary-tree-maximum-path-sum/) - Hard
6. [Lowest Common Ancestor of a Binary Tree](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/) - Medium

### BST Operations
1. [Search in a Binary Search Tree](https://leetcode.com/problems/search-in-a-binary-search-tree/) - Easy
2. [Insert into a Binary Search Tree](https://leetcode.com/problems/insert-into-a-binary-search-tree/) - Medium
3. [Delete Node in a BST](https://leetcode.com/problems/delete-node-in-a-bst/) - Medium
4. [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/) - Medium
5. [Kth Smallest Element in a BST](https://leetcode.com/problems/kth-smallest-element-in-a-bst/) - Medium

### Tree Construction
1. [Construct Binary Tree from Preorder and Inorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/) - Medium
2. [Construct Binary Tree from Inorder and Postorder Traversal](https://leetcode.com/problems/construct-binary-tree-from-inorder-and-postorder-traversal/) - Medium
3. [Serialize and Deserialize Binary Tree](https://leetcode.com/problems/serialize-and-deserialize-binary-tree/) - Hard

---

# 6. GRAPHS

## 📚 Basic Terminology

### Graph Types
- **Directed Graph (Digraph)**: Edges have direction
- **Undirected Graph**: Edges are bidirectional
- **Weighted Graph**: Edges have weights/costs
- **Cyclic Graph**: Contains at least one cycle
- **Acyclic Graph**: No cycles (DAG - Directed Acyclic Graph)
- **Connected Graph**: Path exists between all vertices
- **Disconnected Graph**: Some vertices unreachable

### Graph Representations
- **Adjacency Matrix**: 2D array (space: O(V²))
- **Adjacency List**: Array of lists (space: O(V + E))
- **Edge List**: List of edges (space: O(E))

### Graph Terminology
- **Vertex/Node**: Point in graph
- **Edge**: Connection between vertices
- **Degree**: Number of edges connected to vertex
- **Path**: Sequence of vertices
- **Cycle**: Path that starts and ends at same vertex
- **Component**: Maximal connected subgraph

## 🔧 Major Algorithms with Java Code

### 1. Graph Representations

```java
class GraphRepresentation {
    // Adjacency List (Most Common)
    class Graph {
        private int V;
        private List<List<Integer>> adj;
        
        public Graph(int v) {
            V = v;
            adj = new ArrayList<>();
            for (int i = 0; i < v; i++) {
                adj.add(new ArrayList<>());
            }
        }
        
        public void addEdge(int u, int v) {
            adj.get(u).add(v);
            // For undirected graph, add reverse edge
            // adj.get(v).add(u);
        }
        
        public List<Integer> getNeighbors(int u) {
            return adj.get(u);
        }
    }
    
    // Weighted Graph
    class WeightedGraph {
        private Map<Integer, List<int[]>> adj; // node -> [(neighbor, weight)]
        
        public WeightedGraph() {
            adj = new HashMap<>();
        }
        
        public void addEdge(int u, int v, int weight) {
            adj.putIfAbsent(u, new ArrayList<>());
            adj.putIfAbsent(v, new ArrayList<>());
            adj.get(u).add(new int[]{v, weight});
            // For undirected: adj.get(v).add(new int[]{u, weight});
        }
    }
}
```

### 2. BFS (Breadth-First Search)

**When to use**: Shortest path (unweighted), level-based traversal

```java
class BFS {
    // Basic BFS
    public void bfs(int[][] graph, int start) {
        int n = graph.length;
        boolean[] visited = new boolean[n];
        Queue<Integer> queue = new LinkedList<>();
        
        queue.offer(start);
        visited[start] = true;
        
        while (!queue.isEmpty()) {
            int node = queue.poll();
            System.out.print(node + " ");
            
            for (int neighbor : graph[node]) {
                if (!visited[neighbor]) {
                    visited[neighbor] = true;
                    queue.offer(neighbor);
                }
            }
        }
    }
    
    // Number of Islands
    public int numIslands(char[][] grid) {
        if (grid == null || grid.length == 0) return 0;
        
        int rows = grid.length, cols = grid[0].length;
        int count = 0;
        
        for (int i = 0; i < rows; i++) {
            for (int j = 0; j < cols; j++) {
                if (grid[i][j] == '1') {
                    bfsIsland(grid, i, j);
                    count++;
                }
            }
        }
        return count;
    }
    
    private void bfsIsland(char[][] grid, int i, int j) {
        int rows = grid.length, cols = grid[0].length;
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{i, j});
        grid[i][j] = '0';
        
        int[][] dirs = {{0,1}, {0,-1}, {1,0}, {-1,0}};
        
        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            
            for (int[] dir : dirs) {
                int x = curr[0] + dir[0];
                int y = curr[1] + dir[1];
                
                if (x >= 0 && x < rows && y >= 0 && y < cols && grid[x][y] == '1') {
                    queue.offer(new int[]{x, y});
                    grid[x][y] = '0';
                }
            }
        }
    }
    
    // Shortest Path in Binary Matrix
    public int shortestPathBinaryMatrix(int[][] grid) {
        if (grid[0][0] == 1) return -1;
        
        int n = grid.length;
        Queue<int[]> queue = new LinkedList<>();
        queue.offer(new int[]{0, 0, 1}); // row, col, distance
        grid[0][0] = 1;
        
        int[][] dirs = {{0,1},{0,-1},{1,0},{-1,0},{1,1},{1,-1},{-1,1},{-1,-1}};
        
        while (!queue.isEmpty()) {
            int[] curr = queue.poll();
            int row = curr[0], col = curr[1], dist = curr[2];
            
            if (row == n - 1 && col == n - 1) return dist;
            
            for (int[] dir : dirs) {
                int x = row + dir[0];
                int y = col + dir[1];
                
                if (x >= 0 && x < n && y >= 0 && y < n && grid[x][y] == 0) {
                    queue.offer(new int[]{x, y, dist + 1});
                    grid[x][y] = 1;
                }
            }
        }
        return -1;
    }
}
```

### 3. DFS (Depth-First Search)

**When to use**: Connected components, cycles, paths

```java
class DFS {
    // Basic DFS (Recursive)
    public void dfs(int[][] graph, int node, boolean[] visited) {
        visited[node] = true;
        System.out.print(node + " ");
        
        for (int neighbor : graph[node]) {
            if (!visited[neighbor]) {
                dfs(graph, neighbor, visited);
            }
        }
    }
    
    // DFS Iterative
    public void dfsIterative(int[][] graph, int start) {
        int n = graph.length;
        boolean[] visited = new boolean[n];
        Stack<Integer> stack = new Stack<>();
        
        stack.push(start);
        
        while (!stack.isEmpty()) {
            int node = stack.pop();
            
            if (visited[node]) continue;
            visited[node] = true;
            System.out.print(node + " ");
            
            for (int neighbor : graph[node]) {
                if (!visited[neighbor]) {
                    stack.push(neighbor);
                }
            }
        }
    }
    
    // Clone Graph
    public Node cloneGraph(Node node) {
        if (node == null) return null;
        
        Map<Node, Node> map = new HashMap<>();
        return dfsClone(node, map);
    }
    
    private Node dfsClone(Node node, Map<Node, Node> map) {
        if (map.containsKey(node)) return map.get(node);
        
        Node clone = new Node(node.val);
        map.put(node, clone);
        
        for (Node neighbor : node.neighbors) {
            clone.neighbors.add(dfsClone(neighbor, map));
        }
        
        return clone;
    }
    
    // Course Schedule (Cycle Detection)
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        for (int i = 0; i < numCourses; i++) {
            graph.add(new ArrayList<>());
        }
        
        for (int[] pre : prerequisites) {
            graph.get(pre[1]).add(pre[0]);
        }
        
        int[] state = new int[numCourses]; // 0: unvisited, 1: visiting, 2: visited
        
        for (int i = 0; i < numCourses; i++) {
            if (hasCycle(graph, i, state)) {
                return false;
            }
        }
        return true;
    }
    
    private boolean hasCycle(List<List<Integer>> graph, int node, int[] state) {
        if (state[node] == 1) return true;  // Cycle detected
        if (state[node] == 2) return false; // Already processed
        
        state[node] = 1; // Mark as visiting
        
        for (int neighbor : graph.get(node)) {
            if (hasCycle(graph, neighbor, state)) {
                return true;
            }
        }
        
        state[node] = 2; // Mark as visited
        return false;
    }
}
```

### 4. Union-Find (Disjoint Set Union)

**When to use**: Connected components, cycle detection in undirected graphs

```java
class UnionFind {
    private int[] parent;
    private int[] rank;
    
    public UnionFind(int n) {
        parent = new int[n];
        rank = new int[n];
        for (int i = 0; i < n; i++) {
            parent[i] = i;
            rank[i] = 1;
        }
    }
    
    // Find with path compression
    public int find(int x) {
        if (parent[x] != x) {
            parent[x] = find(parent[x]); // Path compression
        }
        return parent[x];
    }
    
    // Union by rank
    public boolean union(int x, int y) {
        int rootX = find(x);
        int rootY = find(y);
        
        if (rootX == rootY) return false; // Already connected
        
        if (rank[rootX] < rank[rootY]) {
            parent[rootX] = rootY;
        } else if (rank[rootX] > rank[rootY]) {
            parent[rootY] = rootX;
        } else {
            parent[rootY] = rootX;
            rank[rootX]++;
        }
        return true;
    }
    
    // Number of Connected Components
    public int countComponents(int n, int[][] edges) {
        UnionFind uf = new UnionFind(n);
        int components = n;
        
        for (int[] edge : edges) {
            if (uf.union(edge[0], edge[1])) {
                components--;
            }
        }
        return components;
    }
    
    // Redundant Connection (Find cycle edge)
    public int[] findRedundantConnection(int[][] edges) {
        int n = edges.length;
        UnionFind uf = new UnionFind(n + 1);
        
        for (int[] edge : edges) {
            if (!uf.union(edge[0], edge[1])) {
                return edge; // This edge creates a cycle
            }
        }
        return new int[]{};
    }
}
```

### 5. Topological Sort

**When to use**: Dependency resolution, ordering tasks

```java
class TopologicalSort {
    // Kahn's Algorithm (BFS-based)
    public int[] findOrder(int numCourses, int[][] prerequisites) {
        List<List<Integer>> graph = new ArrayList<>();
        int[] indegree = new int[numCourses];
        
        for (int i = 0; i < numCourses; i++) {
            graph.add(new ArrayList<>());
        }
        
        for (int[] pre : prerequisites) {
            graph.get(pre[1]).add(pre[0]);
            indegree[pre[0]]++;
        }
        
        Queue<Integer> queue = new LinkedList<>();
        for (int i = 0; i < numCourses; i++) {
            if (indegree[i] == 0) {
                queue.offer(i);
            }
        }
        
        int[] result = new int[numCourses];
        int index = 0;
        
        while (!queue.isEmpty()) {
            int course = queue.poll();
            result[index++] = course;
            
            for (int next : graph.get(course)) {
                indegree[next]--;
                if (indegree[next] == 0) {
                    queue.offer(next);
                }
            }
        }
        
        return index == numCourses ? result : new int[]{};
    }
    
    // DFS-based Topological Sort
    public List<Integer> topologicalSortDFS(int n, List<List<Integer>> graph) {
        boolean[] visited = new boolean[n];
        Stack<Integer> stack = new Stack<>();
        
        for (int i = 0; i < n; i++) {
            if (!visited[i]) {
                dfsTopSort(i, graph, visited, stack);
            }
        }
        
        List<Integer> result = new ArrayList<>();
        while (!stack.isEmpty()) {
            result.add(stack.pop());
        }
        return result;
    }
    
    private void dfsTopSort(int node, List<List<Integer>> graph, 
                            boolean[] visited, Stack<Integer> stack) {
        visited[node] = true;
        
        for (int neighbor : graph.get(node)) {
            if (!visited[neighbor]) {
                dfsTopSort(neighbor, graph, visited, stack);
            }
        }
        
        stack.push(node);
    }
}
```

### 6. Dijkstra's Algorithm (Shortest Path - Weighted)

**When to use**: Weighted shortest path, non-negative weights

```java
class Dijkstra {
    // Network Delay Time
    public int networkDelayTime(int[][] times, int n, int k) {
        // Build graph
        Map<Integer, List<int[]>> graph = new HashMap<>();
        for (int[] time : times) {
            graph.putIfAbsent(time[0], new ArrayList<>());
            graph.get(time[0]).add(new int[]{time[1], time[2]}); // neighbor, weight
        }
        
        // Dijkstra's algorithm
        PriorityQueue<int[]> pq = new PriorityQueue<>((a, b) -> a[1] - b[1]); // node, distance
        pq.offer(new int[]{k, 0});
        
        Map<Integer, Integer> dist = new HashMap<>();
        
        while (!pq.isEmpty()) {
            int[] curr = pq.poll();
            int node = curr[0], time = curr[1];
            
            if (dist.containsKey(node)) continue;
            dist.put(node, time);
            
            if (graph.containsKey(node)) {
                for (int[] neighbor : graph.get(node)) {
                    int nextNode = neighbor[0], nextTime = neighbor[1];
                    if (!dist.containsKey(nextNode)) {
                        pq.offer(new int[]{nextNode, time + nextTime});
                    }
                }
            }
        }
        
        if (dist.size() != n) return -1;
        
        int maxTime = 0;
        for (int time : dist.values()) {
            maxTime = Math.max(maxTime, time);
        }
        return maxTime;
    }
}
```

## 📝 LeetCode Problems

### BFS (Shortest Path - Unweighted)
1. [Number of Islands](https://leetcode.com/problems/number-of-islands/) - Medium
2. [Rotting Oranges](https://leetcode.com/problems/rotting-oranges/) - Medium
3. [Word Ladder](https://leetcode.com/problems/word-ladder/) - Hard
4. [Shortest Path in Binary Matrix](https://leetcode.com/problems/shortest-path-in-binary-matrix/) - Medium
5. [01 Matrix](https://leetcode.com/problems/01-matrix/) - Medium

### DFS (Graph Traversal)
1. [Clone Graph](https://leetcode.com/problems/clone-graph/) - Medium
2. [Pacific Atlantic Water Flow](https://leetcode.com/problems/pacific-atlantic-water-flow/) - Medium
3. [Surrounded Regions](https://leetcode.com/problems/surrounded-regions/) - Medium
4. [Course Schedule](https://leetcode.com/problems/course-schedule/) - Medium

### Union-Find
1. [Number of Connected Components in an Undirected Graph](https://leetcode.com/problems/number-of-connected-components-in-an-undirected-graph/) - Medium
2. [Redundant Connection](https://leetcode.com/problems/redundant-connection/) - Medium
3. [Accounts Merge](https://leetcode.com/problems/accounts-merge/) - Medium
4. [Number of Provinces](https://leetcode.com/problems/number-of-provinces/) - Medium

### Topological Sort
1. [Course Schedule](https://leetcode.com/problems/course-schedule/) - Medium
2. [Course Schedule II](https://leetcode.com/problems/course-schedule-ii/) - Medium
3. [Alien Dictionary](https://leetcode.com/problems/alien-dictionary/) - Hard
4. [Minimum Height Trees](https://leetcode.com/problems/minimum-height-trees/) - Medium

### Dijkstra & Shortest Path
1. [Network Delay Time](https://leetcode.com/problems/network-delay-time/) - Medium
2. [Path with Maximum Probability](https://leetcode.com/problems/path-with-maximum-probability/) - Medium
3. [Cheapest Flights Within K Stops](https://leetcode.com/problems/cheapest-flights-within-k-stops/) - Medium

---

# 7. DYNAMIC PROGRAMMING

## 📚 Basic Terminology

- **Dynamic Programming (DP)**: Solving problems by breaking into subproblems and storing results
- **Memoization**: Top-down approach (recursion + cache)
- **Tabulation**: Bottom-up approach (iterative)
- **State**: Variables that define a subproblem
- **Transition**: How to compute current state from previous states
- **Base Case**: Simplest subproblem with known solution
- **Optimal Substructure**: Optimal solution contains optimal solutions to subproblems
- **Overlapping Subproblems**: Same subproblems solved multiple times

## 🔧 Major Algorithms with Java Code

### 1. 1D DP (Linear)

**When to use**: Single sequence problems

```java
class LinearDP {
    // Climbing Stairs
    public int climbStairs(int n) {
        if (n <= 2) return n;
        
        int[] dp = new int[n + 1];
        dp[1] = 1;
        dp[2] = 2;
        
        for (int i = 3; i <= n; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[n];
    }
    
    // Space Optimized
    public int climbStairsOptimized(int n) {
        if (n <= 2) return n;
        
        int prev2 = 1, prev1 = 2;
        for (int i = 3; i <= n; i++) {
            int curr = prev1 + prev2;
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }
    
    // House Robber
    public int rob(int[] nums) {
        if (nums.length == 0) return 0;
        if (nums.length == 1) return nums[0];
        
        int prev2 = 0, prev1 = 0;
        
        for (int num : nums) {
            int curr = Math.max(prev1, prev2 + num);
            prev2 = prev1;
            prev1 = curr;
        }
        return prev1;
    }
    
    // Longest Increasing Subsequence
    public int lengthOfLIS(int[] nums) {
        int[] dp = new int[nums.length];
        Arrays.fill(dp, 1);
        int maxLen = 1;
        
        for (int i = 1; i < nums.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) {
                    dp[i] = Math.max(dp[i], dp[j] + 1);
                }
            }
            maxLen = Math.max(maxLen, dp[i]);
        }
        return maxLen;
    }
    
    // Maximum Product Subarray
    public int maxProduct(int[] nums) {
        int maxSoFar = nums[0];
        int maxEndingHere = nums[0];
        int minEndingHere = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            int temp = maxEndingHere;
            maxEndingHere = Math.max(nums[i], 
                Math.max(maxEndingHere * nums[i], minEndingHere * nums[i]));
            minEndingHere = Math.min(nums[i], 
                Math.min(temp * nums[i], minEndingHere * nums[i]));
            maxSoFar = Math.max(maxSoFar, maxEndingHere);
        }
        return maxSoFar;
    }
}
```

### 2. 2D DP (Grid/Matrix)

**When to use**: Two sequences, grid problems

```java
class GridDP {
    // Unique Paths
    public int uniquePaths(int m, int n) {
        int[][] dp = new int[m][n];
        
        for (int i = 0; i < m; i++) dp[i][0] = 1;
        for (int j = 0; j < n; j++) dp[0][j] = 1;
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = dp[i - 1][j] + dp[i][j - 1];
            }
        }
        return dp[m - 1][n - 1];
    }
    
    // Minimum Path Sum
    public int minPathSum(int[][] grid) {
        int m = grid.length, n = grid[0].length;
        int[][] dp = new int[m][n];
        
        dp[0][0] = grid[0][0];
        
        for (int i = 1; i < m; i++) {
            dp[i][0] = dp[i - 1][0] + grid[i][0];
        }
        for (int j = 1; j < n; j++) {
            dp[0][j] = dp[0][j - 1] + grid[0][j];
        }
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                dp[i][j] = Math.min(dp[i - 1][j], dp[i][j - 1]) + grid[i][j];
            }
        }
        return dp[m - 1][n - 1];
    }
    
    // Longest Common Subsequence
    public int longestCommonSubsequence(String text1, String text2) {
        int m = text1.length(), n = text2.length();
        int[][] dp = new int[m + 1][n + 1];
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + 1;
                } else {
                    dp[i][j] = Math.max(dp[i - 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[m][n];
    }
    
    // Edit Distance
    public int minDistance(String word1, String word2) {
        int m = word1.length(), n = word2.length();
        int[][] dp = new int[m + 1][n + 1];
        
        for (int i = 0; i <= m; i++) dp[i][0] = i;
        for (int j = 0; j <= n; j++) dp[0][j] = j;
        
        for (int i = 1; i <= m; i++) {
            for (int j = 1; j <= n; j++) {
                if (word1.charAt(i - 1) == word2.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1];
                } else {
                    dp[i][j] = 1 + Math.min(dp[i - 1][j - 1], 
                        Math.min(dp[i - 1][j], dp[i][j - 1]));
                }
            }
        }
        return dp[m][n];
    }
}
```

### 3. Knapsack Problems

**When to use**: Subset selection, optimization

```java
class Knapsack {
    // 0/1 Knapsack
    public int knapsack(int[] weights, int[] values, int capacity) {
        int n = weights.length;
        int[][] dp = new int[n + 1][capacity + 1];
        
        for (int i = 1; i <= n; i++) {
            for (int w = 1; w <= capacity; w++) {
                if (weights[i - 1] <= w) {
                    dp[i][w] = Math.max(dp[i - 1][w], 
                        values[i - 1] + dp[i - 1][w - weights[i - 1]]);
                } else {
                    dp[i][w] = dp[i - 1][w];
                }
            }
        }
        return dp[n][capacity];
    }
    
    // Partition Equal Subset Sum
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int num : nums) sum += num;
        
        if (sum % 2 != 0) return false;
        int target = sum / 2;
        
        boolean[] dp = new boolean[target + 1];
        dp[0] = true;
        
        for (int num : nums) {
            for (int j = target; j >= num; j--) {
                dp[j] = dp[j] || dp[j - num];
            }
        }
        return dp[target];
    }
    
    // Coin Change
    public int coinChange(int[] coins, int amount) {
        int[] dp = new int[amount + 1];
        Arrays.fill(dp, amount + 1);
        dp[0] = 0;
        
        for (int i = 1; i <= amount; i++) {
            for (int coin : coins) {
                if (coin <= i) {
                    dp[i] = Math.min(dp[i], dp[i - coin] + 1);
                }
            }
        }
        return dp[amount] > amount ? -1 : dp[amount];
    }
    
    // Coin Change 2 (Number of ways)
    public int change(int amount, int[] coins) {
        int[] dp = new int[amount + 1];
        dp[0] = 1;
        
        for (int coin : coins) {
            for (int i = coin; i <= amount; i++) {
                dp[i] += dp[i - coin];
            }
        }
        return dp[amount];
    }
}
```

### 4. DP on Strings

**When to use**: String matching, transformations

```java
class StringDP {
    // Longest Palindromic Substring
    public String longestPalindrome(String s) {
        int n = s.length();
        boolean[][] dp = new boolean[n][n];
        int start = 0, maxLen = 1;
        
        // All single characters are palindromes
        for (int i = 0; i < n; i++) {
            dp[i][i] = true;
        }
        
        // Check for length 2
        for (int i = 0; i < n - 1; i++) {
            if (s.charAt(i) == s.charAt(i + 1)) {
                dp[i][i + 1] = true;
                start = i;
                maxLen = 2;
            }
        }
        
        // Check for lengths 3 to n
        for (int len = 3; len <= n; len++) {
            for (int i = 0; i < n - len + 1; i++) {
                int j = i + len - 1;
                
                if (s.charAt(i) == s.charAt(j) && dp[i + 1][j - 1]) {
                    dp[i][j] = true;
                    start = i;
                    maxLen = len;
                }
            }
        }
        
        return s.substring(start, start + maxLen);
    }
    
    // Word Break
    public boolean wordBreak(String s, List<String> wordDict) {
        Set<String> dict = new HashSet<>(wordDict);
        int n = s.length();
        boolean[] dp = new boolean[n + 1];
        dp[0] = true;
        
        for (int i = 1; i <= n; i++) {
            for (int j = 0; j < i; j++) {
                if (dp[j] && dict.contains(s.substring(j, i))) {
                    dp[i] = true;
                    break;
                }
            }
        }
        return dp[n];
    }
    
    // Longest Palindromic Subsequence
    public int longestPalindromeSubseq(String s) {
        int n = s.length();
        int[][] dp = new int[n][n];
        
        for (int i = n - 1; i >= 0; i--) {
            dp[i][i] = 1;
            for (int j = i + 1; j < n; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], dp[i][j - 1]);
                }
            }
        }
        return dp[0][n - 1];
    }
}
```

## 📝 LeetCode Problems

### 1D DP
1. [Climbing Stairs](https://leetcode.com/problems/climbing-stairs/) - Easy
2. [House Robber](https://leetcode.com/problems/house-robber/) - Medium
3. [House Robber II](https://leetcode.com/problems/house-robber-ii/) - Medium
4. [Decode Ways](https://leetcode.com/problems/decode-ways/) - Medium
5. [Maximum Product Subarray](https://leetcode.com/problems/maximum-product-subarray/) - Medium
6. [Longest Increasing Subsequence](https://leetcode.com/problems/longest-increasing-subsequence/) - Medium

### 2D DP
1. [Unique Paths](https://leetcode.com/problems/unique-paths/) - Medium
2. [Unique Paths II](https://leetcode.com/problems/unique-paths-ii/) - Medium
3. [Minimum Path Sum](https://leetcode.com/problems/minimum-path-sum/) - Medium
4. [Longest Common Subsequence](https://leetcode.com/problems/longest-common-subsequence/) - Medium
5. [Edit Distance](https://leetcode.com/problems/edit-distance/) - Hard

### Knapsack
1. [Partition Equal Subset Sum](https://leetcode.com/problems/partition-equal-subset-sum/) - Medium
2. [Target Sum](https://leetcode.com/problems/target-sum/) - Medium
3. [Coin Change](https://leetcode.com/problems/coin-change/) - Medium
4. [Coin Change 2](https://leetcode.com/problems/coin-change-2/) - Medium

### DP on Strings
1. [Longest Palindromic Substring](https://leetcode.com/problems/longest-palindromic-substring/) - Medium
2. [Longest Palindromic Subsequence](https://leetcode.com/problems/longest-palindromic-subsequence/) - Medium
3. [Palindromic Substrings](https://leetcode.com/problems/palindromic-substrings/) - Medium
4. [Word Break](https://leetcode.com/problems/word-break/) - Medium

---

# 8. ADVANCED TOPICS

## Backtracking

### When to use
Generating combinations, permutations, subsets

```java
class Backtracking {
    // Subsets
    public List<List<Integer>> subsets(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrack(result, new ArrayList<>(), nums, 0);
        return result;
    }
    
    private void backtrack(List<List<Integer>> result, List<Integer> temp, 
                          int[] nums, int start) {
        result.add(new ArrayList<>(temp));
        
        for (int i = start; i < nums.length; i++) {
            temp.add(nums[i]);
            backtrack(result, temp, nums, i + 1);
            temp.remove(temp.size() - 1);
        }
    }
    
    // Permutations
    public List<List<Integer>> permute(int[] nums) {
        List<List<Integer>> result = new ArrayList<>();
        backtrackPermute(result, new ArrayList<>(), nums);
        return result;
    }
    
    private void backtrackPermute(List<List<Integer>> result, 
                                 List<Integer> temp, int[] nums) {
        if (temp.size() == nums.length) {
            result.add(new ArrayList<>(temp));
            return;
        }
        
        for (int num : nums) {
            if (temp.contains(num)) continue;
            temp.add(num);
            backtrackPermute(result, temp, nums);
            temp.remove(temp.size() - 1);
        }
    }
    
    // N-Queens
    public List<List<String>> solveNQueens(int n) {
        List<List<String>> result = new ArrayList<>();
        char[][] board = new char[n][n];
        for (int i = 0; i < n; i++) {
            Arrays.fill(board[i], '.');
        }
        backtrackQueens(result, board, 0);
        return result;
    }
    
    private void backtrackQueens(List<List<String>> result, char[][] board, int row) {
        if (row == board.length) {
            result.add(construct(board));
            return;
        }
        
        for (int col = 0; col < board.length; col++) {
            if (isValid(board, row, col)) {
                board[row][col] = 'Q';
                backtrackQueens(result, board, row + 1);
                board[row][col] = '.';
            }
        }
    }
    
    private boolean isValid(char[][] board, int row, int col) {
        for (int i = 0; i < row; i++) {
            if (board[i][col] == 'Q') return false;
        }
        
        for (int i = row - 1, j = col - 1; i >= 0 && j >= 0; i--, j--) {
            if (board[i][j] == 'Q') return false;
        }
        
        for (int i = row - 1, j = col + 1; i >= 0 && j < board.length; i--, j++) {
            if (board[i][j] == 'Q') return false;
        }
        
        return true;
    }
    
    private List<String> construct(char[][] board) {
        List<String> result = new ArrayList<>();
        for (char[] row : board) {
            result.add(new String(row));
        }
        return result;
    }
}
```

## Trie (Prefix Tree)

### When to use
Prefix matching, word problems

```java
class Trie {
    private class TrieNode {
        Map<Character, TrieNode> children;
        boolean isEndOfWord;
        
        public TrieNode() {
            children = new HashMap<>();
            isEndOfWord = false;
        }
    }
    
    private TrieNode root;
    
    public Trie() {
        root = new TrieNode();
    }
    
    public void insert(String word) {
        TrieNode curr = root;
        for (char c : word.toCharArray()) {
            curr.children.putIfAbsent(c, new TrieNode());
            curr = curr.children.get(c);
        }
        curr.isEndOfWord = true;
    }
    
    public boolean search(String word) {
        TrieNode curr = root;
        for (char c : word.toCharArray()) {
            if (!curr.children.containsKey(c)) {
                return false;
            }
            curr = curr.children.get(c);
        }
        return curr.isEndOfWord;
    }
    
    public boolean startsWith(String prefix) {
        TrieNode curr = root;
        for (char c : prefix.toCharArray()) {
            if (!curr.children.containsKey(c)) {
                return false;
            }
            curr = curr.children.get(c);
        }
        return true;
    }
}
```

## Bit Manipulation

```java
class BitManipulation {
    // Single Number
    public int singleNumber(int[] nums) {
        int result = 0;
        for (int num : nums) {
            result ^= num;
        }
        return result;
    }
    
    // Number of 1 Bits
    public int hammingWeight(int n) {
        int count = 0;
        while (n != 0) {
            count++;
            n &= (n - 1); // Remove rightmost 1
        }
        return count;
    }
    
    // Power of Two
    public boolean isPowerOfTwo(int n) {
        return n > 0 && (n & (n - 1)) == 0;
    }
    
    // Counting Bits
    public int[] countBits(int n) {
        int[] result = new int[n + 1];
        for (int i = 1; i <= n; i++) {
            result[i] = result[i >> 1] + (i & 1);
        }
        return result;
    }
}
```

## 📝 LeetCode Problems

### Backtracking
1. [Subsets](https://leetcode.com/problems/subsets/) - Medium
2. [Subsets II](https://leetcode.com/problems/subsets-ii/) - Medium
3. [Permutations](https://leetcode.com/problems/permutations/) - Medium
4. [Permutations II](https://leetcode.com/problems/permutations-ii/) - Medium
5. [Combination Sum](https://leetcode.com/problems/combination-sum/) - Medium
6. [N-Queens](https://leetcode.com/problems/n-queens/) - Hard
7. [Word Search](https://leetcode.com/problems/word-search/) - Medium

### Trie
1. [Implement Trie](https://leetcode.com/problems/implement-trie-prefix-tree/) - Medium
2. [Word Search II](https://leetcode.com/problems/word-search-ii/) - Hard
3. [Design Add and Search Words Data Structure](https://leetcode.com/problems/design-add-and-search-words-data-structure/) - Medium

### Bit Manipulation
1. [Single Number](https://leetcode.com/problems/single-number/) - Easy
2. [Single Number II](https://leetcode.com/problems/single-number-ii/) - Medium
3. [Number of 1 Bits](https://leetcode.com/problems/number-of-1-bits/) - Easy
4. [Counting Bits](https://leetcode.com/problems/counting-bits/) - Easy
5. [Missing Number](https://leetcode.com/problems/missing-number/) - Easy

---

Perfect 👍
Here are the **official LeetCode links** for **all 50 problems**, organized **phase-wise**, exactly matching your list.

I’ll reference **LeetCode** once and then give you **clean clickable links**.

---

# 🟢 Phase 1: The Foundations (Arrays / Hashing)

1. **Two Sum**
   [https://leetcode.com/problems/two-sum/](https://leetcode.com/problems/two-sum/)

2. **Valid Anagram**
   [https://leetcode.com/problems/valid-anagram/](https://leetcode.com/problems/valid-anagram/)

3. **Contains Duplicate**
   [https://leetcode.com/problems/contains-duplicate/](https://leetcode.com/problems/contains-duplicate/)

4. **Group Anagrams**
   [https://leetcode.com/problems/group-anagrams/](https://leetcode.com/problems/group-anagrams/)

5. **Top K Frequent Elements**
   [https://leetcode.com/problems/top-k-frequent-elements/](https://leetcode.com/problems/top-k-frequent-elements/)

6. **Product of Array Except Self**
   [https://leetcode.com/problems/product-of-array-except-self/](https://leetcode.com/problems/product-of-array-except-self/)

7. **Valid Sudoku**
   [https://leetcode.com/problems/valid-sudoku/](https://leetcode.com/problems/valid-sudoku/)

8. **Longest Consecutive Sequence**
   [https://leetcode.com/problems/longest-consecutive-sequence/](https://leetcode.com/problems/longest-consecutive-sequence/)

9. **Two Sum II – Input Array Is Sorted**
   [https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/](https://leetcode.com/problems/two-sum-ii-input-array-is-sorted/)

10. **3Sum**
    [https://leetcode.com/problems/3sum/](https://leetcode.com/problems/3sum/)

---

# 🟡 Phase 2: Pointers & Sliding Window

11. **Valid Palindrome**
    [https://leetcode.com/problems/valid-palindrome/](https://leetcode.com/problems/valid-palindrome/)

12. **Container With Most Water**
    [https://leetcode.com/problems/container-with-most-water/](https://leetcode.com/problems/container-with-most-water/)

13. **Best Time to Buy and Sell Stock**
    [https://leetcode.com/problems/best-time-to-buy-and-sell-stock/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock/)

14. **Longest Substring Without Repeating Characters**
    [https://leetcode.com/problems/longest-substring-without-repeating-characters/](https://leetcode.com/problems/longest-substring-without-repeating-characters/)

15. **Longest Repeating Character Replacement**
    [https://leetcode.com/problems/longest-repeating-character-replacement/](https://leetcode.com/problems/longest-repeating-character-replacement/)

16. **Minimum Window Substring**
    [https://leetcode.com/problems/minimum-window-substring/](https://leetcode.com/problems/minimum-window-substring/)

17. **Sliding Window Maximum**
    [https://leetcode.com/problems/sliding-window-maximum/](https://leetcode.com/problems/sliding-window-maximum/)

18. **Trapping Rain Water**
    [https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/)

---

# 🔵 Phase 3: Structure & Logic (Stacks / Lists / Trees)

19. **Valid Parentheses**
    [https://leetcode.com/problems/valid-parentheses/](https://leetcode.com/problems/valid-parentheses/)

20. **Min Stack**
    [https://leetcode.com/problems/min-stack/](https://leetcode.com/problems/min-stack/)

21. **Generate Parentheses**
    [https://leetcode.com/problems/generate-parentheses/](https://leetcode.com/problems/generate-parentheses/)

22. **Daily Temperatures**
    [https://leetcode.com/problems/daily-temperatures/](https://leetcode.com/problems/daily-temperatures/)

23. **Reverse Linked List**
    [https://leetcode.com/problems/reverse-linked-list/](https://leetcode.com/problems/reverse-linked-list/)

24. **Merge Two Sorted Lists**
    [https://leetcode.com/problems/merge-two-sorted-lists/](https://leetcode.com/problems/merge-two-sorted-lists/)

25. **Reorder List**
    [https://leetcode.com/problems/reorder-list/](https://leetcode.com/problems/reorder-list/)

26. **Remove Nth Node From End of List**
    [https://leetcode.com/problems/remove-nth-node-from-end-of-list/](https://leetcode.com/problems/remove-nth-node-from-end-of-list/)

27. **Linked List Cycle**
    [https://leetcode.com/problems/linked-list-cycle/](https://leetcode.com/problems/linked-list-cycle/)

28. **Invert Binary Tree**
    [https://leetcode.com/problems/invert-binary-tree/](https://leetcode.com/problems/invert-binary-tree/)

29. **Maximum Depth of Binary Tree**
    [https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

30. **Diameter of Binary Tree**
    [https://leetcode.com/problems/diameter-of-binary-tree/](https://leetcode.com/problems/diameter-of-binary-tree/)

31. **Balanced Binary Tree**
    [https://leetcode.com/problems/balanced-binary-tree/](https://leetcode.com/problems/balanced-binary-tree/)

32. **Binary Tree Level Order Traversal**
    [https://leetcode.com/problems/binary-tree-level-order-traversal/](https://leetcode.com/problems/binary-tree-level-order-traversal/)

33. **Validate Binary Search Tree**
    [https://leetcode.com/problems/validate-binary-search-tree/](https://leetcode.com/problems/validate-binary-search-tree/)

34. **Kth Smallest Element in a BST**
    [https://leetcode.com/problems/kth-smallest-element-in-a-bst/](https://leetcode.com/problems/kth-smallest-element-in-a-bst/)

35. **Implement Trie (Prefix Tree)**
    [https://leetcode.com/problems/implement-trie-prefix-tree/](https://leetcode.com/problems/implement-trie-prefix-tree/)

36. **Word Search II**
    [https://leetcode.com/problems/word-search-ii/](https://leetcode.com/problems/word-search-ii/)

---

# 🔴 Phase 4: The Offer Makers (Graphs / DP / Design)

37. **Number of Islands**
    [https://leetcode.com/problems/number-of-islands/](https://leetcode.com/problems/number-of-islands/)

38. **Clone Graph**
    [https://leetcode.com/problems/clone-graph/](https://leetcode.com/problems/clone-graph/)

39. **Max Area of Island**
    [https://leetcode.com/problems/max-area-of-island/](https://leetcode.com/problems/max-area-of-island/)

40. **Pacific Atlantic Water Flow**
    [https://leetcode.com/problems/pacific-atlantic-water-flow/](https://leetcode.com/problems/pacific-atlantic-water-flow/)

41. **Course Schedule**
    [https://leetcode.com/problems/course-schedule/](https://leetcode.com/problems/course-schedule/)

42. **Alien Dictionary**
    [https://leetcode.com/problems/alien-dictionary/](https://leetcode.com/problems/alien-dictionary/)

43. **Combination Sum**
    [https://leetcode.com/problems/combination-sum/](https://leetcode.com/problems/combination-sum/)

44. **Merge k Sorted Lists**
    [https://leetcode.com/problems/merge-k-sorted-lists/](https://leetcode.com/problems/merge-k-sorted-lists/)

45. **Find Median from Data Stream**
    [https://leetcode.com/problems/find-median-from-data-stream/](https://leetcode.com/problems/find-median-from-data-stream/)

46. **Climbing Stairs**
    [https://leetcode.com/problems/climbing-stairs/](https://leetcode.com/problems/climbing-stairs/)

47. **Coin Change**
    [https://leetcode.com/problems/coin-change/](https://leetcode.com/problems/coin-change/)

48. **Longest Increasing Subsequence**
    [https://leetcode.com/problems/longest-increasing-subsequence/](https://leetcode.com/problems/longest-increasing-subsequence/)

49. **Edit Distance**
    [https://leetcode.com/problems/edit-distance/](https://leetcode.com/problems/edit-distance/)

50. **LRU Cache**
    [https://leetcode.com/problems/lru-cache/](https://leetcode.com/problems/lru-cache/)


## Study Tips

### Pattern Recognition
- Before coding, identify which pattern applies
- Ask yourself: "What's the constraint?" "What's being optimized?"
- Look for keywords: "subarray" → sliding window, "sorted" → binary search, "path" → DFS/BFS

### Time Management
- Spend 5-10 min understanding the problem
- Spend 30-45 min per problem initially
- Look at hints if stuck for > 30 min
- Always review optimal solutions

### Practice Strategy
1. **Week 1-2**: Arrays & Strings (Foundation)
2. **Week 3-4**: Linked Lists, Stacks, Queues
3. **Week 5-6**: Trees & BST
4. **Week 7-8**: Graphs & BFS/DFS
5. **Week 9-10**: Dynamic Programming
6. **Week 11-12**: Advanced Topics & Review

### Consistency
- 2-3 problems daily > 20 problems once a week
- Review solved problems weekly
- Participate in weekly contests
- Do mock interviews on Pramp/interviewing.io

---

## Complexity Cheat Sheet

| Data Structure | Access | Search | Insert | Delete | Space |
|---------------|--------|--------|--------|--------|-------|
| Array | O(1) | O(n) | O(n) | O(n) | O(n) |
| Linked List | O(n) | O(n) | O(1) | O(1) | O(n) |
| Stack | O(n) | O(n) | O(1) | O(1) | O(n) |
| Queue | O(n) | O(n) | O(1) | O(1) | O(n) |
| Hash Table | - | O(1) | O(1) | O(1) | O(n) |
| BST | O(log n) | O(log n) | O(log n) | O(log n) | O(n) |
| Heap | - | O(n) | O(log n) | O(log n) | O(n) |

| Algorithm | Best | Average | Worst | Space |
|-----------|------|---------|-------|-------|
| Quick Sort | O(n log n) | O(n log n) | O(n²) | O(log n) |
| Merge Sort | O(n log n) | O(n log n) | O(n log n) | O(n) |
| Heap Sort | O(n log n) | O(n log n) | O(n log n) | O(1) |
| Binary Search | O(1) | O(log n) | O(log n) | O(1) |
| DFS | O(V+E) | O(V+E) | O(V+E) | O(V) |
| BFS | O(V+E) | O(V+E) | O(V+E) | O(V) |

---

## Additional Resources

- **LeetCode Patterns**: https://leetcode.com/explore/
- **NeetCode Roadmap**: https://neetcode.io/roadmap
- **Blind 75**: Essential problems list
- **AlgoExpert**: Structured learning path
- **Cracking the Coding Interview**: Classic book
- **Elements of Programming Interviews**: Advanced prep

---

*Good luck with your DSA journey! Remember: consistency and pattern recognition are key to mastering these concepts.*
