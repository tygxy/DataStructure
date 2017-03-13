# AVLTree
- AVLTree.java
```java
package AVLTree;

public class AVLTree {
    public AVLTreeNode root;

    public class AVLTreeNode{
        int key;
        int height;
        AVLTreeNode left;
        AVLTreeNode right;

        public AVLTreeNode(int val){
            this(val,null,null);
        }

        public AVLTreeNode(int val,AVLTreeNode left,AVLTreeNode right){
            this.key = val;
            this.left = left;
            this.right = right;
            height =0;
        }
    }

    /**
     * 构造AVL树
     */

    public AVLTree(){
        root = null;
    }

    /**
     * 获取树的高度
     */

    public int height(AVLTreeNode tree){
        if(tree!=null){
            return tree.height;
        }
        return 0;
    }

    public int height(){
        return root.height;
    }

    /**
     * 比较两个值得大小
     */
    private int max(int a ,int b){
        return a>b ? a:b;
    }

    /**
     * 先序遍历
     */
    public void PreOrder(){
        if(root==null){
            System.out.println("树为空");
        }else{
            PreOrder(root);
        }
    }

    public void PreOrder(AVLTreeNode p){
        System.out.println(p.key);
        if(p.left!=null){
            PreOrder(p.left);
        }
        if(p.right!=null){
            PreOrder(p.right);
        }
    }


    /**
     * 查找节点
     */

    public AVLTreeNode search(int val){
        if(root == null){
            System.out.println("树为空");
            return null;
        }else{
            AVLTreeNode tmp = root;
            while(tmp!=null){
                if(tmp.key == val){
                    return tmp;
                }else if(tmp.key<val){
                    tmp = tmp.right;
                }else {
                    tmp = tmp.left;
                }
            }
            System.out.println("没有改值");
            return null;
        }
    }

    /**
     * 查找最小节点
     */
    private AVLTreeNode minimum(AVLTreeNode tree){
        if(tree == null){
            return null;
        }
        AVLTreeNode tmp = tree;
        while(tmp.left!=null){
            tmp = tmp.left;
        }
        return tmp;
    }

    public int minimum(){
        AVLTreeNode p = minimum(root);
        if(p!=null){
            return p.key;
        }
        return -1;
    }

    /**
     * 查找最大节点
     */
    private AVLTreeNode maximum(AVLTreeNode tree){
        if(tree == null){
            return null;
        }
        AVLTreeNode tmp = tree;
        while(tmp.right!=null){
            tmp = tmp.right;
        }
        return tmp;
    }

    public int maximum(){
        AVLTreeNode p = maximum(root);
        if(p!=null){
            return p.key;
        }
        return -1;
    }

    /**
     * LL:左左对应的情况(左单旋转)
     */
    private AVLTreeNode leftLeftRotation(AVLTreeNode k2){
        AVLTreeNode k1;
        // 完成旋转
        k1 = k2.left;
        k2.left = k1.right;
        k1.right = k2;
        // 更新高度
        k2.height = max( height(k2.left),height(k2.right))+1;
        k1.height = max(height(k1.left),k2.height)+1;

        return k1;
    }

    /**
     * RR:右右对应的情况(右单旋转)
     */
    private AVLTreeNode rightRightRotation(AVLTreeNode k2){
        AVLTreeNode k1;
        // 完成旋转
        k1 = k2.right;
        k2.right = k1.left;
        k1.left = k2;
        // 更新高度
        k2.height = max(height(k2.left),height(k2.right))+1;
        k1.height = max(height(k1.right),k2.height)+1;

        return k1;

    }

    /**
     * LR:左右对应的情况(先左旋，后右旋)
     */
    private AVLTreeNode leftRightRotation(AVLTreeNode k1){
        k1.left = rightRightRotation(k1.left);
        return leftLeftRotation(k1);
    }

    /**
     * RL:右左对应的情况(先右旋，后左旋)
     */
    private AVLTreeNode rightLeftRotation(AVLTreeNode k1){
        k1.right = leftLeftRotation(k1.right);
        return rightRightRotation(k1);
    }

    /**
     * 插入节点
     */
    public AVLTreeNode insert(AVLTreeNode tree,int val){
        // 实质是完成了插入操作
        if(tree == null){
            tree = new AVLTreeNode(val,null,null);
            if(tree == null){
                System.out.println("ERROR:create avltree node failed");
                return null;
            }
        }else {
            if(val< tree.key){
                // 插入到左子树
                tree.left = insert(tree.left,val);
                // 插入节点后，判断根节点是否失衡，若失衡，则平衡树
                if(height(tree.left)-height(tree.right) == 2){
                    if(val<tree.left.key){
                        // LL
                        tree = leftLeftRotation(tree);
                    }else{
                        // LR
                        tree = leftRightRotation(tree);
                    }
                }
            }else if( val > tree.key){
                tree.right = insert(tree.right,val);
                if(height(tree.right)-height(tree.left) ==2){
                    if(val>tree.right.key){
                        // RR
                        tree = rightRightRotation(tree);
                    }else{
                        // RL
                        tree = rightLeftRotation(tree);
                    }
                }
            }else{
                System.out.println("添加失败，不允许添加相同的节点");
            }
        }

        tree.height = max(height(tree.left),height(tree.right))+1;
        return  tree;

    }

    public void insert(int val){
        root = insert(root,val);
    }

    /**
     * 删除节点
     */
    public AVLTreeNode remove(AVLTreeNode tree , AVLTreeNode z){
        // 根为空 或者 没有要删除的节点，直接返回null。
        if(tree == null || z == null){
            return null;
        }else{
            if(z.key<tree.key){  // 待删除的节点在"tree的左子树"中
                tree.left = remove(tree.left,z);
                // 删除节点后，若AVL树失去平衡，则进行相应的调节。
                if(height(tree.right)-height(tree.left)==2){
                    AVLTreeNode r = tree.right;
                    if(height(r.left)>height(r.right)){
                        tree = rightLeftRotation(tree);
                    }else{
                        tree = rightRightRotation(tree);
                    }
                }
            }else if (z.key > tree.key){ // 待删除的节点在"tree的右子树"中
                tree.right = remove(tree.right,z);
                // 删除节点后，若AVL树失去平衡，则进行相应的调节。
                if(height(tree.left)-height(tree.right)==2){
                    AVLTreeNode l =tree.left;
                    if(height(l.right)>height(l.left)){
                        tree = leftRightRotation(tree);
                    }else {
                        tree = leftLeftRotation(tree);
                    }
                }
            }else{  // tree是对应要删除的节点。
                // tree的左右孩子都非空
                if((tree.left!=null) && (tree.right!=null)){
                    if(height(tree.left)>height(tree.right)){

                         // 如果tree的左子树比右子树高；
                         // 则(01)找出tree的左子树中的最大节点
                         //   (02)将该最大节点的值赋值给tree。
                         //   (03)删除该最大节点。
                         // 这类似于用"tree的左子树中最大节点"做"tree"的替身；
                         // 采用这种方式的好处是：删除"tree的左子树中最大节点"之后，AVL树仍然是平衡的。
                        AVLTreeNode max = maximum(tree.left);
                        tree.key = max.key;
                        tree.left = remove(tree.left,max);
                    }else{
                         // 如果tree的左子树不比右子树高(即它们相等，或右子树比左子树高1)
                         // 则(01)找出tree的右子树中的最小节点
                         //   (02)将该最小节点的值赋值给tree。
                         //   (03)删除该最小节点。
                         // 这类似于用"tree的右子树中最小节点"做"tree"的替身；
                         // 采用这种方式的好处是：删除"tree的右子树中最小节点"之后，AVL树仍然是平衡的。
                        AVLTreeNode min = minimum(tree.right);
                        tree.key = min.key;
                        tree.right = remove(tree.right,min);
                    }
                }else{                 // tree的左右孩子都为空
                    AVLTreeNode tmp = tree;
                    tree = (tree.left!=null)? tree.left :tree.right;
                    tmp = null;
                }
            }
        }
        return tree;
    }

    public void remove(int val){
        AVLTreeNode z;
        if((z= search(val))!=null){
            root = remove(root,z);
        }
    }

}
```

- AVLTreeTest.java
```java
package AVLTree;

public class AVLTreeTest {
    public static void main(String[] args) {
        AVLTree tree = new AVLTree();
        tree.insert(3);
        tree.insert(2);
        tree.insert(1);
        tree.insert(4);
        tree.insert(5);
        tree.insert(6);
        tree.insert(7);
        tree.insert(16);
        tree.insert(15);
        tree.insert(14);
        tree.insert(13);

        tree.remove(4);

        tree.PreOrder();


    }
}


```