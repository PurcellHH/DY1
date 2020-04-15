1.	实现下列多叉树节点结构与方法，并简单按下图一结构初始化一个多叉树，图中数据为节点值。按照层级遍历的方式遍历该二叉树并输出结果为图二。
![image](http://q8o7v0znl.bkt.clouddn.com/456.png)
![image](http://q8o7v0znl.bkt.clouddn.com/789.png)

**代码：**

```
import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

class Node {
    Integer val;
    List<Node> child;

    public Node(Integer val) {
        this.val = val;
    }

    /**
     * @param val
     * @return 返回添加的结点
     */
    public Node addChild(Integer val) {
        if (child == null) {
            child = new ArrayList<>();
        }
        Node node = new Node(val);
        child.add(node);
        return node;
    }
}

class Solution {
    public static void main(String[] args) {
        //初始化
        Node rootNode = new Node(1);
        Node node2 = rootNode.addChild(2);
        node2.addChild(5);
        node2.addChild(6);
        node2.addChild(7);
        rootNode.addChild(3);
        Node node4 = rootNode.addChild(4);
        node4.addChild(8);
        node4.addChild(9);

        //遍历输出
        List<List<Integer>> lists = levelOrder(rootNode);
        for (List<Integer> level : lists) {
            for (int i = 0; i < level.size(); i++) {
                if (i == 0) {
                    System.out.print(level.get(i));
                } else {
                    System.out.print("," + level.get(i));
                }
            }
            System.out.println();
        }
    }


    /**
     * 层级遍历实现
     *
     * @param rootNode
     * @return 层级List
     */
    public static List<List<Integer>> levelOrder(Node rootNode) {
        if (rootNode == null) {
            return new ArrayList<>();
        }
        Queue<Node> queue = new LinkedList<>();
        List<List<Integer>> result = new ArrayList<>();
        queue.offer(rootNode);

        while (!queue.isEmpty()) {
            int length = queue.size();  //记录层级的结点数
            List<Integer> level = new ArrayList<>();
            while (length > 0) {    //遍历层级
                Node node = queue.poll();
                if (node.child != null){    //把下一层的结点进队
                    queue.addAll(node.child);
                }
                level.add(node.val);
                length--;
            }
            result.add(level);
        }
        return result;
    }
}

```

