# BST(Binary Search Tree)

1. add() : Node를 추가하여 Tree를 구성/재구성
2. search() : 검색하고자하는 value가 Tree에 존재하는지 확인
3. getMinVal() / getMaxVal() : Tree내 최대/최소값 확인
4. remove() : Tree내 원하는 값을 삭제하고, 삭제결과를 확인
5. printTree() : 전위, 중위, 후위, level 순서로 Tree를 조회하는 각각의 메소드를 구현

~~~ java
package test2;

import java.util.ArrayList;
import java.util.LinkedList;
import java.util.List;
import java.util.Queue;

class Node {
	Node left;
	Node right;
	int val;

	Node(int val) {
		left = right = null;
		this.val = val;
	}
}

class BinarySerachTree {
	private Node root;

	public BinarySerachTree() {
		root = null;
	}

	public void add(int val) {
		Node newNode = new Node(val);
		Node current = root;
		if(root == null) {
			root = newNode;
		}else {
			while(current!=null) {
				if(current.val < val) {
				if(current.right != null) {
					current = current.right;
				}else {
					current.right = newNode;
					break;
				}
			}else if(current.val>val) {
				if(current.left != null) {
					current = current.left;
				}else {
					current.left = newNode;
					break;
				}
			}
			}
		}
		
	}

	public Boolean search(int val) {
		Node current = root;
		while(current!=null) {
			if(current.val>val) {
				current = current.left;
			}else if(current.val<val) {
				current = current.right;
			}else {
				return true;
			}
		}
		return false;
	}

	public Boolean remove(int val) {
		if (root != null) {
			Node current = root;
			Node prev = null;
			if (root.val == val) { // 루트가 삭제할 노드인 경우
				current = root;
			} else { // 루트가 삭제대상이 아닌 경우
				prev = root;
				if (val < root.val)
					current = root.left;
				else
					current = root.right;
				while (current != null) { // 만약 삭제하려는 값이 없으면 current는 null값이 된다.
					if (val == current.val)
						break;
					else {
						prev = current;
						if (val < current.val)
							current = current.left;
						else
							current = current.right;
					}
				}
			}
			if (current != null) { // 삭제한 값을 찾은 경우
				if (current.left == null && current.right == null) { // 삭제할 노드의 하위노드가 없을 때
					if (prev != null) { // 삭제할 대상노드의 이전노드가 root가 아닐 때
						if (current == prev.left) // 이전노드의 왼쪽노드 == 삭제할 노드
							prev.left = null;
						else if (current == prev.right)// 이전노드의 오른쪽노드 == 삭제할 노드
							prev.right = null;
					} else
						root = null;
				} else { // 삭제할 노드의 하위노드가 존재할 때
					if (current.left != null) {
						Node leftMax = current.left;
						Node leftMaxParent = current;
						for (; leftMax.right != null; leftMaxParent = leftMax, leftMax = leftMax.right)
							;
						int maxValue = leftMax.val;
						if (leftMax == leftMaxParent.left)
							leftMaxParent.left = leftMax.left;
						else if (leftMax == leftMaxParent.right)
							leftMaxParent.right = leftMax.left;
						leftMax.left = null;
						current.val = maxValue;
					} else if (current.right != null) {
						Node rightMin = current.left;
						Node rightMinParent = current;
						for (; rightMin.right != null; rightMinParent = rightMin, rightMin = rightMin.left)
							;
						int minValue = rightMin.val;
						if (rightMin == rightMinParent.left)
							rightMinParent.left = rightMin.right;
						else if (rightMin == rightMinParent.right)
							rightMinParent.right = rightMin.right;
						rightMin.left = null;
						current.val = minValue;
					}
				}
				return true;
			} else
				return false;
		} else
			return false;
	}

	private int getkMinVal() {
		if (root == null)
			return Integer.MIN_VALUE;
		else {
			Node current = root;
			while (current.left != null)
				current = current.left;
			return current.val;
		}
	}

	private int getkMaxVal() {
		if (root == null)
			return Integer.MAX_VALUE;
		else {
			Node current = root;
			while (current.right != null)
				current = current.right;
			return current.val;
		}
	}
	

	public void printTree() {
		System.out.print("[Print tree]");
		System.out.printf("\nMin value: %d", getkMinVal());
		System.out.printf("\nMax value: %d", getkMaxVal());
		System.out.print("\nIn-order : ");
		printInOrder(this.root);
		System.out.print("\nPre-order : ");
		printPreOrder(this.root);
		System.out.print("\nPost-order : ");
		printPostOrder(this.root);
		System.out.print("\nLevel-order : ");
		printLevelOrder(this.root);
	}

	private void printInOrder(Node current) {
		if(current == null) {
			return;
		}else {
			System.out.print(current.val+" ");
			printInOrder(current.left);
			printInOrder(current.right);
		}
	}

	private void printPreOrder(Node current) {
		if(current == null) {
			return;
		}else {
			printPreOrder(current.left);
			System.out.print(current.val+" ");
			printPreOrder(current.right);
		}
	}
	

	private void printPostOrder(Node current) {
		if(current == null) {
			return;
		}else {
			printPostOrder(current.right);
			System.out.print(current.val+" ");
			printPostOrder(current.left);
		}
	}
	

	private void printLevelOrder(Node current) {
		List<List<Integer>> result = new ArrayList<>();
		if (root == null)
			return;
		Queue<Node> q = new LinkedList<>();
		q.offer(root);
		while (!q.isEmpty()) {
			List<Integer> level = new ArrayList<>();
			int size = q.size();
			for (int i = 0; i < size; i++) {
				Node node = q.poll();
				level.add(node.val);
				if (node.left != null)
					q.offer(node.left);
				if (node.right != null)
					q.offer(node.right);
			}
			result.add(level);
		}
		System.out.println(result);
	}
}

public class Main2 {
	public static void main(String[] args) {
		int arr[] = { 8, 4, 2, 1, 3, 6, 5, 7, 12, 10, 9, 11, 14, 13, 15 };
		BinarySerachTree bst = new BinarySerachTree();
		for (int i = 0; i < arr.length; i++) {
			bst.add(arr[i]);
		}

		bst.printTree();
		System.out.println();
		System.out.print("\n--------------------");
		System.out.print("\nremove data : " + 4);
		bst.remove(4);
		System.out.print("\nremove data : " + 15);
		bst.remove(15);
		System.out.print("\nremove data : " + 2);
		bst.remove(2);
		System.out.println("\n-------------------\n");
		bst.printTree();
	}
}

~~~

