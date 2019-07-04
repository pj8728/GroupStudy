## 프로그래머스 DFS 여행경로

* ICN 에서 시작해서 여행 경로를 만드는 DFS형 문제
* 배열을 2번째 열로 정렬하고 시작
* 첫번째 (k=0) 일때 ICN을 탐색, 최초 ICN 탐색된 위치에서 2번째 열 값이 다음 시작점이 될 수
   있는지 여부를 보고 가능하다면 answer에 1열값(ICN)과 2열값(같은 행의 String값) 을 넣음
* k=1부터 k=tickets.length-1 까지는 answer에 마지막에 들어간 값을 시작점으로 두고, 배열의
  1열을 탐색해 k=0일때와 같은 형식으로 비교하여 answer[k] 값을 넣어줌
* 위의 과정간에 표를 중복으로 사용하지 않기 위해 tickets 의 i행 1열 값을 "***" 로 변경
* k=tickets.length 일 때 "***" 이 아닌 값을 찾아서 그 값과 같은 행의 2열 값을 answer[k] 즉 
  answer 배열의 마지막에 넣어주고, dfs를 끝냄

* 구현한 코드에 문제가 없다고 생각했으나, 어떤 이유때문인지 정확성 테스트 1번 케이스가 실패, 수정해야 할듯함.

~~~ java
import java.util.Arrays;
import java.util.Comparator;

class Solution {
    public String[] solution(String[][] tickets) {
    String[] answer = new String[tickets.length+1];
	Arrays.sort(tickets, new Comparator<String[]>() {
	    public int compare(String[] o1,String[] o2) {
		    String s1 = o1[1];
			String s2 = o2[1];
			return s1.compareTo(s2);
		}
	});	
	dfs(tickets,answer,0,"ICN");
    return answer;      
    }
    
public void dfs(String[][] tickets,String[] answer,int k,String start) {
    if(k==0) {
        loop:
            for(int i=0;i<tickets.length;i++) {
            	if(tickets[i][0].equals(start)) {
                 for(int j=0;j<tickets.length;j++){
                    if(tickets[i][1].equals(tickets[j][0])){
                    answer[0]=tickets[i][0];
            		answer[1]=tickets[i][1];
            		tickets[i][0]="***";
            		break loop; 
                    }
                 }
               }
            }
    	}
    	else if(k<tickets.length){
    	loop:
    	for(int i=0;i<tickets.length;i++) {
    		if(tickets[i][0].equals(start)) {
                for(int j=0;j<tickets.length;j++){
                    if(tickets[i][1].equals(tickets[j][0])){
                    answer[k]=tickets[i][1];
    		    	tickets[i][0]="***";
    			    break loop;  
                    }
                }
    		}
    	}
        }
        else if(k==tickets.length){
            loop:
    	for(int i=0;i<tickets.length;i++) {
    		if(tickets[i][0].equals(start)) {
                    answer[k]=tickets[i][1];
    			    break loop;  
    		     }
             }
    	}
    	if(k!=tickets.length) {
    		if(k==0) {
    			dfs(tickets,answer,k+2,answer[k+1]);
    		}else {
    			dfs(tickets,answer,k+1,answer[k]);
    		}
    	}
    }
}
~~~

