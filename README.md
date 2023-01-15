# COS PRO Java 1급 - 모의고사1

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

### 1차) 문제 4 - 병합 and 정렬
```Java
import java.util.*;

class Main {
    public int[] solution(int[] arrA, int[] arrB) {
	//1. 각 배열의 시작 인덱스 번호를 0으로 초기화
        int arrA_idx = 0, arrB_idx = 0;
        int arrA_len = arrA.length;
        int arrB_len = arrB.length;
	//answer 변수 생성 : 배열 크기는 arrA, arrB 두 배열의 길이의 합
        int answer[] = new int[arrA_len + arrB_len];
        int answer_idx = 0;
	//2. 각 배열의 맨 앞 인덱스부터 비교해서 둘 중 작은 값을 answer배열에 추가
	//(반복 조건: 인덱스 < 배열 길이)
	//(종료 조건: 인덱스 == 배열 길이)
        while(arrA_idx<arrA_len && arrB_idx<arrB_len){
		//if 배열 A의 값이 배열 B의 값보다 작을 경우 >> answer에 A값을 넣는다.
		//else 배열 B의 값이 배열 A의 값보다 작을 경우 >> answer에 B값을 넣는다.
		if(arrA[arrA_idx] < arrB[arrB_idx])
			answer[answer_idx++] = arrA[arrA_idx++];
		else 
                	answer[answer_idx++] = arrB[arrB_idx++];
        }
	// 3. 두 배열 중 하나가 끝까지 모두 수행되면
	// 남은 배열의 데이터를 순서대로 넣기
        while(arrA_idx < arrA_len)
        	answer[answer_idx++] = arrA[arrA_idx++];
        while(arrB_idx < arrB_len)
        	answer[answer_idx++] = arrB[arrB_idx++];
        return answer;
    }
    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        int[] arrA = {-2, 3, 5, 9};
        int[] arrB = {0, 1, 5};
        int[] ret = sol.solution(arrA, arrB);
 
 	System.out.println("solution 메소드의 반환 값은 " + Arrays.toString(ret) + " 입니다.");
    }
}
```

### 1차) 문제 5 - 가장 많은 표를 받은 후보 번호 찾기
```Java
// 다음과 같이 import를 사용할 수 있습니다.
import java.util.*;
class Main {
    public int[] solution(int N, int[] votes) {
        // 1. 후보자별 득표수를 계산한다.
	//votes의 원소를 하나씩 읽어와서 voteCounter의 index번호와 같으면 갯수를 증가시킨다.
        int voteCounter[] = new int[11];
        for (int i = 0; i < votes.length; i++) {
            voteCounter[votes[i]] += 1;
        }
	// 2. 최대득표수(maxVal)와 최대 득표수를 얻은 후보 수(cnt)를 계산한다.
	// 최댓값이 변경되면 cnt = 1,
	// 최댓값과 같은 값이 다시 나오면 같은 최대 득표자가 또 있는 것이므로 cnt+=1
        int maxVal = 0;
        int cnt = 0;
        for (int i = 1; i <= N; i++) { //0은 의미없기에 1부터 시작하면된다.
            if (maxVal < voteCounter[i]) {
                maxVal = voteCounter[i];
                cnt = 1;
            }
            else if(maxVal == voteCounter[i]){
                cnt += 1;
            }
        }
	// 3. 결과값을 넣을 answer 변수 크기를 cnt로 정하기
	// 최대 득표를 얻은 후보자 번호를 answer에 추가(2개 이상이면 후보자 번호를 오름차순 정렬)
        int answer[] = new int[cnt];
        for (int i = 1, idx = 0; i <= N; i++){
            if (voteCounter[i] == maxVal) {
                answer[idx] = i; //득표수는 voteCounter[i] 이고, 후보자의 번호는 i이다. 
                idx += 1;
            }
        }
        return answer;
    }
    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        int N1 = 5;
        int[] votes1 = {1,5,4,3,2,5,2,5,5,4};
        int[] ret1 = sol.solution(N1, votes1);
 
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + Arrays.toString(ret1) + " 입니다.");

        int N2 = 4;
        int[] votes2 = {1, 3, 2, 3, 2};
        int[] ret2 = sol.solution(N2, votes2);
 
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + Arrays.toString(ret2) + " 입니다.");
    }
}
```
### 1차) 문제 6 - 계단게임
```Java
// 다음과 같이 import를 사용할 수 있습니다.
// 다음과 같이 import를 사용할 수 있습니다.
import java.util.*;

class Main{
		// 1. func() 함수 : 매개변수로 받은 값에 대해 승리하는 경우를 리턴
		// 매개변수로 0:가위 1:바위 2:보 >> 1:바위, 2:보, 0:가위
		// 그래서 가위 >> 바위(1), 바위 >> 보(2), 보 >> 가위(0)
    public int func(int record){
        if(record == 0) return 1;
        else if(record == 1) return 2;
        return 0;
    }
    public int solution(int[] recordA, int[] recordB){
        // 2. recordA와 recordB를 순서대로 비교하여, 무승부일 때 cnt 변화없이 계속(continue)
				// 승리했을 때 cnt + 3
				// 패배했을 때 cnt -1, (단, 현재 위치가 계단의 제일 아래인 경우 그대로 0)
        int cnt = 0;
        for(int i = 0; i < recordA.length; i++){
            if(recordA[i] == recordB[i]) //무승부
                continue;
            else if(recordA[i] == func(recordB[i])) //A가 승리한 것을 냈을 경우
                cnt = cnt + 3;
            else //A가 패배한 경우
                cnt = Math.max(0, cnt - 1); //처음 위치에서 cnt가 0보다 작아지면 제자리니깐 0을 선택
        }
        return cnt;
    }
    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        int[] recordA = {2,0,0,0,0,0,1,1,0,0};
        int[] recordB = {0,0,0,0,2,2,0,2,2,2};
        int ret = sol.solution(recordA, recordB);

        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret + " 입니다.");

    }
}
```

### 1차) 문제 7 - 주식 최대 수익 찾기
```Java
// 다음과 같이 import를 사용할 수 있습니다.
import java.util.*;
class Main{
    int solution(int[] prices){
			  //1. price(가격), tmp(이전 가격 중 최소), price-tmp(현재 수익:매도-매수), 최대수익:-inf
        int inf = 1000000001;
        int tmp = inf;
        int answer = -inf;
				//주식의 가격들을 받아와서 현재수익(매도-매수) 중 최댓값(answer)
        for(int price : prices){//배열에 있는 값을 받아 price변수에 하나씩 대입
            if(tmp != inf)
                answer = Math.max(answer, price - tmp);//price - tmp : 매도가격 - 매수가격 >> 최대수익:answer과 현재수익:price-tmp 더 큰 값을 찾아서 answer에 넣어주면됨.
            tmp = Math.min(tmp, price);//매수값 : 이전 데이터들 중 최솟값을 미리 찾아놓는것.
        }
        return answer;
    }
    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        int[] prices1 = {1, 2, 3};
        int ret1 = sol.solution(prices1);
        
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret1 + " 입니다.");

        int[] prices2 = {3, 1};
        int ret2 = sol.solution(prices2);
        
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret2 + " 입니다.");
    }
}
```

### 1차) 문제 8 - 음식전문점 운영
```Java
// 다음과 같이 import를 사용할 수 있습니다.
import java.util.*;

class Main {
    interface DeliveryStore{
        public void setOrderList(String[] orderList);
        public int getTotalPrice();
    }
    
    class Food{
        public String name;
        public int price;
        public Food(String name, int price){
            this.name = name;
            this.price = price;
        }
    }
    class PizzaStore implements DeliveryStore {//피자스토어는 딜리버리스토어로부터 상속받음
        private ArrayList<Food> menuList; //메뉴판
        private ArrayList<String> orderList; //주문서
        
        public PizzaStore(){
            menuList = new ArrayList<Food>();
            String[] menuNames = {"Cheese", "Potato", "Shrimp", "Pineapple", "Meatball"};
            int[] menuPrices = {11100, 12600, 13300, 21000, 19500};
            for(int i = 0; i < 5; i++)
                menuList.add(new Food(menuNames[i], menuPrices[i])); //메뉴리스트에 메뉴이름과 가격을 하나씩 추가.
            
            orderList = new ArrayList<String>(); //orderList 생성
        }
        //주문한 내역을 저장하는 함수로 orderList에서 받은걸 멤버변수 orderList에 추가해줘야한다.
        public void setOrderList(String[] orderList){
            for(int i = 0; i < orderList.length; i++)
                this.orderList.add(orderList[i]); //주문내역 추가
        }
        //총액 계산 : orderList의 iterator생성 >> 하나의 리모콘을 갖게됨
        public int getTotalPrice(){
            int totalPrice = 0;
            Iterator<String> iter = orderList.iterator();
	    //다음 데이터가 있는동안 order라는 변수에 집어넣는다.
            while (iter.hasNext()) {
                String order = iter.next();
		//주문한 메뉴가 가격이 얼마인지 찾아야됨, 메뉴판 사이즈만큼 돌면서 주문한 메뉴이름이 있는지 확인, 주문메뉴이름과 메뉴판에 있는 이름이 같으면 메뉴판의 금액을 추가.
                for(int i = 0; i < menuList.size(); i++)
                    if(order.equals(menuList.get(i).name))
                        totalPrice += menuList.get(i).price;
            }
            return totalPrice;
        }
    }
    
    public int solution(String[] orderList) {
        DeliveryStore deliveryStore = new PizzaStore();
        
        deliveryStore.setOrderList(orderList);
        int totalPrice = deliveryStore.getTotalPrice();
        
        return totalPrice;
    }
     // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        String[] orderList = {"Cheese", "Pineapple", "Meatball"};
        int ret = sol.solution(orderList);
        
        System.out.println("solution 메소드의 반환 값은 " + ret + " 입니다.");
    }
}
```

### 1차) 문제 9 - 해밍거리 구하기
```Java
// 다음과 같이 import를 사용할 수 있습니다.
import java.util.*;

class Main {
    // 2. func_a() : 긴 문자열의 길이에 맞춰 짧은 문자열의 앞에 0 넣기
    // func_a()를 사용하여 binaryA, binaryB 중 문자열의 길이가 더 짧다면 
    // 문자열 앞에 0을 채워 넣어 길이 맞추기
    public String func_a(String str, int len){
        String padZero = "";
        int padSize = len - str.length(); //최대길이를 가진 len - 현재길이str.length();
        // 앞에 0을 채워놓을 길이만큼 0을 채워놓자
	for(int i = 0; i < padSize; i++)
            padZero += "0";
        return padZero + str; // padZero(0을 채워놓은값)+원래문자(str)
    }
    
    public int solution(String binaryA, String binaryB) {
	//1. 둘 중 긴 문자열의 길이를 구하기
        int maxLength = Math.max(binaryA.length(), binaryB.length());
        if(maxLength > binaryA.length())
            binaryA = func_a(binaryA, maxLength);//func_a()함수 사용후 앞에 0이 필요한만큼 생성되어 110 >> 00110이된다.
        if(maxLength > binaryB.length())
            binaryB = func_a(binaryB, maxLength);
        
        int hammingDistance = 0;//해밍거리 0 초기화
	// 두 거리의 차이가 얼마인지 구한다.
        for(int i = 0; i < maxLength; i++) //i는 0~최대길이미만
	//두 개의 인덱스번호에 해당하는 위치의 데이터가 서로 다르면
	//즉, (binaryA의 i번째있는 문자와 binaryB의 i번째있는 문자가 다르면)
            if(binaryA.charAt(i) != binaryB.charAt(i))
                hammingDistance += 1;
        return hammingDistance;
    }
    
    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        String binaryA = "10010";
        String binaryB = "110";
        int ret = sol.solution(binaryA, binaryB);
        
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret + " 입니다.");
    }
}
```

### 1차) 문제 10 - 계산기(문자열 형태의 식을 계산하기)
```Java
// 다음과 같이 import를 사용할 수 있습니다.
import java.util.*;

class Main {
    class Pair{
        public int firstNum;
        public int secondNum;
    }
    
		//1. 주어진 연산자에 맞게 연산을 수행
    public int func_a(int numA, int numB, char exp){
        if (exp == '+')
            return numA + numB;
        else if (exp == '-')
            return numA - numB;
        else
            return numA * numB;
    }
    //1. 주어진 식에서 연산자의 위치 찾기
    public int func_b(String exp){
        for(int i = 0; i < exp.length(); i++){
            char e = exp.charAt(i);
            if(e == '+' || e == '-' || e == '*')
                return i; //연산자 위치 index 리턴
        }
        return -1; //에러일 경우
    }
		//2. 연산자의 앞과 뒤에 있는 문자열을 숫자로 변환
    public Pair func_c(String exp, int idx){
        Pair ret = new Pair();
        ret.firstNum = Integer.parseInt(exp.substring(0, idx));//0 ~ (idx-1) 변환
        ret.secondNum = Integer.parseInt(exp.substring(idx + 1)); // (idx+1)~ 끝까지
        return ret;
    }
    // 4. 위의 함수를 모두 수행해서 결과값 도출
    public int solution(String expression) {
				//연산자의 index번호 찾아서 expIndex변수에 넣음
        int expIndex = func_b(expression);
				//expression과 (연산자의 index번호를 expIndex)라는 매개변수로 받음
        Pair numbers = func_c(expression, expIndex); 
				//첫번째 숫자, 두번째 숫자, 연산자(expression의 인덱스 값에 해당하는 char)를 넣어준다.
        int result = func_a(numbers.firstNum, numbers.secondNum, expression.charAt(expIndex)); 
        return result;
    }

    // 아래는 테스트케이스 출력을 해보기 위한 main 메소드입니다.
    public static void main(String[] args) {
        Main sol = new Main();
        String expression = "123+12";
        int ret = sol.solution(expression);

        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("solution 메소드의 반환 값은 " + ret + " 입니다.");
    }
}
```
