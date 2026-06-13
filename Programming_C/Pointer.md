0. 포인터는 변수는 ADDRESS를 저장. 
 e.g.) int *p = &x; // 1)p== &x. 2)*p==x. 
		*p= 99; // p의 가지고 있는 값(x의 주소)로 가서 99를 씀. >> x가 99됨.

0. 포인터 앞의 자료형은 포인터 변수가 담고 있는 ADDRESS로 가서
	데이터를 몇 바이트 단위로 끊어서 읽어야 하는지를 알려주는 것이 바로 포인터 앞의 자료형

# Pointer

1. 포인터의 종류
 1-1 int * p; // int 포인터
 1-2 int *a[5]; // a는 int를 가르키는 pointer 5개의 array // 로직 순서 a[5] >> *a[5] : 배열의 각 요소는 포인터(5개). >> int *a[5] : 포인터들이 가리키는 도착지에는 int형 데이터가 있다
 1-3 int (*f)(); // f 는 int를 반환형으로 하는 함수를 가르키는 포인터


2. pass by reference 
 e.g,) int my_first_pointer_function(int *a, int *b) // 하고 main 에서 my_first_pointer_function(&x,&y)이렇게 주소값을 인자로 주기.


3.NULL pointer // pointer 변수를 선언하고 할게 없으면 그냥 int *p; 하지말고  int *p=NULL; 이렇게라도 해라. 꼭.

4. 포인터 연산 : 타입 크기 고려해서 +- 이동.(p+n은 n 요소 크기 만큼 이동)
  1)	e.g.,) int a[5]= {10, 20 ,30 ,40 ,50};
		int *p=a; // p == &a[0]
		p+2; // >>&a[2], 즉 1바이트 이동이 아니라 4바이트씩 이동함.
		p++  // &a[3]; 
  2) 포인터 끼리 -+ 해서 배열의 길이 산출 가능. (단 연산하는 포인터는 같은 배열을 가르켜야함.)


  5. 포인터와 배열
  1)	e.g.)int a[]= {10, 20 ,30 ,40 ,50};
		int *p=a;
		 *(p+i)=a[i];//동일!  역도 성립. 
		 a[i]== *(p+i); //동일 C언어 문법상 완전 동일.
		 a[i]는 *(a+i)와 완전히 똑같.

		 a==&a[0]; //배열의배열이름이 포인터 처럼 작동.
		 a[i]==*(a+i)
		 &a[i]==a+i;

		 단,배열의배열이름은 포인터와 달리 고정. 바꿀수 없음.
  
  6.포인터와 상수
   1)조합 
		1.pointer to const : 
		const int *p=&x; (읽기 전용 pointer)
		can change WHAT p points to. cannot change the VALUE through p (*p=5 ERROR)
		(내용은 못바꾸지만 , 가르키는건 바꾸기 가능)
		
		2. Const pointer :
		int* const p = &x;
		cannot change WHAT p points to. can change the VALUE through p (p= &y ERROR, *p=5 OK)

		3. Const pointer to const : const int *const p = &x;
		 p neither  WHAT points nor VALUE can change.


 7. void* : void* can point to any type. but Must cast to use . so casting(형변환)  하기전엔 쓸수 없음. 

	e.g.,) void *malloc(size_t n);
		int *p= (int *)malloc; // 이렇게 쓸때 맞게 casting 해야함.
		char *s= (char *)malloc; //

8. sizeof(*pointer) : sizeof what it points to 
 e.g.,) char *s; sizeof(*s) == sizeof(char)==1
 ++ sizeof(int *) ==8;
	sizeof(double *) ==8;
	sizeof(void *) ==8; >>> same 8!

9. common pointer patterns	
	*ptr++: *(ptr++) 와 같음.

	1) 배열 전체 순회 : while(p<end) {p++;}
	2)  copy :  *dst++=*src++;(읽기 ,쓰기 , 이동 다 포함됨.)
	3)  search : while(*p && *p != c) p++;
	4) length : while (*p)p++; len= p-star; //배열의 길이 . star 는 배열의 첫번째 pointer
	
10. volatile : tells compiler this can change without C code (이 변수는 예측 불가능 하게 변할수 있으니까 최적화 하지마라.)

11. 포인터를 함수로 : function that returns pointer가 됨.
	: pointer를 함수로 만들수 ㅇ
	e.g., ) int* find(int a[], int n) {

	~~~return &a[i];

	return NULL;

} // main 에서 포인터 함수 호출할땐 * 때고 하기 . 여기선 *find(b[], 6) 이 아니라 find(b[], 6) 이렇게.

   11-1 함수 지역변수의 주소를 외부로 반환 하면X
   :함수가 종료되면 스택(Stack) 메모리에 있던 지역 변수 local_val은 자동으로 소멸. so
   그 주소값을 반환해버리면, 이 함수를 호출해 값을 넘겨받은 쪽에선 이미 스택에서 사라진 메모리 공간을 계속 가리키게됨.
	
12. char array vs pointer array : char arr[] lives on the stack(modifiable); const char *ptr points to read-only.

e.g.,) 
char name[]="Alice"; // modfiable
const char *msg= "Hello"; //points to read-only	literal

name[0]='E'; // OK 
msg[0]='J' // CRASH 
msg= "World "// OK - this behavior is ressign the pointer. not change.



12-1 Two ways to store multiple stings.
	1)1,2D char array(fixed size):
	e.g.,)
	char name[3][20]={"alice", "ano", "ice" } // 각행 마다 이름이 들어가는 구조인. 20글자 이상의 이름은 에러. 남는 공간은 all '\0'
	
	2)array of char pointer(variable length)
	e.g.,)
	const char * days[]={
	"Monday","Wednesday","tuseday",
	"THursday",
	
	} //days[0]==Monday. days[3]==THursday.

	>> const char * name[20]; 이라는 선언은 '문자열을 가리킬 수 있는 포인터 20개를 담을 상자'를 만든 것일 뿐,
	실제 문자열 데이터(글자들)를 저장할 공간을 만든 것이 아님. 그래서 char namememo[20][30];을 만들고 여기다 scanf로 넣어야함.



13. command line argument :main 함수를 보다 활용 하는것 . 
	형태:int main(int argc , char *argv[]). 
	// argc(Argument count)는 argv(Argument vector)의 인자 개수이다(프로그램명 포함해서 카운트). 
	argv는 array of string. 이다 .  문자 형태로 저장되기 때문에 atoi를 써서 argument vector에 있는 인자(숫자)를 사용하자.
	
	e.g.,)  
	argv가 pro 10 Hello 이면 argc는 3이고 argv[2]==Hello 이다.

14. pointer to functon : functions  have also addreses. - pointers prey.

e.g.,)
int add(int a, int b){return a+b;}
int (*fp)(int, int)=add;
int result = fp(3,4); // >> call through pointer. result==7;
 
 ++ 원래는 fp를 통해 add 를 쓰려면 (*fp)(3,4) 하는게 맞다(편의를 위해 예외적으로 단축 표현을 허용해 준 것).
 단, 그냥 *fp(3,4)는 *7이 되므로 안된다.




 15. Array of pointers vs pointer to array
	int *ap[3]; >> array of pointers; //*가 나중에 컴파일 되어서 요소 3개가 *가됨.

	int (*ap)[4] >> points to array of 4ints.//*가 ()때문에 가장 먼저 컴파일 되어서 포인터 하나가 요소4개를 가르키는 포인터가됨.

 Q)그냥 일반 포인터로 4개요소를 배열을 가르키면 되는데 굳이 배열 포인터를 따로 만든 이유가 있나?
 A)ㅇㅇ.2차원 배열 사용할때 편의가 존재하기 때문.
 (int* a와 int (*ap)[4]의 가장 큰 차이는 "포인터 연산(+1)을 했을 때 이동하는 바이트 수"에 있음.)

e.g.,)
int arr[3][4];

int* ptr = arr[0]; //이 포인터는 단지 정수 한 개(int)의 주소를 가리킴.
//so. ptr + 1을 하면 sizeof(int)(4바이트)만큼 뒤로 이동하여 다음 원소인 arr[0][1]을 가리키게 됨.

int (*ap)[4] = arr; //이 포인터는 정수 4개짜리 배열 전체를 하나의 단위로 가리킵니다.
//so. ap + 1을 하면 sizeof(int) * 4(16바이트)만큼 뒤로 이동하여 다음 행인 arr[1] 전체를 가리키게 됩니다.


16. 포인터의 형변환 
const void *로 들어온 포인터를 int *로 형변환

e.g.,)
	int compare_int(const void *a, const void *b) {
    int num1 = *(int *)a;
    int num2 = *(int *)b;}

17. 

# Pointer to Pointer
e.g.,) int x=42;
		int y= 92;
		int *p= &x;
		int **pp=&p; // *pp=p; **pp=x; 
		*pp=&y; //now p points to y , not x



