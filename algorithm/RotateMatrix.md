# Rotate Matrix

首先要说这道题非常有趣，是一个绵里藏针的题目，一般来讲，看到这道题目我们自然会想到利用模拟的办法去做，也就是一步一步去模拟替换的过程，一开始我的代码确实是这样写的：


```C++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) {
        int begin = 0;
        int end   = matrix.size()-1;
        cout<<begin<<' '<<end<<endl;
        while(begin < end){
            int length = end - begin;
            for(int i = 0; i < length; i++){
                int tmp = matrix[begin + i][begin];
                //bottom->left
                cout<<matrix[begin + i][begin] <<' '<< matrix[end][begin + i]<<endl;
                matrix[begin + i][begin] = matrix[end][begin + i];
                //right->bottom
                cout<<matrix[end][begin + i] <<' '<< matrix[end - i][end]<<endl;
                matrix[end][begin + i] = matrix[end - i][end];
                //top->right
                cout<<matrix[end - i][end] <<' '<< matrix[begin][end - i]<<endl;
                matrix[end - i][end] = matrix[begin][end - i];
                //left->top
                cout<<matrix[begin][end - i] <<' '<< tmp<<endl;
                matrix[begin][end - i] = tmp;
            }
            begin++;
            end--;
        }
    }
};
```

但是这个写法只是个中等速度，为啥呢？看到了更快的写法是：

```C++
class Solution {
public:
    void rotate(vector<vector<int>>& matrix) 
    {
        if (matrix.size() < 2)
            return;
        
        reverse(matrix.begin(), matrix.end());
        
        for (int i = 0; i < matrix.size(); i++)
            for (int j = 0; j < i; j++)
                swap(matrix[i][j], matrix[j][i]);
    }
};
```

这里面说明了一个什么数学原理呢？说明了顺时针旋转90度相当于倒换行之后转置，看上去确实很神奇，可以自行推演，表明这个过程是对的，那举一反三来看，如果逆时针旋转90度的话，相当于每一行内部元素逆序后转置，旋转180度呢？相当于按行逆序后，每一行继续逆序，然后转置。在这里面需要总结出来的一个哲学就是说转置这个东西，对于矩阵运算的含义究竟是什么。我们知道在计算机内部，我们存储一个矩阵的时候是按照行存储的，那么如果需要对矩阵进行按列操作的时候就需要矩阵转置登场了。在这道题目中，我们发现旋转90度之后的矩阵按照行已经是不连续的了，但是按照列确实有序的，这就说明我们需要引入矩阵转置来简化这个旋转操作。【画一个图来验证是最好的】