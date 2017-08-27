# LinkedList

## 典型单链表和部分常见操作
- ListNode
```java
public class ListNode {
    public ListNode next = null;
    public int data;

    public ListNode(int val) {
        data = val;
    }
}
```

- LinkedList
```java
import java.util.ArrayList;
import java.util.HashSet;
import java.util.List;
import java.util.Stack;


/**
 * 目录:
 * 1. 判断链表是否为空
 * 2. 添加结点到链表尾部
 * 3. 返回链表长度
 * 4. 插入结点到链表的任意位置
 * 5. 正序遍历链表
 * 6. 逆序遍历链表
 * 7. 链表反转，两种方式
 * 8. 删除指定位置元素
 * 9. 链表冒泡排序
 * 10.删除重复元素，两种方式
 * 11.找到倒数K个结点
 * 12.返回中间结点
 * 13.删除某个节点，只能访问该结点，无法删除尾结点
 * 14.判断是否有环
 * 15.判断是否有环，并返回环路的开头节点
 * 16.判断是否为回文
 * 17.判断两个链表是否相交
 * 18.判断是否相交，并返回第一个交点结点
 */


public class LinkedList {

    public ListNode head = null;

    /**
     * 判断链表是否为空
     * @return
     */
    public boolean isEmpty() {
        if (head == null) {
            return true;
        }else {
            return false;
        }
    }

    /**
     * 为单链表添加结点到链表尾部
     * @param val
     */
    public void addNode(int val) {
       ListNode p = new ListNode(val);
       if (head == null) {
           head = p;
       }else {
           ListNode tmp = head;
           while (tmp.next != null) {
               tmp = tmp.next;
           }
           tmp.next = p;
       }
    }

    /**
     * 计算链表长度
     * @return
     */
    public int length() {
        int length = 0;
        if (head != null) {
            ListNode p = head;
            while (p.next != null) {
                length += 1;
                p = p.next;
            }
            length +=1;
        }
        return length;
    }

    /**
     * 结点插入到单链表的指定位置
     * @param index
     * @param val
     */
    public void insertNodeByIndex(int index,int val) {
        if (index > this.length() + 1 || index < 1) {
            System.out.println("插入位置不合理，超过链表长度");
        }else {
            ListNode p = head;
            ListNode tmp = new ListNode(val);
            if (index == 1) {
                tmp.next = head;
                head = tmp;
            } else {
                while (index > 2) {
                    p = p.next;
                    index -=1;
                }
                tmp.next = p.next;
                p.next = tmp;
            }
        }
    }

    /**
     * 遍历显示单链表所有元素
     */
    public void display() {
        ListNode p = head;
        while (p != null) {
            System.out.println(p.data);
            p = p.next;
        }
    }

    /**
     * 从尾到头输出链表
     */
    public void reverseDisplay() {
        List<Integer> list = new ArrayList<Integer>();
        ListNode curNode = head;
        while (curNode != null) {
            list.add(curNode.data);
            curNode = curNode.next;
        }
        for (int i = list.size() - 1; i >= 0; i--) {
            System.out.println(list.get(i));
        }

    }

    /**
     * 链表的反转
     */
    public void reverseLinkedList() {
        ListNode curNode = head;
        ListNode preNode = null;
        while (curNode != null) {
            ListNode nextNode = curNode.next;
            if (nextNode == null) {
                this.head = curNode;
            }
            curNode.next = preNode;
            preNode = curNode;
            curNode = nextNode;
        }
    }


    /**
     * 单链表反转，借助stack
     */
    public void reverseList() {
        if (getListLength() == 0) {
            System.out.println("链表为空");
        } else {
            Stack<ListNode> stack = new Stack<ListNode>();
            ListNode tmp = head;
            while (tmp != null) {
                stack.push(tmp);
                tmp = tmp.next;
            }
            head = stack.pop();
            tmp = head;
            while (!stack.isEmpty()) {
                tmp.next = stack.pop();
                tmp = tmp.next;
            }
            tmp.next = null;
        }
    }

    /**
     * 删除指定位置元素
     * @param index
     * @return
     */
    public boolean delete(int index) {
        if (index < 1 || index > length()) {
            System.out.println("删除位置不合理，超过链表长度");
            return false;
        }else {
            ListNode tmp = head;
            if (index == 1) {
                head = head.next;
                return true;
            }
            while (index > 2) {
                tmp = tmp.next;
                index -= 1;
            }
            tmp.next = tmp.next.next;
            return true;
        }
    }

    /**
     * 单链表冒泡排序
     */
    public void orderLinkedList() {
        if (length() < 1) {
            System.out.println("链表中没有元素，无法排序");
        }else {
            ListNode curNode = head;
            ListNode nextNode = null;
            int temp = 0;
            while (curNode != null) {
                nextNode = curNode.next;
                while (nextNode != null) {
                    if (curNode.data > nextNode.data) {
                        temp = curNode.data;
                        curNode.data = nextNode.data;
                        nextNode.data = temp;
                    }
                    nextNode = nextNode.next;
                }
                curNode = curNode.next;
            }
        }
    }


    /**
     * 2.1 删除重复元素(使用额外空间)
     */
    public void deleteRepetitionElement() {
        if (length() < 1) {
            System.out.println("链表为空");
        }else {
            ListNode curNode = head.next;
            ListNode preNode = head;
            HashSet<Integer> hashSet = new HashSet<Integer>();
            hashSet.add(preNode.data);
            while (curNode != null) {
                if (hashSet.contains(curNode.data)) {
                    preNode.next = curNode.next;
                    curNode = curNode.next;
                }else {
                    hashSet.add(curNode.data);
                    curNode = curNode.next;
                    preNode = preNode.next;
                }
            }
        }
    }

    /**
     *  2.1 删除重复元素(不能使用额外空间)
     */
    public void deleteRepetitionElement2() {
        if (length() < 1) {
            System.out.println("链表为空");
        }else {
            ListNode curNode = head;
            while (curNode != null) {
                ListNode tmp = curNode;
                while (tmp.next != null) {
                    if (curNode.data == tmp.next.data) {
                        tmp.next = tmp.next.next;
                    }else {
                        tmp = tmp.next;
                    }
                }
                curNode = curNode.next;
            }
        }
    }

    /**
     * 2.2 找到倒数K个节点
     * @param k
     * @return
     */
    public ListNode findElem(int k) {
        if ( length() < 1) {
            System.out.println("链表为空");
            return null;
        }

        if (k > length()) {
            System.out.println("超过链表长度，无法取到");
            return null;
        }

        ListNode curNode = head;
        ListNode kNode = head;
        while (k > 1) {
            kNode = kNode.next;
            k -= 1;
        }
        while (kNode.next != null) {
            curNode = curNode.next;
            kNode = kNode.next;
        }
        return curNode;
    }

    /**
     * 查询中间的节点
     * @return
     */
    public ListNode findMiddleElememt() {
        ListNode slowNode = head;
        ListNode fastNode = head;
        while (fastNode != null && fastNode.next != null && fastNode.next.next != null) {
            fastNode = fastNode.next.next;
            slowNode = slowNode.next;
        }
        return slowNode;
    }

    /**
     * 2.3 删除某个节点，只能访问该节点，并且无法删除尾节点
     * @param node
     * @return
     */
    public boolean deleteNode(ListNode node) {
        if (node == null || node.next == null) {
            return false;
        }
        ListNode nextNode = node.next;
        node.data = nextNode.data;
        node.next = nextNode.next;
        return true;
    }

    /**
     * 判断单链表是否有环
     * @return
     */
    public boolean hasCycye() {
        if (getListLength() == 0) {
            System.out.println("链表无元素");
            return false;
        } else {
            ListNode fastNode = head;
            ListNode slowNode = head;
            while (fastNode != null && fastNode.next != null) {
                fastNode = fastNode.next.next;
                slowNode = slowNode.next;
                if (fastNode == slowNode) {
                    return true;
                }
            }
            return false;
        }
    }

    /**
     * 2.6 判断是否为环，并返回环路的开头起点
     * @return
     */
    public ListNode ifListIsHoop() {
        if (length() < 1) {
            System.out.println("链表无元素");
            return null;
        }else {
           ListNode fastNode = head;
           ListNode slowNode = head;
           // 找到碰撞位置，位于链表LOOP_SIZE - k步处
           while (fastNode != null && fastNode.next != null) {
               slowNode = slowNode.next;
               fastNode = fastNode.next.next;
               if (slowNode == fastNode) {
                   break;
               }
           }
           // 如果没碰撞，则无环
           if (fastNode == null || fastNode.next == null) {
               return null;
           }
           // slowNode指向head，fastNode和slowNode与环起始位置都距离K步，按相同速度前进，再次碰撞位置就是环的起点
           slowNode = head;
           while (slowNode != fastNode) {
               fastNode = fastNode.next;
               slowNode = slowNode.next;
           }
           return fastNode;
        }
    }

    /**
     * 2.7 判断是否为回文
     * @return
     */
    public boolean ifListPalindrome() {
        if (length() < 1) {
            System.out.println("链表无元素");
            return false;
        }else {
            ListNode fastNode = head;
            ListNode slowNode = head;
            // 链表前半部分元素入栈
            Stack<Integer> stack = new Stack<Integer>();
            while (fastNode != null && fastNode.next != null) {
                stack.push(slowNode.data);
                fastNode = fastNode.next.next;
                slowNode = slowNode.next;
            }
            // 链表元素为奇数的话，跳过中间元素
            if (fastNode != null) {
                slowNode = slowNode.next;
            }
            // 判断两部分是否相同，不相同则不是回文
            while (slowNode != null) {
                int val = stack.pop().intValue();
                if (val != slowNode.data) {
                    return false;
                }
                slowNode = slowNode.next;
            }
            return true;
        }
    }

    /**
     * 判断两个单链表是否相交
     * @param head1
     * @param head2
     * @return
     */
    public boolean isIntersect(ListNode head1, ListNode head2) {
        if (head1 == null || head2 == null) {
            return false;
        }
        ListNode tail1 = head1;
        while (tail1.next != null) {
            tail1 = tail1.next;
        }
        ListNode tail2 = head2;
        while (tail2.next != null) {
            tail2 = tail2.next;
        }
        if (tail1 == tail2) {
            return true;
        } else {
            return false;
        }
    }

     /**
     * 判断是否相交，并返回第一个交点结点
     * @param head1
     * @param head2
     * @return
     */
    public ListNode getFirstCommonNode(ListNode head1, ListNode head2) {
        if (head1 == null || head2 == null) {
            return null;
        }
        ListNode tail1 = head1;
        ListNode tail2 = head2;
        int length1 = 1;
        int length2 = 1;
        while (tail1.next != null) {
            tail1 = tail1.next;
            length1 += 1;
        }
        while (tail2.next != null) {
            tail2 = tail2.next;
            length2 += 1;
        }
        // 不相交直接返回
        if (tail1 != tail2) {
            return null;
        }
        // 略过较长链的多余部分
        ListNode curNode1 = head1;
        ListNode curNode2 = head2;
        if (length1 > length2) {
            int k = length1 - length2;
            while (k > 0) {
                curNode1 = curNode1.next;
                k -= 1;
            }
        } else {
            int k = length2 - length1;
            while (k > 0) {
                curNode2 = curNode2.next;
                k -= 1;
            }
        }
        // 一起向后遍历，直到找到交点
        while (curNode1 != curNode2) {
            curNode1 = curNode1.next;
            curNode2 = curNode2.next;
        }
        return curNode1;
    }


}

```

## 非典型单链表
- ListNode
```java
public class ListNode {
	public int val;
	public ListNode next;
	public ListNode(int i){
		this(i,null);
	}
	public ListNode(int i,ListNode n){
		val=i;
		next=n;
	}
}
```

- LinkedList
```java
public class LinkedList {
  protected ListNode head,tail;
  
  public IntLinkedList(){
		head = tail = null;
	}
  
  public boolean isEmpty(){
		if (head == null){
			return true;
		}else{
			return false;
		}
	}
  
  public void addToHead(int el){
		head = new ListNode(el,head);
		if(tail==null){
			tail = head;
		}
	}
  
  public void addToTail(int el){
		if( !isEmpty() ){
			tail.next = new ListNode(el);
			tail = tail.next;
		}else{
			head = tail = new ListNode(el);
		}	
	}
  
  public int deleteFromHead(){
		int val = head.val;
		if(head == tail){
			head = tail = null;
		}else{
			head = head.next;
		}
		return val;
	}
  
  public int deleteFromTail(){
		int val = tail.val;
		if(head == tail){
			head = tail = null;
		}else{
			ListNode tmp;
			tmp = head;
			while (tmp.next!=tail){
				tmp = tmp.next;
			}
			tail = tmp;
			tail.next = null;
			
		}
		return val;
	}
  
  public void delete(int val){
		ListNode tmp,pred;
		if ( !isEmpty()){
			if (head == tail && head.val == val){
				head = tail = null;
			}else if( head.val == val){
				head = head.next;
			}else{
				pred = head;
				tmp = head.next;
				while(tmp!=null && tmp.val!=val){
					pred = pred.next;
					tmp = tmp.next;
				}
				if(tmp!=null){
					pred.next = tmp.next;
					if (tmp == tail){
						tail = pred;
					}
				}
				if(tmp==null){
					System.out.println("没有找到该值");
				}
			}
		}else{
			System.out.println("链表为空");
		}
	}
  
  public void printAll(){
		if ( !isEmpty() ){
			ListNode tmp;
			tmp = head;
			while(tmp!=null){
				System.out.println(tmp.val);
				tmp = tmp.next;
			}
		}
	}
  
  public boolean isInList(int val){
		if( !isEmpty() ){
			ListNode tmp;
			tmp = head;
			while( tmp!=null && tmp.val != val){
				tmp = tmp.next;
			}
			if(tmp!=null){
				System.out.println(val+"存在");
				return true;
			}else{
				System.out.println(val+"不存在");
				return false;
			}
		}else{
			System.out.println("链表为空");
			return false;		
		}
	}
  
}  
  
```
