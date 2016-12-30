Given an array S of n integers, are there elements a, b, c, and d in S such that
a + b + c + d = target? Find all unique quadruplets in the array which gives the sum of target.

Note: The solution set must not contain duplicate quadruplets.

```
For example, given array S = [1, 0, -1, 0, -2, 2], and target = 0.

A solution set is:
[
  [-1,  0, 0, 1],
  [-2, -1, 1, 2],
  [-2,  0, 0, 2]
]
```

```
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * Created by omengye on 2016/12/28.
 */
public class FourSum {

    public List<List<Integer>> fourSum(int[] nums, int target) {

        List<List<Integer>> res = new ArrayList<>();
        if (nums.length < 4) {
            return res;
        }

        Arrays.sort(nums);

        int oldValue = nums[0];
        int listSize = nums.length-3;
        for (int i=0; i<listSize; ) {
            int first = nums[i];
            if (i>0 && first == oldValue) {
                i=i+1;
                continue;
            }
            i=i+1;
            List<List<Integer>> l = threeSum(nums, i, first, target);
            res.addAll(l);

            oldValue = first;
        }

        return res;
    }

    public List<List<Integer>> threeSum(int[] nums, int startIdx, int first, int target) {

        List<List<Integer>> res = new ArrayList<>();

        boolean isStart = true;
        int n = nums.length;

        for (int i=startIdx; i<n-2; i++) {
            //skip the duplication
            if (!isStart && nums[i-1] == nums[i]) {
                continue;
            }
            isStart = false;
            int a = nums[i];
            int low = i+1;
            int high = n-1;
            while ( low < high ) {
                int b = nums[low];
                int c = nums[high];
                if (a+b+c + first == target) {
                    //got the soultion
                    List<Integer> v = new ArrayList<>();
                    v.add(first);
                    v.add(a);
                    v.add(b);
                    v.add(c);
                    res.add(v);
                    // Continue search for all triplet combinations summing to zero.
                    //skip the duplication
                    while(low<n-1 && nums[low] == nums[low+1]) {
                        low++;
                    }
                    while(high>0 && nums[high]==nums[high-1]) {
                        high--;
                    }
                    low++;
                    high--;
                } else if (a+b+c + first > target) {
                    //skip the duplication
                    while(high>0 && nums[high]==nums[high-1]) {
                        high--;
                    }
                    high--;
                } else{
                    //skip the duplication
                    while(low<n-1 && nums[low] == nums[low+1]) {
                        low++;
                    }
                    low++;
                }
            }
        }
        return res;
    }



    public static void main(String[] args) {
        FourSum solution = new FourSum();

        int[] S = new int[]{0,0,0,0};//{1, 0, -1, 0, -2, 2};
        int target = 0;

        List<List<Integer>> res = solution.fourSum(S, target);

    }
}

```

难度：

M

思路：

固定一个数字，然后将剩下的数字按照3Sum的方式进行处理，当固定的数字在循环的过程中有重复时，
避免重复计算而跳过。需要注意的一点是，尽量不去操作数组的增加和删除，只记录数组的位置，这样
能避免leetcode超时。
