# 프로그래머스 완전탐색 카펫(6.18 수정)

* i,j (가로와 세로의 길이) 를 조건문으로 나타내는 데 어려움을 겪음
* brown과 red의 합(=sum) 의 값의 약수에 관해 생각해보니 조건문을 나타낼만했음
* (6.18) for문 조건문에서 이상함을 느껴 재확인해보니 이중포문 break가 잘못되었음 

~~~ java
class Solution {
    public int[] solution(int brown, int red) {
        int[] answer = new int[2];
        int sum = brown+red;
        loop:
        for(int i=sum/3;i>=3;i--){
            for(int j=3;j<=sum/i;j++){
                if(i*j==brown+red && (i-2)*(j-2)==red){
                    answer[0] = i;
                    answer[1] = j;
                    break loop;
                }
            }
        }
        return answer;
    }
}
~~~

