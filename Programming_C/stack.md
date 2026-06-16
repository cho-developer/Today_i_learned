0. stack 관련 용어
 0-1 push: stack 에 데이터 넣기
 0-2 pop : stack의 가장 상단의 데이터를 뺴는거
 0-3 stack:  배열을 세로로 세운게 stack임. 

1. stack 구현을 위한 주요 함수 
 1-1 데이터를 스택에 넣는 함수(push 함수)
 1-2 데이터를 스택에서 빼는 함수(pop 함수)
 1-3 스택이 꽉 차있는지 판단하는 함수
 1-4 스택이 비어 있는지 판단하는 함수

e.g.,)
    #define SIZE 100
    typedef struct StackType {
        int arr[SIZE];
        int top;// 항상 스택의 탑을 가르킬 녀석 필요
    }StackType;

    void inti(StackType* s) {


        s->top = -1; // 배열의 인덱스를 가르킬 녀석. top이 -1이면 데이터는 0개(empty), 0이면 데이터는 1개.

    }// 스택 초기화 하는 함수



    int is_empty(StackType* s) {


        if ((s->top) == -1)return 1;
            
        return 0;

    }//1-4 스택이 비었는지 검사하는 함수 



    int is_full(StackType* s) {

        if ((s->top)==SIZE-1)
            return 1;
        return 0;
    }

    // 1-3 스택이 꽉차 있는지 판단하는 함수

    void push(StackType* s, int val) {

        if (is_full(&s)) {
            printf("Stack is full"); exit(1);
        }

        printf("Pushed %d\n", val);
        s->arr[++(s->top)] = val;//첫번째 데이터를 넣을떄 top은 -1 이니까 먼저 ++하기.

    } //1-1 push 함수

    int pop(StackType* s) {

        if (is_empty(s)){ printf("Stack is empty"); exit(1);}

        return s->arr[(s->top)--];
    }// 1-2 pop 함수 


    int peek(StackType* s) {


        if (is_empty(s)) { printf("Stack is empty"); exit(1); }
        return s->arr[s->top];
    }//top에 뭐가 있는지만 보는 함수. 

2. 