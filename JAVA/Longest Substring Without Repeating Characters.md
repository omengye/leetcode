Given a string, find the length of the longest substring without repeating characters.

Examples:
```
Given "abcabcbb", the answer is "abc", which the length is 3.

Given "bbbbb", the answer is "b", with the length of 1.

Given "pwwkew", the answer is "wke", with the length of 3. Note that the
answer must be a substring, "pwke" is a subsequence and not a substring.
```

```
import java.util.HashMap;

/**
 * Created by omengye on 2016/12/14.
 */
public class LongestSubstringWithoutRepeatingCharacters {


    public int lengthOfLongestSubstring(String s) {
        HashMap<Character, Integer> sMap = new HashMap<>();
        int step = 0;
        int interrupt = 0; // 中断位置
        int maxLength = 0;

        for (int i=0; i<s.length(); ++i) {
            char iter = s.charAt(i);
            if (sMap.get(iter) != null) {
                maxLength = Math.max(step, maxLength);
                step = i-Math.max(interrupt,sMap.get(iter)); //回溯
                interrupt = Math.max(interrupt,sMap.get(iter)); //中断字符
            }
            else {
                ++step;
            }
            sMap.put(iter, i);
        }

        maxLength = Math.max(step, maxLength);
        return maxLength;
    }


    public static void main(String[] args) {

        LongestSubstringWithoutRepeatingCharacters solution =
                new LongestSubstringWithoutRepeatingCharacters();

        String[] strs = new String[] {"abcabcbb", "dvdf", "pwwkew", "au",
                "audd", "ddddd", "zwnigfunjwz", "abba"};

        for (String l : strs) {
            System.out.println(solution.lengthOfLongestSubstring(l));
        }
    }

}
```

难度：

M

思考：

遍历字符串，设置两个变量，一个用来计算每次到达重复字符所走过的字符个数；另一个记录中断位置，
用来计算每次到达重复字符时，其所重复的字符的索引。

需要注意的是：

1. 回溯。到达重复的字符时，需要回溯到上一个中断位置，或者是重复字符的索引位置。
2. 中断位置。中断位置只能是随着step所走过的字符，越来越靠后。否则之前重复的字符也被包含进去
