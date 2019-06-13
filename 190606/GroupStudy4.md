## GroupStudy 4주차 문제 中 정렬

* 프로그래머스 정렬 '가장 큰 수' 문제
* Arrays.sort 를 단순히 사용할 때 문제가 생겨 정렬 중 조건을 주는 것이 있는지 찾아본 결과, compareTo 라는 것을 사용하여 전후 문자열을 합해서 int형으로 볼 때 큰 숫자가 되는 쪽으로 정렬이 되게 만듬
* 인터넷에서 찾아보던 구문들과 좀 다르지만, 결과값이 잘 나옴. 구문에 대한 숙지가 좀 더 필요할듯

~~~ java
package test2;

import java.util.Arrays;
import java.util.Comparator;

public class MaxSort {

	public static void main(String[] args) {
		int[] numbers = {10, 0, 0, 0, 0};

		String answer = "";
		String[] str = new String[numbers.length];

		for (int i = 0; i < str.length; i++) {
			str[i] = Integer.toString(numbers[i]);
		}

		Arrays.sort(str,(o1,o2) -> (o2+o1).compareTo(o1+o2));
		
		//Arrays.sort(str, new Comparator<String>() {
		//    public int compare(String o1, String o2) {
		//	return (o2+o1).compareTo(o1+o2);
		//	}
		//});
		
		for (int i = 0; i < str.length; i++) {
			System.out.print(str[i]+" ");
		}

		System.out.println();

		if(str[0].equals("0")) {
			answer="0";
		}else {
			for (int i = 0; i < str.length; i++) {
				answer += str[i];
			}
		}
		
		System.out.println(answer);

	}

}

~~~

