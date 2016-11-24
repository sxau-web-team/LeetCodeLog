##LeetCode 刷题记录 Easy（二）

##前言

继上次写题解之后，某人又在催稿了，哎，前几天一不小心入了一个小说的坑，感觉自己挖坑自己跳。

题文无关。

##Remove Nth Node From End of List

Given a linked list, remove the nth node from the end of list and return its head.

For example,

	Given linked list: 1->2->3->4->5, and n = 2.
	
	After removing the second node from the end, the linked list becomes 1->2->3->5.

Note:
Given n will always be valid.
Try to do this in one pass.

题目大意：

对于一个给定的指针链表，删除其倒数第N个元素。

这道题用到了双指针法，一种面试题常见的思想方法。这里的指针只是一种索引而已，类似于游标一样。

具体可以访问以下链接：

https://www.google.com.hk/search?q=%E5%8F%8C%E6%8C%87%E9%92%88%E6%B3%95

大家可以想象两只兔子赛跑，一只兔子先走了几步，在这个时候两只兔子开始同时同速度的跑，而跑到终点以后，跑的慢的那只兔子就会被吃掉，噢，不对，跑的慢的那只就在倒数几步的地方，这挺适合那种不知道赛道有多长，然后不能从后遍历的情况。

了解到这个思路了以后，代码就相对来说有逻辑了，用两个指针，一个走比另一个快点，提前几步、

然后注意java里如何去弄指针就可以了。

并且简单给大家提一下白板编程。通常没有受过训练的，写一些算法比较难度高的没有思路，这就往往需要在纸上去画一些图。而有些面试当中，要求面试者在白板上写出代码，就是手写代码，当然一般点的公司让手写个快排，手写个单例。而大公司对这的要求往往比较高。

解法1：

```java
	/**
	 * Definition for singly-linked list.
	 * public class ListNode {
	 *     int val;
	 *     ListNode next;
	 *     ListNode(int x) { val = x; }
	 * }
	 */
	public class Solution {
	    public ListNode removeNthFromEnd(ListNode head, int n) {
	        ListNode slow, fast;
	        ListNode result = new ListNode(0);
	        result.next = head;
	        slow = result;
	        fast = head;
	        for(int i = 0; i < n; i++) {
                fast = fast.next;
	        }
	        
	        while(fast != null) {
	            fast = fast.next;
	            slow = slow.next;
	        }
	      
	        slow.next = slow.next.next;
	    
	        return result.next;
	    }
	}
```

##Valid Parentheses

Given a string containing just the characters '(', ')', '{', '}', '[' and ']', determine if the input string is valid.

The brackets must close in the correct order, "()" and "()[]{}" are all valid but "(]" and "([)]" are not.

很经典的栈的应用，不多说了。。可以进一步熟悉一些方法之类的。以及Stack栈这个东西。

```java
	public class Solution {
	    public boolean isValid(String s) {
	        Stack stack = new Stack();
	        for(int i = 0; i < s.length(); i++) {
	            switch(s.charAt(i)) {
	                case '{':
	                    stack.push('{');
	                    break;
	                case '}':
	                    if (!stack.empty() && (char)stack.peek() == '{') {
	                        stack.pop();
	                    } else {
	                        stack.push('}');
	                    }
	                    break;
	                case '(':
	                    stack.push('(');
	                    break;
	                case ')':
	                    if (!stack.empty() && (char)stack.peek() == '(') {
	                        stack.pop();
	                    } else {
	                        stack.push(')');
	                    }
	                    break;
	                case '[':
	                    stack.push('[');
	                    break;
	                case ']':
	                    if (!stack.empty() && (char)stack.peek() == '[') {
	                        stack.pop();
	                    } else {
	                        stack.push(']');
	                    }
	                    break;
	            }
	        }
	        if (stack.empty()) {
	            return true;
	        } else {
	            return false;
	        }
	    }
	}
```
##Merge Two Sorted Lists

Merge two sorted linked lists and return it as a new list. The new list should be made by splicing together the nodes of the first two lists.

合并两个有序数组。这个在数据结构的课上也讲过类似的，比较经典的链表操作，希望大家可以回去自己练习练习，时间复杂度是O(m+n)，空间复杂度是O(1)，并且也可以用其他语言实现，leetcode支持的语言那么多呢。

当然注意边界条件的判断，这个对于程序思维的培养比较重要。

如果对这解法不熟悉的话，建议还是看《数据结构》吧，把自己基础打好。

```java
	/**
	 * Definition for singly-linked list.
	 * public class ListNode {
	 *     int val;
	 *     ListNode next;
	 *     ListNode(int x) { val = x; }
	 * }
	 */
	public class Solution {
	    public ListNode mergeTwoLists(ListNode l1, ListNode l2) {
	        ListNode result = new ListNode(0);
	        ListNode last = result;
	        while(l1 != null && l2 != null) {
	            if (l1.val <= l2.val) {
	                last.next = l1;
	                l1 = l1.next;
	            } else {
	                last.next = l2;
	                l2 = l2.next;
	            }
	            last = last.next;
	        }
	        
	        if(l1 != null) {
	            last.next = l1;
	        } else {
	            last.next = l2;
	        }
	        
	        return result.next;
	    }
	}
```

##闲言碎语

算法是很重要的，正如张无忌的九阳神功一样，作为一名IT工作者，需要不断磨练自己的内功、不断地锻炼身体，以防哪一天突然加班猝死了呢。

![](http://i.imgur.com/cn9Kdue.jpg)

每天刷点题，迟早要到450的。

希望可以将双指针法熟练应用。

##后记

其实浪子才是重感情的，说着过去的终会过去，可是那年，那景。最后不也成为了天涯沦落客，看着旅途上的人们，有些人充满着喜悦，也有些人在踌躇。最后一场雪，掩盖这一切。

人的一生是短暂的，人的一生就像一场旅程，会有进站口，出站口，总会在那么几个关键的地方停靠。在这场旅途中，会遇到来来往往的各种人。浪子何时不想着，可以有个家，可以不那么漂泊的家，不需要灯红酒绿，只需要有那种气氛足以。

那些名利并不是那么重要，重要的是有一个心爱的人，正如七种武器里的一样，有人看重义，有人看重情，而有人看重名利，最后什么也得不到。所以还是珍惜拥有，无愧于心。。

希望一切平安。

标签：浪子、情怀
