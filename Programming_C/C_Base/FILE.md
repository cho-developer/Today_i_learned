1. 모든 파일 입출력 할땐 다음 3단계를 반드시 do.
1-1 :FILE *=fpfopen("파일") // 파일 내부를 돌아다닐 커서 만들기. 포인터로 선언하면 fp는 파일 내부를 돌아다니는 커서처럼 쓰임.
1-2 :read/wrtie via text file : fprintf/fscanf/  binary file : fread/fwrite
1-3 :fclose("파일")// realease and flush


2. 파일의 종류 

2-1 Text 파일
•  Human - readable characters
•  Lines separated by \n
•  fprintf / fscanf / fgets / fputs
•  Examples : .txt, .csv, .log, source code


2-2 Binary 파일
•  Raw bytes — exact memory representation
•  No newline translation
•  fread / fwrite
•  Examples : .exe, .jpg, .bin, struct dumps



3. FILE 구조체의 내부구성
	FILE is NOT just a pointer; it is a struct that holds :
• File descriptor(OS handle) : 파일을 식별하고 관리하기 위해 부여한 일종의 '일련번호'
• Current position : 파일 내에서 다음에 읽거나 쓸 바이트의 위치(오프셋)를 기억하는 커서 역할
• Buffer(typically 4KB or 8KB) : 데이터를 임시로 모아두는 메모리 공간, 보통 시스템에 따라 4KB 또는 8KB 크기로 잡음.
• error and EOF flag : 파일 읽기/ 쓰기 중 에러가 났는지, 아니면 파일 끝(EOF)에 도달했는지를 체크하는 상태 깃발

4.fopen mode
: FILE * fopen(const char* filename, const char* mode); //여기서  2번쨰 인자가 mode.
• Modes :
• "r" read only(file must exist)
• "w" write only(creates / truncates)
• "a" append only(creates if not exists)
• "r+" read + write(file must exist)
• "w+" read + write(creates / truncates)
>>>>>모드들 뒤에 b붙이면 binary mode로 됨 .e.g.,) a+b : 이진수로 read + append(write at end)

5.perror- Why did the file operation fail?
perror("msg") prints : your message + ": " + the OS reason for the last error


5. fprintf(fp, "%s\n",a ) //변수 a를 fprintf를 통해 fp가 가르키는 파일에 씀/

6. Reading Text Files with fscanf and fgets//파일에서 한 줄(string)을 읽어와 배열에 저장
	6-1 fgets(header, sizeof(header), fp);// fgets 형식.fp 자리: 읽어올 파일. header 자리: 파일에서 읽어온 문자열을 저장할 곳.

header: 파일에서 읽어온 문자열을 저장할 공간(배열)입니다.
	6-2 fscanf로 main에서 선언된 변수들에 값넣고 printf하기
	e.g.,)

	char name[50];
	int id;
	double gpa;
	char header[100];

		while (fscanf(fp, "%[^,],%d,%lf\n", name, &id, &gpa) == 3)
	{
		printf("%-15s %d %.2f\n", name, id, gpa);
	}

7. fflush 와 stream(output stream , input stream)
	7-1 fflush(fp) — immediately writes the buffer contents to disk.
	7-2 output stream : 프로그램에서 외부(파일, 모니터 화면 등)로 데이터가 나가는 통로
		input stream  : 외부(파일, 키보드 입력 등)에서 프로그램으로 데이터가 들어오는 통로
	7-3fflush(NULL) flushes ALL open output streams at once. //모든 출력 통로의 버퍼에 쌓인 데이터들을 한 방에 밀어내서 진짜 디스크에 저장
	7-4fflush on an input stream is undefined behavior // don't do it  

8. fgetc,fputc
8-1형식:
int fgetc(FILE * fp); // 파일에서 딱 하나의 문자(character)를 읽어옴. returns int, not char! 
int fputc(int c, FILE * fp); //  Why int and not char?
//EOF is - 1, which doesn't fit in unsigned char.
//Storing fgetc result in a char loses the EOF signal

e.g.,)
int c;
while ((c = fgetc(fp)) != EOF) {
	if (c == '\n') lines++;
	chars++;
}




9.binary file

 9-1쓰기 형식 : fwrite(a, sizeof(int), 5, fp);
 9-2읽기 형식 : fread(b, sizeof(int), 5, fp);
//



