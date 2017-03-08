# Queue

## 数组实现队列，能存储任意类型数据
- GeneralArrayQueue.java
```java
package GeneralArrayQueue;

import java.lang.reflect.Array;

public class GeneralArrayQueue<T>{
	private static final int DEFAULT_SIZE = 12;
	private T[] mArray;
	private int count;
	
	public GeneralArrayQueue(Class<T> type){
		this(type,DEFAULT_SIZE);
	}
	
	public GeneralArrayQueue(Class<T> type, int size){
		mArray = (T[]) Array.newInstance(type, size);
		count = 0;
	}
	
	public int size(){
		return count;
	}
	
	public boolean isEmpty(){
		if(size()==0){
			return true;
		}else{
			return false;
		}
	}
	
	public void add(T val){
		mArray[count] = val;
		count++;
	}
	
	public T front(){
		return mArray[0];
	}
	
	public T pop(){
		T tmp = mArray[0];
		for(int i=0;i<count-1;i++){
			mArray[i]=mArray[i+1];
		}
		count--;
		return tmp;
	}
	
	public void printAll(){
		for(int i=0;i<count;i++){
			System.out.println(mArray[i]);
		}
	}
	
	public int search(T val){
		if(isEmpty()){
			System.out.println("队列为空");
			return -1;
		}else{
			for(int i=0;i<count;i++){
				if(mArray[i]==val){
					return i;
				}
			}
			System.out.println("队列没有该值");
			return -1;
		}
	}	
}
```

- Test.java
```java
package GeneralArrayQueue;

public class Test {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		GeneralArrayQueue<String> queue = new GeneralArrayQueue<String>(String.class);
		queue.add("a1");
		queue.add("b2");
		queue.add("c3")
		;
		System.out.println("fonrt:");
		System.out.println(queue.front());
		
		System.out.println("pop:");
		queue.pop();
		queue.printAll();
		
		System.out.println("size:");
		System.out.println(queue.size());
		
		System.out.println(queue.search("c3"));
		
	}

}

```