# 1.6 树/二叉查找树/平衡树
### 二叉树 中序-前序-后序 / 层序 遍历
##### 一、前序/中序/后序
* 前序遍历 [根-左-右]：先输出父节点，再遍历左子树和右子树
* 中序遍历 [左-根-右]：先遍历左子树，再输出父节点，再遍历右子树
* 后序遍历 [左-右-根]：先遍历左子树，再遍历右子树，最后输出父节点

**递归版**
```cpp
// 先序
public void preOrder(node t) {
	if (t != null) {
		cout << t.value << " ";
		preOrder(t.left);
		preOrder(t.right);
	}
}
// 中序
public void inOrder(node t) {
	if (t != null) {
		inOrder(t.left);
		cout << t.value << " ";
		inOrder(t.right);
	}
}
// 后序
public void postOrder(node t) {
	if (t != null) {
		postOrder(t.left);
		postOrder(t.right);
		cout << t.value << " ";
	}
}
```

**非递归版** (利用 **栈** )
```cpp
// 中序
public void inOrder(node t) {
	Stack s = new Stack();
	while (!s.isEmpty() || t != null) {
		if (t != null) {
			s.push(t);
			t = t.left;
		} else {
			t = s.pop();
			cout << t.value << " ";
			t = t.right
		}
	}
}
```
参考链接：
https://www.cnblogs.com/bigsai/p/11393609.html

##### 二、层序 (用 队列 实现)
cpp
```cpp
int levelOrder(Node* root) {
	if (root == NULL) return;

	queue<Node*> q1;
	q1.push(root);
	int cursize = 1, maxsize = 1;
	while (!q1.empty()) {
		Node* temp = q1.front();
		q1.pop();
		cursize--;
		cout << temp->val; // 只要当前层里的节点没打印完，就继续逐个打印

		if (temp->left != NULL)
			q1.push(temp->left);
		if (temp->right != NULL)
			q1.push(temp->right);
		if (cursize == 0) {
			cursize = q1.size();	// 记录每一层有多少个节点
			maxsize = cursize > maxsize ? cursize : maxsize; //记录树的最大宽度
		}
	}
	return maxsize;
}
```

python
```python
    def zigzagLevelOrder(self, root):
        res = list()
        if root:
            queue = deque()
            queue.append(root)

            while len(queue) > 0:
                # 记录每一层节点数量
                level_count = len(queue)
                cur_list = deque()

                # 把每层N节点都遍历一遍，每遍历完一层，就将其放入到res里面
                while level_count > 0:
                    node = queue.popleft()
                    if len(res) % 2 == 0:
                        cur_list.append(node.val)
                    else:
                        cur_list.appendleft(node.val)

                    if node.left:
                        queue.append(node.left)
                    if node.right:
                        queue.append(node.right)
                    level_count -= 1
                res.append(list(cur_list))
        return res
```

参考链接：
* https://blog.csdn.net/weixin_42245930/article/details/95175434
* https://www.cnblogs.com/LUO77/p/5839273.html