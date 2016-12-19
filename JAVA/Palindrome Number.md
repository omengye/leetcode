Determine whether an integer is a palindrome. Do this without extra space.

click to show spoilers.

Some hints:

Could negative integers be palindromes? (ie, -1)

If you are thinking of converting the integer to string, note the restriction of using extra space.

You could also try reversing an integer. However, if you have solved the problem "Reverse Integer", you know that the reversed integer might overflow. How would you handle such case?

```
/**
 * Created by omengye on 2016/12/19.
 */
public class PalindromeNumber {


    public boolean isPalindrome(int x) {
        if (x<0) {
            return false;
        }
        if (0<=x && x<=9) {
            return true;
        }

        String str = ""+x;
        int mid = str.length()/2-1;
        int iter = mid + 1;

        if (str.length() % 2 != 0) {
            ++iter;
        }

        while (mid>=0 && iter< str.length() && str.charAt(mid) == str.charAt(iter)) {
            --mid;
            ++iter;
        }

        if (mid < 0) {
            return true;
        }
        else {
            return false;
        }

    }

    public static void main(String[] args) {
        PalindromeNumber solution = new PalindromeNumber();

        int[] s = new int[]{12,121,55,313};

        for (int i : s) {
            System.out.println(solution.isPalindrome(i));
        }

    }

}

```

难度：

E

思路：

注意判断对称轴是在哪里就行了
