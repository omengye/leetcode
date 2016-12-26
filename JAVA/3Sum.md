Given an array S of n integers, are there elements a, b, c in S such that a + b + c = 0? Find all unique triplets in the array which gives the sum of zero.

Note: The solution set must not contain duplicate triplets.

```
For example, given array S = [-1, 0, 1, 2, -1, -4],

A solution set is:
[
  [-1, 0, 1],
  [-1, -1, 2]
]
```

```
import java.util.*;

/**
 * Created by omengye on 2016/12/24.
 */
public class ThreeSum {

    public List<List<Integer>> threeSum(int[] nums) {

        Arrays.sort(nums);

        List<List<Integer>> res = new ArrayList<>();

        int n = nums.length;

        for (int i=0; i<n-2; i++) {
            //skip the duplication
            if (i>0 && nums[i-1]==nums[i]) {
                continue;
            }
            int a = nums[i];
            int low = i+1;
            int high = n-1;
            while ( low < high ) {
                int b = nums[low];
                int c = nums[high];
                if (a+b+c == 0) {
                    //got the soultion
                    List<Integer> v = new ArrayList<>();
                    v.add(a);
                    v.add(b);
                    v.add(c);
                    res.add(v);
                    // Continue search for all triplet combinations summing to zero.
                    //skip the duplication
                    while(low<n-1 && nums[low]==nums[low+1]) {
                        low++;
                    }
                    while(high>0 && nums[high]==nums[high-1]) {
                        high--;
                    }
                    low++;
                    high--;
                } else if (a+b+c > 0) {
                    //skip the duplication
                    while(high>0 && nums[high]==nums[high-1]) {
                        high--;
                    }
                    high--;
                } else{
                    //skip the duplication
                    while(low<n-1 && nums[low]==nums[low+1]) {
                        low++;
                    }
                    low++;
                }
            }
        }
        return res;
    }

    public static void main(String[] args) {
        ThreeSum solution = new ThreeSum();

        int[] nums = new int[]{-12,4,12,-4,3,2,-3,14,-14,3,-12,-7,2,14,-11,3,-6,
          6,4,-2,-7,8,8,10,1,3,10,-9,8,5,11,3,-6,0,6,12,-13,-11,12,10,-1,-15,-12,
          -14,6,-15,-3,-14,6,8,-9,6,1,7,1,10,-5,-4,-14,-12,-14,4,-2,-5,-11,-10,
          -7,14,-6,12,1,8,4,5,1,-13,-3,5,10,10,-1,-13,1,-15,9,-13,2,11,-2,3,6,
          -9,14,-11,1,11,-6,1,10,3,-10,-4,-12,9,8,-3,12,12,-13,7,7,1,1,-7,-6,-13,
          -13,11,13,-8};

        System.out.println(solution.threeSum(nums));

    }
}

```

难度:

M

思路:

先排序，然后固定一个数i，接着把另外两个数的位置定在i+1和n-1上。分别左移和右移另外两个数，
当移动过程中遇到相同数字时因为最后的集合不包括重复则跳过
