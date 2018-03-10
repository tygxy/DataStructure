# Sort
- 冒泡排序
    - 时间复杂度：最坏：O(n2) 最好: O(n) 平均: O(n2) 
    - 空间复杂度：O(1) 
    - 稳定性：稳定，相邻的关键字两两比较，如果相等则不交换。所以排序前后的相等数字相对位置不变
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
    - 最坏:O(n2) 最好: O(nlogn) 平均: O(nlogn) 
        - 最坏的情况出现在顺序或者逆序，这样分的时候没法平分
        - 最好的情况出现在选择的元素正好可以将数组平分，可以选择array[(left+right)/2]的元素作为基准元素
    - 存储空间为O(nlog(n)),用于递归的方法栈
    - 稳定性：不稳定 快排会将大于等于基准元素的关键词放在基准元素右边
```java
public void quickSort(int[] array, int left,int right) {
    if (left < right) {
        int p = partition(array,left,right);
        quickSort(array,left,p - 1);
        quickSort(array,p + 1,right);
    }
}

public int partition(int[] array,int left, int right) {
    int val = array[left];
    while (left < right) {
        while (left < right && array[right] > val) {
            right -= 1;
        }
        if (left < right) {
            array[left] = array[right];
            left += 1;
        }
        while (left < right && array[left] < val) {
            left += 1;
        }
        if (left < right) {
            array[right] = array[left];
            right -= 1;
        }
    }
    array[left] = val;
    return left;
}
```

- 插入排序
    - 时间复杂度：O(n^2) O(n) O(n^2) （最坏 最好 平均） 
    - 空间复杂度：O(1) 
    = 稳定性：稳定每次都是在前面已排好序的序列中找到适当的位置，只有小的数字会往前插入，所以原来相同的两个数字在排序后相对位置不变

```java
public static void insertSort(int[] array) {
    for (int i = 2; i < array.length; i++ ) {
        int val = array[i];
        int j = i -1;
        while (j >= 0 && array[j] > val) {  // array[j] > val
            array[j+1] = array[j];
            j--;
        }
        array[j+1] = val; //  array[j+1] 不是array[j]
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

- 选择排序,平均与最差情况为O(n2),存储空间为O(1)
```java
public void selectionSort(int[] nums) {
    for (int i = 0; i < nums.length - 1; i++) {
        for (int j = i + 1; j < nums.length; j++) {
            if (nums[i] > nums[j]) {
                int tmp = nums[i];
                nums[i] = nums[j];
                nums[j] = tmp;
            }
        }
    }
}
```

- 归并排序,
    - 时间复杂度：最坏:O(nlogn) 最好: O(nlogn) 平均: O(nlogn)
    - 空间复杂度：O(n)
    - 稳定
```java
public void mergeSort(int[] nums, int left, int right) {
    if (left < right) {
        int center = (left + right) / 2;
        mergeSort(nums,left,center);
        mergeSort(nums,center + 1, right);
        merge(nums,left,center,right);
    }
}

private void merge(int[] nums, int left, int center, int right) {
    int[] tmpArr = new int[right - left + 1];

    int i = left; // 左指针
    int j = center + 1; // 右指针
    int k = 0;

    // 把较小的数先移到新数组中
    while (i <= center && j <= right) {
        if (nums[i] <= nums[j]) {
            tmpArr[k] = nums[i];
            i++;
        } else {
            tmpArr[k] = nums[j];
            j++;
        }
        k++;
    }

    // 将左半部分剩余元素，复制到目标数组中
    while (i <= center) {
        tmpArr[k] = nums[i];
        i++;
        k++;
    }
    // 将右半部分剩余元素，就复制到目标数组中
    while ( j <= right) {
        tmpArr[k] = nums[j];
        j++;
        k++;
    }
    // 新数组元素覆盖旧数组
    for (int m = 0; m < tmpArr.length; m++) {
        nums[m + left] = tmpArr[m];
    }
}
```

- 二分查找
```
/**
 * 非递归二分查找
 * @param nums
 * @param x
 * @return
 */
public int binarySearch(int[] nums, int x) {
    int left = 0;
    int right = nums.length - 1;
    int middle;
    while (left <= right) {
        middle = (left + right) / 2;
        if (nums[middle] < x) {
            left = middle + 1;
        } else if (nums[middle] > x) {
            right = middle - 1;
        } else {
            return middle;
        }
    }
    return -1;
}

/**
 * 递归二分查找
 * @param nums
 * @param x
 * @param left
 * @param right
 * @return
 */
public int binarySearchRec(int[] nums, int x, int left, int right) {
    if (left > right) {
        return -1;
    }
    int middle = (left + right) / 2;
    if (nums[middle] < x) {
        return binarySearchRec(nums,x,middle + 1,right);
    } else if (nums[middle] > x) {
        return binarySearchRec(nums, x, left, middle - 1);
    } else {
        return middle;
    }
}
```
