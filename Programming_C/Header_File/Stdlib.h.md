1. qsort(Quick Sort):
	1-1형식 :
	void qsort(void* base, size_t num, size_t size, int (*compar)(const void*, const void*));
	//	base: 정렬할 배열의 이름(배열의 시작 주소)
	//	num : 배열에 들어있는 요소의 총 개수 = sizeof(base) / sizeof(base[0])
	//  size : 배열 요소 하나당 크기(보통 sizeof(자료형)을 사용)
	//  compar : 두 값을 비교하여 정렬 기준을 결정하는 비교 함수(직접 작성해야 함)

		1-1-1 비교함수 만들기:
		e.g.,)	
		int compare(const void* a, const void* b) {
			// a와 b를 원하는 자료형으로 변환(캐스팅)하여 비교한 값을 반환
		}
		
		
			[비교 함수의 반환값 규칙]

			양수 반환 : a가 b보다 뒤로 감(자리를 바꿈)

			음수 반환 : a가 b보다 앞에 남음(자리를 바꾸지 않음)

			0 반환 : 두 값이 같음



2. malloc : runtime시 메모리 할당해주는 함수.

2-1 구성 : (void *)malloc(n*sizeof(element))

e.g.,)

char *a= (char*)malloc(n*sizeof(char)) // 이렇게 하면 a에 n 크기만큼 메모리 할당됨. (이게 바로 동적 메모리 할당)


3. calloc : malloc + 할당한 메모리 안에 0넣어줌.

3-1 구성 : (void*)calloc(n, sizeof(element))



4. realloc

4.atoi : 문자를 integer로
5.atof : 문자를 float 으로

e.g., )
char s1[] = "123";
char s2[] = "3.14";

int n1 = atoi(s1);
double n2 = atof(s2);
