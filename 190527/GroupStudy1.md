# 1.다항식 곱셈

* 첫 시도시 exp배열(지수배열)이 숫자가 겹치게 나와서 실패
* 객체생성 메소드에서 최초에 썼던 coefx 와 coefy 를 반대로 썼더니 결과값이 제대로 나옴

~~~java
package test;
import java.util.ArrayList;
class Multiple{
	Multiple(){}
	public int[] add1(int[] expx,int[] expy,int[] coefx,int[] coefy) {
		int i=0;
		int j=0;
		ArrayList<Integer> list = new ArrayList<>();
		while(i<expx.length && j<expy.length) {
			if(expx[i]==expy[j]) {
				list.add(coefx[i++]+coefy[j++]);
			}else if(expx[i]>expy[j]) {
				list.add(coefx[i++]);
			}else if(expx[i]<expy[j]) {
				list.add(coefy[j++]);
			}		
		}
			for( ; i<expx.length;i++) {
				list.add(coefx[i]);
			}
			for( ; j<expy.length;j++) {
				list.add(coefy[j]);
			}		
			int result[] = new int[list.size()];
			for(int k=0;k<list.size();k++) {
					result[k] = list.get(k);
			}
			return result;	
	}
	public int[] add2(int[] expx,int[] expy){
		int i=0;
		int j=0;
		ArrayList<Integer> list = new ArrayList<>();
		while(i<expx.length && j<expy.length) {
			if(expx[i]==expy[j]) {
				list.add(expx[i++]);
						j++;
			}else if(expx[i]>expy[j]) {
				list.add(expx[i++]);
			}else if(expx[i]<expy[j]) {
				list.add(expy[j++]);
			}		
		}
			for( ; i<expx.length;i++) {
				list.add(expx[i]);
			}
			for( ; j<expy.length;j++) {
				list.add(expy[j]);
			}
		int result[] = new int[list.size()];
		for(int k=0;k<list.size();k++) {
				result[k] = list.get(k);
		}
		return result;	
	}
}
public class Coef {
	public static void main(String[] args) {
		int[] coefx = {1,1};
		int[] coefy = {5,-10,5,-10};
		int[] expx = {1,0};
		int[] expy = {3,2,1,0};
		int[][] exp = new int[expx.length][expy.length];
		int[][] coef = new int[coefx.length][coefy.length];
		for(int j=0;j<coefy.length;j++) {
			for(int i=0;i<coefx.length;i++) {
				coef[i][j]=coefx[i]*coefy[j];
			}
		}
		for(int j=0;j<expy.length;j++) {
			for(int i=0;i<expx.length;i++) {
				exp[i][j]=expx[i]+expy[j];
			}
		}
		Multiple aa= new Multiple();
		int a1[]=aa.add1(exp[0], exp[1], coef[0], coef[1]);
		for(int semi : a1) {
			System.out.print(semi+" ");
		}
		System.out.println();
		int[] a2=aa.add2(exp[0], exp[1]);
		for(int semi : a2) {
			System.out.print(semi+" ");
		}
		System.out.println();
	}
}
~~~



# 2.Stack 문제(프로그래머스 쇠막대기)

* 열린 괄호와 닫힌 괄호로 이루어진 String 변수를 이용한 문제

* 열린 괄호 다음 바로 닫힌 괄호가 들어오면 레이저(=쇠막대기를 나누는 역할)

* 열린 괄호 ~ 닫힌 괄호 = 쇠막대기

* 첫 문제를 접했을 때 어떻게 접근해야 할지 고민되었고 Stack 에 대해 아는 정보가 많이 없어서 Stack 함수에 대해 검색 후 활용

* Stack.push / Stack.pop / Stack.size 를 이용하여 문제 해결

* Stack.push : 열린 괄호를 인식시 Stack 에 저장

* Stack.pop : 닫힌 괄호를 인식시 Stack 에 저장된 열린 괄호값을(=Stack의 size를) 1 감소

* Stack.size : Stack에 저장된 열린 괄호 갯수

  ~~~ java
  package test;
  
  import java.util.Stack; 
  
  class Sq{
  Sq(){}
  int solution(String arrangement) {
      int answer = 0;
      Stack<Character> stack = new Stack<Character>();
      
      for(int i=0;i<arrangement.length();i++) {
      	if(arrangement.charAt(i)=='(') {
      		stack.push(arrangement.charAt(i));
      	} else {
              stack.pop();
              if (arrangement.charAt(i-1) == '(')
                  answer+=stack.size();
              else
                  answer++;
          }
      }
      return answer;
      }
  }
  public class StackQueue {
  	public static void main(String[] args) {
  		Sq ex = new Sq();
  		String col = "()(((()())(())()))(())";
  		int result = ex.solution(col);
  		System.out.println(result);
  	}
  }
  ~~~

# 3.배열 회전 문제

1. 정사각 배열을 모두 시계방향으로 회전시킴(=RotateMatrix)
2. 정사각 배열을 홀수번째 테두리는 시계,짝수번째 테두리는 반시계 방향으로 회전시킴 (=RotateMatrix1)

* 상,하,좌,우로 삼각형 모양 or 사다리꼴 모양으로 보고 생각
* 1. 상 : 시계방향 = j+1열로 이동 / 반시계방향=j-1열로 이동
  2. 하 : 시계방향 = j-1열로 이동 / 반시계방향=j+1열로 이동
  3. 좌 : 시계방향=i-1행으로 이동 / 반시계방향=i+1행으로 이동
  4. 우 : 시계방향=i+1행으로 이동 / 반시계방향=i-1행으로 이동
* 배열의 길이(행/열의 길이) 가 홀수일때는 가운데 숫자는 회전하지 않으므로 같은 숫자를 지정

~~~java
package test;

public class RotationMatrix {
	public static void main(String[] args) {
		int[][] arr = { { 1, 2, 3 }, { 4, 5, 6 }, { 7, 8, 9 } };
		int[][] arr1 = { { 1, 2, 3, 4, 5 }, { 6, 7, 8, 9, 10 }, { 11, 12, 13, 14, 15 }, { 16, 17, 18, 19, 20 },
				{ 21, 22, 23, 24, 25 } };
		int[][] arr2 = new int[10][10];
		int count = 1;
		for (int i = 0; i < arr2.length; i++) {
			for (int j = 0; j < arr2[i].length; j++) {
				arr2[i][j] = count++;
			}
		}
		// rotateMatrix testCase
		printMatrix(arr);
		printMatrix(rotateMatrix(arr));
		printMatrix(arr1);
		printMatrix(rotateMatrix(arr1));
		printMatrix(arr2);
		printMatrix(rotateMatrix(arr2));

		// rotateMatrix1 testCase
		printMatrix(arr);
		printMatrix(rotateMatrix1(arr));
		printMatrix(arr1);
		printMatrix(rotateMatrix1(arr1));
		printMatrix(arr2);
		printMatrix(rotateMatrix1(arr2));
	}

	public static int[][] rotateMatrix(int[][] arr) {
		int[][] result = new int[arr.length][arr[0].length];
		int k = arr.length - 1;
		for (int i = 1; i < arr.length; i++) {
			for (int j = 0; j < i; j++) {
				if (i + j <= k)
					result[i - 1][j] = arr[i][j];
			}
		}
		for (int i = 0; i < arr.length; i++) {
			for (int j = 1; j <= i; j++) {
				if (i + j > k)
					result[i][j - 1] = arr[i][j];
			}
		}
		for (int j = 0; j < arr.length; j++) {
			for (int i = 0; i < j; i++) {
				if (i + j >= k)
					result[i + 1][j] = arr[i][j];
			}
			for (int i = 0; i <= j; i++) {
				if (i + j < k)
					result[i][j + 1] = arr[i][j];
			}
		}
		int m = arr.length / 2;
		if (arr.length % 2 == 1)
			result[m][m] = arr[m][m];
		return result;
	}

	public static int[][] rotateMatrix1(int[][] arr) {
		int[][] result = new int[arr.length][arr[0].length];
		int k = arr.length - 1;
		if (arr.length % 2 == 0) {
			for (int i = 1; i < arr.length; i++) {
				for (int j = 0; j < i; j++) {
					if (i + j <= k && j % 2 == 0)
						result[i - 1][j] = arr[i][j];
					if (i + j >= k && i % 2 == 0)
						result[i][j + 1] = arr[i][j];
				}
			}
			for (int i = 0; i < arr.length; i++) {
				for (int j = 1; j <= i; j++) {
					if (i + j > k && i % 2 == 1)
						result[i][j - 1] = arr[i][j];
					if (i + j < k && j % 2 == 1)
						result[i + 1][j] = arr[i][j];
				}
			}
			for (int j = 0; j < arr.length; j++) {
				for (int i = 0; i < j; i++) {
					if (i + j >= k && j % 2 == 1)
						result[i + 1][j] = arr[i][j];
					if (i + j <= k && i % 2 == 1)
						result[i][j - 1] = arr[i][j];
				}
				for (int i = 0; i <= j; i++) {
					if (i + j < k && i % 2 == 0)
						result[i][j + 1] = arr[i][j];
					if (i + j > k && j % 2 == 0)
						result[i - 1][j] = arr[i][j];
				}
			}
		} else {
			for (int i = 1; i < arr.length; i++) {
				for (int j = 0; j < i; j++) {
					if (i + j <= k && j % 2 == 0)
						result[i - 1][j] = arr[i][j];
					if (i + j >= k && i % 2 == 1)
						result[i][j + 1] = arr[i][j];
				}
			}
			for (int i = 0; i < arr.length; i++) {
				for (int j = 1; j <= i; j++) {
					if (i + j > k && i % 2 == 0)
						result[i][j - 1] = arr[i][j];
					if (i + j < k && j % 2 == 1)
						result[i + 1][j] = arr[i][j];
				}
			}
			for (int j = 0; j < arr.length; j++) {
				for (int i = 0; i < j; i++) {
					if (i + j >= k && j % 2 == 0)
						result[i + 1][j] = arr[i][j];
					if (i + j <= k && i % 2 == 1)
						result[i][j - 1] = arr[i][j];
				}
				for (int i = 0; i <= j; i++) {
					if (i + j < k && i % 2 == 0)
						result[i][j + 1] = arr[i][j];
					if (i + j > k && j % 2 == 1)
						result[i - 1][j] = arr[i][j];
				}
			}
			int m = arr.length / 2;
			result[m][m] = arr[m][m];
		}
		return result;
	}

	public static void printMatrix(int[][] arr) {
		for (int i = 0; i < arr.length; i++) {
			for (int j = 0; j < arr[i].length; j++) {
				if (j > 0) {
					System.out.print(" ");
					if (arr[i][j] < 10)
						System.out.print(" ");
				} else if (j == 0 && arr[i][j] < 10)
					System.out.print(" ");
				System.out.print(arr[i][j]);
			}
			System.out.println();
		}
		System.out.println();
	}
}

~~~

