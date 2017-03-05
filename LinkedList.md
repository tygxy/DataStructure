# LinkedList

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
