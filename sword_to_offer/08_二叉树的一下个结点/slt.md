### 思路1 根据二叉树的中序遍历的特点来找

对于给定的结点，大体上可以分为3种情况。

1. 这个结点有右子树。那么下一个结点就是右子树的最左结点。若没有右子树则：
2. 这个结点是其父节点的左子节点。那么下一个结点就是这个结点的父节点。若是右子节点则：
3. 这个结点是其父节点的右子节点。那么沿着其父节点向上遍历，直到找到一个是其父节点的左子节点的结点。这个父节点就是下一个结点。若找不到这样一个结点，则说明当前结点就是最后一个结点。

if (has right child):
    return leftest node of right child

else if (is left child of parent):
    return parent

else if (is right child of parent):
    find first ancester node(labeled as B) which itself is left child of B's parent (labeled as A), then return A. if no such node as B, means no next node, current input node is the last node.
