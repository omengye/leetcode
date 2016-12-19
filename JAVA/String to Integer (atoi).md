Implement atoi to convert a string to an integer.

Hint: Carefully consider all possible input cases. If you want a challenge, please do not see below and ask yourself what are the possible input cases.

Notes: It is intended for this problem to be specified vaguely (ie, no given input specs). You are responsible to gather all the input requirements up front.

```
import java.util.regex.Matcher;
import java.util.regex.Pattern;

/**
 * Created by omengye on 2016/12/19.
 */

// atoi
public class StringtoInteger {
    public int myAtoi(String str) {
        if (str.length()==0) {
            return 0;
        }

        str = str.trim();

        String rs = "([\\+-]?\\d+)";
        Pattern reg = Pattern.compile(rs);
        Matcher m = reg.matcher(str);
        if (m.find()) {
            str = m.group(0);
        }
        else {
            return 0;
        }

        double ds = Double.parseDouble(str);

        return (int)ds;
    }


    public static void main(String[] args) {

        String[] strs = new String[]{"123", "-123", "", "+-2", "    010", "   -04f", "  -0012a42", "-2147483648", "      -11919730356x", " b11228552307"};

        for (String str :strs) {
            StringtoInteger solution = new StringtoInteger();
            System.out.println(solution.myAtoi(str));
        }

    }

}

```

难度：

E

思考：

用正则的话虽然能够通过测试，不过在leetcode上耗时长

主要考虑以下几点

  1. 去掉空格
  2. 正负号
  3. 是否有除0-9外的其他字符
  4. 是否越界
