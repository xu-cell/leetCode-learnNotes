#  剑指offer

- 剑指offer09

用两个栈实现一个队列。队列的声明如下，请实现它的两个函数 appendTail 和 deleteHead ，分别完成在队列尾部插入整数和在队列头部删除整数的功能。(若队列中没有元素，deleteHead 操作返回 -1 )

 示例 1：

输入：
["CQueue","appendTail","deleteHead","deleteHead"]
[[],[3],[],[]]
输出：[null,null,3,-1]
示例 2：

输入：
["CQueue","deleteHead","appendTail","appendTail","deleteHead","deleteHead"]
[[],[],[5],[2],[],[]]
输出：[null,-1,null,null,5,2]
提示：

1 <= values <= 10000
最多会对 appendTail、deleteHead 进行 10000 次调用

思路：题目意思是用两个栈实现对列，栈只有先进后出，队列先进先出，所以我们设置一个栈为存储栈，插入元素的时候，将元素push进去，设置一个输出栈，当需要输出元素的时候先把存储栈的元素插入到输出栈中，然后再输出。这样就实现了先进先出.

  题目的输出输入，当插入元素的时候什么也不发生，那么就返回空，弹出元素，就需要返回弹出元素的值。如果输出栈中没有元素那么就返回-1。题目中的CQueue为创建一个CQueue对象，然后什么也不干，就返回空。



```c++
class CQueue {
public:
    //插入元素，我们就把元素插入存储栈中，如果要输出就把存储栈中的元素存入输出栈中，再输出，这样就能达到队列的先进先出的效果
    stack<int>stin;//用于存储的栈
    stack<int>stout;//用于输出的栈
    CQueue() {
      
    }
    
    void appendTail(int value) {
        stin.push(value);
        return;
    }
    
    int deleteHead() {
       if(stout.empty()){
             while(!stin.empty()){
                 stout.push(stin.top());
                 stin.pop();
             }
       }
       if(stout.empty()){
           return -1; 
       }
       int result=stout.top();
           stout.pop();
           return result;
       
    }
};
```
- 剑指offer 10-1斐波那契数列
```c++
//我采用的是动态规划的方法 时间复杂度O(n),空间复杂度O(n)
//注意每一次运算都要除摸运算
class Solution {
public:
    int fib(int n) {
     int MOD=1000000007;
     if(n<2){
         return n;
     }
     vector<int>dp(n+1);
     dp[0]=0;
     dp[1]=1;
     for(int i=2;i<=n;i++){
         dp[i]=(dp[i-1]+dp[i-2])%MOD;
        
     }
     return dp[n];
    }
};
```
- 剑指offer 10-Ⅱ-青蛙跳台阶

 一只青蛙一次可以跳上1级台阶，也可以跳上2级台阶。求该青蛙跳上一个 n 级的台阶总共有多少种跳法。

答案需要取模 1e9+7（1000000007），如计算初始结果为：1000000008，请返回 1。

示例 1：

输入：n = 2
输出：2
示例 2：

输入：n = 7
输出：21
示例 3：

输入：n = 0
输出：1
提示：

0 <= n <= 100
```c++
//我采用的还是动态规划解题
class Solution {
public:
    int numWays(int n) {
      int Mod=1000000007;
      if(n<2)return 1;
      if(n==2)return 2;
      vector<int>dp(n+1);
      dp[0]=1;
      dp[1]=1;
      for(int i=2;i<=n;i++){
          dp[i]=(dp[i-1]+dp[i-2])%Mod;
      }
      return dp[n];
    }
};
```

- 剑指offer03-数组中的重复数

在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字重复了，也不知道每个数字重复了几次。请找出数组中任意一个重复的数字。
示例 1：
输入：
[2, 3, 1, 0, 2, 5, 3]
输出：2 或 3 
 
限制：2 <= n <= 100000
思路：
```c++
//首先这道题有3种解法 第一种排序+遍历（时间复杂度为O（n*logn）,空间为O（1）) 第二种为哈希表法，使用哈希表记录出现过的数字，下次再出现就返回这个数字；第三种方法为所谓的字典法（根据题目中的条件所来：在一个长度为 n 的数组 nums 里的所有数字都在 0～n-1 的范围内。像字典一样，一个字符对应着一个位置。他们是一一对应的，我们遍历这个数组，如果nums[i]=i,说明这个位置的数字就是其本来的数字，就继续遍历，如果nums[nums[i]]==nums[i]说明索引位置的数字重复了，否则就交换nums[nums[i]]与nums[i]）
//法三时间复杂读O(n)空间复杂度O(1)
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
       int i=0;
       while(i<nums.size()){
           if(nums[i]==i){
               i++;
               continue;
           }
           if(nums[nums[i]]==nums[i]){
               return nums[i];
           }
           else{
               swap(nums[nums[i]],nums[i]);
           }
       }
       return -1;
    }
};
//法二 时间复杂度O(n) 空间空间复杂度O(n)
class Solution {
public:
    int findRepeatNumber(vector<int>& nums) {
       unordered_map<int,bool>map;
       for(int num:nums){
           if(map[num])return num;
           else map[num]=true;
       }
       return -1;
    }
};
