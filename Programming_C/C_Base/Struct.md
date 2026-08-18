0.C 언어는 struct 이나 union을 정의할 때 내부 멤버의 기본값을 직접 초기화할 수 없음.



1. 구조체의 내부 데이터 접근법 : . 쓰기
e.g.,) struct i ={3,4};
		i.x=5; //3이 5로 바뀜.

2. typedef로 struct 줄이기. 
Without typedef must write 'struct' everywhere 
e.g.,)
	struct Point p = {3, 4};
	void print_pt(struct Point p);

	>>해결법 : typedef로 구조체 선언하기  
e.g.,)
typedef struct { int x; int y; } Point;
Point p = {3, 4}; // no 'struct' keyword! 
void print_pt(Point p);


3. 구조체에 다른 구조체 복사해서 넣기 가능.
e.g.,)typedef struct { int x; int y; } Point;
	Point a={1,2};
	Point b=a; //b에 a값들(1,2)이 들어감.

4. Nested struct 
e.g.,)
struct Employee
{
char name[50];
int id;
struct Date hire_date; /* nested struct */
double salary;
};

Employee e = {
 "Alice", 1001,
 {2024, 3, 15}, // nested init 값 주는법
 55000.0
 };

5.Function that returning struct : C allows a function to return a struct(caller gets a copy)

e.g.,)
Point midpoint(Point a, Point b)
{
Point m;
m.x = (a.x + b.x) / 2.0;
m.y = (a.y + b.y) / 2.0;
return m; /* struct returned by value */
}

Point mid = midpoint(p1, p2); /* stc1 uses this */

6.Pointer to struct
• Rule to remember:
  1: (dot) -- variable IS the struct (. 앞에 변수는 구조체)
  2: (arrow) -- variable is a POINTER to struct(-> 앞에 변수는 POINTER to struct)

e.g.,)
Student alice = {...};

Student *ps = &alice;
ps->gpa = 3.9; /* ps POINTS TO the struct */
/* same as: (*ps).gpa = 3.9  */


7.
Array of Structs

Student arr[MAX]; >> Student가 typedef로 struct으로 선언된거라 arr은 구조체 의 배열임.

6&7 : 구조체 배열을 함수(구조체 포인터)의 인자로 줄수 있다.

e.g.,)
void printStudents(Student* ptr, int size) {
    for (int i = 0; i < size; i++) {
   
        printf("ID: %d, Name: %s\n", ptr[i].id, ptr[i].name);} // 이런식으로 활용 가능.
          }

 Student classList[3] = {
        {1, "Alice"},
        {2, "Bob"},
        {3, "Charlie"}
    };
    printStudents(classList, 3);



8. union : struct와 비슷 , 차이점 은 변수들이 같은 메모리 주소를 갖는다는 거임.
so.맴버에 한번 값을 쓰고 다른 맴버를 부르면 첫번째 맴버의 값이 나옴. 

8-1 union의 크기 : 맴버의 크기 중 가장 큰값이 union의 사이즈가 됨.
(struct의 사이즈는 모든 맴버의 사이즈 +a);


8-2 Endianness and union

e.g.,)
union{unsigned int i; unsigned char b[4];}w; //union 

w.i=0x12345678;
//little-endian: b[0]=0x78, ~, b[3]=0x12;
//big-endian : b[0]=0x12, ~, b[3]=78;





9.Tagged Union(union과 struct,enum을 같이 쓰는것)(for 안헷갈리게)

e.g.,)
typedef enum{INT_VAL,FLOAT_VAL,CHAR_VAL }Vtype;  // enum은 개발자가 직관적인 단어(INT_VAL)들을 숫자로 바꿔주는것.(이래하면 이제 INT_VAL을 0으로 읽음.) 

typedef struct{
    Vtype vtype;
    union {
        int i;
        float j;
        char k;
    }V_union;


}V;


void V_unionvalue(V s){
    
    switch(s.vtype){
        case INT_VAL : printf("%d",s.V_union.i); break;
        case FLOAT_VAL : printf("%f",s.V_union.j); break;
        case CHAR_VAL : printf("%c",s.V_union.k); break;
   
    }
}

int main(){
V data1={INT_VAL, {.i=10;}}; // TIP : struct or union 의 특정 맴버들에만 값을 주는법.(.변수이름=값)
V data2={FLOAT_VAL, {.j=3.14;}};
V data3={CHAR_VAL, {.k='c';}};
		
		}

10. Bit Fields

10 -1  변수에 N'비트'만 할당 하는법(struct 안에서만 쓸수 있는 기능) : 자료형 변수명: 숫자 

e.g.,)
struct StatusReg {

    unsigned int ready : 1; // ready는 0 or 1만 담을수 있음.
    unsigned int mode : 3;// mode는 0 ~ 7만 담을수 있음.
    unsigned int count : 11;  // count는 0 ~ 2047 만 담을수 있음.
    unsigned int error : 1;
}; >>>>>>>>>>>> >//StatusReg의 메모리 구조 : 총 16비트 차지(1+3+ 11+ 1)
//이렇게 하나의 struct안에서 비트 필드를 구성하면 
// 개발자가 지정한 비트 수만큼 레고 블록처럼 빈틈없이 연속적으로 메모리 공간을 차지

10-2 union내부에 있는 bit-filed의 맴버들에 값줄때: 임시 변수를 선언하고 임시변수의 값을 
bit-filed 맴버에 할당하기.


e.g.,) union
struct {
        unsigned int a : 1;
        unsigned int b : 3;
}vv;
    unsigned int j;
 }v;
 
 
 int main() { int x; int y; scanf("%d", &x); scanf("%d", &y); v.vv.a = x; v.vv.a = y;}
 // scanf 안쓰고 굳이 이렇게 하는 이유: scanf의 &은 바이트 단위. so 안먹음. 임시 변수 선언해서 할당해야함.


11. struct * a 로 구조체의 맴버를 ->로 가리키면 그 맴버의 값이 바로 나옴.

e.g.,)

void printf_app(const Appointment* a) {

    printf("%d", a->point); // 하면 a가 받은 구조체의 맴버인 point값을 바로 읽음. 
}

12. union 포인터로 union 내에 있는 struct 내에 있는 맴버를 가르키는 RULE : 
first access from pointer은 arrow(->)로
every access after that dot(.)으로

e.g.
UNION const* s = &u;
s->bits.rx;//s내에 있는 구조체 bits내에 있는 맴버 rx를 가르키는법.