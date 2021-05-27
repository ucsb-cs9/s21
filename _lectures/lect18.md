---
num: "Lecture 18"
desc: "Binary Search Trees cont."
ready: true
lecture_date: 2021-05-27 14:00:00.00-7:00
---

Recorded Lecture: [5_27_21](https://drive.google.com/file/d/1quMaw1lEkyJDshEeRBjvc3ijYRakmDzx/view?usp=sharing)

# BST Implementation Continued

```
# BinarySearchTree.py (continuing on from last lecture)

def get(self,key): # returns payload for key if it exists
	if self.root:
		res = self._get(key,self.root)
		if res:
			return res.payload
		else:
			return None
	else:
		return None

# helper method to recursively walk down the tree
def _get(self,key,currentNode): 
	if not currentNode:
		return None
	elif currentNode.key == key:
		return currentNode
	elif key < currentNode.key:
		return self._get(key,currentNode.leftChild)
	else:
		return self._get(key,currentNode.rightChild)
```
```
# pytests

from BinarySearchTree import BinarySearchTree

def test_constructBST():
	BST = BinarySearchTree()
	assert BST.root == None
	assert BST.length() == 0

def test_insertRoot():
	BST = BinarySearchTree()
	BST.put(10, "ten")
	assert BST.root.key == 10
	assert BST.root.payload == "ten"
	assert BST.root.hasLeftChild() == None
	assert BST.root.hasRightChild() == None
	assert BST.root.isLeftChild() == None
	assert BST.root.isRightChild() == None
	assert BST.root.isRoot() == True
	assert BST.root.hasAnyChildren() == None
	assert BST.root.isLeaf() == True
	assert BST.root.hasBothChildren() == None
	BST.root.replaceNodeData(20, "twenty", None, None)
	assert BST.root.key == 20
	assert BST.root.payload == "twenty"

def test_insertNodes():
	BST = BinarySearchTree()
	BST.put(10, "ten")
	BST.put(20, "twenty")
	BST.put(15, "fifteen")
	BST.put(5, "five")
	assert BST.root.key == 10
	assert BST.root.leftChild.key == 5
	assert BST.root.rightChild.key == 20
	assert BST.root.rightChild.leftChild.key == 15

def test_get():
	BST = BinarySearchTree()
	BST.put(10, "ten")
	BST.put(20, "twenty")
	BST.put(15, "fifteen")
	BST.put(5, "five")
	assert BST.get(10) == "ten"
	assert BST.get(20) == "twenty"
	assert BST.get(15) == "fifteen"
	assert BST.get(5) == "five"
	assert BST.get(30) == None
```

# BST Deletion

* We can break up deletion in three cases:
	* **Case 1:** When the node to be deleted is a leaf node (no children)
	* **Case 2:** When the node to be deleted has one child
	* **Case 3:** When the node to be deleted has two children

## Case 1: Delete a leaf node
* Find the node that needs to be deleted
* Simply remove the parent reference (either left child or right child) to the deleted node

![BSTDeleteCase1.png](BSTDeleteCase1.png)

## Case 2: Delete a node with one child
* Connect the deleted Node’s parent and the deleted Node’s child together

![BSTDeleteCase2.png](BSTDeleteCase2.png)

## Case 3: Delete a node with two children
* First find the successor (node with next greater value) in the right subtree
	* This can be done by traversing the left children of the node to be deleted’s right subtree
	* Also note that the successor will always only have **at most** one child
		* If the successor had a left child, then it wouldn’t be the successor!
* Temporarily store the successor and delete the successor from the tree
	* Deleting the successor will fall in either Case 1 or Case 2
* Replace the deleted node’s value with the successor’s value

![BSTDeleteCase3.png](BSTDeleteCase3.png)

# BST Deletion Implementation

```
# BinarySearchTree.py (continued)

def delete(self,key):
	if self.size > 1:
		nodeToRemove = self._get(key,self.root)
		if nodeToRemove:
			self.remove(nodeToRemove) # remove modifies the tree
			self.size = self.size-1
		else:
			raise KeyError('Error, key not in tree')
	elif self.size == 1 and self.root.key == key:
		self.root = None
		self.size = self.size - 1
	else:
		raise KeyError('Error, key not in tree')

# Used to remove the node and account for BST deletion cases
def remove(self,currentNode):
	# Case 1: Node to remove is leaf
	if currentNode.isLeaf():
		if currentNode == currentNode.parent.leftChild:
			currentNode.parent.leftChild = None
		else:
			currentNode.parent.rightChild = None

	# Case 3: Node to remove has both children
	elif currentNode.hasBothChildren():
		# TBD

	# Case 2: Node to remove has one child
	else:
		# Node has leftChild
		if currentNode.hasLeftChild():
			if currentNode.isLeftChild():
				currentNode.leftChild.parent = currentNode.parent
				currentNode.parent.leftChild = currentNode.leftChild
			elif currentNode.isRightChild():
				currentNode.leftChild.parent = currentNode.parent
				currentNode.parent.rightChild = currentNode.leftChild
			else: # currentNode is the Root
				currentNode.replaceNodeData(currentNode.leftChild.key,
					currentNode.leftChild.payload,
					currentNode.leftChild.leftChild,
					currentNode.leftChild.rightChild)
            
		# Node has rightChild
		else:
			if currentNode.isLeftChild():
				currentNode.rightChild.parent = currentNode.parent
				currentNode.parent.leftChild = currentNode.rightChild
			elif currentNode.isRightChild():
				currentNode.rightChild.parent = currentNode.parent
				currentNode.parent.rightChild = currentNode.rightChild
			else:
				currentNode.replaceNodeData(currentNode.rightChild.key,
					currentNode.rightChild.payload,
					currentNode.rightChild.leftChild,
					currentNode.rightChild.rightChild)
```
