# 《剑指offer》

3. 数组中重复的数字
        - 排序后，找出重复数字
	- Hash表
	- 利用数组的下标

4. 二维数组的查找
	- 从右上角开始查找

5. 替换空格
	- 先计算出需要的替换后数组需要的长度，从后往前填字符

6. 从尾到头打印链表
	- 利用栈
	- 把链表翻转

7. 重建二叉树
	- 在先序中找到根节点，然后把中序一分为二；中序前半部分是左子树，后半部分是右子树；使用递归解决

8. 二叉树的下一个节点

9. 用两个栈实现队列
	- 栈A存储新插入的节点，当有删除需求时，如果栈B非空，直接pop(),否则把栈A导入栈B，然后pop()

10. 斐波那契数列
	- 递归
	- 计算N，可以先通过f1,f2计算出f3,然后是f4,直到fn

11. 旋转数组的最小数字
	- 二分查找

15. 二进制中1的个数
	- 位运算，flag = 1,左移flag做位运算

18. 删除链表中的重复节点
	- preNode,curNode,nextNode,bool needTodelete
	- 确保preNode指针指向下一个没有重复的节点连接
	- 注意头节点也可能是重复，所以如果preNode==null 则要把head = nexteNode

21. 调整数组顺序使奇数位于偶数前面
	- 维护两个指针，一个在头，一个在尾，直到相遇为止

22. 链表倒数第K个节点
	- 快慢指针
	- 注意两个特殊情况，一是头节点，二是K大于链表长度的情况

23. 链表中环的入口
	- 快慢指针可以判断是否有环，找到环后，数环的个数为n,然后都从头开始，一个快n步，正常遍历，直到相遇则为入口

24. 反转链表
	- 栈
	- 三个指针做反转

25. 合并两个排序的链表
	- 判断两个链表的节点，选出最小的作为当前节点，然后递归

26. 树的子结构
	- 遍历两个树产生字符串，判断字符串是否包含

27. 二叉树的镜像
	- 先序遍历二叉树，如果有子节点，交换子节点；递归进行

28. 对称的二叉树
	- 把null算进来先序遍历二叉树，另外一个也是先序，但先遍历右节点，再遍历左节点，判断两个遍历是否相同

30. 包括min函数的栈
	- 把最小元素压入辅助栈

31. 栈的压入，弹出序列
	- stack做栈，遍历弹出序列，如果在栈顶则pop，如果不在，则往stack中压入还没入栈的元素，如果压入完都没有这个元素，则返回false

32. 从上到下打印二叉树
	- 广度优先遍历，用队列，先入头结点，然后弹出，遍历这个节点的所有子节点，并把子节点继续入队列，直到队列为空

33. 二叉搜索树的后序遍历序列
	- 根节点把序列分成两部分，左边的值都比跟节点小，右边的值都比跟节点大，满足这个条件，继续递归判断

34. 二叉树中和为某一值的路径
	- 

36. 二叉搜索树和双向链表
	- 根节点，左子树，右子树，把左右子树都转换成双向链表后，在跟根节点连起来；左子树最大节点跟根节点的左支；后子树的最小节点跟根节点的右支，递归解决

37. 序列化二叉树
	- 空节点用其他字符代替

39. 数组中出现次数超过一半的数字
	- 一个是数组中的数字，一个是次数；遍历数组，相同次数加1，不同减1，如果次数为0，换数字

40. 最小的k个数
	- 创建存放k个数的最大堆

42. 连续子数组的最大和
	- 累加和小于0，直接放弃之前的所有累加和

46. 把数字翻译成字符串
	- 从尾到头，计算不同翻译的数目；f(i) = 1 * f(i + 1) + g(i,i+1) * f(i + 2);其中g(i,i+1)是0或1，取决于是否在10-25之间

48. 最长不含重复字符的子字符串
	- 

49. 丑数
	- 新的丑数肯定是丑数的2倍，或者3倍，或者5倍

50. 第一个只出现一次的字符
	- hashmap存字符和个数，然后按照字符串遍历，最先获得的字符就是第一次出现的字符

51. 数组中的逆序对

52. 两个链表的第一个公共节点
	- 先分别算出链表长度，然后计算差值，先在长的链表移动差值这部分，然后比较两个链表的每个节点，返回第一个相同的节点

53. 在排序数组中查找数字
	- 二分查找，多次使用找到重复数字的第一个位置和最后一个位置

54. 二叉搜索树的第k大节点
	- 中序遍历，取第K个

55. 二叉树的深度
	- 递归

56. 数组中数字出现的次数
	- 只有一个数字出现一次，位运算
	- 只有两个数字出现一次，先位运算求和，然后找到哪位是1，按照这个把数组分为两类，分别求位运算和，可以分别找出

57. 和为s的数字
	- 双指针，一个在头，一个在尾，根据求和的大小移动指针

58. 反转字符串
	- 两次反转字符串

59. 队列的最大值
	- 















	
