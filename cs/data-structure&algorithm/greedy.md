# 그리디 알고리즘
- 그리디(탐욕) 알고리즘은 주어진 조건에서 가장 최적의 해를 구하는 알고리즘이다.
- 여러 경우 중 하나를 결정해야 할 때마다 그 순간에 최적이라고 생각되는 것을 선택해 나가는 방식이다.
- 그리디 알고리즘 문제에서는 최소한의 아이디어를 떠올리고 이것이 정답인지 검토할 수 있어야 한다.

- `주어진 숫자 중 가장 큰 숫자가 나머지 숫자들의 배수라면 가장 큰 숫자부터 시작해 결과를 도출 해낼 수 있음.`
  - `가장 큰 수가 나머지 숫자들의 배수가 단 하나라도 아니라면 ?`
<br><br>
### 예시문제 1
당신은 음식점의 계산을 도와주는 점원입니다. 카운터에는 거스름돈으로 사용할 500원, 100원, 50원, 10원짜리 동전이 무한히 존재한다고 가정합니다. 손님에게 거슬러 주어야 할 돈이 N원일 때 거슬러 주어야 할 동전의 최소 개수를 구하세요. 단, 거슬러 줘야 할 돈 N은 항상 10의 배수입니다.

<br><br>
#### 해결방법
- 최적의 해를 빠르게 구하기 위해서는 가장 큰 화폐 단위부터 돈을 거슬러 주면된다.
- 500원부터 거슬러 줄 수 있을만큼 거슬러 주고, 그 다음 큰 화폐 단위대로 거슬러 주면된다.
- `만약 800원을 거슬러주어야 한다고 가정하고 화폐 단위는 500원, 400원, 100원이라고 가정해보자. 가장 큰 숫자 500원은 400원의 배수가 아니기 때문에 500원 3개, 100원 3개 고르는 것이 최적의 방법이 아니다. 400원 2개만 거슬러주면 끝난다.`
<br><br>

#### 시간복잡도 분석
- 화폐의 종류가 K라고 할 때, 소스코드의 시간 복잡도는 **O(K)** 이다.
- 이 알고리즘의 시간 복잡도는 거슬러줘야 하는 금액과는 무관하며, 동전의 총 종류에만 영향을 받는다.
<br><br>

#### 코드
```java
int n = 1260;   // 거스름돈
int cnt = 0;    // 거스름돈 개수
int[] coin = {500, 100, 50, 10};    //화폐 단위

for (int i = 0; i < coin.length; i++) {
    cnt += n / coin[i]; 
    //배열의 첫 요소인 500부터 순서대로 1260을 나누고 
    //500으로는 2번 나눌 수 있으니 cnt에 2개 저장해준다.
    n %= coin[i];   
    //500원을 2개 거슬러주어 거슬러주어야 할 돈은 260원이니
    //1260 % 500 = 260. n에는 260이 저장되어 다시 루프반복.
}
System.out.println(cnt);
```
<br><br>

### 예시문제 2
- 어떠한 수 **N이 1이 될 때까지** 다음의 두 과정 중 하나를 반복적으로 선택하여 수행하려고 합니다. 단, 두 번째 연산은 N이 K로 나누어 떨어질 때만 선택할 수 있습니다.
  - N에서 1을 뺍니다.
  - N을 K로 나눕니다.  
- 예를 들어 N이 17, K가 4라고 가정합시다. 이때 1번의 과정을 한 번 수행하면 N은 16이 됩니다. 이후에 2번의 과정을 두 번 수행하면 N은 1이 됩니다. 결과적으로 이 경우 전체 과정을 실행한 횟수는 3이 됩니다. 이는 N을 1로 만드는 최소 횟수입니다.  

- N과 K가 주어질 때 N이 1이 될 때까지 1번 혹은 2번의 **과정을 수행해야 하는 최소 횟수**를 구하는 프로그램을 작성하세요.
<br><br>

#### 해결방법
- 주어진 N에 대하여 최대한 많이 나누기를 수행하면 된다.
- N의 값을 줄일 때 2 이상의 수로 나누는 작업이 1을 빼는 작업보다 수를 훨씬 많이 줄일 수 있다.
<br><br>

#### 코드
```java
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
int k = sc.nextInt();
int cnt = 0;

while(n > 1) {
    if(n % k == 0) {
        n /= k;
        cnt++;
    } else {
        n -= 1;
        cnt++;
    }
}
System.out.println(cnt);
```
위의 코드가 내가 풀어본 방법인데, 위의 방법으로 풀게 되면 만약 n이 100,000 이상으로 큰 숫자라고 가정하면 n을 k로 나누어 떨어지는지를 계속 조건판단을 하게되어 시간 복잡도 측면에서 굉장히 비효율적이다.

#### 모범 코드
```java
Scanner sc = new Scanner(System.in);
int n = sc.nextInt();
int k = sc.nextInt();
int cnt = 0;
// 입력받는 n을 14, k를 4라고 가정 해보자.
while(true) {
    // 14 / 4 * 4 = 12
    // 14는 4로 나누었을때 몫은 3이다. 3을 다시 4로 곱하면 12가 나오게되는데,
    // 이 연산식을 이용하면 4로 나눌 수 있는 n보다 낮은 수중 가장 가까운 수를 얻을 수 있다.
    int target = (n / k) * k;

    // 1을 빼는 연산을 수행하는 횟수가 몇번인지
    // 14에서 4로 나누어 떨어지는 숫자인 12까지 총 2번 1을 빼니 14 - 12 = 2
    cnt += (n - target);
    n = target;
    // n이 k보다 작을 때 (더 이상 나눌 수 없을 때) 반복문 탈출
    if(n < k) break;

    // K로 나누기
    cnt += 1;
    n /= k;
}
// 마지막으로 남은 수에 대하여 1씩 빼기
cnt += (n - 1);
System.out.println(cnt);
```

