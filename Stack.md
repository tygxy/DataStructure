# Stack

- GeneralArrayStack.java
```java
public class GeneralArrayStack<T>{
	private static final int DEFAULT_SIZE = 12;
	private T[] mArray;
	private int count;

	public GeneralArrayStack(Class<T> type){
		this(type,DEFAULT_SIZE);
	}

	public GeneralArrayStack(Class<T> type , int size){
		mArray = (T[])Array.newInstance(type,size);
		count = 0;
	}

	public void push(T val){
		mArray[count] = val;
		count++;
	}
	
	public T peek(){
		if(count!=0){
			return mArray[count-1];
		}else{
			throw new EmptyStackException();
		}

	}
	
	public T pop(){
		T result = mArray[count-1];
		count--;
		return result;
	}
	
	public boolean isEmpty(){
		if(count==0){
			return true;
		}else{
			return false;
		}
	}
	
	public int size(){
		return count;
	}
	
	public int serach(T val){
		int i;
		if(!isEmpty()){
			for(i=count-1;i>=0;i--){
				if (mArray[i] == val){
					return i;
				}
				if(i==0){
					System.out.println("没有该元素");
					return -1;
				}
			}
			return -1;
		}else{
			System.out.println("栈为空");
			return -1;
		}
	}
	
	public void printAll(){
		if(isEmpty()){
			System.out.println("栈为空");
		}else{
			for(int i=count-1;i>=0;i--){
				System.out.println(mArray[i]);
			}
		}
		
	}
}
```

- Test.java
```java
public static void main(String[] args){
	GeneralArrayStack<Integer> stack = new GeneralArrayStack<Integer>(Integer.class);

	stack.push(1);
	stack.push(2);
	stack.push(3);
	stack.printAll();

	System.out.println("peek:");
	if(!stack.isEmpty()){
		int result1 = stack.peek();
		System.out.println(result1);
	}else{
		System.out.println("栈为空");
	}
	stack.printAll();
	
	System.out.println("pop:");
	int result2 = stack.pop();
	System.out.println(result2);
	stack.printAll();
	
	System.out.println(stack.serach(4));

}
```