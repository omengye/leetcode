The string "PAYPALISHIRING" is written in a zigzag pattern on a given number of rows like this: (you may want to display this pattern in a fixed font for better legibility)

```
P   A   H   N
A P L S I I G
Y   I   R
```

And then read line by line: "PAHNAPLSIIGYIR"

Write the code that will take a string and make this conversion given a number of rows:

```
string convert(string text, int nRows);
```

convert("PAYPALISHIRING", 3) should return "PAHNAPLSIIGYIR".

```
/**
 * Created by omengye on 2016/12/18.
 */
public class ZigZagConversion {


    public String convert(String s, int numRows) {
        if (numRows == 1) {
            return s;
        }

        // 计算 上行回路个数
        int backNum = numRows -2;
        // 计算周期
        int loopNum = numRows + backNum;
        // 每个周期所占列数
        int loopCol = 1+backNum;
        // 计算列数
        int lastNum = s.length() % loopNum;
        int loops = s.length() / loopNum;
        int colNum = loops*loopCol;
        if (lastNum > 0) {
            colNum += lastNum>numRows ? (lastNum-numRows+1) : 1;
        }

        char[][] strs = new char[numRows][colNum];

        for (int i=0; i<s.length(); ++i) {
            // 之前有几个周期
            int loop = i/loopNum;
            // 判断第i个在哪行哪列
            if (i%loopNum < numRows) {
                strs[i%loopNum][loop*loopCol] = s.charAt(i);
            }
            else {
                // 上行
                strs[numRows-2-(i%loopNum-numRows)][loop*loopCol+1+i%loopNum-numRows] = s.charAt(i);
            }

        }

        String res = "";
        for (int i=0; i<numRows; ++i) {
            for (int j=0; j<colNum; ++j) {
                if (strs[i][j] == 0)
                    continue;
                res += strs[i][j];
            }
        }

        return res;
    }


    public static void main(String[] args) {

        ZigZagConversion solution = new ZigZagConversion();
        System.out.println(solution.convert("PAYPALISHIRING", 3));

    }

}
```

难度：

E

思路：

ZigZag的意思是之字形，这道题是将字符串按照之字形从上到下再从下到上排列，例如

```
0     6
1   5 7   11
2 4   8 10
3     9

P       H
A     S I
Y   I   R
P L     I G
A       N
```

将字符串分成周期，周期中有下行都在一列中，上行的处于不同的列。
