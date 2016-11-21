##LeetCode 刷题记录 Easy（一）

##什么是LeetCode？

作为一名本科应届生来讲，面试重点会看重基础，个人的基础算法数据结构，以及语言基础，某些公司还会问一些TCP/IP、组成原理方面的知识。

当然有些人可能会想，做算法，实际工作的时候用得不多呀，但是你也得想，一些语言已经帮我们包装好了一些数据结构和一些模板，比如一些STL等。但是选择合适的数据结构以及算法可以将效率提升很多，选择一个O(n)的算法就是不如选择一个O(lgn)的算法效率高，当然也需要考虑空间复杂度，看情况去用空间换取时间。

![](http://i.imgur.com/EGuCv5n.jpg)

尽早的去准备这些东西，可以使得在校招或者面试当中占有一定的优势，毕竟面试里面除了项目的部分，大部分是算法和语言基础，以Java举例，面试官很有可能去问HashMap的底层实现，如果只是知道HashMap的一些peek方法、pop方法、push方法等，而不清楚其底层实现的话，面试就很有可能挂掉。而其底层实现又和数据结构有关，主要和数组和链表有关系，所以问完底层实现以后，可以展开问一些数据结构。然后这一部分基础过关以后，面试官可能会问一些DP，DFS等的一些套路。当这些都满意了以后，就会从一些方向去问一些问题了，比如投的后端就会问一些HTTP协议，投的NLP会问一些基础，投的Java很可能会问GC。

而我们又如何去准备这些基础呢，毕竟大部分大学里并没有ACM的氛围，没有相关的集训队，也没有相关的实验室。而且大部分大学只是去浅显地教数据结构，而不去进行大量的实践，这就会导致学了之后，过段时间就会忘却。所幸的是，ACM有一些OJ平台，可以不断的去练习，实践，国内也有几个出名的OJ，比如POJ，HDOJ，并且好大学都有自己的OJ。而这些OJ对于没有基础的人来说，还是刷起来有点吃力。所以LeetCode定位在为面试者准备的一个OJ，涵盖了一些基础算法，常见数据结构等，应该没有网络流等的一些东西。并且我们可以在这个平台上学到一些东西，一些对边界值的思考，多写一些TestCase。

##Two Sum

题目：

Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

    Given nums = [2, 7, 11, 15], target = 9,
    
    Because nums[0] + nums[1] = 2 + 7 = 9,
    return [0, 1].

题解：

通过阅读题目，就是从给定的一个数组里，然后找出可以相加成target这个数的数组下标。

新手很容易写出以下的代码：
```java
	public class Solution {
	    public int[] twoSum(int[] nums, int target) {
	        int[] result = new int[2];
	        for(int i = 0; i < nums.length; i++) {
	            for(int j = i + 1; j < nums.length; j++) {
	                if (nums[i]+nums[j] == target) {
	                    result[0] = i;
	                    result[1] = j;
	                }
	            }
	        }
	        return result;
	    }
	}
```
当提交之后发现，会提示**Your runtime beats 10.32% of java submissions.**，为什么只打败那么多呢，思考后会发现，双重for循环以后，会导致时间复杂度的增加。并且好像以前有人说过，能不用双重循环就不用双重循环。

那么这道题是否有其他的思路呢？通过Java的一些集合类可以达到相同的效果吗？

我们是否可以用HashMap去存放相关的数字，去省去一层for循环，也就是以下的代码。
```java
	public class Solution {
	    public int[] twoSum(int[] nums, int target) {
	        HashMap<Integer, Integer> map = new HashMap();
	        for(int i = 0; i < nums.length; i++) {
	            if(map.get(nums[i])!=null) {
	                int[] result = {i, map.get(nums[i])};
	                return result;
	            }
	            map.put(target - nums[i], i);
	        }
	        int[] result = null;
	        return result;
	    }
	}
```
至此，提交后会得到**Your runtime beats 95.65% of java submissions.**。

![](http://i.imgur.com/V8mvmfE.png)

并且我们可以从上图可以看到，C的效率是最高的，其次是C++和Golang，而像swift，JavaScript这些语言的效率是比较低的。

##Reverse Integer

Reverse digits of an integer.

Example1: x = 123, return 321
Example2: x = -123, return -321

这道题要逆转数字，属于数学题，有了思路以后不难。主要就是一直取10的余数然后循环。

主要里面好多TestCase需要考虑临界情况，这就使得想起了是用防御式编程呢还是契约式编程。不过实际情况里还是需要考虑到各种情况。

```java
	public class Solution {
	    public int reverse(int x) {
	        int result = 0;
	        while(true) {
				if (result > (Integer.MAX_VALUE / 10)){
					return 0;
				}
				
				if (result < (-Integer.MIN_VALUE / 10)){
					return 0;
				}
	            result = result * 10 + x % 10;
	            x = x / 10;
	            if (x ==0)
	            {
	                break;
	            }
	        }
	        return result;
	    }
	}
```
##Palindrome Number

Determine whether an integer is a palindrome. Do this without extra space.

这道题，可以通过除法和取余，去对比数字，可以通过逆转数字，然后去判断与原数字是否相同。其负数的情况是直接返回false的。

当然还有很多优化空间或者还有其他的思路。

```java
	public class Solution {
	    public boolean isPalindrome(int x) {
	        int result = 0;
	        int before = x;
	        if (x > 0 && x < 10) {
	            return true;
	        }
	        if (x < 0) {
	            return false;
	        }
	        while(true) {
				if (result > (Integer.MAX_VALUE / 10)){
					return false;
				}
	            result = result * 10 + x % 10;
	            x = x / 10;
	            if (x ==0)
	            {
	                break;
	            }
	        }
	        return before == result;
	    }
	}
```
##Roman to Integer

罗马数字转数字

Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

很常见的逻辑题。

```java
	public class Solution {
	    public int romanToInt(String s) {
	        int result = 0;
	        if (s.length() == 0) {
	            return result;
	        }
	        
	        for (int i = s.length() - 1; i >= 0; i--) {
	            char c = s.charAt(i);
	            switch(c) {
	                case 'I':
	                    if (result >= 5) {
	                        result = result - 1;
	                    } else {
	                        result = result + 1;
	                    }
	                    break;
	                case 'V':
	                    result = result + 5;
	                    break;
	                case 'X':
	                    if (result >= 50) {
	                        result = result - 10;
	                    } else {
	                        result = result + 10;
	                    }
	                    break;
	                case 'L':
	                    result = result + 50;
	                    break;
	                case 'C':
	                    if (result >= 500) {
	                        result = result - 100;
	                    } else {
	                        result = result + 100;
	                    }
	                    break;
	                case 'D':
	                    result = result + 500;
	                    break;
	                case 'M':
	                    result = result + 1000;
	                    break;
	                default:
	            }
	        }
	        
	        return result;
	    }
	}
```

主要是注意右加左减，在较大的罗马数字的右边记上较小的罗马数字，表示大数字加小数字。

##Longest Common Prefix

Write a function to find the longest common prefix string amongst an array of strings.

输出字符串的公共前缀，字符串的一些操作。其中可以学到了Java如何跳出多重循环。并且也可以学到length()和length的区别。

```java
	public class Solution {
	    public String longestCommonPrefix(String[] strs) {
	        if (strs == null || strs.length == 0) {
	            return "";
	        }
	        
	        if (strs.length == 1) {
	            return strs[0];
	        }
	        
	        String result = "";
	        Label:
	            for(int j = 0; j < strs[0].length(); j++) {
	                for(int i = 1; i < strs.length; i++) {
	                    if (j >= strs[i].length() || strs[i].charAt(j) != strs[0].charAt(j)) {
	                        break Label;
	                    }
	                }
	                result = result + strs[0].charAt(j);
	            }
	        
	        return result;
	    }
	}
```

##后记

当然代码有点渣，接触leetcode不久，希望可以一块在其中成长，下次写一些链表，栈，字符串等的一些解题记录。并且还有可以从中思考的地方，比如Palindrome Number一题的其他解法，逆转数字可能会导致overflow，这些就留下，需要各位继续思考。以及Longest Common Prefix这题，也可以第0个字符串和其他字符串逐个求前缀。
