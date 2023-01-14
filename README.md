# COS PRO Java 1급

### 1차) 문제 1 - 타임머신
```Java
class Main {
    public long solution(long num) {
        
        long answer = 0;
	num++;
	long digit = 1;
	while(num/digit%10==0){
		num+=digit;
		digit*=10;
		// System.out.println(num + " "+ digit);
	}
	answer = num;
        return answer;
    }

// 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        long num = 9949999;
        long ret = sol.solution(num);

        System.out.println("solution 메소드의 반환 값은 " + ret + " 입니다.");
    }
}
```

### 1차) 문제 2 - n 소용돌이 수
```Java
import java.util.*;

class Main {
	
	int[][] pane; // 2차원 배열 전역변수
	int di[] = {0,1,0,-1}; //소용돌이 변화규칙
  int dj[] = {1,0,-1,0}; //소용돌이 변화규칙
	
	//범위 체크 함수 행:i 열:j 격자크기:n
	boolean inRange(int i, int j, int n){
		return (0<=i && i<n) && (0<=j && j<n); //행이 0이상 n미만, 열이 0이상 n미만
	}
	public int solution(int n) {
		pane = new int[n][n]; //n*n배열 선언
		int ci=0;//현재 좌표점의 위치
		int cj=0;//현재 좌표점의 위치
		int num=1; //입력할 숫자 선언 (1부터 시작)
		int k=0; //인덱스 변화를 위한 변수 >> 맨앞에 있는 규칙부터 적용하고자 0으로 선언
		
		//n*n범위 안에 있거나 해당 칸에 숫자를 넣지 않은 동안
		while(inRange(ci,cj,n) && pane[ci][cj]==0){
			pane[ci][cj]=num;
			num++;
			//다음에 넣을 좌표위치를 정하는 방법
			int ni = ci+di[k]; //다음번 좌표점 ni변수 선언, 현재좌표에 해당하는 di[k]를 더하면됨
			int nj = cj+dj[k];
			//다음번 좌표점이 범위안에 있지않거나 이미 숫자값이 들어있을 경우(0이 아닌값이 있으면)
			if(!inRange(ni,nj,n) || pane[ni][nj]!=0){
				// 인덱스 번호인 k를 1증가시키고, 그 다음 4로 나눈 나머지를 이용한 값을 적용하면 매번 끝까지 간다음 앞에 규칙으로 돌아옴 
				k = (k+1)%4;
			}
			// 정해진 좌표 규칙에 맞게 현재 i좌표와 j좌표의 위치를 구한다
			ci+=di[k];
			cj+=dj[k];
			
		}
		//값이 제대로 들어갔는지 테스트
		for(int a = 0; a<n; a++){
			for(int b=0; b<n; b++){
				System.out.print(pane[a][b]+ " ");
			}
			System.out.println();
		}
		int answer = 0;
		for(int a = 0; a<n; a++){
			answer += pane[a][a];
		}
		return answer;
	}
	
// 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        int n1 = 3;
        int ret1 = sol.solution(n1);
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret1 + " 입니다.");

        int n2 = 2;
        int ret2 = sol.solution(n2);
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret2 + " 입니다.");
    }
}
```

### 1차) 문제 3 - 체스의 나이트
```Java
import java.util.*;
class Main {
    public int solution(String pos) {
    	int answer = 0;

	//1. 이동 가능한 8가지 방향 정의 >> x,y로 몇칸 이동했는지
	int dx[] = {1,2,2,1,-1,-2,-2,-1};
	int dy[] = {2,1,-1,-2,-2,-1,1,2};

	//2. pos(현재 위치)를 숫자로 변경
	// cx:'A'를 0으로, cy:'7'을 6으로
	int cx = pos.charAt(0)-'A'; // 'A'를 숫자로 바꾸려면 'A'를 빼야함
	int cy = pos.charAt(1)-'0'-1; // '7'을 숫자로 바꾸려면 '0'을 빼고 하나씩 작으니 -1을 해준다.
	
	//3. 8가지 방향 중 각 위치로 이동 가능하면 개수 증가
	// 이동하고자 하는 위치를 구한 후
	// 해당 위치로 이동 가능하면(체스판 범위 안에 있으면)개수 증가
	for(int i=0;i<8;i++){
		int nx = cx + dx[i]; //다음번 x좌표점 = 현재 좌표점 + dx[i]번째 규칙 적용
		int ny = cy + dy[i]; //다음번 y좌표점 = 현재 좌표점 + dy[i]번째 규칙 적용
		// 다음번 좌표가 0~7 사이에 있으면 체스판 안에 위치기 때문에 이동가능
		// 이동가능한 갯수 증가
		if(nx>=0 && nx<8 && ny>=0 && ny<8){
		// System.out.println(nx+","+ny);
			answer++;
		}
	}
      return answer;
    }
    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        String pos = "A7";
        int ret = sol.solution(pos);
    	
        System.out.println("solution 메소드의 반환 값은 " + ret + " 입니다.");
    }
}
```
