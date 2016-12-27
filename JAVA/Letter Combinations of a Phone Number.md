Given a digit string, return all possible letter combinations that the number could represent.

A mapping of digit to letters (just like on the telephone buttons) is given below.

    Input:Digit string "23"
    Output: ["ad", "ae", "af", "bd", "be", "bf", "cd", "ce", "cf"].

Note:

Although the above answer is in lexicographical order, your answer could be in any order you want.

```
import java.util.ArrayList;
import java.util.List;

/**
 * Created by omengye on 2016/12/27.
 */
public class LetterCombinationsofaPhoneNumber {

    public void getLetters(List<String> res, String current, String digits, int idx) {

        if (current.length() == digits.length()) {
            res.add(current);
            return;
        }

        int count = 0;
        String[] curs = new String[]{};
        switch (digits.charAt(idx)) {
            case '2': {
                curs = new String[]{"a", "b", "c"};
                count = curs.length;
                break;
            }
            case '3': {
                curs = new String[]{"d", "e", "f"};
                count = curs.length;
                break;
            }
            case '4': {
                curs = new String[]{"g", "h", "i"};
                count = curs.length;
                break;
            }
            case '5': {
                curs = new String[]{"j", "k", "l"};
                count = curs.length;
                break;
            }
            case '6': {
                curs = new String[]{"m", "n", "o"};
                count = curs.length;
                break;
            }
            case '7': {
                curs = new String[]{"p", "q", "r", "s"};
                count = curs.length;
                break;
            }
            case '8': {
                curs = new String[]{"t", "u", "v"};
                count = curs.length;
                break;
            }
            case '9': {
                curs = new String[]{"w", "x", "y", "z"};
                count = curs.length;
                break;
            }
            default:
                break;
        }

        for (int i=0; i<count; ++i) {
            getLetters(res, current+curs[i], digits, idx+1);
        }
    }


    public List<String> letterCombinations(String digits) {

        List<String> res = new ArrayList<>();
        if (digits.length()<1) {
            return res;
        }
        getLetters(res, "", digits, 0);

        return res;
    }

    public static void main(String[] args) {

        LetterCombinationsofaPhoneNumber solution = new LetterCombinationsofaPhoneNumber();

        String digits = "02";
        List<String> letters = solution.letterCombinations(digits);
        for (String l : letters) {
            System.out.println(l);
        }

    }


}

```

难度：

M

思路：

递归回溯，每次记录此时到达的位置，保存的前一个字符，现有的整个字符集list。需要注意的是边界，输入""输出[]，输入"03"输出[]
