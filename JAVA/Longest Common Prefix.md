Write a function to find the longest common prefix string amongst an array of strings.

```
/**
 * Created by omengye on 2016/12/23.
 */
public class LongestCommonPrefixSolution {


    public String longestCommonPrefix(String[] strs) {
        if (strs.length==0 || strs[0].length() == 0) {
            return "";
        }

        String firstStr = strs[0];

        int iter = -1;
        boolean isBreak = false;
        for (int i=0; i<firstStr.length(); ++i) {

            for (int j=0; j<strs.length; ++j) {
                if (strs[j].length()<=i || strs[j].charAt(i)!=firstStr.charAt(i)) {
                    iter = i;
                    isBreak = true;
                    break;
                }
            }

            if (isBreak) {
                break;
            }

        }

        if (iter==-1) {
            return "";
        }
        else if (!isBreak) {
            return firstStr;
        }
        else {
            return firstStr.substring(0, iter);
        }

    }


    public static void main (String[] args) {

        LongestCommonPrefixSolution solution = new LongestCommonPrefixSolution();

        String[] s = new String[]{"asss","asvc","ac","av"};

        String[] ss = new String[]{"a"};

        System.out.println(solution.longestCommonPrefix(ss));



    }
}

```

难度：

E

思路：

寻找n个字符串中最长的相同子串，字串从字符串起始开始算起。拿第一个字符串遍历，与剩余的字
符串比较即可
