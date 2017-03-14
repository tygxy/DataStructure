# Sort
- 冒泡排序
```java
	public static void bubbleSort2(int [] a , int n){
	    int i,j;
	    boolean flag;
	    for (i=n-1; i>0; i-- ){
	        flag = false;
	        for(j=0; j<i; j++){
	            if (a[j] > a[j+1]){
	                int tmp = a[j];
	                a[j] = a[j+1];
	                a[j+1] = tmp;

	                flag = true;
	            }
	        }
	        if (flag == false){
	            break;
	        }
	    }

	}
```

- 快速排序
```java
	public static void quickSort(int[] a, int l ,int r){
        if (l<r){
            int i,j,x;

            i = l;
            j = r;
            x = a[i];
            while (i < j){
                while (i < j && a[j] > x){
                    j--; // 从右向左找第一个小于x的数
                }
                if (i < j){
                    a[i] = a[j];
                    i++;
                }
                while (i < j && a[i] < x){
                    i++; // 从左向右找第一个大于x的数
                }
                if (i < j){
                    a[j] = a[i];
                    j--;
                }
            }
            a[i] = x;
            quickSort(a,l,i-1);
            quickSort(a,i+1,r);
        }
	}
```

- 插入排序
```java
    public static void insertSort(int[] a , int n ) {
        int i, j, k;
        for (i = 1; i < n; i++) {
            // 为a[i]找到前面有序区间的合适位置
            for (j=i-1; j>=0; j--){
                if (a[j] < a[i])
                    break;
            }
            // 如果找到一个合适的位置
            if (j!=i-1){
                int tmp = a[i];
                // 将比a[i]大的后移
                for (k=i-1; k>j; k--){
                    a[k+1] = a[k];
                }
                a[k+1] = tmp;
            }
        }
    }
```

- 希尔排序
```java
    public static void shellSort(int[] a){
        // gap为步长，每次减为原来的一半
        for (int gap = a.length/2; gap>0 ; gap/=2){
            // 共gap个组，对每一组都执行直接插入排序
            for (int i=0; i<gap; i++){
                for (int j=i+gap; j<a.length; j+=gap){
                    // 如果a[j] < a[j-gap]，则寻找a[j]位置，并将后面数据的位置都后移。
                    if (a[j] < a[j-gap]){
                        int tmp = a[j];
                        int k = j - gap;
                        while (k>=0 && a[k] > tmp){
                            a[k+gap] = a[k];
                            k-=gap;
                        }
                        a[k+gap] = tmp;
                    }
                }
            }
        }
    } 
```