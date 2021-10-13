#  剑指offer

## 09

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

