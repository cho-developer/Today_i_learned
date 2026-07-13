0. Queue 
 0-1 enqueue: 데이터 삽입
 0-2 dequeue: 데이터 빼기
 0-3Queue는 stack과 반대로 first in first out (선착순 )
 0-4 배열 or 연결 리스트로 queue구현.
 0-5 배열->> Queue(circular queue 포함)의 dequeue는 물리적 삭제x. 논리적 삭제.
1. Queue 구현을 위한 주요 함수
 1-1 데이터를 큐에 넣는 함수
 1-2 데이터를 큐에서 뺴는 함수
 1-3 큐가 꽉 차있는지 판단하는 함수
 1-4 큐가 비어 있는지 판단하는 함수
 
 e.g.,)배열 ->>QUeue
 
typedef struct Queue {

	int front;// 앞 쪽 index
	int rear;// 뒤 쪽 index
	int data[MAX];
}Queue;//Queue 만들기



void init(Queue* q) {


	q->front = -1;
	q->rear = -1;
	
	

}// Queue 초기화




int is_full(Queue* q) {


	if (q->rear == MAX - 1)
		return 1;
	
	return 0;
}// 1-3 함수


int is_empty(Queue* q) {

	if (q->front == q->rear)
		return 1;


	return 0;
} // 1-4 함수

void enqueue(Queue* q, int item)
{

	if (is_full(q))
	{

		printf("Error Queue is full");
		exit(1);



	}
	q->data[++(q->rear)] = item;

} // 1-1 함수


int dequeue(Queue* q) {

	if (is_empty(q)) {
	
		printf("Error Queue is empty");
		exit(1);
	
	}
	return q->data[++(q->front)];


} // 1-2 함수

2. 선형 Queue의 문제점 :
 전부다 deque하면 해당 Queue 는 더 이상 못씀. 해결법은 바로 circular Queue(선형 queue 를 동그랗게 만든거.)

3. Circular Queue를 위한 정의
    3-1 enqueue: rear=(rear+1)% MAX_QUEUE_SIZE
    3-2 dequeue: front=(front+1)% MAX_QUEUE_SIZE
    3-3 is_empty: front==rear
    3-4 is_full: (rear+1)% MAX_QUEUE_SIZE==front 

 e.g.,)배열->>circular Queue
#define MAX 3

typedef struct Queue {

	int front;// 앞 쪽 index
	int rear;// 뒤 쪽 index
	int data[MAX];
}Queue;



void init(Queue* q) {


	q->front = 0;
	q->rear = 0;
	}

int is_full(Queue* q) {


	if (q->front == ((q->rear)+1) % MAX)
		return 1;
	
	return 0;
}//3-4 원형 queue의 is_fill


int is_empty(Queue* q) {
 return q->front == q->rear;
} // 3-3 원형 queue의 is_empty

void enqueue(Queue* q, int item)
{

	if (is_full(q))
	{

		printf("Error Queue is full");
		exit(1);



	}
	q->rear = (q->rear + 1) % MAX;
	q->data[q->rear] = item;

}// 3-1 원형 queue의 enqueue


int dequeue(Queue* q) {

	if (is_empty(q)) {
	
		printf("Error Queue is empty");
		exit(1);
	
	}
	q->front = (q->front + 1) % MAX;

	return q->data[(q->front)];


 } // 3-2 원형 queue의 dequeue

#define MAX_SIZE_QUEUE 5

typedef struct queue{
	int *arr;
	int front;
	int rear;

}queue;

void init_queue(queue *q){
	q->arr=(int*)malloc(sizeof(MAX_SIZE_QUEUE)*4);
	q->front=q->rear=0;

}


void enqueue(queue *q,int val){

		if((q->rear+1)%MAX_SIZE_QUEUE == q->front)
			{printf("Queue is full");return;}

		q->arr[q->rear]=val;

		q->rear=(q->rear+1)%MAX_SIZE_QUEUE;


}

int  dequeue(queue *q){

	if(q->front==q->rear){
		printf("queue is empty"); return;
	}
	int idx=q->front;
q->front=(q->front+1)% MAX_SIZE_QUEUE;

	return q->arr[idx];
}




int main(){
	queue q1;
	init_queue(&q1);


}

 e.g.,)연결->>circular Queue// 맨뒤 삽입. 이중 포인터. head와 tail 필요.