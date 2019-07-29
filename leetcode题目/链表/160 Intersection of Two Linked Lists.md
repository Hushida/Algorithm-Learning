思路1： 
假设链表A和链表B的公共部分长度是c，A的单独部分长度a，B的单独部分长度b   
则链表A的总长度a+c加上链表B的单独部分长度b    a+c+b  
等于链表B的总长度b+c加上链表A的单独长度a  也就是 a+c+b == b+c+a    
这表明：如果一个指针沿着a+c+b这个路线走，另一个指针沿着b+c+a 这个路线走，最后相遇的位置，就是链表相交的节点。  
如果两个链表不相交，两个指针相交的节点就是尾部后面的Null节点。返回null。   
```
package com.company;

public class IntersectionOfTwoLinkedList {
    static class Node{
        int val;
        Node next = null;
        Node(int val, Node next) {
            this.val  = val;
            this.next = next;
        }
    }
    public static void main(String[] args) {
        Node fourth = new Node(3, null);
        Node third = new Node(2, fourth);
        Node second = new Node(1, third);
        Node headA  = new Node(0, second);

        //Node fifthB= new Node(3, null);
        //Node fourthB = new Node(2, fifthB);
        //必须节点连接数才算是，仅仅值相同，并不是链表交
        Node thirdB = new Node(9, third);
        Node secondB = new Node(7, thirdB);
        Node headB = new Node(5, secondB);

        Node nodeA = headA;
        while(nodeA != null) {
            System.out.println(nodeA.val);
            nodeA = nodeA.next;
        }
        System.out.println("************");
        Node nodeB = headB;
        while(nodeB != null) {
            System.out.println(nodeB.val);
            nodeB = nodeB.next;
        }

        Node intersectionNode = intersectionOfTwoLinkedList(headA, headB);
        //打印出值
        System.out.println("intersecton node = " + intersectionNode.val);
    }
    public static Node intersectionOfTwoLinkedList(Node headA, Node headB) {
        if(headA == null || headB == null) {
            return null;
        }
        Node a = headA ;
        Node b = headB;
        while(a != b) {
            a = (a == null) ? headB : a.next;
            b = (b == null) ? headA : b.next;

        }
        return a;
    }
}

```
运行结果
```
0
1
2
3
************
5
7
9
2
3
intersecton node = 2
```
