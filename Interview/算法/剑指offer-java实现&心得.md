3.数组中重复的数字
在一个长度为 n 的数组里的所有数字都在 0 到 n-1 的范围内。数组中某些数字是重复的，但不知道有几个数字是重复的，也不知道每个数字重复几次。请找出数组中任意一个重复的数字。
本题思考：

- 考虑非法边界
- 考虑算法的时间复杂度与空间复杂度
个人写法：
```
public class Solution {
    // Parameters:
    //    numbers:     an array of integers
    //    length:      the length of array numbers
    //    duplication: (Output) the duplicated number in the array number,length of duplication array is 1,so using duplication[0] = ? in implementation;
    //                  Here duplication like pointor in C/C++, duplication[0] equal *duplication in C/C++
    //    这里要特别注意~返回任意重复的一个，赋值duplication[0]
    // Return value:       true if the input is valid, and there are some duplications in the array number
    //                     otherwise false
    public boolean duplicate(int numbers[],int length,int [] duplication) {
        // 非法边界处理
        if (numbers == null || length <= 1) {
            return false;
        }
        for (int i = 0; i < length; i++) {
            for (int j = i+1; j < length; j++) {
                if (numbers[i] == numbers[j]) {
                    duplication[0] = numbers[i];
                    return true;
                }
            }
        }
        return false;
    }
}
```
个人思考：

这里本人主要考虑对边界以及无效值处理，比如，数组长度只有1或者没有，那么肯定不存在重复数组。而实际判断实现根据遍历所有数组，以i作为游标，进行往后遍历，查找对应重复数组。
推荐写法：
```
public boolean duplicate(int[] nums, int length, int[] duplication) {
    if (nums == null || length <= 0)
        return false;
    for (int i = 0; i < length; i++) {
        while (nums[i] != i) {
            if (nums[i] == nums[nums[i]]) {
                duplication[0] = nums[i];
                return true;
            }
            swap(nums, i, nums[i]);
        }
    }
    return false;
}
 
private void swap(int[] nums, int i, int j) {
    int t = nums[i];
    nums[i] = nums[j];
    nums[j] = t;
}
```
个人思考2:

这也是本书作者的官方实现方式，对比本人和作者的写法，我们的空间复杂度都是o(1),但是时间复杂度上，本人的写法，算法实现时间复杂度比作者的要高。所以后续学习过程中要考虑时间复杂度与空间复杂度，权衡两者，实现最优解。