# BinarySearchTree

## 基础BSTree
- BSTNode
```java
package BinarySearchTree;

public class BSTNode {
    public int key;
    public BSTNode left;
    public BSTNode right;

    public  BSTNode(){
        left = right = null;
    }
    public BSTNode(int key){
        this.key = key;
        this.right = null;
        this.left = null;
    }
}
```
- BinarySearchTree
```java
package BinarySearchTree;

import java.util.Queue;
import  java.util.LinkedList;


/**
 * 目录:
 * 1. 判断树是否为空
 * 2. 插入节点
 * 3. 查找节点并返回该节点
 * 4. 广度优先遍历
 * 5. 遍历三种方式，递归和非递归
 * 6. 找到树的最小节点
 * 7. 归返回二叉树结点个数（递归，非递归）
 * 8. 返回二叉树深度（递归，非递归）
 * 9. 将二叉查找树变为有序单链表
 * 10.二叉树第K层节点个数
 * 11.二叉树叶子结点个数
 */

public class BinarySearchTree {
    private BSTNode root;

    public BinarySearchTree(){
        root = null;
    }

    /**
     * 判断树是否为空
     */
    public boolean isEmpty(){
        if(root == null){
            return true;
        }else{
            return false;
        }
    }

    /**
     *   插入节点
     */

    public boolean insert(BSTNode p) {
        if (isEmpty()) {
            root = p;
            return true;
        } else {
            BSTNode tmp = root;
            while (tmp != null) {
                if (tmp.key < p.key) {
                    if (tmp.right == null) {
                        tmp.right = p;
                        return true;
                    } else {
                        tmp = tmp.right;
                    }
                }
                if (tmp.key > p.key) {
                    if (tmp.left == null) {
                        tmp.left = p;
                        return true;
                    } else {
                        tmp = tmp.left;
                    }
                }
            }
        }
        return false;
    }

    /**
     *  查找节点，并返回节点
     */
    public BSTNode search(int val){
        BSTNode tmp = root;
        if(tmp == null){
            System.out.println("树为空");
            return null;
        }else{
            while(tmp!=null){
                if(tmp.key == val){
                    return tmp;
                }else if(tmp.key < val){
                    tmp = tmp.right;
                }else{
                    tmp = tmp.left;
                }
            }
            System.out.println("没有该节点");
            return null;
        }
    }

    /**
     *  广度优先遍历
     */
    public void BFTraversal(){
        if (isEmpty()){
            System.out.println("树为空");
        }else {
            Queue<BSTNode> queue = new LinkedList<BSTNode>();
            BSTNode tmp = new BSTNode();
            queue.add(root);
            tmp = root;
            while(tmp!=null){
                System.out.println(tmp.key);
                if(tmp.left!=null){
                    queue.add(tmp.left);
                }
                if(tmp.right!=null){
                    queue.add(tmp.right);
                }
                queue.poll();
                tmp = queue.peek();
            }

        }
    }

    /**
     *   递归先序遍历
     */

    public void PreOrderTraversal(){
        if(root ==null){
            System.out.println("树为空");
        }else{
            PreOrderTraversal(root);
        }
    }

    public void PreOrderTraversal(BSTNode p){
        System.out.println(p.key);
        if (p.left!=null){
            PreOrderTraversal(p.left);
        }
        if (p.right!=null){
            PreOrderTraversal(p.right);
        }
    }

    /**
     *  递归中序遍历
     */
    public void InOrderTraversal(){
        if(root ==null){
            System.out.println("树为空");
        }else{
            InOrderTraversal(root);
        }
    }

    public void InOrderTraversal(BSTNode p){
        if (p.left!=null){
            InOrderTraversal(p.left);
        }
        System.out.println(p.key);
        if(p.right!=null){
            InOrderTraversal(p.right);
        }
    }

    /**
     *  递归后序遍历
     */
    public void PostOrderTraversal(){
        if(root ==null){
            System.out.println("树为空");
        }else{
            PostOrderTraversal(root);
        }
    }

    public void PostOrderTraversal(BSTNode p){
        if (p.left!=null){
            PostOrderTraversal(p.left);
        }
        if(p.right!=null){
            PostOrderTraversal(p.right);
        }
        System.out.println(p.key);
    }

    /**
     * 前序非递归遍历
     */

    public void preOrder(BSTreeNode p) {
        Stack<BSTreeNode> stack = new Stack<BSTreeNode>();
        while (p != null || !stack.empty()) {
            while (p != null) {
                System.out.println(p.val);
                stack.push(p);
                p = p.left;
            }
            if (!stack.empty()) {
                p = stack.pop();
                p = p.right;
            }
        }
    }

    /**
     * 中序非递归遍历
     */
    public void inOrder(BSTreeNode p) {
        Stack<BSTreeNode> stack = new Stack<BSTreeNode>();
        while (p != null || !stack.empty()) {
            while (p != null) {
                stack.push(p);
                p = p.left;
            }

            if (!stack.empty()) {
                p = stack.pop();
                System.out.println(p.val);
                p = p.right;
            }
        }
    }

    /**
     * 后序非递归遍历
     */
    public void postOrder(BSTreeNode root) {
        Stack<BSTreeNode> stack = new Stack<>();
        Stack<BSTreeNode> output = new Stack<>();//构造一个中间栈来存储逆后序遍历的结果
        BSTreeNode node = root;
        while (node != null || stack.size() > 0) {
            if (node != null) {
                output.push(node);
                stack.push(node);               
                node = node.right;
            } else {
                node = stack.pop();             
                node = node.left; 
            }
        }
        // 输出结果
        while (output.size() > 0) {
            System.out.println(output.pop().val);
        }
    }


    /**
     * 获取树中的最小值节点
     */

    public BSTNode getMinNode(){
        BSTNode tmp = root;
        if(tmp == null){
            System.out.println("树为空");
            return null;
        }
        while(tmp!=null){
            if(tmp.left!=null){
                tmp = tmp.left;
            }else{
                return tmp;
            }
        }
        return null;
    }


    /**
     * 获取树中的最大值节点
     */

    public BSTNode getMaxNode(){
        BSTNode tmp = root;
        if(tmp == null){
            System.out.println("树为空");
            return null;
        }
        while(tmp!=null){
            if(tmp.right!=null){
                tmp = tmp.right;
            }else{
                return tmp;
            }
        }
        return null;
    }

    /**
     * 删除节点
     */
    public boolean delete(int val){
        if(root == null){
            System.out.println("树为空");
            return false;
        }

        BSTNode targetNodeParent = root;
        BSTNode targetNode = root;
        boolean isLeftNode = true;

        while(targetNode.key != val){
            if(targetNode.key > val){
                targetNodeParent = targetNode;
                targetNode = targetNode.left;
                isLeftNode = true;
            }else{
                targetNodeParent = targetNode;
                targetNode = targetNode.right;
                isLeftNode = false;
            }
            if(targetNode == null){
                System.out.println("没有该节点");
                return false;
            }
        }

        // 如果删除的节点为叶子节点
        if(targetNode.right == null && targetNode.left == null){
            if(targetNode.key == root.key){
                root = null;
                return  true;
            }
            if(isLeftNode){
                targetNodeParent.left = null;
            }else{
                targetNodeParent.right = null;
            }
        }

        // 如果删除节点为单节点
        // 删除节点有左子节点
        else if(targetNode.right != null && targetNode.left == null){
            if(targetNode.key == root.key){
                root = targetNode.right;
                return  true;
            }
            if(isLeftNode){
                targetNodeParent.left = targetNode.right;
            }else{
                targetNodeParent.right = targetNode.right;
            }
        }

        // 删除节点有右子节点
        else if(targetNode.right == null && targetNode.left != null){
            if(targetNode.key == root.key){
                root = targetNode.left;
                return  true;
            }
            if(isLeftNode){
                targetNodeParent.left = targetNode.left;
            }else{
                targetNodeParent.right = targetNode.left;
            }
        }

        // 如果删除节点为双节点
        // 思路：找到删除节点右子树的最小值，用找到的最小值与删除节点替换，将最小值的原节点进行删除
        else{
            BSTNode followingNode = this.getFollowingNode(targetNode);
            // 最小值与删除节点替换
            if(targetNode.key == root.key){
                root = followingNode;
            }else if(isLeftNode){
                targetNodeParent.left = followingNode;
            }else{
                targetNodeParent.right = followingNode;
            }
            followingNode.left = targetNode.left;
            followingNode.right = targetNode.right;
        }
        return  true;
    }

    private BSTNode getFollowingNode(BSTNode node2Del){
        BSTNode nodeParent = node2Del;
        BSTNode node = node2Del.right;
        // node右支的最小值
        while (node.left != null){
            nodeParent = node;
            node = node.left;
        }
        // 删除最小值的原节点的右支
        if(node.key != node2Del.right.key){
            nodeParent.left = node.right;
        }else{
            nodeParent.right = node.right;
        }
        return node;
    }

}
```
- BSTTest
```java
package BinarySearchTree;

public class BSTTest {
    public static void main(String[] args) {
        BinarySearchTree tree = new BinarySearchTree();
        BSTNode node1 = new BSTNode(13);
        BSTNode node2 = new BSTNode(10);
        BSTNode node3 = new BSTNode(2);
        BSTNode node4 = new BSTNode(12);
        BSTNode node5 = new BSTNode(25);
        BSTNode node6 = new BSTNode(20);
        BSTNode node7 = new BSTNode(31);
        BSTNode node8 = new BSTNode(29);

        // 插入
        tree.insert(node1);
        tree.insert(node2);
        tree.insert(node3);
        tree.insert(node4);
        tree.insert(node5);
        tree.insert(node6);
        tree.insert(node7);
        tree.insert(node8);

        // 查找

//        BSTNode result = new BSTNode();
//        result = tree.search(10);
//        if(result!=null){
//            System.out.println(result.left.key);
//        }

        // 广度优先遍历
//        tree.BFTraversal();

        // 递归先序遍历
//        tree.PreOrderTraversal();

        // 递归中序遍历
//        tree.InOrderTraversal();

        // 递归后序遍历
//        tree.PostOrderTraversal();

        // 获取树中的最小节点
//        BSTNode result = new BSTNode();
//        result = tree.getMinNode();
//        if(result!=null){
//            System.out.println(result.key);
//        }

        // 获取树中的最大节点
//        BSTNode result = new BSTNode();
//        result = tree.getMaxNode();
//        if(result!=null){
//            System.out.println(result.key);
//        }

        // 删除节点
        boolean result = tree.delete(25);
        System.out.println(result);
        tree.BFTraversal();
    }
}

```

## BSTree相关操作
```java
- BSTNode
public class BSTNode {
    public BSTNode left = null;
    public BSTNode right = null;
    public int data;

    public BSTNode(int val) {
        this.data = val;
    }
}

- BSTree
import java.util.*;
import java.util.LinkedList;

/**
 * Created by guoxingyu on 2017/8/24.
 */
public class BinarySearchTree {
    public BSTNode root;

    public BinarySearchTree() {
        root = null;
    }

    /**
     * 判断树是否为空
     * @return
     */
    public boolean isEmpty() {
        if (root == null) {
            return true;
        }else {
            return false;
        }
    }

    /**
     * 插入节点
     * @param p
     * @return
     */
    public boolean insert(BSTNode p) {
        if (root == null) {
            root = p;
            return true;
        }
        BSTNode tmp = root;
        while (tmp != null) {
            if (tmp.data > p.data) {
                if (tmp.left == null) {
                    tmp.left = p;
                    return true;
                }
                tmp = tmp.left;
            } else {
                if (tmp.right == null) {
                    tmp.right = p;
                    return true;
                }
                tmp = tmp.right;
            }
        }
        return false;
    }

    /**
     * 查找节点，并返回该节点
     * @param val
     * @return
     */
    public BSTNode search(int val) {
        if (this.isEmpty()) {
            System.out.println("树为空");
            return null;
        }else {
            BSTNode tmp = root;
            while (tmp != null) {
                if (tmp.data == val) {
                    return tmp;
                }
                if (tmp.data < val) {
                    tmp = tmp.left;
                }
                if (tmp.data > val) {
                    tmp = tmp.right;
                }
            }
            System.out.println("无法找到该元素");
            return null;
        }
    }

    /**
     * 广度优先遍历
     */
    public void BFTraversal() {
        if (this.isEmpty()) {
            System.out.println("树为空");
        } else {
            BSTNode tmp = root;
            Queue<BSTNode> queue = new LinkedList<BSTNode>();
            queue.add(tmp);
            while (tmp != null) {
                System.out.println(tmp.data);
                if (tmp.left != null) {
                    queue.add(tmp.left);
                }
                if (tmp.right != null) {
                    queue.add(tmp.right);
                }
                queue.poll();
                tmp = queue.peek();
            }
        }
    }

    /**
     * 递归先序遍历
     */
    public void preOrderTraversal() {
        if (isEmpty()) {
            System.out.println("树为空");
        } else {
            preOrderTraversal(this.root);
        }
    }

    private void preOrderTraversal(BSTNode p) {
        if (p != null) {
            System.out.println(p.data);
            if (p.left != null) {
                preOrderTraversal(p.left);
            }
            if (p.right != null) {
                preOrderTraversal(p.right);
            }
        }
    }

    /**
     * 非递归先序遍历
     */
    public void preOrder() {
        BSTNode tmp = root;
        Stack<BSTNode> stack = new Stack<BSTNode>();
        while (!stack.isEmpty() || tmp != null) {
            while (tmp != null) {
                System.out.println(tmp.data);
                stack.push(tmp);
                tmp = tmp.left;
            }
            if (!stack.isEmpty()) {
                tmp = stack.pop();
                tmp = tmp.right;
            }
        }
    }

    /**
     * 递归中序遍历
     * @param p
     */
    public void inOrderTraversal(BSTNode p) {
        if (p != null) {
            if (p.left != null) {
                inOrderTraversal(p.left);
            }
            System.out.println(p.data);
            if (p.right != null) {
                inOrderTraversal(p.right);
            }
        }
    }

    /**
     * 非递归中序遍历
     */
    public void inOrder() {
        BSTNode tmp = root;
        Stack<BSTNode> stack = new Stack<BSTNode>();
        while (tmp != null || !stack.isEmpty()) {
            while (tmp != null) {
                stack.push(tmp);
                tmp = tmp.left;
            }
            if (!stack.isEmpty()) {
                tmp = stack.pop();
                System.out.println(tmp.data);
                tmp = tmp.right;
            }
        }
    }

    /**
     * 非递归后序遍历
     */
   public void postOrder() {
       BSTNode tmp = root;
       Stack<BSTNode> stack = new Stack<BSTNode>();
       Stack<BSTNode> output = new Stack<BSTNode>();
       while (tmp != null || !stack.isEmpty()) {
           if (tmp != null) {
               output.push(tmp);
               stack.push(tmp);
               tmp = tmp.right;
           } else {
               tmp = stack.pop();
               tmp = tmp.left;
           }
       }
       while (!output.isEmpty()) {
           System.out.println(output.pop().data);
       }
   }

    /**
     * 找到树的最小节点
     * @return
     */
   public BSTNode findMinNode() {
        BSTNode tmp = root;
        while (tmp != null) {
            if (tmp.left != null) {
                tmp = tmp.left;
            }
            return tmp;
        }
        return null;
   }

    /**
     * 非递归返回二叉树结点个数
     * @return
     */
   public int getNodeNum() {
       if (root == null) {
           return 0;
       } else {
           int nodeNum = 1;
           Queue<BSTNode> queue = new LinkedList<BSTNode>();
           queue.add(root);
           while (!queue.isEmpty()) {
               BSTNode curNode = queue.remove();
               if (curNode.left != null) {
                   queue.add(curNode.left);
                   nodeNum += 1;
               }
               if (curNode.right != null) {
                   queue.add(curNode.right);
                   nodeNum += 1;
               }
           }
           return nodeNum;
       }
   }

    /**
     * 递归返回二叉树结点个数
     * @param root
     * @return
     */
   public int getNodeNumRec(BSTNode root) {
       if (root == null) {
           return 0;
       } else {
           return getNodeNumRec(root.left) + getNodeNumRec(root.right) + 1;
       }
   }

    /**
     * 非递归返回二叉树深度
     * @return
     */
   public int getDepth() {
       if (root == null) {
           return 0;
       } else {
           int depth = 0;
           int curLevelNodes = 1; //当前level,node的数量
           int nextLevelNodes = 0; //下层level,node的数量

           Queue<BSTNode> queue = new LinkedList<>();
           queue.add(root);
           while (!queue.isEmpty()) {
               BSTNode curNode = queue.remove();
               curLevelNodes -= 1; //减少当前Level node的数量
               if (curNode.left != null) {
                   queue.add(curNode.left);
                   nextLevelNodes += 1;
               }
               if (curNode.right != null) {
                   queue.add(curNode.right);
                   nextLevelNodes += 1;
               }

               if (curLevelNodes == 0) {
                   depth += 1;
                   curLevelNodes = nextLevelNodes;
                   nextLevelNodes = 0;
               }
           }
           return depth;
       }
   }

    /**
     * 递归返回二叉树深度
     * @param root
     * @return
     */
   public int getDepthRec(BSTNode root) {
       if (root == null) {
           return 0;
       } else {
           int leftDepth = getDepthRec(root.left);
           int rightDepth = getDepthRec(root.right);
           return Math.max(leftDepth,rightDepth) + 1;
       }
   }

    /**
     * 非递归将二叉查找树变为有序单链表
     * @return
     */
   public Queue<Integer> convertBST2DLL() {
       if (root == null) {
           System.out.println("树为空");
           return null;
       } else {
           BSTNode curNode = root;
           Stack<BSTNode> stack = new Stack<>();
           Queue<Integer> queue = new LinkedList<>();
           Integer head;
           while (curNode != null || !stack.isEmpty()) {
               while (curNode != null) {
                   stack.push(curNode);
                   curNode = curNode.left;
               }
               if (!stack.isEmpty()) {
                   curNode = stack.pop();
                   queue.add(curNode.data);
                   curNode = curNode.right;
               }
           }
           return queue;
       }
   }

    /**
     * 二叉树第K层节点个数
     * @param k
     * @return
     */
   public int getNodeNumKthLevel(int k) {
       if (root == null) {
           System.out.println("树为空");
           return 0;
       } else {
           Queue<BSTNode> queue = new LinkedList<>();
           queue.add(root);
           int i = 1;
           int curLevelNodes = 1;
           int nextLevelNodes = 0;
           while (!queue.isEmpty() && i < k) {
               BSTNode cur = queue.remove();
               curLevelNodes -= 1;
               if (cur.left != null) {
                   queue.add(cur.left);
                   nextLevelNodes += 1;
               }
               if (cur.right != null) {
                   queue.add(cur.right);
                   nextLevelNodes += 1;
               }
               if (curLevelNodes == 0) {
                   curLevelNodes = nextLevelNodes;
                   nextLevelNodes = 0;
                   i ++;
               }
           }
           return curLevelNodes;
       }
   }

    /**
     * 二叉树叶子结点个数
     * @return
     */
   public int getNodeNumLeaf() {
       if (root == null) {
           return 0;
       } else {
           int numLeaf = 0;
           BSTNode curNode = root;
           Stack<BSTNode> stack = new Stack<>();
           while (curNode != null || !stack.isEmpty()) {
               while (curNode != null) {
                   stack.push(curNode);
                   curNode = curNode.left;
               }
               if (!stack.isEmpty()) {
                   curNode = stack.pop();
                   if (curNode.left == null && curNode.right == null) {
                       numLeaf += 1;
                   }
                   curNode = curNode.right;
               }
           }
           return numLeaf;
       }
   }
}
```
