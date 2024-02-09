

<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
<link href="https://fonts.googleapis.com/css2?family=Work+Sans:wght@500&display=swap" rel="stylesheet">


<div>

# SDE sheet problems
## Binary Tree
### Approaches:
* ** ** :  
E.g.:  
    *   

### Problems:
1. #### [Height of Binary Tree](https://practice.geeksforgeeks.org/problems/height-of-binary-tree/1) :

**Question** :

Given a binary tree, find its height.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution {
    //Function to find the height of a binary tree.
    int height(Node node,int... h) 
    {
        if(node==null && h.length==0) return 0;
        
        if(h.length==0) return Math.max(height(node.left,1),height(node.right,1));
        
        if(node==null) return h[0];
        
        return Math.max(height(node.left,h[0]+1),height(node.right,h[0]+1));
    }
}
```  
---  

2. #### [Number of leaf nodes](https://practice.geeksforgeeks.org/problems/count-leaves-in-binary-tree/1) :

**Question** :

Given a Binary Tree of size N, You have to count leaves in it. For example, there are two leaves in following tree

        1
     /      \
   10      39
  /
5

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Tree
{
    int countLeaves(Node node) 
    {
        if(node ==null) return 0;
        if(node.left==null && node.right==null) return 1;
        return countLeaves(node.left)+countLeaves(node.right);
    }
}
```  
--- 
3. #### [Check if given Binary Tree is Height Balanced or Not](https://practice.geeksforgeeks.org/problems/check-for-balanced-tree/1) :

**Question** :

Given a binary tree, find if it is height balanced or not. 
A tree is height balanced if difference between heights of left and right subtrees is not more than one for all nodes of tree. 

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class Tree{
    int height(Node node, int h){
        if(node==null) return h;
        return Math.max(height(node.left,h+1),height(node.right,h+1));
    }
    boolean isBalanced(Node root){
        if(root==null) return true;
        if(Math.abs(height(root.left,0)-height(root.right,0))>1) return false;
        return isBalanced(root.left) && isBalanced(root.right);
    }
}
```  
--- 

4. #### [Given a binary tree, check whether it is a mirror of itself](https://practice.geeksforgeeks.org/problems/symmetric-tree/1) :

**Question** :

Given a Binary Tree. Check whether it is Symmetric or not, i.e. whether the binary tree is a Mirror image of itself or not.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class GfG{
    public static boolean isSymmetric(Node root){
        if(root==null) return true;
        return sym(root.left,root.right);
    }
    static boolean sym(Node left,Node right){
        if(left==null && right==null) return true;
        if((left==null ^ right==null)||(left.data!=right.data)) return false;
        return sym(left.left,right.right) && sym(left.right,right.left);
    }
}
```  
--- 
5. #### [Print Left View of Binary Tree](https://practice.geeksforgeeks.org/problems/left-view-of-binary-tree/1) :

**Question** :

Given a Binary Tree, print Left view of it. Left view of a Binary Tree is set of nodes visible when tree is visited from Left side. The task is to complete the function leftView(), which accepts root of the tree as argument.

Left view of following tree is 1 2 4 8.

          1
       /     \
     2        3
      /     \    /    \
     4     5   6    7
      \
        8   

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class Tree
{
    //Function to return list containing elements of left view of binary tree.
    ArrayList<Integer> leftView(Node root){
      ArrayList<Integer> sol=new ArrayList<Integer>();
      for(int i=0;i<height(root,0);i++) sol.add(Integer.MIN_VALUE);
      func(root,sol,0);
      return sol;
    }
    void func(Node node,ArrayList sol,int h){
        if(node==null) return;
        if((int)sol.get(h)==Integer.MIN_VALUE) sol.set(h,node.data);
        func(node.left,sol,h+1);
        func(node.right,sol,h+1);
    }
    int height(Node node, int h){
        if(node==null) return h;
        return Math.max(height(node.left,h+1),height(node.right,h+1));
    }
}
```  
--- 
6. #### [Print Bottom View of Binary Tree](https://practice.geeksforgeeks.org/problems/bottom-view-of-binary-tree/1) :

**Question** :

Given a Binary Tree, The task is to print the bottom view from left to right. A node x is there in output if x is the bottommost node at its horizontal distance. The horizontal distance of the left child of a node x is equal to a horizontal distance of x minus 1, and that of a right child is the horizontal distance of x plus 1. 

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n log n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    //Function to return a list containing the bottom view of the given tree.
    void width(Node node, int i, int[] dim){
        if(node==null) return;
        if(i<dim[0]) dim[0]=i;
        if(i>dim[1]) dim[1]=i;
        if(node.left!=null) width(node.left,i-1,dim);
        if(node.right!=null) width(node.right,i+1,dim);
    }
    void func(Node root, HashMap<Integer,Integer> map, ArrayList<Integer> arr, int h, int i){
        if(root==null) return;
        if(arr.get(i)==0){
            arr.set(i,root.data);
            map.put(i,h);
        }
        else{
            if(h>=map.get(i)){
                arr.set(i,root.data);
                map.put(i,h);
            }
        }
        func(root.left,map,arr,h+1,i-1);
        func(root.right,map,arr,h+1,i+1);
    }
    public ArrayList <Integer> bottomView(Node root)
    {
        int[] dim=new int[2];
        width(root,0,dim);
        ArrayList<Integer> arr=new ArrayList<Integer>();
        for(int i=0;i<dim[1]-dim[0]+1;i++) arr.add(0);
        HashMap<Integer,Integer> map=new HashMap<Integer,Integer>();
        func(root,map,arr,0,0-dim[0]);
        return arr;
    }
}
```  
---  
7. #### [Diameter of a Binary Tree](https://practice.geeksforgeeks.org/problems/diameter-of-binary-tree/1) :

**Question** :

The diameter of a tree (sometimes called the width) is the number of nodes on the longest path between two end nodes. The diagram below shows two trees each with diameter nine, the leaves that form the ends of the longest path are shaded (note that there is more than one path in each tree of length nine, but no path longer than nine nodes). 

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(h)$ 

```java
class Solution {
    // Function to return the diameter of a Binary Tree.
    int func(Node root, int h, int[] max){
        if(root==null) return h;
        if(root.left==null && root.right==null) return h+1;
        h+=1;
        int h1=func(root.right,h,max);
        int h2=func(root.left,h,max);
        if(h2+h1+1-2*h>max[0]) max[0]= h2+h1+1-2*h;
        return Math.max(h2,h1);
    }
    int diameter(Node root) {
        int []max={1};
        func(root,0,max);
        return max[0];
    }
}

```  
---  
8. #### [Connect Nodes at Same Level](https://practice.geeksforgeeks.org/problems/connect-nodes-at-same-level/1) :

**Question** :

Given a Binary Tree, The task is to connect all the adjacent nodes at the same level starting from the left-most node of that level, and ending at the right-most node using nextRight pointer by setting these pointers to point the next right for each node.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Solution
{
    int height(Node root,int h){
        if(root==null) return h;
        return Math.max(height(root.left,h+1),height(root.right,h+1));
    }
    //Function to connect nodes at same level.
    void makeList(Node root, int h,Node[] arr){
        if(root==null)return ;
        if(arr[h]==null) arr[h]=root;
        else{
            arr[h].nextRight=root;
            arr[h]=arr[h].nextRight;
        }
        makeList(root.left,h+1,arr);
        makeList(root.right,h+1,arr);
    }
    public void connect(Node root)
    {
        int h;
        h=height(root,0);
        Node[] arr=new Node[h];
        for(int i=0;i<h;i++) arr[i]=null;
        makeList(root,0,arr);
    }
}
```  
---  
9. #### [Level order traversal in spiral form](https://practice.geeksforgeeks.org/problems/level-order-traversal-in-spiral-form/1) :

**Question** :

Given a Binary Tree, the task is to print the Level order traversal of the Binary Tree in spiral form i.e, alternate order.

**Intuition** :



**Approach** :



**Complexity** :  

- Time complexity: $O(n)$  

- Space complexity: $O(n)$ 

```java
class Spiral
{
    //Function to return a list containing the level order 
    //traversal in spiral form.	
    int height(Node root, int h){
        if(root==null) return h;
        return(Math.max(height(root.left,h+1),height(root.right,h+1)));
    }
    void makeSpiral(Node root, int h, ArrayList<LinkedList<Integer>> arr ){
        if(root==null) return;
        arr.get(h).addLast(root.data);
        makeSpiral(root.left,h+1, arr);
        makeSpiral(root.right,h+1, arr);
    }
    ArrayList<Integer> findSpiral(Node root) 
    {
        int h;
        h=height(root,0);
        ArrayList<LinkedList<Integer>> arr= new ArrayList<LinkedList<Integer>>();
        for(int i=0;i<h;i++) arr.add(new LinkedList<Integer>());
        ArrayList<Integer> sol=new ArrayList<Integer>();
        makeSpiral(root,0,arr);
        Iterator iter;
        for(int i=0;i<h;i++){
            if(i%2!=0) iter=arr.get(i).listIterator();
            else iter=arr.get(i).descendingIterator();
            while(iter.hasNext()) sol.add((Integer)iter.next());
        }
        return sol;
    }
}
```  
---  

</div>
