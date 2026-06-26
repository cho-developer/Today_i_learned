# Memory model

1. 메모리는 바이트 단위로 주소 저장
2. Little - endian : 가장 낮은 주소에 Least Signficant Byte(최하위 바이트)저장. 
e.g.) unsigned int x= 0x12345678;
// Address : 0x100 0x101 0x102 0x103
	byte   : 78		56    34     12  >> 가장 낮은 주소에 LSB 저장됨.(BIg-endian 은 0x103에 76 저장됨)

2. memeory layout : 4계층

stack :정적으로 메모리 할당된것들. 지역 변수, 매개변수 functuoncall frames//{} 안에서만 생존.//OS가 메모리 할당하고 제거.

heap : 동적으로 메모리 할당 된것들. malloc / free //큰 파일 받고 쓸대 사이즈 모를때 //개발자(너)가 메모리 할당하고 제거.

data : 전역 변수, static variables = const//프로그램이 실행되고 종료될때까지 생존//OS가 메모리 할당하고 제거.

text : 프로그램으로 쓴것들. char* p[] >> read only// letter literal 


3. 포인터로 문자열 리터럴을 선언하면, 해당 문자열의 데이터는 읽기 전용 메모리 영역에 저장.//so 이걸 수정하려시도 하면 segment error.

4. arr[size] = *(arr + size) // 완전 똑같. 즉 arr[size]를 만나면 컴파일러는 *(arr+size)로 처리함 >>>>(배열)arr의 시작 주소에서 size만큼 이동해서 *그곳의 데이터를 읽어라 
 

5.	 포인터 함수로 malloc된 메모리를 반환 -> 메인의 포인터 변수에 메모리 할당 가능.
e.g.,)

int* make_squares(int n)
{
	int* arr = (int*)malloc(n * sizeof(int));
	if (!arr) return NULL;
	int i;
	for (i = 0; i < n; i++)
		arr[i] = i * i;
	return arr; /* heap memory survives return */
}

int main(void)
{
	int* squares = make_squares(5);// squares에 메모리 할당.
	if (!squares) return 1;
	...
		return 0;
}

6. buffer 와 Disk 
 6-1buffer는 임시 저장소(왜냐하면 1바이트 같이 작은 단위를 호출할때마다 디스크에 접근하면  연산이 너무느려진다)
	So. 수 kb를 임시로 buffer에 저장, 디스크로 가지않고 buffer로 가서 처리. 
 6-2. 버퍼가 비어 있다면 디스크에서 kb를 가져오고, 가득 차면 디스크로 보냄.