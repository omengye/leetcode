Given an integer, convert it to a roman numeral.

Input is guaranteed to be within the range from 1 to 3999.


```
/**
 * Created by omengye on 2016/12/21.
 */

import java.util.HashMap;

/**
 *
 基本字符             I V  X  L   C   D   M
 相应的阿拉伯数字表示为 1 5 10 50 100 500 1000
 整数从 1 到 3999.
 */

public class IntegertoRoman {

    public String intToRoman(int num) {

        int max_num = 0; // 最大位

        // 个位
        int num_O = num - num/10 * 10;
        if (num_O>0) {
            max_num = num_O;
        }
        // 十位
        int num_T = (num - num/100 * 100) / 10 * 10;
        if (num_T>0) {
            max_num = num_T;
        }
        // 百位
        int num_H = (num - num/1000 * 1000) / 100 * 100;
        if (num_H>0) {
            max_num = num_H;
        }
        // 千位
        int num_M = num / 1000 * 1000;
        if (num_M>0) {
            max_num = num_M;
        }

        HashMap<Integer, String> roman = genRoman(max_num);

        String res = "";

        int[] nums = new int[]{num_M, num_H, num_T, num_O};

        for (int i : nums) {
            if (i > 0) {
                res += roman.get(i);
            }
        }

        return res;
    }

    public HashMap<Integer, String> genRoman(int max_num) {

        String[] strs = new String[]{"I","V","X","L","C","D","M"};
        int[] vals = new int[]{1,5,10,50,100,500,1000};

        HashMap<Integer, String> map = new HashMap<>();

        int n = 1;
        int iter = 1;
        for (int i=1; i<=max_num; i=i+n) {
            if (iter < strs.length && i == vals[iter]) {
                map.put(i, strs[iter]);
            } else if (iter < strs.length && i == vals[iter] - vals[iter - 1]) {
                map.put(i, strs[iter - 1] + strs[iter]);
            } else if (iter < strs.length && i == vals[iter + 1] - vals[iter - 1]) {
                map.put(i, strs[iter - 1] + strs[iter + 1]);
            } else if (iter < strs.length && i == vals[iter + 1]) {
                map.put(i, strs[iter + 1]);
                n = 10 * n;
                iter = iter + 2;
            } else if (iter < strs.length && i > vals[iter]) {
                String s = "";
                for (int j = 0; j < (i - vals[iter]) / n; ++j) {
                    s += strs[iter - 1];
                }
                map.put(i, strs[iter] + s);
            } else {
                String s = "";
                for (int j = 0; j < i / n; ++j) {
                    s += strs[iter - 1];
                }
                map.put(i, s);
            }
        }

        return map;
    }

    public static void main(String[] args) {
        IntegertoRoman solution = new IntegertoRoman();

        int[] nums = new int[]{3,4,9,10,1437};

        for (int num : nums) {
            System.out.println(solution.intToRoman(num));
        }
    }

}

```

难度：

M

思路：

转换整型为罗马字符
```
基本字符              I V  X  L   C   D   M
相应的阿拉伯数字表示为 1 5 10 50 100 500 1000
```
注意罗马字符4为IV 9为IX
