Reverse digits of an integer.

Example1: x = 123, return 321

Example2: x = -123, return -321

```
import java.math.BigInteger;

/**
 * Created by omengye on 2016/12/18.
 */
public class ReverseInteger {

    public int reverse(int x) {
        boolean isNegative = false;

        if (x<0) {
            isNegative = true;
        }

        String xS = ""+x;

        String res = "";
        for (int j=xS.length()-1; j>=0; --j) {
            if (j==0 && xS.charAt(j) == '-') {
                continue;
            }
            res += xS.charAt(j);
        }

        if ((!isNegative && Double.parseDouble(res) > Integer.MAX_VALUE)
                || (isNegative && Double.parseDouble(res) -1 > Integer.MAX_VALUE)) {
            return 0;
        }

        if (isNegative) {
            return 0 - Integer.parseInt(res);
        } else {
            return Integer.parseInt(res);
        }

    }

    public static void main(String[] args) {
        ReverseInteger solution = new ReverseInteger();

        int[] rs = new int[]{123, -123, 1534236469, -2147483648};

        for (int r : rs) {
            System.out.println(solution.reverse(r));
        }

    }
}
```

难度：

E

思考：

记得需要处理整形越界的问题，肯定有更好的方法
