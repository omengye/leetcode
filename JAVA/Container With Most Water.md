Given n non-negative integers a1, a2, ..., an, where each represents a point at
 coordinate (i, ai). n vertical lines are drawn such that the two endpoints of
 line i is at (i, ai) and (i, 0). Find two lines, which together with x-axis
 forms a container, such that the container contains the most water.

Note: You may not slant the container.

```
/**
 * Created by omengye on 2016/12/20.
 */
public class ContainerWithMostWater {


    public int maxArea(int[] height) {

        if (height.length < 2) {
            return 0;
        }

        int i = 0;
        int j = height.length-1;

        int maxArea = area(height[i], height[j], j-i);

        int lastI = 0;
        int lastJ = 0;

        while(i<j) {

            if (height[i] <= height[j]) {
                if (height[i] > lastI) {
                    maxArea = Math.max(maxArea, area(height[i], height[j], j-i));
                    lastI = height[i];
                }
                else {
                    ++i;
                }

            }
            else {
                if (height[j] > lastJ) {
                    maxArea = Math.max(maxArea, area(height[i], height[j], j-i));
                    lastJ = height[j];
                }
                else {
                    --j;
                }
            }
        }

        return maxArea;
    }

    public int area(int h1, int h2, int w) {
        return Math.min(h1, h2) * w;
    }

    public static void main(String[] args) {

        ContainerWithMostWater solution = new ContainerWithMostWater();

        int[] l1 = new int[]{2,3,10,5,7,8,9};

        System.out.println(solution.maxArea(l1));

    }
}

```

难度：

M

思路：

计算最大能盛多少水，木桶原理。a1, a2, ..., an看作是木板，假如从中选取两个ai和aj，则面
积的计算公式为
```
Min(a1, aj) * (j-i)
```
这里选取数组的起始a0和a1作为初始值，假如a0<=an，那么就将a0向后移动直到ai>a0再计算面积，
因为假如a0>=ai那么面积肯定没有初始在a0时的大；。假如ai>an，那么就将an向前移动直到aj>ai
再计算面积。这样遍历数组直到i>=j可以保证每次得到的面积都比之前的大。
