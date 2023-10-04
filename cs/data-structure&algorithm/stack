# 스택
스택(stack)은 데이터를 일시적으로 쌓아 놓는 자료구조로, 데이터의 입력과 출력 순서는 **후입선출(LIFO: Last In First Out)**이다. 즉, 가장 나중에 넣은 데이터를 가장 먼저 꺼낸다.

> 스택에 데이터를 넣는 작업을 푸시(push)라고 하고, 스택에서 데이터를 꺼내는 작업을 팝(pop)이라고 한다. 
> 
> 스택에 데이터를 푸시하고 팝하는 과정이다.
>

테이블 위에 접시를 겹겹이 쌓는 것처럼 데이터를 넣고 꺼내는 작업을 위쪽부터 수행한다.  
이렇게 푸시와 팝이 이루어지는 쪽을 꼭대기(top)라 하고, 그 반대쪽인 스택의 가장 아랫부분을 바닥(bottom)이라고 한다.

```java
void x() { /*...*/ }

void y() { /*...*/ }

void z() {
    x();
    y();
}

void main() {
    z();
}
```

자바 프로그램에서 메서드를 호출하고 실행할 때 프로그램 내부에서 스택을 사용하는데 위의 코드를 예시로 실행과정을 살펴보겠다.  

1. main 메서드가 실행되기 전의 상태이다.
2. main 메서드가 호출되어 실행을 시작한다.
3. z 메서드를 호출한다.
4. x 메서드를 호출한다.
5. x 메서드가 실행을 종료하고 z 메서드로 돌아온다.
6. y 메서드를 호출한다.
7. y 메서드가 실행을 종료하고 z 메서드로 돌아온다.
8. z 메서드가 실행을 종료하고 main 메서드로 돌아온다.
9. main 메서드가 실행을 종료한다.  



### 스택 만들기

```java
// int형 고정 길이 스택
public class IntStack {
    private int[] stk;  //스택용 배열
    private int capacity; //스택 용량
    private int ptr; //스택 포인터

    //실행 시 예외: 스택이 비어 있음
    public class EmptyIntStackException extends RuntimeException {
        public EmptyIntStackException() {}
    }

    //실행 시 예외 : 스택이 가득 참
    public class OverflowIntStackException extends RuntimeException {
        public OverflowIntStackException() {}
    }

    //생성자

    public IntStack(int maxlen) {
        ptr = 0;
        capacity = maxlen;
        try {
            stk = new int[capacity];    //스택 본체용 배열을 생성
        } catch(OutOfMemoryError e) {   //생성할 수 없음
            capacity = 0;
        }
    }
}
```

#### 스택용 배열 stk

> 푸시된 데이터를 저장하는 스택용 배열이다. 인덱스 0인 요소가 스택의 바닥이다. 가장 먼저 푸시된 데이터를 저장하는 곳은 stk[0]이다.  

#### 스택 용량 capacity
> 스택의 용량(스택에 쌓을 수 있는 최대 데이터 수)을 나타내는 int형 필드이다.

#### 스택 포인터 ptr
> 스택에 쌓여 있는 데이터 수를 나타내는 필드이다. 이 값을 스택 포인터(stack pointer)라고 한다. 물론 스택이 비어 있으면 ptr값은 0이 되고, 가득 차 있으면 capacity값과 같다.

#### 생성자 IntStack
> 생성자는 스택용 배열 본체를 생성하는 등 준비 작업을 한다. 생성할 때 스택은 비어 있으므로(데이터가 하나도 쌓여 있지 않은 상태) 스택 포인터 ptr값을 0으로 한다 그리고 매개변수 maxlen으로 전달받은 값을 스택 용량을 나타내는 capacity에 대입하고 요솟수가 capacity인 배열 본체를 생성한다.

### 푸시 메서드 push
```java
// 스택에 x를 푸시
public int push(int x) throws OverflowIntStackException {
    if(ptr >= capacity) throw new OverflowIntStackException();
    return stk[ptr++] = x;
}
```

스택에 데이터를 푸시하는 메서드이다. 스택이 가득 차서 푸시할 수 없는 경우 예외 OverflowIntStackException을 내보낸다.  

전달받은 데이터 x를 배열 요소 stk[ptr]에 저장하고 스택 포인터를 1 증가시킨다. 메서드의 반환값은 푸시한 값이다.

> 여기서 스택 포인터 ptr은 포인터 변수를 의미하지 않는다. 새로운 데이터를 삽입할 인덱스를 저장하는 변수이며, '스택의 인덱스를 가리킨다'는 의미로 '스택 포인터'라고 한다.  


### 팝 메서드 pop
```java
// 스택에서 데이터를 팝(꼭대기에 있는 데이터를 꺼냄)
public int pop() throws EmptyIntStackException {
    if(ptr <= 0) throw new EmptyIntStackException();
    return stk[--ptr];
}
```

스택의 꼭대기에 있는 데이터를 팝(제거)하고 그 값을 반환하는 메서드이다. 스택이 비어 있어 팝을 할 수 없는 경우 예외처리한다.  

먼저 스택 포인터 ptr값을 1 감소시키고 그때 stk[ptr]에 저장되어 있는 값을 반환한다.

### 피크 메서드 peek
```java
// 스택에서 데이터를 피크(꼭대기에 있는 데이터를 들여다봄)
public int peek() throws EmptyIntStackException {
    if (ptr <= 0) throw new EmptyIntStackException();
    return stk[ptr - 1];
}
```
스택의 꼭대기에 있는 데이터를 '들여다보는' 메서드이다. 스택이 비어 있으면 예외 EmptyIntStackException을 내보낸다.  

스택이 비어 있지 않으면 꼭대기에 있는 요소 stk[ptr - 1]의 값을 반환한다. 이때 데이터를 넣거나 빼지 않으므로 스택 포인터는 변화시키지 않는다.  

-----  
> 메서드 push, pop, peek에서는 스택이 가득 찼는지 또는 비어 있는지를 메서드 첫머리에서 판단한다. 이때 연산자는 <= 또는 >=를 사용한다.
>
> 그런데 스택이 가득 차 있는지를 판단할 때 등가 연산자 ==를 사용해서 다음과 같이 수행할 수 있다.  
> `if (ptr == capacity)  //스택이 가득 찼는가?`
>
> 그리고 마찬가지로 스택이 비어 있는지도 다음과 같이 판단할 수 있다.  
> `if (ptr == 0)`
>
> 이렇게 해도 클래스 IntStack의 생성자와 메서드를 사용하여 스택 관련 작업을 하는 한, 스택 포인터 ptr값은 반드시 0 이상 capacity 이하가 되기 때문에 별 문제 없어보인다. 하지만 프로그램 오류 등으로 ptr값이 잘못되면 0보다 작거나 capacity보다 클 수 있다. 그러므로 이 프로그램처럼 부등호를 붙여 판단하면 스택 본체 배열의 범위를 벗어나 접근하는 것을 방지할 수 있는것이다. (이런 작은 노력이 프로그램의 안정성을 향상시킨다.)


### 스택의 모든 요소를 삭제하는 메서드 clear
```java
// 스택을 비움
public void clear() {
    ptr = 0;
}
```
스택에서 푸시하고 팝하는 모든 작업은 스택 포인터를 바탕으로 이루어진다. 따라서 스택의 배열 요솟값을 변경할 필요가 없다. 모든 요소를 삭제하는 작업은 스택 포인터 ptr값을 0으로 하면 끝난다.

### 검색 메서드 indexOf
```java
// 스택에서 x를 찾아 인덱스(없으면 -1)를 반환
public int indexOf(int x) {
    for(int i = ptr - 1; i >= 0; i--) { //꼭대기부터 선형 검색
        if(stk[i] == x) return i;   //검색 성공
    }
    return -1;  // 검색 실패
}
```
스택 본체의 배열 stk에 x와 같은 값의 데이터가 포함되어 있는지, 포함되어 있다면 배열의 어디에 들어 있는지를 조사하는 메서드이다.  

검색은 꼭대기부터 바닥쪽으로 선형 검색을 수행한다. 즉, 배열 인덱스가 큰 쪽부터 작은 쪽으로 스캔한다. 꼭대기쪽부터 스캔하는 이유는 '먼저 팝이 되는 데이터'를 찾기 위해서이다. 검색에 성공하면 찾아낸 요소의 인덱스를 반환하고, 실패하면 -1을 반환한다.

### 용량을 확인하는 메서드 getCapacity
```java
// 스택의 용량을 반환
public int getCapacity() {
    return capacity;
}
```
스택의 용량을 반환하는 메서드이다. capacity값을 그대로 반환한다.

### 데이터 개수를 확인하는 메서드 size
```java
// 스택에 쌓여 있는 데이터 개수를 반환
public int size() {
    return ptr;
}
```
현재 스택에 쌓여있는 데이터 개수(ptr값)를 반환하는 메서드이다.

### 스택이 비어 있는지 검사하는 메서드 isEmpty
```java
// 스택이 비어 있는가?
public boolean isEmpty() {
    return ptr <= 0;
}
```
스택이 비어 있는지 검사하는 메서드이다. 비어 있으면 true 그렇지 않으면 false를 반환한다.

### 스택이 가득 찼는지 검사하는 메서드 isFull
```java
// 스택이 가득 찼는가?
public boolean isFull() {
    return ptr >= capacity;
}
```
스택이 가득 찼는지 검사하는 메서드이다. 가득 찼으면 true를, 그렇지 않으면 false를 반환한다.

### 스택 안에 있는 모든 데이터를 출력하는 메서드 dump
```java
//스택 안의 모든 데이터를 바닥 -> 꼭대기 순서로 출력
public void dump() {
    if(ptr <= 0) {
        System.out.println("스택이 비어 있습니다");
    } else {
        for(int i = 0; i < ptr; i++) {
            System.out.print(stk[i] + " ");
        }
        System.out.println();
    }
}
```
스택에 쌓여 있는 모든 데이터를 바닥부터 꼭대기순으로 출력하는 메서드이다.