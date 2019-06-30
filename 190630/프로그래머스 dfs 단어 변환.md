# 프로그래머스 dfs 단어 변환

* 최초 단어(begin)에서부터 한글자씩만 다른 경우를 찾아 돌아다니면서 찾으려는 단어(target) 에 도달할 때 끝내도록 구현함
* 첫 구현때, dfs 등의 함수를 불러오는 것을 많이 돌리게 되어 StackFlowOver 오류를 만남
* 몇몇 시행착오를 거쳐 오류가 나지 않을 정도로 수정했으나, 정확성 테스트에서 1개의 오류가 생김
* 단어를 찾는 과정이 for문을 사용해 배열의 1번째부터 탐색하는 것을 생각함
* 그렇다면, 내가 찾으려는 target이 배열의 첫번째라면 횟수가 증가하는 일이 없지 않을까 생각하고 구현해보니, 성공함.

~~~ java
class Solution {
    int answer;
    public int solution(String begin, String target, String[] words) {
        int search=0;
        String targetword="";
        for(int a=0;a<words.length;a++) {
            if(words[a].equals(target)) {
                search++;
                targetword = words[a];
                words[a]=words[0];
                words[0]=targetword;
                break;
            }
        }
        if(search==0 || begin.equals(target)) {
            answer=0;
        }
        else {
            dfs(begin,target,words,0);
        }
        return answer;
    }
    
    public void dfs(String str, String target, String[] words,int num) {
    		int len;
		String next;
		loop:
			for(int i=0;i<words.length;i++) {
				for(int j=0;j<words[i].length();j++) {
					len = words[i].length();
					if(str.substring(0,j).equals(words[i].substring(0,j)) 
							&& str.substring(j+1,len).equals(words[i].substring(j+1,len))) {
						num++;
						next = words[i];
						words[i]="***";
						if(next.equals(target)) {
							answer=num;
							break loop;
						}else {
							dfs(next,target,words,num);
						}
					} 
				}			
			}    
    }
}
~~~



