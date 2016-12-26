Given an array S of n integers, find three integers in S such that the sum is
closest to a given number, target. Return the sum of the three integers. You
may assume that each input would have exactly one solution.

    For example, given array S = {-1 2 1 -4}, and target = 1.

    The sum that is closest to the target is 2. (-1 + 2 + 1 = 2).

```
import java.util.ArrayList;
import java.util.Arrays;
import java.util.List;

/**
 * Created by omengye on 2016/12/26.
 */
public class ThreeSumClosestSolution {

    public int threeSumClosest(int[] nums, int target) {
        Arrays.sort(nums);

        int minCount = 0;

        int res = 0;
        int n = nums.length;

        minCount = Math.abs(nums[0]+nums[1]+nums[2] - target);
        res = nums[0]+nums[1]+nums[2];

        if (n==3) {
            return res;
        }

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

                if (low<n && high>i && minCount > Math.abs(a+b+c-target)) {
                    minCount = Math.abs(a+b+c-target);
                    res = a+b+c;
                }

                if (a+b+c - target == 0) {
                    //got the soultion
                    return target;

                } else if (a+b+c - target> 0) {
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
        ThreeSumClosestSolution solution = new ThreeSumClosestSolution();

        int[] nums = new int[]{1,1,1,0};//{-1, 2, 1, -4};

        System.out.println(solution.threeSumClosest(nums, -100));

    }
}

```

难度：

M

思路：

这道题实际上是3Sum的衍生版，这里只需要注意以下3Sum减去Target的绝对值最小就行了
