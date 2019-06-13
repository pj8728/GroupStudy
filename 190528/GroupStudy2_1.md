## 그룹스터디 문제 2회차_1

#### 3.Stack , Queue 구현

~~~ java
package test2;

class LinkedNode {// LinekedList를 구성하는 node 클래스
	int val;
	LinkedNode next; //다음 node를 가르키기 위한 객체

	LinkedNode(int val) {
		next = null;
		this.val = val;
	}
}

class LinkedList {
	LinkedNode first; // LinekedList의 첫 node
	LinkedNode last; // LinekedList의 마지막 node
	
	LinkedList() {
		first = null;
		last = null;
	}

	protected void addFirst(int val) {
		LinkedNode Fnode = new LinkedNode(val);
		Fnode.next = first;
		first = Fnode;
		if(first.next==null) {
			last = first;
		}
	}

	protected void addLast(int val) { 
		LinkedNode Lnode = new LinkedNode(val);
		if(first==null) {
			addFirst(val);
		}else {
			last.next = Lnode;
			last = Lnode;
		}
	}

	protected Boolean removeFirst() {
		LinkedNode temp = first;
		first = temp.next;
		temp = null;
		return true;
	}

	protected Boolean removeLast() {
		return false;
	}

	protected void printList() {
		LinkedNode current = first;
		while (current != null) { //current 노드가 null 아닐때 까지 실행
			System.out.println(current.val);
			current = current.next; //next 노드를 current에 덮어 씌움
		}
	}
}

class Queue extends LinkedList {
	Queue() {
		super();
	}

	public void add(int val) {
		super.addLast(val);
	}

	public void remove() {
		System.out.println("삭제 결과 : " + super.removeFirst());
	}

	public void printList() {
		System.out.println("----------queue print----------");
		super.printList();
		System.out.println("------------------------------");
	}
}



class Stack extends LinkedList{
	Stack(){
		 super(); //LinkedList의 생성자를 실행
	}
	
	public void add(int val) {
		super.addFirst(val);
	}
	
	public void remove() {
		System.out.println("삭제 결과 : " + super.removeFirst());
	}
	
	public void printList() {
		System.out.println("----------stack print----------");
		super.printList();
		System.out.println("------------------------------");
	}
}


public class Main {
	public static void main(String[] args) {
		Stack s = new Stack();
		s.add(1);
		s.add(2);
		s.add(3);
		s.add(4);
		s.add(5);
		s.printList();
		s.remove();
		s.remove();
		s.remove();
		s.printList();
		
		Queue q = new Queue();
		q.add(1);
		q.add(2);
		q.add(3);
		q.add(4);
		q.add(5);
		q.printList();
		q.remove();
		q.remove();
		q.printList();
	}
}
~~~

 
