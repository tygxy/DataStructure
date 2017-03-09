# BinarySearchTree
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
        else{
            BSTNode followingNode = this.getFollowingNode(targetNode);
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
        while (node.left != null){
            nodeParent = node;
            node = node.left;
        }
        if(node.key != node2Del.right.key){
            nodeParent.left = node.right;
        }else{
            nodeParent.right = node.right;
        }
        return node;
    }

}
```
