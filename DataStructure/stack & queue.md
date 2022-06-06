# stack & queue

## Stack

### 스택이란

- 창고에 쌓여 있는 상자 , 후입 선출 (Last In First Out)
- 자료의 출력 순서가 입력 순서의 역순으로 이루어져야 할 경우에 긴요함
- 예시 : 함수는 실행이 끝나면 자신을 호출한 함수로 되돌아감 이 때 스택을 사용하여 호출된 함수가 역순으로 되돌아감 —> 시스템 스택이 사용된다. 시스템 스택에서는 활성레코드가 만들어졌다가 없어지면서 호출된 함수를 리턴할 때 역순으로 돌아간다.이때 활성 레코드에는 프로그램 카운터와 매개변수, 함수 안에 선언된 지역변수들이 같이 생성된다.

![stack](https://user-images.githubusercontent.com/46683113/172124605-4f590836-8c6c-4a62-8c10-60f680edbb24.jpeg)

- 주요 연산
    - push(s,a) : a가 스택에 삽입 , 스택이 가득 차서 입력이 불가능 하다면 오류 발생
    - pop(s) : 맨 위의 원소 제거해서 반환
    - peek(s) : 맨 위의 원소를 제거하지 않고 반환
    - is_empty(s), is_full(s)
    
- 구현 : 배열 (크기를 고정시켜야 함)  , 연결리스트

## Queue

## 큐란

- 먼저 들어온 데어터가 먼저 나가는 구조, 선입 선출 FIFO (First In First Out)
- 후단(rear) : 삽입이 일어남, 전단 (front): 삭제가 일어남
- 운영체제에서 cpu와 주변기기 사이에 속도차이로 인해 큐가 존재, 버퍼형태로
- 주요 연산
    - enqueue() : 큐에 연산 요소 추가, rear 에 요소를 추가함
    - dequeue() : 큐의 요소 삭제, front에 요소 삭제
    - 
    - peek() :
    - is_full(), is_empty() :
    - 
- 구현 : 배열, 연결리스트

## 선형큐

- 가장 간단한 방법, 한개의 rear와 한개의 front로 구현함
- 배열로 간단하게 구현 가능 , 작업스케줄링에 응용 (cpu 스케줄링 fifo 참고)
- 단 rear, front의 값이 계속 증가만 하기 때문에 언젠가 배열의 끝에 도달한다. 그리고 앞부분이 점점 비는데 사용하지 못한다.

## 원형큐

- 원형으로 생각, 즉 front와 rear 값이 배열의 끝인 MAX_QUEUE_SIZE-1에 도달하면 다음에 증가되는 값은 0이 되도록 함
- front는 맨 앞의 요소 값의 하나 앞을 가리키고 rear 값은 맨 마지막 요소를 가리킨다. 그러므로 rear값과 front의 값이 같으면 큐가 비어있는 것이다.
    
    ![queue](https://user-images.githubusercontent.com/46683113/172124688-8d7a6fcc-ccd5-4eb1-8043-9c97e63bd788.jpeg)

    

## 덱

- deque, double -ended queue , 큐의 전단과 후단에서 모두 삽입과 삭제가 가능한 큐
- add_rear(), delete_front(), delete_rear(), add_front(), get_rear(), get_front()

##