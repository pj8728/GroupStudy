# 그룹스터디 문제 2회차

### 1. 배열 정렬 / 값 출력 (프로그래머스 정렬 1번 K번째)

* 어떤 배열에서 i번째부터 j번째까지 숫자를 받은 후 정렬
* 정렬한 배열(=semi)에서 k번째 숫자를 result 값으로 저장 후 리턴

~~~java
package test;
import java.util.Arrays;
class Sort{
	public int[] SortSelect(int[] array,int[][] com){
		int[] result = new int[com.length];
		for(int x=0;x<com.length;x++) {
			
//for y : com 배열에 i,j,k 값을 넣기 위한 반복문
			for(int y=0;y<com[x].length;y++) {
				int i=(int)(Math.random()*array.length)+1;
				int j=(int)(Math.random()*array.length)+1;
				int k=1;
				if(i<j) {
					com[x][0]=i;  com[x][1]=j;
					k=(int)(Math.random()*(j-i))+2;
					com[x][2]=k;
				}else if(i>j) {
					com[x][0]=j;  com[x][1]=i;
					k=(int)(Math.random()*(i-j))+2;
					com[x][2]=k;
				}else {
					com[x][0]=i; com[x][1]=j; com[x][2]=k;
				}
			}
//for y의 끝	
			
/*for x 반복문 이어서 semi 배열에 i번째~j번째 숫자를 넣고 정렬
result 배열에는 for x 반복 중 정렬된 semi 배열에서 k번째 숫자를 추출 후
result 배열에 결과값을 넣음.
결과적으로 com.length(=com의 행 갯수) 만큼 result 가 나옴 */
			int[] semi = new int[com[x][1]-com[x][0]+1];
			for(int col=0;col<semi.length;col++) {
				semi[col]=array[com[x][0]+col-1];
		}
			Arrays.sort(semi);
			result[x]=semi[com[x][2]-1];
		}	
//for x의 끝		

		return result;
	}
}

public class ArraySort {
	public static void main(String[] args) {
		int [] array = {1,5,2,6,3,7,4};
		int[][] com = new int[3][3];
		Sort aa = new Sort();
		int[] result = aa.SortSelect(array, com);
		for(int i=0;i<result.length;i++) {
			System.out.print(result[i]+" ");
		}
	}
}

~~~



### 2. 군수열 문제

* 문제 설명
  수열을 어떤 규칙에 의해 여러 가지 항으로 나누었을 때, 각각의 항으로 이루어진 수열을 군수열이라고 합니다.

  무한수열 S = (1), (1, 2), (1, 2, 3), (1, 2, 3, 4).... 입니다. 이 수열의 규칙은 다음과 같습니다.

  N 번째 군에는 1부터 N까지의 자연수가 크기 순서대로 있습니다.
  수열의 k 번째 항은, 군에 상관없이 맨 앞부터 세기 시작합니다. 즉, 수열 S의 4번째 항은 1이 됩니다.
  수 k가 주어질 때, 수열 S에서 k 번째 항의 수를 반환하는 solution 함수를 완성하세요.

  제한사항
  k는 50,000,000,000,000 이하의 자연수입니다.

* k가 n번째 군수열 내에 있다면 k의 위치는 이전(=n-1)군수열 까지의 항 갯수의 합보다 크고 n번째 군수열 까지의 항 갯수의 합보다 작거나 같다. (n(n-1)/2<k=<n(n+1)/2)
* 각 군수열은 1부터 n까지 1씩 증가하는 n개의 항을 갖는 수열
* 전체 중 k번째 숫자를 구할 때 : k값에서 이전 군수열까지의 항 갯수의 합을 빼면 결과가 나옴

~~~java
package test;
public class Sequence {
	public static void main(String[] args) {
    //초기 변수 지정
		long n=1;
		long a=n*(n-1)/2;
		long b=n*(n+1)/2;
		long result=0;
		long k=(long)(Math.random()*50000000000000L)+1;
    //k>a 일때 반복,k>b면 n값을 증가시켜 a,b값을 다시 지정
    //k<=b 가 될때 result 값(k-a)를 넣어줌
		while(k>a) {
			if(k<=b) {
				result = k-a;
				break;
			}else {
			n++;
			a =n*(n-1)/2;			
			b =n*(n+1)/2;
		}
		}
		System.out.println(a);
		System.out.println(k);
		System.out.println(result);	 	
	}
}
~~~
