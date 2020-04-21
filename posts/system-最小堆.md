---
title: "System 最小堆"
date: 2019-04-25T17:38:44+08:00
categories: [System]
---

**最大—最小堆**是最大层和最小层交替出现的[二叉树](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%8F%89%E6%A0%91)，即最大层结点的子节点属于最小层，最小层结点的子节点属于最大层。 以最大（小）层结n点为根结点的子树保有最大（小）堆性质：根结点的键值为该子树结点键值中最大（小）项。

![最大堆](https://wiki.jikexueyuan.com/project/easy-learn-algorithm/images/11.3.png)

![最小堆](https://wiki.jikexueyuan.com/project/easy-learn-algorithm/images/11.1.png)



[最大堆](https://zh.wikipedia.org/w/index.php?title=%E6%9C%80%E5%A4%A7%E5%A0%86&action=edit&redlink=1)和[最小堆](https://zh.wikipedia.org/w/index.php?title=%E6%9C%80%E5%B0%8F%E5%A0%86&action=edit&redlink=1)是[二叉堆](https://zh.wikipedia.org/wiki/%E4%BA%8C%E5%8F%89%E5%A0%86)的两种形式。

- 最大堆：根结点的键值是所有堆结点键值中最大者的堆。
- 最小堆：根结点的键值是所有堆结点键值中最小者的堆。

而最大—最小堆集结了最大堆和最小堆的优点，这也是其名字的由来。

## 主要操作

### 插入

将节点插在二叉树的最后一个叶子结点位置，然后比较它与它父亲节点的大小：如果大则停止；如果小则交换位置，然后对父亲节点递归该过程直至根节点。复杂度为{\displaystyle O(log(n))}![{\displaystyle O(log(n))}](https://wikimedia.org/api/rest_v1/media/math/render/svg/c0bedb281b1771b1dad14e5916d4979f3b57c6b8)。

一般来说，插入的位置可以不是最后一个叶子节点，可以作为任意中间节点的孩子节点插入，将这个叶子节点变为中间节点后，按上文所说的方法调整节点顺序以保证维持堆特性不变。

### 删除

要从堆中删除一个节点，用最后一个节点替换掉要删除的节点，然后调整节点顺序以维持堆特性。

## 应用

- [双端优先队列](https://zh.wikipedia.org/w/index.php?title=%E5%8F%8C%E7%AB%AF%E4%BC%98%E5%85%88%E9%98%9F%E5%88%97&action=edit&redlink=1)