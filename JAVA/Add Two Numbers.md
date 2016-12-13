You are given two linked lists representing two non-negative numbers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8

```
/**
 * Created by omengye on 2016/12/13.
 */

import java.util.List;

/**
 * Definition for singly-linked list.
 * public class ListNode {
 * int val;
 * ListNode next;
 * ListNode(int x) { val = x; }
 * }
 */

public class AddTwoNumbers {

    public class ListNode {
        int val;
        ListNode next;

        ListNode(int x) {
            val = x;
        }
    }

    public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
        int val = l1.val + l2.val;
        ListNode res = new ListNode(val);

        if (val / 10 > 0) {
            res.val = val % 10;
            res.next = new ListNode(val / 10);
        }

        recursion(l1.next, l2.next, res);

        return res;
    }

    public void recursion(ListNode l1, ListNode l2, ListNode res) {
        boolean flag = false;
        int val = 0;

        if (l1 != null) {
            val += l1.val;
            flag = true;
        }
        else {
            l1 = new ListNode(0);
        }

        if (l2 != null) {
            val += l2.val;
            flag = true;
        }
        else {
            l2 = new ListNode(0);
        }

        if (res.next != null) {
            val += res.next.val;
        }
        else if (flag){
            res.next = new ListNode(val);
        }

        if (flag && val / 10 == 0) {
            res.next.val = val;

            recursion(l1.next, l2.next, res.next);
        }
        else if (flag) {
            res.next.val = val % 10;
            res.next.next = new ListNode(val / 10);

            recursion(l1.next, l2.next, res.next);
        }
    }

    public ListNode generateListNode(int[] array) {

        ListNode l = new ListNode(array[0]);
        int iter = 1;

        addNodeToList(iter, array, l);
        return l;
    }

    public void addNodeToList(int iter, int[] array, ListNode l) {
        if (iter < array.length) {
            l.next = new ListNode(array[iter]);
            ++iter;
            addNodeToList(iter, array, l.next);
        }
    }

    public static void main(String[] args) {
        int[] l1Int = {0,3,9,3,4,9,2,5,8};//{2,4,3};
        int[] l2Int = {0,5,0,0,3,7,0,7,2,1};//{5,6,4};

        AddTwoNumbers addTwoNumbers = new AddTwoNumbers();
        ListNode l1 = addTwoNumbers.generateListNode(l1Int);
        ListNode l2 = addTwoNumbers.generateListNode(l2Int);

        ListNode resList = addTwoNumbers.addTwoNumbers(l1, l2);


        String spliter = "";
        while (resList != null) {
            System.out.print(spliter + resList.val);
            spliter = " -> ";

            resList = resList.next;
        }

    }
}

```

难度：

M

思考：

把链表的操作全用递归来实现，当l1或l2的长度不足时，用0弥补当前值来使两个链表长度相同。思路还有待优化，肯定有更好的解法。
