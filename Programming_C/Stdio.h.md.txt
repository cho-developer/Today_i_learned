0.파일에서 데이터를 읽고(Input) 파일에 데이터를 쓰는(Output) 등, 파일 및 화면 통신과 관련된 모든 함수


1.fseek(fp, k(지정 위치에서 앞으로 k 바이트 만큼 이동), 지정 위치 )// fseek 함수는 파일 포인터 내부의 위치(커서)를 알아서 직접 이동시켜 줌.따라서 반환값을 변수에 다시 담을 필요 없음, 그냥 함수만 단독으로 호출 끝.
e.g.,)
fseek(fp,0,SEEK_END)//fp를 맨끝(END)에서 0만큼 이동
fseek(fp, 0, SEEK_SET)//fp를 시작점(SET)에서 0만큼 이동
fseek(fp,a,SEEK_CUR)//fp를 현재시점(CUR)에서 a만큼 이동

2.ftell(fp)//현재 커서가 파일의 시작점으로부터 몇 바이트 지점에 위치해 있는지 숫자로 output 

3.fread(저장할 곳, 단위 크기, 총 개수, 파일 통로) // malloc과 ftell을 이용해 파일크기에 해당하는 메모리를 할당 buff(저장할곳)에 할당.
 e.g.,)fread(b, sizeof(int), 5, fp); //int 5개 읽기. 

4. fpoen
5. fclose
6. rewind(fp) // go back to beginning(same as fseek(fp, 0, SEEK_SET))
