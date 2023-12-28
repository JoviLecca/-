# 力扣977. 有序数组的平方

存在负数的升序数组，则可能存在负数的平方结果大于正数的平方结果的情况。采用双指针的作用在于，对数组前后两端的平方值进行比较，选出更大的一个，接着从后向前填充到一个新的数组中。

```c#
public class Solution {
    public int[] SortedSquares(int[] nums) {
        int[] rst = new int[nums.Length];// 构建与原数组同样大小的新数组
        int head = 0;// 头指针
        int tail = nums.Length - 1;// 尾指针
        int putInIndex = nums.Length - 1;// 需要填入新数组的位置的索引值
        while(head <= tail){ //可能存在头指针与尾指针重合的情况
            // 如果头指针处的数小于等于尾指针，则将尾指针的数填入新数组，尾指针向前移动
            if ((nums[head] * nums[head]) <= (nums[tail] * nums[tail])){
                rst[putInIndex] = (nums[tail] * nums[tail]);
                tail--;
            }
            // 否则将头指针的数填入新数组，头指针向后移动
            else{
                rst[putInIndex] = (nums[head] * nums[head]);
                head++;
            }
            // 每填入一个新数，索引向前移动一位，直到填入完毕
            putInIndex--;
        }
        // 返回结果
        return rst;
    }
}
```



# 力扣209. 长度最小的子数组

 滑动窗口本质上也是双指针，但它的作用在于利用双指针形成一个区间，滑动指针的位置就能控制区间的大小以及区间数值总和，可以简化一些原本需要双循环来解决的问题。

```c#
public class Solution {
    public int MinSubArrayLen(int target, int[] nums) {
        int result = int.MaxValue; // 设结果为该类型最大值，方便与后续窗口区间总和相比较
        int sum = 0; // 窗口区间总和变量
        int start = 0; // 起始指针
        for (int end = 0; end < nums.Length; end++) {// 终点指针
            sum += nums[end]; //将每个终点指针经过的值相加
            while (sum >= target) { // 而只要总和超过了目标值
                result = Math.Min(result, end - start + 1); // 与现有结果进行比较，如果新子数组长度比现有结果小，则更新结果变量为新子数组长度
                sum -= nums[start]; // 同时减去起始指针出的数值，向后移动起始指针，如果总和值仍超过目标值，则循环处理，直到不符合循环条件
                start++;
            }
        }
        // 如果result仍是最大值，则证明没有符合目标值的子数组，返回0，否则返回子数组长度
        return result == int.MaxValue ? 0 : result;
    }
}
```



# 力扣59. 螺旋矩阵 II

这题没什么好说的，主要还是看能否掌握对区间边界的处理和for循环的运用，不能有默认循环次数起始值为0的印象。

```c#
public class Solution {
    public int[][] GenerateMatrix(int n) {
        int[][] rst = new int[n][];
        for (int i = 0; i < n; i++) {
            rst[i] = new int[n];
        }

        int start = 0;
        int end = n - 1;
        int count = 1;

        while (count < n * n) {
            for (int i = start; i < end; i++) {
                rst[start][i] = count;
                count++;
            }
            for (int i = start; i < end; i++) {
                rst[i][end] = count;
                count++;
            }
            for (int i = end; i > start; i--) {
                rst[end][i] = count;
                count++;
            }
            for (int i = end; i > start; i--) {
                rst[i][start] = count;
                count++;
            }
            start++;
            end--;
        }

        if (n%2 == 1) {
            rst[n / 2][n / 2] = n * n;
        }

        return rst;
    }
}
```



# 数组总结

数组的特点在于连续且无法删除，如果要对数组进行修改，只能覆盖。

对于数组相关的题型，常用**二分法、双指针、滑动窗口**等方法思路。

区间的定义就是不变量，那么在循环中坚持根据查找区间的定义来做边界处理，就是**循环不变量规则**。