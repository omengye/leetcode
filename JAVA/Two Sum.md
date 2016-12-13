Given an array of integers, return indices of the two numbers such that they add up to a specific target.

You may assume that each input would have exactly one solution.

Example:
```
Given nums = [2, 7, 11, 15], target = 9,

Because nums[0] + nums[1] = 2 + 7 = 9,
return [0, 1].
```

UPDATE (2016/2/13):

The return format had been changed to zero-based indices. Please read the above updated description carefully.


```
public int[] twoSum(int[] nums, int target) {
    int[] index = new int[2];
    HashMap<Integer, Integer> hash = new HashMap<>();

    for(int i=0; i<nums.length; ++i) {
        if(hash.get(target-nums[i]) != null) {
            index[0] = hash.get(target-nums[i]);
            index[1] = i;
            return index;
        }
        else
            hash.put(nums[i],  i);
    }

    return null;
}


public static void main(String[] args) {

    TwoSum twosum = new TwoSum();

    int[] nums = {2, 7, 11, 15};
    int target = 9;

    int[] res = twosum.twoSum(nums, target);

    System.out.println(res[0] + " " + res[1]);
}
```
难度：

E

思考：

循环所要查询的数组，把数组中的值与索引对应放到HashMap中，若目标值减去当前数组循环到的值
仍然存在于HashMap中，说明此前保存数组的值与当前数组循环到的值之和为目标值。
