You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.

`Example:`
```java
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

- - -
- ### 解析：
> 将两个链表的值进行相加，然后输出一个链表，虽然链表存储的是值的逆序，但是因为我们的结果要的是一个链表，所以可以直接进行处理，不需转置。
>
> 先构建一个ummy节点用于保存结果链表的头信息，防止丢失信息。定一个carry变量，用于处理进位的情况，两个链表的每个节点相加我们只需要保存个位的信息，其他的信息给carry保存，所以我们遍历两个链表，构建一个新的节点，新的节点的值是两个链表节点中的值相加再加上进位，然后在`mod10`,取个位，carry取结果的商。将新的节点添加到结果链表尾部。循环完毕之后，我们还需要对carry进行处理，此时carry可能为1可能为0，当carry为1说明结果比最两个数中较大数的位数还多，需要再构建一个头部标志的进位，但是链表逆序的原因，我们直接追加到结果链表的尾部即可。最后我们返回的是dummy.next。dummy.next记录的是初始链表的表头。

- ### 代码：
```java
public ListNode addTwoNumbers(ListNode l1, ListNode l2) {
    ListNode  result = new ListNode(-1);
    //定义一个临时节点
    ListNode cur = result ;
    //进位处理
    int carry = 0;
    while(l1!=null||l2!=null){
        int d1 = l1==null?0:l1.val;
        int d2 = l2==null?0:l2.val;
        int sum = d1+d2+carry;
        //是否进位
        carry= sum/10;
        cur.next = new ListNode(sum%10);
        //后移一位
        cur = cur.next;
        if(l1!=null){
            l1 = l1.next;
        }

        if(l2!=null){
            l2 = l2.next;
        }
    }

    //处理最后一位进位的情况
    if(carry ==1) cur.next = new ListNode(1);
    return result.next;    
}
```
