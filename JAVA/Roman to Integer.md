Given a roman numeral, convert it to an integer.

Input is guaranteed to be within the range from 1 to 3999.

```
import java.util.HashMap;

/**
 * Created by omengye on 2016/12/22.
 */
public class RomantoInteger {

    public int romanToInt(String s) {

        if (s.length()==0) {
            return 0;
        }

        char[] strs = new char[]{'I','V','X','L','C','D','M'};
        int[] vals = new int[]{1,5,10,50,100,500,1000};

        HashMap<Character, Integer> map = new HashMap<>();
        for (int i=0; i<strs.length; ++i) {
            map.put(strs[i], vals[i]);
        }

        int res = 0;

        int n=1;
        for (int i=0; i<s.length(); i=i+n) {
            if (i+1<s.length() && map.get(s.charAt(i))<map.get(s.charAt(i+1))) {
                res += map.get(s.charAt(i+1)) - map.get(s.charAt(i));
                n=2;
            }
            else {
                res += map.get(s.charAt(i));
                n=1;
            }
        }

        return res;
    }

    public static void main(String[] args) {

        RomantoInteger solution = new RomantoInteger();

        String[] strs = new String[]{"IX", "XLV", "MMMCMXCIX"};

        for (String str : strs) {
            System.out.println(solution.romanToInt(str));
        }
    }

}
```

难度：

E

思路：

罗马数字，如果左侧比右侧小，则这两个字符是一个整体，代表一个数字，其值用右侧罗马数字减
去左侧计算而得
