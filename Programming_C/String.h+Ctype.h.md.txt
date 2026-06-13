
# string.h

0. n 붙은 함수 : 처리할 문자의 수를 명시적으로 지정할수 있음.(더 안전한 함수)

0.remove trailing '\n' after fgets: 
s[strlen(s) - 1] = '\0' // if last char is '\n' 


1.strlen(s) : length, '\0'제외한 문자열의 길이.인자에 '\0' 있어야함.

2.strcpy(dest, src) : copy src into dest//기존 내용을 덮어씀. dest에 무엇이 들어있었든 상관없이 완전히 지워지고 새 문자열이 처음부터 들어감.
strncpy(dest, src, n) : bounded copy(소스가 데스티네이션보다 크면 생기는 문제 방지.) >> 최대 src의 n 바이트 복사 to dest.
e.g., ) strncpy(dest, src, sizeof(dest) - 1)


3.strcat(dest, src) : append  src to end of dest >> dest must have enough room : strlen(dest) + strelen(src) + 1 // strcat 함수는 "문자열과 문자열"을 합치는 함수
strncat(dest, src, n) : destination에다  최대 n 개의 source 붙임. //  문자열에 단일 문자를 붙일땐 이렇게 >> strncat(an, &in[j], 1); 


3 - 1 strcat는 문자열의 끝(\0)을 찾아 \0에서부터 새로운 문자열을 붙임.so \0위치 중요.
char b[100] = ""; //처음부터 문자열b에 strcat주고 싶을땐 b에다 빈문자열("")을 할당하여 b[0]="\0"만들기.

e.g.1)
char dest[] = "Hello";
char src[] = "world"; 
strcat(dest, src)하면 "Helloworld" 나옴.
2)
char buff[100];
buff[0] = '\0';
strcat(buf, "Score: ");
strcat(buf, name);
strcat(buf, "Pts: ");



4.strcmp(a,b) : compare .
strncmp(a,b,n): compare first n chars only
e.g)
1)만약 a랑 b가 같으면 strcmp(a, b) = 0;
2)a < b 이면 strcmp(a, b) = < 0;
3)a > b 이면 strcmp(a, b) = > 0;

e.g.) 접두사 비교 
strncmp(s, "LED", 4)==0 // s의 시작점부터 최대 4글자가 "LED\0"과 완벽히 일치하는지 비교. s가 LED이면 0 반환.

if(s=="Hello") X(compares address. not contents)
if(strcmp(s,"Hello")==0) O.(compare contents.)



5.strstr(s,sub) : s안에 sub 있는지 확인 .substring / char 의 위치(index)를 반환.없으면 NULL 반환.




8.strtok : Tokenizing.(문자열 나누기)


8-1.원본 문자열을 변형.(구분자를 \0으로 바꿈)
strtok은 새로운 문자열을 만들어내는 것이 아니라, 
원본 문자열을 돌아다니면서 구분자를 발견하면 그 자리널 문자(\0)로 덮어씌워 버림.


8-2. 자기가 어디까지 읽었는지 기억.(내부 포인터 유지)
함수가 끝나도 내부적으로 포인터(정적 변수)를 유지하여 "아까 여기까지 잘랐지? 다음엔 여기서부터 시작해야지" 하고 기억.

8-3. strtok은 
e.g.,)
str= [a][p][p][l][e][, ][b][a][n][a][n][a][\0]
1. 첫 번째 호출 : token = strtok(str, ",");
strtok이 str의 처음부터 읽기 시작하다가 쉼표, 를 발견.
쉼표 자리를 \0으로.
그리고 'a'가 있는 첫 번째 메모리 주소를 token 상자에 반환합니다.

	메모리 상태 : [a] [p] [p] [l] [e] [\0] [b] [a] [n] [a] [n] [a] [\0]
	내부적으로는 'b'가 있는 곳의 주소를 은밀하게 기억.

2. 두 번째 호출 : token = strtok(NULL, ",");
	인자로 NULL이 들어왔으므로, 아까 기억해 둔 'b' 위치부터 다시 탐색을 시작.
	끝(\0)을 만날 때까지 구분자가 없으므로, 문자열이 끝났음.

'b'가 있는 곳의 메모리 주소를 token 상자에 반환.

8-4 strcat 과 strtok을 활용

e.g.,)


    char a[] = "i am the destroyer. and, i like mango";

   
    char b[100] = '\0'; // '\0'대신 "" 할당 해도됨.1. b 배열을 빈 문자열로 초기화하여 strcat이 정상 동작하게 만듦


    char* token = strtok(a, " ,."); //첫번쨰 토큰 추출, 공백을 추출하려고 ' ' 쓰면 X.그냥 (스페이스 바)

 
    while (token != NULL) {   // 3. token이 NULL이 아닐 때까지 반복
        strcat(b, token);             // 추출된 토큰을 b에 이어 붙임
        token = strtok(NULL, " ,.");  // 다음 토큰 추출
    }

 b 는 iamthedestroyerandilikemango 됨.


# ctype.h

1. char test : isalpha, isdigit, isspace, islower, isupper

2. toupper(c) : convert char to uppercase
3.tolower(c) : convert char to lowercase
//1. 한번에 하나의 문자만 처리하므로 string은 for문으로 바꾸기( a[i]=tolower(a[i]) ) 2.영어가 아닌건 안건듬.