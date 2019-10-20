# LeetCode
利用python和C++来刷题

## 两数之和
题目：[给定一个整数数组和一个目标值，找出数组中和为目标值的两个数](https://leetcode-cn.com/problems/two-sum/description/)  
解析：这道题一开始看的时候，有点类似于《剑指offer》的面试题57：和为s的数字。  
这那道题中，数组时排序数组，设置两个指针，分别指向头和尾。  
当两者之和大于s时，把尾指针向前移；当两者之和小于s时，把头指针向后移。  

但这题不是排序数组，是一个普通的序列。  
这里有几种方法，leetcode都有详解。
1. 暴力方法：把target-nums[i]与后面n-i项相比，看是否存在。此时复杂度为O(n^2)
2. 利用哈希表，遍历两次。在第一次迭代中，我们将每个元素的值和它的索引添加到表中。
        然后，在第二次迭代中，我们将检查每个元素所对应的目标元素（target - nums[i]）是否存在于表中。
        注意，该目标元素不能是 nums[i]本身！此时时间复杂度为O(n)，空间复杂度为O(n)
3. 利用哈希表，遍历一次。如果存在两数之和为target的话，数字是成对出现的，只是会有遍历的先后问题。所以我们可以一边
        把target - nums[i]存入哈希表，一边判断num[i]是否已经存在哈希表。此时间复杂度为O(n)，空间复杂度为O(n)。

## 两数相加
题目：[给定两个非空链表来表示两个非负整数。位数按照逆序方式存储，它们的每个节点只存储单个数字。将两数相加返回一个新的链表。](https://leetcode-cn.com/problems/add-two-numbers/description/)  
解析：这道题思路很简单，就是模拟加法的过程，有点类似于归并排序是的merge。  
但写代码的时候可以简化些写法，例如使用p1+p2+carry，而不是先将p1+p2，再判断其进位和余数。  
这样写会让思路更加清晰。  
具体解答https://leetcode-cn.com/problems/add-two-numbers/solution/  
另外，变式是说如果数字是按顺序存储在链表中，例如123：1-2-3，此时要如何相加呢？  
我的想法是，类似于《剑指offer》的反转链表，可以利用辅助空间（两个栈）。

update 2019.1.12  
本题主要考察的两个链表的操作，难点在于，当一个链表遍历完而另外一个链表可以遍历的时候，该如何操作。

##  无重复字符的最长子串
题目：[给定一个字符串，找出不含有重复字符的最长子串的长度。](https://leetcode-cn.com/problems/longest-substring-without-repeating-characters/description/)  
解析：这道题是《剑指offer》的面试题48  
其思路是这样的，利用空间来换取效率，需要一个哈希表，只需要遍历一次字符串。  
如果第i个字符没有出现过，则让curlength加一。  
如果第i个字符出现过，设第i个字符和上一次出现过的距离为d：  
    1. 如果d>curlength，说明第i个字符不在当前子串中，可以curlength加一  
    2. 如果d<=curlength，说明第i个字符在当前子串中，此时让curlength=d  
《剑指offer》上利用了动态规划的想法来讲解，和我的简易思路一致。

另外leetcode上有种“滑动窗口的解法”，其思路是，判断第i个字符是否在[j,i-1]的子串中，如果存在，则滑动窗口变成[i+1,i];
如果不存在，则滑动窗口为[j,i]

update 2019.1.12  
本题可以使用vector来进行查询，建立vector<int> letter(128,-1)，128表示ascii有128个字符（题目没有说只是字母），letter[s[i]]即能查询，挺方便的一个小技巧。

update 2019.2.14  
用上面方法在LEETCODE上跑，竟然不是最快的。首先建立创建一个unorder_set用来存储不重复的字符，每读取到一个字符时，判断是否存在于unorder_set中。如果不存在，则插入；如果存在，则不断删除此字符前的字符，直到unorder_set剩下不重复的字符。  
这种方法也是O(N)，但是其需要不断查找和操作unorder_set，按道理来说，不应该比上面的方法快。
        

## 最长回文子串
题目：[给定一个字符串 s，找到 s 中最长的回文子串。你可以假设 s 的最大长度为1000。](https://leetcode-cn.com/problems/longest-palindromic-substring/description/)  
解析：可以使用中心扩展法，找到一个中心，向两边扩展，当不是回文就退出，当是回文，则继续扩展。  
一个字符串一共有2n-1个中心，分别是n个类似于[aba]这样的字符串，和n-1个类似于[abba]这样的字符串。

update 2019.2.27  
再做一遍，依然没想到这个方法。中心扩展法的时间复杂度是O(n^2)，但网上有种更快的方法，时间复杂度是O(n)，但我没弄懂，等以后再说。

update 2019.9.16  
这次想到中心扩展法了，以后面对对称的问题，可以从中间向两边进行考虑。

## Z字形变换  
题目：[将一个给定字符串根据给定的行数，以从上往下、从左到右进行 Z 字形排列](https://leetcode-cn.com/problems/zigzag-conversion/)  
update 2019.2.27  
这道题，主要考察的是找规律，也就是下标的控制，我自己一开始写的代码比较臃肿，分成首、尾和中部分别控制；网上的方便比较凝练，同一在一个循环解决，i是用于控制每个循环中的下标，j用于控制每个循环。说到底，还是我自己思路不太清晰，没想清楚就动手。  
update 2019.9.17  
这道题，依然没有在限定时间内做出来，说明自己对规律的总结还不到位，能力不足。

## 整数反转
题目：[给出一个 32 位的有符号整数，你需要将这个整数中每位上的数字进行反转。](https://leetcode-cn.com/problems/reverse-integer/)  
update 2019.2.28  
将x取余，得到每位的值，加上res上，再讲x/10。这道题主要考察的应该是越界。  
update 2019.9.18  
本题相对简单，主要就是考察越界情况的判断。

## 字符串转换整数 (atoi)
题目：[请你来实现一个 atoi 函数，使其能将字符串转换成整数。](https://leetcode-cn.com/problems/string-to-integer-atoi/)  
update 2019.2.28  
第二次做这道题的时候，考虑还是不全，没考虑到'+'号，导致出错。而且，往前的写法，将正数和负数分开处理，思路相对更加清晰，值得推荐。

update 2019.9.21  
再次做这道题的时候，依然没有考虑到'+'号的情况。这边写法思路很清晰，把正数和负数统一处理。其实，这道题应该还可以使用[正则表达式来进行解决](https://leetcode-cn.com/problems/string-to-integer-atoi/solution/python-1xing-zheng-ze-biao-da-shi-by-knifezhu/)。

## 回文数
题目：[判断一个整数是否是回文数。回文数是指正序（从左向右）和倒序（从右向左）读都是一样的整数](https://leetcode-cn.com/problems/palindrome-number/)  
update 2019.3.1   
题目要求，不能转换为字符串，只能存储32位的int，说明不能使用更高位数的结构来存储该数字。所以，想到的方法是将该数字进行反转来比较，/10和%10。但是，反转的过程可能会导致越出，因此，我们考虑反转一半的数字，来比较两个数字，x==num||x==num/10。此时，对于特殊情况，我们就需要单独处理，例如负数，10,20等。

update 2019.9.23  
这次想到了翻转一半的数字，但是写法还是过于臃肿，在每次循坏中都进行判断。其实不必要，只要x>翻转的数字，才需要挑出循坏，进行判断。而还有特殊情况没有考虑到，例如只有个位数的情况。

## 盛最多水的容器
题目：[给定 n 个非负整数 a1，a2，...，an，每个数代表坐标中的一个点 (i, ai) 。在坐标内画 n 条垂直线，垂直线 i 的两个端点分别为 (i, ai) 和 (i, 0)。找出其中的两条线，使得它们与 x 轴共同构成的容器可以容纳最多的水](https://leetcode-cn.com/problems/container-with-most-water/)  
update 2019.3.1  
使用两个下标，来计算当前的体积。难的地方在于，如何计算下一次的提及，该移动哪个下标。盛水的提及取决于最短的高，因此，我们移动最短的高的下标，来试探能否得到更大的体积。

update 2019.9.24  
思路很简单，利用双指针即可。

## 整数转罗马数字
题目：[给定一个整数，将其转为罗马数字](https://leetcode-cn.com/problems/integer-to-roman/)  
update 2019.3.1  
第二次做，依然采用建立一个查询表来做，但跑出来的成绩不高。看了别人的方法，采用多个if分支来进行判断，不断减去数值，来叠加数字，这种方法跑出来的成绩较好，省去了一定的空间。  
update 2019.9.25  
这次利用建表，很容易就做出来了。但我在网上看到一种更好的解法。先用字典列出特殊的数字，然后num逐步减最大数字来得到字符，例如1999，先减去1000，得到999，再减去900，得到99，减去90得到9，然后将得到的值与字典对应起来，就是输出结果。

## 罗马数字转整数
题目：[给定一个罗马数字，将其转换成整数](https://leetcode-cn.com/problems/roman-to-integer/)  
update 2019.3.2  
解法一，就是判断第i位与第i+1位的关系，用if-else分支来不断进行累加和改变i。解法二，不需要解法一如此如此麻烦，利用一个flag标志位，如果第i位小于第i+1位，则flag为负，否则为正。当第i位小于第i+1位，res减去该s[i]对应的值。  
update 2019.9.26  
这次解法，还是比较优雅的，先建立一个映射字典，然后从后往前读，判断第i位与第i+1位的大小，若第i位小于第i+1位，则当前结果减去第i位，否则则加上。

## 最长公共前缀
题目：[编写一个函数来查找字符串数组中的最长公共前缀](https://leetcode-cn.com/problems/longest-common-prefix/)  
update 2019.3.3  
解法一，将比较n个字符串转化成比较2个字符串的相比，一个为最长公共前缀和一个为strs[i]。通过不断改变最长公共前缀，来得到最终结果。解法二，由于解法一需要不断改变最长公共前缀的值，增加字符串的操作。因此，我们首先将最长公共前缀定义为strs[0]，然后定义一个变量i，用于表示最长公共前缀应该是从strs[0]到strs[0][i]，在过程中，只需不断缩小i的值即可。  
update 2019.9.27  
之前的解法是，先寻找前两个字符串的最长公共前缀，最终结果一定是这个最长公共前缀的子集，之后将这个最长公共前缀与剩下的字符进行匹对，缩小这个值。而这次我的做法思路比较简单，代码也比较优雅。设置两个指针i和m，指针i循环第1个字符，指针j循环所有字符，判断strs[0][i]是否与strs[j][i]相等，相等则说明属于最长公共前缀，不相等就返回这个结果。

## Ksum总结
Ksum表示k个数进行相加。
1. 2Sum即2个数进行相加，思路一是利用hash表，将target-a作为key，a的index作为value，存入hash中，遍历一次，即可得到答案。思路二是先对数组进行排序，然后设置双指针left和right，当\*left+\*right>0时，移动right，否则移动left。当\*left+\*right==target时，存入list。这种算法记得要处理重复元素。
2. 3Sum可以将其退化成2Sum，枚举数组里面的所有元素，让这个元素等于2Sum中的target。
3. 4Sum退化成3Sum
4. Ksum可以退化成(K-1)sum，此时复杂度是O(N^(K-1))

## 三数之和
题目：[给定一个包含n个整数的数组nums，判断nums中是否存在三个元素a，b，c，使得a+b+c=0？找出所有满足条件且不重复的三元组](https://leetcode-cn.com/problems/3sum/)  
update 2019.3.18  
再次做，依然没有做出来。首先将数组进行排序，然后逐一读取数字，并设置双指针，使得双指针之和等于负数的数字。  
update 2019.9.28  
这次做出来了，但这边界case上卡了很久，没有考虑到全是0的情况，会超时，这里要设置判断条件，跳过重复的数字。主要是这一步卡了很久。

## 最接近的三数之和
题目：[给定一个包括n个整数的数组nums和一个目标值target。找出nums中的三个整数，使得它们的和与target最接近。返回这三个数的和。](https://leetcode-cn.com/problems/3sum-closest/)  
update 2019.3.18  
和上一题的做法类似，设置三个指针。但我以前的做法更加好，会跳过重复的元素。  
update 2019.9.29  
和上道题一样，只是判断条件不一样。

## 电话号码的字母组合
题目：[给定一个仅包含数字2-9的字符串，返回所有它能表示的字母组合。给出数字到字母的映射如下（与电话按键相同）](https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/)  
update 2019.3.18  
方法一：利用递归。当digits读取完后，插入到res中；否则继续递归新的字符。  
方法二：利用队列。可以简化成下面实例。依次将该数字对应的字符插入队列，然后记录此时队列的长度，并弹出元素，该元素与新的数字结合，并插入到队列中。  
[]->[a,b,c]->[ad,ae,af,bd,be,bf,cd,ce,cf]  
update 2019.10.1  
这次试用了递归的做法，若digits为空，说明应该将该结果插入res中，否则，循环读取对应的字符，并进入下一步递归。

## 删除链表的倒数第N个节点
题目：[给定一个链表，删除链表的倒数第 n 个节点，并且返回链表的头结点](https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/)  
update 2019.10.6  
设置双指针，让其中一个指针先走n步，然后两个指针同时前进，直至先走的指针到达链尾，这样，前面的指针刚好指向需要删除的结点的前一个位置。这次主要的错误是，没有考虑到删除链头的情况。

## 有效的括号
题目：[给定一个只包括 '('，')'，'{'，'}'，'\['，'\]' 的字符串，判断字符串是否有效](https://leetcode-cn.com/problems/valid-parentheses/)  
update 2019.10.7  
利用堆这种数据结构。循环遍历字符，遇到左括号，则压入堆中；遇到右括号，判断堆顶的元素能否和右括号匹配，若能则弹出该堆顶元素，否则返回false。最后判断对是否为空，来确定该字符串是否有效。

## 合并两个有序链表
题目：[将两个有序链表合并为一个新的有序链表并返回](https://leetcode-cn.com/problems/merge-two-sorted-lists/)  
update 2019.10.7  
主要考察对指针的操作和思维的清晰程度。比较l1和l2的大小，从而让p指向值小的节点，最后需要判断指针之后到达链表尾部。

## 括号生成
题目：[给出 n 代表生成括号的对数，请你写出一个函数，使其能够生成所有可能的并且有效的括号组合](https://leetcode-cn.com/problems/generate-parentheses/)  
update 2019.10.8  
这道题用回溯法，模仿压入和弹出的行为。但这里还需要控制左括号的数量和右括号的数量，当右括号数量大于坐括号数量时，不进行操作，因此，需要两个指针来进行控制。

## 两两交换链表中的节点
题目：[给定一个链表，两两交换其中相邻的节点，并返回交换后的链表](https://leetcode-cn.com/problems/swap-nodes-in-pairs/)  
update 2019.10.9  
题目要求应该改变节点的连接。这道题应该设置3个指针，分别指向前一个节点，当前节点和下一个节点，这样才能处理好。而我一开始做的时候，只设置了两个指针，导致已经处理过的节点无法与新节点相连。

## 删除排序数组中的重复项
题目：[给定一个排序数组，你需要在原地删除重复出现的元素，使得每个元素只出现一次，返回移除后数组的新长度](https://leetcode-cn.com/problems/remove-duplicates-from-sorted-array/)  
update 2019.10.10  
思路是设置双指针i和j，当nums[i]!=nums[j]时，才进行赋值，直至循环到末尾。但从这题中可以得到例外一种思路，通常都是思考nums[i]==nums[j]，++j；但是如果反过来想，外面设置一个大循环，只有当nums[i]!=nums[j]才赋值，这样的代码会简洁很多。

## 移除元素
题目：[给定一个数组 nums 和一个值 val，你需要原地移除所有数值等于 val 的元素，返回移除后数组的新长度](https://leetcode-cn.com/problems/remove-element/)  
update 2019.10.11  
和上一题一样的思路

## 实现strStr()
题目：[给定一个 haystack 字符串和一个 needle 字符串，在 haystack 字符串中找出 needle 字符串出现的第一个位置 (从0开始)](https://leetcode-cn.com/problems/implement-strstr/)  
update 2019.10.12  
本质上是KMP算法的考察。但你可以用暴力解法，只是复杂度比较高O(MN),而KMP算法的复杂度为O(M+N)。KMP算法可以参考[这篇文章](https://subetter.com/algorithm/kmp-algorithm.html)

## 两数相除
题目：[给定两个整数，被除数 dividend 和除数 divisor](https://leetcode-cn.com/problems/divide-two-integers/)  
这题是真卡了很久，原本以为需要使用位运算，异或，与非之类的，发现都行不通。最后还是暴力解法的优化版本。但这里有个技巧，为了防止越界，都把数字转换为负数进行计算。但这个代码在leetcode上跑不通，因为Leetcode不支持负数移位。

## 下一个序列
题目：[实现获取下一个排列的函数，算法需要将给定数字序列重新排列成字典序中下一个更大的排列](https://leetcode-cn.com/problems/next-permutation/)  
第二次依然没有做出来，方法还是没想到，解法有点巧妙，首先从后往前，找到数组的波峰i，交换位置i与j，此时j的位置应该是波峰右边略比Nums\[i\]大的数字，然后，对波峰右边进行翻转，得到一个递增的数列。

## 搜索旋转排序数组
题目：[假设按照升序排序的数组在预先未知的某个点上进行了旋转。搜索一个给定的目标值，如果数组中存在这个目标值，则返回它的索引，否则返回-1](https://leetcode-cn.com/problems/search-in-rotated-sorted-array/)  
//update 2019.10.15  
第二次做，虽然知道是使用二分查找，但依然没有做出来。首先得先找到旋转点，而旋转点选取最小值比较好，如果选取最大值，比较的话，容易越界。当找到旋转点后，将target与旋转点比较，因为旋转点的左边和右边都是单调的，所以，就可以使用二分查找。

## 在排序数组中查找元素的第一个和最后一个位置
题目：[给定一个按照升序排列的整数数组 nums，和一个目标值 target。找出给定目标值在数组中的开始位置和结束位置](https://leetcode-cn.com/problems/find-first-and-last-position-of-element-in-sorted-array/)  
看到题目要求是logN的复杂度，首先应该想到二分查找。利用二分查找查找重复元素的起点与末尾。但这一次，写的程序依然比较冗余。因为在二分查找的时候，固定思维是判断nums\[mid\]==target，从简洁的代码来看，判断条件不是这个，而是nums\[mid\]>target。说明我对二分理解只是形式上的理解，还未深入。

## 搜索插入位置
题目：[给定一个排序数组和一个目标值，在数组中找到目标值，并返回其索引。如果目标值不存在于数组中，返回它将会被按顺序插入的位置](https://leetcode-cn.com/problems/search-insert-position/)  
update 2019.10.20  
有序数组的搜索，一般都可以用二分查找，注意，需要有序。另外，看了题目的解析，发现自己对二分查找或者说夹逼法不是很了解，可以看看[这篇文章](https://leetcode-cn.com/problems/search-insert-position/solution/te-bie-hao-yong-de-er-fen-cha-fa-fa-mo-ban-python-/)，了解一下夹逼法的模板。夹逼是思想，二分是手段

## 二分查找
题目：[给定一个n个元素有序的（升序）整型数组nums和一个目标值target，写一个函数搜索nums中的target，如果目标值存在返回下标，否则返回-1](https://leetcode-cn.com/problems/binary-search/)  
update 2019.10.20  
练习使用二分查找，这道题注意点是使用unsigner int mid = (left+right)>>1，是为了防止越界。

## x的平方根
题目：[实现int sqrt\(int x\) 函数](https://leetcode-cn.com/problems/sqrtx/)  
update 2019.10.20  
本题有两种方法，一种是二分法，另外一种是牛顿法。这里这次使用了二分法，但这里二分法遇到了问题，就是越界问题，需要使用long long 来处理。同时left+right+1，会先计算right+1,如果right+1是Int的话，就可能会越界，因此，可以将right定义为Long
