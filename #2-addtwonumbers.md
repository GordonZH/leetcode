You are given two non-empty linked lists representing two non-negative integers. The digits are stored in reverse order and each of their nodes contain a single digit. Add the two numbers and return it as a linked list.

You may assume the two numbers do not contain any leading zero, except the number 0 itself.
```javascript
Input: (2 -> 4 -> 3) + (5 -> 6 -> 4)
Output: 7 -> 0 -> 8
Explanation: 342 + 465 = 807.
```

/**
 * Definition for singly-linked list.
 * function ListNode(val) {
 *     this.val = val;
 *     this.next = null;
 * }
 */
/**
 * @param {ListNode} l1
 * @param {ListNode} l2
 * @return {ListNode}
 */

//js在字符串和数组之间来回转换 投机取巧的做法 leetcode测试用例1560 号没通过，结果出现NaN
var addTwoNumbers = function(l1, l2) {
    function getNumber(l) {
        var temp = [];
        while(l.next!==null){
            temp.push(l.val)
            l = l.next;
        }
        temp.push(l.val);
        return parseInt(temp.reverse().join(''));
    }
    var computeResultArray = (getNumber(l1)+getNumber(l2)+'').split(''),
        pre = null,
        result = [];
    for(var i=0,l=computeResultArray.length; i<l; i++ ){
        result.push((function () {
            var node = new ListNode(parseInt(computeResultArray[i]));
            node.next = pre;
            pre = node;
            return node;
        })());
    }
    return result[l-1];
};