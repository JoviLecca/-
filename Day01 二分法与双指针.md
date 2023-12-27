# 力扣704. 二分查找

___

二分法算是比较基础的算法了，中学时就有所教授的。

但在编写代码时需要重点关注边界的情况，如果是闭区间，那么在while判断时可以是<=，否则<。

```c#
// 二分查找有序数组，闭区间解法
public int Search (int[] nums, int target) {
    int left = 0; //左区间初始为0
    int right = nums.Length - 1; // 因为是闭区间，所以右区间为 nums.Length - 1，即最大的下标
    while (left <= right) { // 循环查找；因为是闭区间，所以存在left == right的可能性
        int middle = left + (right - left) / 2; // 为了防溢出
        if (nums[middle] > target) { // 如果中位数比目标值大，则目标值在目前中位数的左侧
            right = middle - 1; // 则将右区间调至目前中位数下标的左侧，缩小区间范围，查询左半部分区间
        }
        else if (nums[middle] < target) { // 如果中位数比目标值小，则目标值在目前中位数的右侧
            left = middle + 1; // 则将左区间调至目前中位数下标的右侧，缩小区间范围，查询右半部分区间
        }
        else { // 如果中位数等于目标值
            return middle; // 返回该中位数的下标
        }
    }
    return -1; // 如果上述算法没有找到目标值，则返回-1，判定为未找到
}

// 二分查找有序数组，左开右闭区间解法
public int Search (int[] nums, int target) {
    int left = 0;
    int right = nums.Length;
    while (left < right) {
        int middle = left + (right - left) / 2;
        if (nums[middle] < target) {
            left = middle + 1;
        }
        else if (nums[middle] > target) {
            right = middle;
        }
        else {
            return middle;
        }
    }
    return -1;
}
```



# 力扣27. 移除元素

虽然暴力解是最直观的，但性能不好看（O(n^2)）。双指针还是有些不好理解，希望之后多接触些类似的题目，深入学习下其中的逻辑。

```c#
// 第一种解法，暴力解法，用两个循环来覆盖与目标值相同的数值，得出新的数组
// 时间复杂度为O(n^2)
public int RemoveElement (int[] nums, int val) {
    int size = nums.Length;
    for (int i = 0; i < size; i++) {
        if (nums[i] == val) {
            for (int j = i + 1; j < size; j++) {
                nums[j - 1] = nums[j];
            }
            i--;
            size--;
        }
    }
    return size;
}

// 第二种解法，双指针，用一个快指针和一个慢指针在一个循环内实现两个循环的效果
// 快指针：寻找新数组的元素，新数组就是不含有目标元素的数组
// 慢指针：指向更新了的新数组下标的位置
// 时间复杂度为O(n)
public int RemoveElement (int[] nums, int val) {
    int slowIndex = 0;
    for	(int fastIndex = 0; fastIndex < nums.Length; fastIndex++) {
        if (val != nums[fastIndex]) { // 如果快指针所指到的元素不等于目标值
            // 则说明该元素是新数组的一部分，应当列入新数组
            // 将其划入新数组的下标位置，即慢指针中，并更新慢指针
            nums[slowIndex] = nums[fastIndex];
            slowIndex++;
        }
        // 如果快指针所指到的元素等于目标值，则忽略，不列入新数组
    }
    return slowIndex;
}
```

