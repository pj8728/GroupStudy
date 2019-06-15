# 그룹스터디 5회차 문제

#### 1. 프로그래머스 정렬 3번 H-Index

* h=1 로 놓고 1부터 배열의 길이(=n편의 논문)까지 비교
* h를 1씩 더해가면서(while) h 이상인 값들을 answer에 1씩 더해가며(for-if) 체크
* 합해진 answer(=h번 이상 인용된 논문의 갯수)가 h와 같을때 while문을 멈추고 answer 리턴
* 이유는 모르겠으나, 테스트 케이스 중 1개가 실패함.

~~~ java
class Solution {
    public int solution(int[] citations) {
        int answer = 0;
        int h = 1;
              
     while(h-1<citations.length){          
         for(int i=0;i<citations.length;i++){
            if(citations[i]>=h){
                answer++;
            }
        }
            if(answer==h){
                break;
            }else {
                answer=0;
                h++;
            }            
        }      
        return answer;              
    }
}
~~~



#### 2. BST(Binary Search Tree) 전위 / 중위 / 후위 탐색 (구현 부분만)

* 뿌리 데이터=D , D의 왼쪽노드=L , D의 오른쪽 노드=R 이라 할 때

* 전위 탐색(=preorder) : DLR 순 (뿌리를 먼저 읽고, 자식노드를 읽음)
* 중위 탐색(=inorder) : LDR 순 (왼쪽 - 뿌리 - 오른쪽 순으로 읽음)
* 후위 탐색(=postorder) : LRD 순 (왼쪽 - 오른쪽 - 뿌리 순으로 읽음)

~~~ java
	//DLR
	private void printPreOrder(Node current) {
		if(current==null) {
			return;
		}else {
			System.out.print(current.val+" ");
			printPreOrder(current.left);
			printPreOrder(current.right);
		}
	}

	//LDR
	private void printInOrder(Node current) {
		if(current==null) {
			return;
		}else {
			printInOrder(current.left);
			System.out.print(current.val+" ");
			printInOrder(current.right);
		}
	}

	//LRD
	private void printPostOrder(Node current) {
		if(current==null) {
			return;
		}else {
			printPostOrder(current.left);
			printPostOrder(current.right);
			System.out.print(current.val+" ");
		}
	}
~~~



#### 3. 프로그래머스 dfs/bfs 1번 타겟 넘버

* 배열의 첫번째부터 배열의 끝까지 더하고 빼는 모든 경우를 나타내봄
* 재귀함수에 대한 이해도가 아직 낮은것 같다. 구현하고 이해하는데 생각보다 오래 걸림

~~~ java
class Solution {
	int answer = 0;
    public int solution(int[] numbers, int target) {
        dfs(numbers,target, 0);
        return answer;
    }
    public void dfs(int[] numbers, int target, int k){
        if(k!=numbers.length){
            numbers[k] = numbers[k]*1;
            dfs(numbers,target,k+1);
            numbers[k] = numbers[k]*(-1);
            dfs(numbers,target,k+1);
        }else{
           int sum = 0;
        for(int i=0;i<numbers.length;i++){
            sum +=numbers[i];
        }
            if(sum==target){
                answer++;
            }
        }
    }
}
~~~

