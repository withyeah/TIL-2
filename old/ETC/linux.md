<2-2 bash 기초>

- 학습목표 : 기존에 짜여진 bash스크립트를 대강 이해할 수 있다.
- bash
    - shell은 여러 가지 종류가 있는데 그 중에 지금 사용하고 있는게 bash
    - Bourne shell을 대치하기 위해 GNU에서 만든 셸입니다.

    - 다른 셸에서 많은 기능을 가져옴

    - 강력 & 편리
- bash의 특징

    - 명령어 실행

    - 파이프, 리다이렉션

    - 자동 완성

    - 변수
    - control - flow (while, if, for)

    - 스크립트 지원
- bash script
    - bash shell에서 지원해주는 스크립트.

    - 일반적인 스크립트 언어와 기능이 거의 같다.

    - 리눅스 시스템을 관리하는데 전반적으로 사용됨 - 그래서 배워야 합니다.

    - 요즘은 펄이나 파이썬에 비해 편리하지는 X - 그래도 배워야 합니다.

    - 셸 명령어를 스크립트 내부에서 빈번히 사용할 경우 사용하면 굳

- 변수

    - 선언 없이 정의만으로 사용 가능

    - 변수의 타입은 무조건 문자열

    - 사용하기 위해선 $를 붙임
    - FILES=$(ls -F)
    - echo $FILES

- 사용자로부터 입력받기
    - echo "What's your name?"
    - read NAME
    - echo "Hello, $NAME"
    - echo "${NAME}님 안녕하세요?"    #변수 뒤에 바로 문자열을 붙여 쓰고 싶을 때 {}로 변수를 감쌉니다.

- 숫자 계산

    - $((<수식>))을 이용해 수식 계산 가능.

    - 주의! $(())안에서는 변수에 $를 붙이지 않는다.

- 출력 리다이렉션
    - echo "hello" > hello.txt     #hello.txt에 echo "hello"를 넣은다.
    - cat hello.txt                     #hello라고 나옴

- 입력 리다이렉션
    - echo "Snoopy">name.txt
    - cat name.txt     #Snoopy
    - ./ex5.sh<name.txt       #Type your name \n Snoopy님 안녕하세요?
- for loop
    - for i in hello 2 3
    - do
    -     echo $i
    - done
    - #hello
    - #2
    - #3
- seq
    - A=$(seq 1 10)

    - $echo $A
    - #1 2 3 4 5 6 7 8 9 10

- 비교문으로 가능한 것들

    - 비교문 형식 : [조건]

    - 숫자비교 [A op B]
        - -eq : ==
        - -ne : !=
        - -lt : <
        - -gt : >
        - -le : <=
        - -ge : >=

    - 문자열 비교
        - =, !=, <, >
        - -n s1 : string s1 is not empty
        - -z s1 : string s1 is empty

    - 파일 검사
        - -d directoryname : Check for directory existence
        - -e filename : Check for file existence
        - -f filename : check for recular file existence not a directory

- 컴파일 과정

    - 전처리 -> 컴파일 -> 링크

    - $ gcc -v -save-temps -g -o hello hello.c
        - -v : 컴파일과정 전체를 화면에 보여줘
        - -save-temps : 중간생성물도 지우지말고 저장해줘
        - cc1, as, collect2가 사용됨
    - cc1이용해 hello.i ->hello.s
    - as이용해 hello.s -> hello.o
- cc1 : 전처리기

    - 전처리 후 생성물 : 파일이름.i

    - 관련옵션 : -I<헤더디렉토리> -D<정의할심볼>
- ELF

    - 리눅스의 바이너리 파일 포맷 규결
    - a.out -> coff ->elf로 변화함.

    - 컴파일 결과물이 a.out인것도 여기서 유래.
    - Elf Header + 테이블 + section으로 이루어짐
    - Section/세그먼트
        - .으로 시작
        - .text : 인스트럭션(기계어)
        - .data : 초기값이 0이 아닌 전역변수
        - .bss : 초기값이 0인 전역변수
        - .rodata : 상수, 문자열 등

    - $ readelf - h test.o      //헤더 정보 보기

    - $ readelf -s test.o       //심볼 정보보기

    - $ readelf -S test.o      //섹션 정보보기

    - 링크 : 여러 ELF 파일에서 각 세션 합쳐서 새로운 섹션 가진 프로그램 만들어내는 작업
        - gcc의 collect2로 링크하는데 collect2는 내부적으로 Id를 호출->결국 링커는 Id

<둘째날>
[ ] 리눅스 명령어

- $ : 프롬프트 또는 명령어의 시작. 사용자는 $를 입력할 필요가 없다.
- # : 명령어의 끝 또는 주석의 시작, 사용자는 #과 뒤의 내용을 입력할 필요가 없음
- [text] : 옵션. 생략가능.
- <text> : 필수 입력 내용

- $ man [번호] <명령어> : 명령어의 도움말을 본다.

    - 번호는 생략가능하고 종류는 다음과 같다.
    - 1 : 일반 명령, 2: 시스템 콜, 3: C라이브러리 함수, 4: 장치파일과 드라이버 8:어드민 관련 명령어

    - $ man printf

    - $ man 3 printf
- pwd : 현재 디렉토리 표시
    - present working directory의 약자

    - 리눅스는 '/'가 최상위 디렉토리. 일반적으로 '루트'디렉토리라고 부름.

    - $echo $PWD #위와 같습니당.
- ls : 현재 디렉토리 안의 목록 표시.
    - ls-R : 해보셈. 보통 R은 recursive의 약자.
    - ll -t : 시간 순서로 보여준다.
    - ls -a : all, 숨긴파일까지 다 보여줌
    - ls -l : long, 긴 형태로 리스팅. ll이라고도 쓸 수 있음
    - ls .. : 한 단계 위 리스팅
- stat <파일명> : 파일 정보 보기

- 기타 명령
    - whoami : 나는 누군가?
    - hostname: 여긴 어딘가?
    - uname -a : 커널 등 시스템 정보
    - w : 서버에 현재 접속자 목록 보기
- echo <내용> : 내용을 화면에 표시
    - echo "hello"
    - echo -e "hello/nhello

    - 생각 외로 매우 유용합니다.
- cat <파일> : 파일의 내용 표시
    - concatenate의 약자. 연결시키다라는 뜻.

    - 뭐랑 뭐를 연결시키냐?
- mkdir <디렉토리 이름> : 현재 디렉토리 아레에 디렉토리를 만든다.
    - mkdir -p <디렉토리1/디렉토리2> : 한꺼번에 여러 단계의 디렉토리 만들기
- cd : 디렉토리 이동
    - cd <디렉토리 이름> : 해당 디렉토리로 이동
    - cd .. : 한 단계 상위 디렉토리로 이동, 공백 하나 있음.
    - cd ../ ../ : 두 단계 상위 디렉토리로 이동
    - cd / : 루트 디렉토리로 이동.
- rm : 파일 삭제
    - rm <파일 이름…> : 해당 파일을 삭제. 복수의 파일삭제도 가능.
    - rm -r <디렉토리 이름> : 디렉토리도 삭제 가능.
    - rm -rf<디렉토리 이름> : 묻지마 삭제.. 위험합니다.
- mv : 파일 이동하기
    - mv <name1> <name2> : name1의 이름을 name2로 바꿉니다. 디렉토리, 파일 모두 가능
    - mv <name> <dir1> : name파일을 dir1위치로 옮깁니다.
- cp : 파일 복사하기
    - cp <name1> <name2> : name1을 name2로 복사한다. 파일, 디렉토리 모두 가능.
    - cp <name1> <path> : name1을 지정된 경로 안으로 복사.

- $ history : 명령어 기록 보기

    - $ !<번호> : 해당 번호의 명령어 실행

    - $ (ctrl)+r : 입력 후 단어를 입력하면 일치하는 가장 마지막 명령이 나옴
- chmod

    - 파일이나 디렉토리의 허가권(퍼미션) 바꾸거나 결정

    - $ chmod +x hellish

    - + : 퍼미션 추가    - : 삭제    = : 퍼미션을 일치시킴
    - r: 읽기      w : 쓰기     x : 실행(디렉토리는 탐색)

- 파일 압축/해제

    - 리눅스 환경에선 주로 tar을 사용하여 압축. tar.gz(2단계구성, 속도빠름) 또는 tar.bz2(크기 작음)로 주로 많이 끝남

    - 압축풀기 : $ tar xvf <압축파일이름>         #eXtract View File

    - 압축하기 : $ tar czvf <생성할 압축 파일이름.tar.gz> <압축할경로>

<셋째날>
[ ] VI

- x : 커서 자리 삭제

- 모드

    - 명령모드(command mode)

        - 최초 실행시 명령 모드

        - 키 입려으로 명령을 내림

        - 입력해도 글자가 화면에 안써짐
        - esc를 누르면 명령모드가 됨

    - 입력모드(insert mode)

        - 일반적인 텍스트 에디터와 동일

        - 명령 모드에서 a, i, o, A, I, O 하나 누르면 입력 모드가 됨

    - 확장 모드(ex mode)

        - 제일 아래줄에 입력한 명령어가 보이는 모드

        - 명령 모드에서 : 를 누름.

- 버퍼
    - vi는 파일을 열고 화면에서 편집할 때 버퍼라 불리는 임시 파일을 만들어서 사용.
    - <원본파일이름>.swp의 이름으로 저장.

    - 사용자가 진짜 저장하기 전까지 원본 파일은 내용이 변하지 않고 그대로 유지.
    - esc, ctrl+z눌러서 shell로 잠깐 나와보면

    - $ ls -al : .buffer_test.txt.swp라는 파일이 있음

    - $ fg : 다시 vi로 돌아감
    - :wq!로 나오면

    - $ls -al : 버퍼파일은 없어졌다.

    - $cat buffer_test : 아까 입력한 내용이 이제 생김

- 저장, 종료
    - :w 현재 파일 저장
    - :w file.txt 이름을 바꿔서 저장
    - :q vi종료
    - :q! 강제 종료
    - wq! 강제 저장 종료
    - :e 현재 파일 다시 불러오기
    - :e file.txt 다른 파일 불러오기
    - ':'을 누르기 전에 앞에 esc를 한번 누르는 습관을 들입시당! ㅎㅎ

- 커서의 이동

    - 상하좌우 : kjhl
    - enter : 다음 줄의 처음
    - w : 다음 단어의 처음으로 이동
    - e : 다음 단어의 마지막으로
    - b : 다른 파일 불러오기
    - ^ : 그 줄의 맨 앞으로

    - $ : 그 줄의 맨 뒤로
    - H : 화면의 맨 앞
    - M : 화면의 중간
    - L : 화면의 맨 아래

- 화면의 이동(커서의 이동과는 달리 커서는 고정되어 있고 화면이 이동)
    - ^f : 다음 페이지
    - ^b : 이전 페이지
    - ^d : 화면 크기의 중간만큼 다음으로 이동
    - G : 문서의 맨 끝

    - 숫자G : 해당 줄로 이동
    - gg : 문서의 맨 처음
    - zz : 커서의 위치가 화면 중간이 됨
    - z<엔터> : 커서의 위치가 화면 맨 위가 됨
    - :숫자 <엔터> : 해당 줄 번호로 이동

- 중요 팁!

    - 화면이 멈췄어요! : 실수로 ctrl+s를 눌렀을 때 이렇게 됩니다. ctrl + q를 살포시 눌러줍니다.
    - ctrl+s를 눌렀어도 여전히 작업은 계속되고 있습니다. 갑자기 ctrl+q를 누르면 짜잔~

- 삭제/복사

    - 편집 명령 중 자주 쓰이는 명령들.

    - 삭제는 단순 삭제가 아니라 오려두기의 기능이라서 레지스터라 불리는 공간에 오려둔 문자들이 임시로 저장됩니다.
    - x : 커서 뒤쪽 한 글자 삭제
    - X : 커서 앞쪽 한 글자 삭제
    - dd : 한줄 삭제
    - D : 커서 위치 이후의 한 줄 삭제
    - gg : 문서의 맨 처음
    - [숫자]dd :  숫자에 적힌 줄 수 만큼 삭제
    - yy또는 [숫자] yy : 숫자에 적힌 줄 수 만큼을 레지스터에 복사해 놓음

- 붙여넣기 및 레지스터 관련 명령

    - 레지스터는 잘라내기, 복사하기를 통해 복사된 내용을 임시 저장하는 공간입니다.
    - p : 가장 최근의 레지스터 내용을 현재 커서의 뒤에 붙여넣기
    - P : 현재 커서의 앞에 붙여넣기
    - :reg : 레지스터 전체의 내용을 봄
    - "[0-9]p : 번호에 해당하는 레지스터의 내용을 붙여넣기 함

- 블록 지정

    - 블록을 지정한 후, 잘라내기(d), 복사하기(v)작업을 할 수 있다.
    - V : 블록을 만듬
    - (ctrl)v : 커서의 위치를 꼭지점으로 하는 블록 만듬
    - > : 해당 블록 앞에 탭 삽입
    - < : 탭 제거

- 기타 중요 명령
    - J : 두 줄을 합쳐서 하나의 줄로 만듬. 매우 자주 쓰임.
    - u : 되돌리기, 역시 매우 중요. 반복 가능.
    - ctrl + r : 앞으로 가기. 되돌리기랑 반대 기능.

- 검색하기
    - /[문자열] , ?[문자열] : 문자열을 찾음
    - * : 커서 위치의 단어를 찾음

- 문자열 바꾸기

    - 문자열 바꾸기는 vi의 편리한 기능중 하나.
    - :[범위]x/[찾을문자열]/[바꿀문자열]/[행의범위]
    - :s/this/This/g      : 현재 행의 모든 this를 This로 바꾼다.
    - :%s/this/This/g   : 문서 내의 모든 this를 This로 바꾼다.
    - 2,4s/this/That/gc : 2~4줄의 this를 That으로 바꾸면서 물어본다.

    - %s/this/What/     : 각 줄의 첫 this만 바꾼다.
    - V로 불록지정 후 :를 누르면 블록 내에서 바꾸기가 됩니다.

- 참고- sed기초 사용법
    - vi의 문자열 바꾸기와 똑같은 일을 할 수 있는 명령어

    - $ sed 's/this/This/g' source.txt > result.txt

- 정규표현식

    - 검색 문자열에는 정규 표현식이라 불리는 문자열 패턴 사용가능.
    - [문자들] : []안의 문자중 하나
    - ^ : 행의 첫 문자. []안에서는 not의 의미.
    - . : 임의의 한 글자
    - * : 앞의 내용이 0번 이상 반복
    - /+ : 앞의 내용이 1번 이상 반복
    - /| : or의 의미

- 창 나누기
    - :vnew    : 세로 창 나누기
    - ^^ww     : 창간 이동
    - :new      : 수형 분할
    - [숫자]^w<
    - [숫자]^w>
    - [숫자]^w_
    - [숫자]^wl (pipe)    : 수평, 수직 창 크기 조절. 숫자가 없을 경우의 동작은 각각 다름.
    - :sp
    - :vs

    - 창간이동
        - ctrl + w ctrl + w
        - ctrl + w + 방향키
    - ctrl + w 한 후 >,<, +, - 누르면 창크기조절

- 셸 명령 실행하기
    - :!<명령> : 셸 명령을 실행
    - :%!<명령> : 셸 명령을 실행, 결과를 현재 창에 표시

- 다른 이름으로 저장하기

    - 다른이름으로 저장 :    :w myfile

    - 현재창의 편집중인 파일을 바꾸기 :     :e myfile

        - 위 명령 없이 이후에 다시 :w를 해보면 옛날 파일에 다시 저장한다.

- 여러 버퍼(화면)이용하기

    - 여러 파일 편집한다는 말.

    - $ vi a.c a.h Makefile   # 동시에 세 파일을 연다
    - :ls  #버퍼의 목록을 본다.
    - :b<숫자>    #해당 버퍼로 이동
    - :ls #버퍼의 목록으 ㄹ본다
    - b<숫자> #해당 버퍼로 이동

[ ] 수업 들으며 vi필기~

- (esc), ctrl+z : shell로 잠깐 나오기
- z+enter : 맨 위로 올라간다
- dd : 삭제
- yy : 복사
- V+방향키 : 블록
- x : 지우기
- p : 붙여넣기(현재줄의 아래에)
- P :현재의 위에 붙여넣기
- ctrl+v : 커서 단위 블록(virtual block), 붙여넣기
- :s/태산/경민 -->태산을 한 줄 찾아서 경민으로 바꿔준다.
- :s/태산/경민/g  -->태산을 한 줄 찾아서 경민으로 바꿔준다.
- :%s/태산/경민/g -->태산을 다 찾아서 경민으로 바꿔준다.
- :'<,
- :new : 창 세로로 나누기
- :vnew- 창 가로로 2개 나누기.
- :!ls : 잠깐 밖으로 나가서 쉘의 명령을 실행. 다시 엔터치면 돌아온다.
- :%!ls : vi 안에 입력이 된다.

<넷째날>

- $ history : 명령어 기록

    - $ !<번호> : 해당 번호의 명령어 실행
    - ctrl+r : 입력 후 단어를 입력하면 일치하는 가장 마지막 명령이 나옴
- ll : ls -al 다 보여주는거!
- grep -r "bash" ./        : bash가 들어가는 걸 찾아주세요!
- cat hong.txt | grep "나는"        : hong.txt에서 "나는"이 들어가느 문장들만 찾는다.

[ ] bash

- A=$(seq 1 10)     : for i in range 10같은 것이다.
- let A=A-1       //그럼 A--이 된다.

<깃 팁들>

- file <파일이름> : 파일정보보기
- nm main.o      : 디버깅 비슷한거인듯?
- gcc -c myprint.c    :  컴파일하기->그럼 myprint.o가 나온다.
- gcc -o yurim myprint.o main.o      : 마이프린트랑 메인을 합쳐서 유림을 만든다. 링크작업. 이 시기에 라이브러리에서 printf같은 걸 자동으로 넣어준다.
- ldd stest : stest의 정보? 뭔 정보냐 무튼 뭔가 동적?
- gcc -c -fPIC myprint.o   : 포지션 인디펜던트 어쩌구. 위치 알 수 있는건 프로그램 시행된 후.
- vnew하고 옆 창 가려면 ctrl ww 아니면 ctrl 방향키
- vi main.c header.h 하면 화면이 하나밖에 안보여

    - 그 후 :ls 라고 하면 1. main.c 2.header.h 가 나온ㄷ.
    - :b2 하면 2번 버퍼로 이동한다.
- byobu : f2, f4로 화면을 왔다갔다 가능!

- 압축

    - 압축풀기 : $ tar xvf <압축파일이름>

    - 압축하기 : $ tar czvf <생성할 압축파일이름.tar.gz> <압축할경로>
- gcc관련 도구 설치 : $ sudo apt-get install build-essential

- 컴파일 및 실행
    - gcc -o hello hello.c
    - ./hello
    - file hello
- ctrl + d : 끝내기

<깃이 에러날때>

- git log로 상태를 보든말든
- git checkout HEAD
- git clean -f
- git pull했는데 또 에러나면
- git status를 본 다음에 에러난 파일을 확인하고
- git checkout week3/proj1/all.c 이런 식으로 그 파일을 초기화해줌
- git pull 완성!

<gcc 사용법>

- $ gcc -g -Wall -o test file1.c file2.c file3.c
    - main.c mod1.c mod2.c 를 컴파일하고 하나로 합쳐 출력파일 test를 만든다.

    - 세 파일 중에는 반드시 하나의 main이 꼭 있어야 한다.
    - -g : 디버깅 정보 포함
    - -Wall : 모든 경고 표시     //꼭 붙이는 습관을 들이는 게 좋다.

- $ gcc hello.c : 가장 간단한 사용법. 출력파일은 자동으로 a.out이 됩니다.

- $ gcc -c hello.c : hello.c를 컴파일해서 hello.o를 만든다.

- $ gcc -o test file1.o file2.o : .o를 링크해서 최종 프로그램 test를 만든다.

<make>

- make clean 하면 .o 파일들을 다 지워줌
- make 하면 gcc-W -Wall 이런거 다 지가 알아서 해준다.

<gdb>

- enter : 앞에 명령 반복적 실행
- l : 리스트. l memo이런 식으로 치면 메모 함수를 보여줌.
- b main : break point를 메인에 건다.
- info b : break point가 어디 걸려있는지 보여줌
    - d 2 : 2번 브렠포인트 지워줌
    - condition 3 n>9990 : 3번 브렠포인트에서 n이 9990이상일때만 보여줌.
- run : 실행
- n : 한 줄씩 내려간다. 함수 만나도 안으로 안들어감
- p n: print n. n변수의 상태 보여줌
- display n : 내가 어떤 명령을 치던지 n을 보여주고 한다.
    - undisplay 1 : 해제해준다.
- u : (until)의 약자. 루프를 한번에 빠져나간다.
- c : 컨티뉴. 다음 브렉포인트까지 간다.
- s : step. 다음 줄 간다. n하고 차이점은 s는 함수를 만나면 함수 안으로 자동으로 들어간다.
- backtrace : 함수들이 포함되고 뭐 이런 경로들을 보여준다. 현업에서 많이 쓰는 명령어.
- info f : gdb를 사용해서 스택을 볼 수 있다. 내공이 쌓이면 공부해라.
- make loop : 루프가 생기고 ./loop 로 실행하면 루프가 된다.
- ps -ef : 현재 돌아가고 있는 프로세스들을 다 보여준다.
    - grep loop : 루프가 돌아가는 것만 필터링해서 보여준다.
    - sudo gdb
    - ctrl+c : 돌아가고 있는 프로그램을 멈춘다
    - continue : 다시 재개.
- core
    - make core
    - ./core          //세그멘테이션 에러(OS가 프로그램을 강제로 죽여버림) 난다.
    - ulimit -S -c 1000000

    - 이제 코어가 생김. 죽은 장소를 보여줌(다잉메시지…)

    - 프로그램이 죽었을 때 코어 덤프를 통해 에러위치를 알아낼 수 있다.

- 프로세스란?

    - 프로그램을 메모리에 올려서 실행할 수 있게 만듦

    - 프로세서의 영역은 크게 몇 가지로 구분될까요? ->4가지

        - 코드(명령어) 기계어

        - 데이터(전역변수..) 스택(지역변수..), 힙(동적 메모리, new())

    - 실행 중인 프로그램 - 메모리에 존재.

    - 디스크의 프로그램과 메모리의 프로세스는 동일한가?

    - 여러 프로세스를 동시에 실행할 수 있나?

    - 프로그램은 어떤 구조를 가지고 있나?
- CPU
    - input을 두개 받아서 결과 보여줌
    - CPU가 뭘까요?

    - 레지스터 : CPU에선 직접 계산 불가능->CPU만의 계산공간(레지스터)에서 계산

- 프로그램
    - CPU가 실행할 수 있는 명령어의 순서 집합

    - 보통 어떤 목적을 달성하거나 결과를 얻기 위해 만들어 짐

    - 초창기 컴 : 프로그램 하나만 실행

    - 현대 컴퓨터 : 메모리에 다수의 프로그램을 적재(저장)하고 실행해야 함

        - 필요에 의해 프로세스의 개념이 탄생
- gcc
    - gnu에서 제작한 컴파일러

    - 사실은 전처리기, 컴파일러, 링커 각각 따로 있다.

- 여러 개로 파일 분할하기

    - 한 프로젝트는 여러 개의 .c 파일과 .h파일로 나뉩니다.
    - .h : 헤더파일. 재사용된 함수, 변수 등을 선언해 놓는다.
    - .c : 소스파일 : 헤더파일에서 선언한 함수를 실제로 구현.

    - 유사한 기능을 하나의 헤더에 묶어서 놓는다.
        - ex) stdio.h와 printf.c scanf.c ->표준 IO관련 함수들

    - 분할된 파일의 컴파일 절차
        - 1. 모든 .c를 컴파일해서 .o로 만든다.실제는 전처리+컴파일 과정
        - 2. 생성된 .o를 모두 묶어서 실행파일로 만든다. 실제는 링크 과정만 수행

- 정적 라이브러리(아카이브)

    - 여러 .o파일들을 하나로 묶어 놓은 것.
    - libXXX.a처럼 lib로 시작하고 .a의 확장자를 가짐(윈도우에선 .lib)

    - 아카이브는 하나 이상의 .o로 구성됨
    - .o는 하나 이상의 함수로 구성됨

    - 컴파일시 링커에 의해 프로그램에 포함됨

    - 프로그램의 용량이 커진다

    - 컴파일 후에는 더이상 .a 가 필요 ㄴㄴ.

- 동적 라이브러리
    - .so는 동적(공유)라이브러리. 윈도우에선 DLL이라 부름

    - 여러 프로그램이 공유해서 사용

    - 프로그램의 크기가 작아짐

    - 매우 약간 속도 느림(찾느라)

    - 에러대처가 훨 쉬움(자동으로 바뀐게 적용되서)

    - 컴파일시엔 포함 안되다가 실행시에 다이나믹링커와 로더에 의해 메모리에 올라감

        - 다이나믹 링커 : /lib/ld-linux.so.2

        - 리눅스의 로더는 exec()시스템 콜을 의미

        - 프로그램에는 plt라 불리는 정보만 추가됨

<4-1 Make>

- make

    - 프로젝트 규모가 커지면 수동으로 컴파일하기 힘들어짐 ->자동으로 빌드해주는 도구가 make
    - makefile이란 파일에 적혀있는 규칙대로 프로그램을 빌드한다.cc

- gdb사용법

    - $ gdb <실행파일이름>

    - $ gdb <실행파일이름> <pid> : 실행중인 프로그램을 디버깅할때

    - $ gdb <실행파일이름> <코어덤프이름> : 덤프만 남기고 죽은 프로세스를 디버깅할때
    - (gdb) q 아니면 ctrl_d : 종료

    - 소스코드 보기 :
        - (gdb) l [줄번호] | [함수이름]    (l은 리스트의 약자)

- 엔터 : 가장 중요한 명령!

    - 엔터만 치면 앞 명령을 반복수행
- (gdb) run [매개변수] : 불러온 프로그램을 실행. 매개변수는 옵션

- 브레이크 포인트
    - (gdb) b <줄번호> | <함수이름> : 브렉포인트 설정
    - (gdb) b [파일이름]:<함수이름>
    - (gdb) info b : 설정된 브뤸포인트의 번호를 볼 수 있음
    - s : 스텝. 한 줄 지나가기. 함수만나면 들어감 s6 하면 6줄 지나감
    - n : 넥스트. 한줄 지나가기. 함수만나면 통과
    - c :  컨티뉴. 다음 브렉포인트까지 계속
    - u : 루프를 빠져나감
    - finish : 현재 함수를 빠져나감
    - info b : 브렉포인트 고유번호 보기
    - d <고유번호> : 브렉포인트 삭제

    - 브렉포인트에 조건걸기 (유용함)
        - b <라인번호> if <조건식>
        - b 19 if n>100
        - condition <고유번호> <조건식>    이런 식으로도 할 수 있다.

- 와치 포인트

    - 특정 변수의 값이 바뀌면 멈춤
    - gdb) watch <변수명>
    - gdb) b 19
    - gdb) run
    - gdb) watch n if n>9000

- 변수값 출력

    - 간단하게 변수값 볼 수 있다
    - gdb) p <변수명>
    - gdb) display <변수명>  : 매번 자동으로 변수값 출력. 해제는 underplay

- 스택 정보 보기
    -   gdb) info f

    - 중요한데 어려움
- backtrace 보기
    -  gdb) backtrace

- 코어 덤프

    - 죽기전에 남기는 파일

    - 키보드로 종료 명령 내리거나, 잘못된 명령 수행하거나, 기타 오류상황일때 생김

- 실행중인 프로그램 디버깅하기
    - sudo gdb <프로그램명> <pid>

[ ] thread

- CPU이용의 기본단위. 독립적으로 실행되는 코드집합.
- light weight process라고 부르기도 함.

- 하나의 프로세스 내에 하나 이상 스레드 존재.

    - 하나의 프로그램을 여러 개의 스레드로 동시에 혹은 나누어서 병렬적으로 수행.

- 각 스레드는 스레드 ID, 프로그램카운터(PC), 레지스터 집합, 스택 을 독립적으로 소유

- 같은 프로그램 내의 스레드는 코드(텍스트 영역), 데이터 영역, 열린 파일 등의 시스템 자원을 공유

    - 같은 프로세스의 스레드들은 코드와 힙 영역을 공유

    - 클래스 멤버변수랑 static변수는 스레드들이 모두 공유

    - 독립적인 주소공간(메모리영역)은 없으며 다른 스레드와 공유

[ ] Multithreading Model

- 사용자스레드와 커널스레드의 관계
    - to 사용자 스레드가 CPU를 할당받아 실행, must 커널스레드에 연결되어야 한다. (mapping, binding)

[ ] Java Thread

- 자바 프로그램에서 프로그램을 실행하는 근본적인 방법
    - main() 메서드 만으로 이루어진 프로그램도 하나의 스레드로 실행됨

    - 호스트 운영체제가 제공하는 스레드 모델을 이용하여 구현

- 자바 프로그램에서 스레드를 생성하는 방법
    - thread클래스에서 파생된 새로운 클래스를 생성하고, run()메서드를 재정의(Override).
    - Runnable인터페이스를 구현하는 클래스를 정의

        - 보다 일반적인 방법

[ ] 의미?

- 태스크 : 작업을 수행하기 위한 작업의 소유권자의 단위

    - 커널 내부의 작업의 단위.

    - 작업하다 밑에 내려놓으면 그게 쓰레드가 됨.(??)

- 프로세스 : 실행 중인 프로그램

- 쓰레드 : 프로세스의 실행 단위

    - 프로세스든, 쓰레드든 리눅스에선 내부적으로 task_struct라는 구조체로 통일 관리됨.

[ ] 리눅스의 작업관리

- 리눅스 내부(=커널)은 작업의 단위를 태스크로 관리.
    - OS책의 커널 쓰레드 : 태스크

- 사용자는 프로세스 혹은 쓰레드를 생성하여 일을 한다.

[ ] 쓰레드

- 프로그램의 흐름 또는 이 흐름의 단위

    - 프로그램을 컴파일하고 실행하면 무언가 흘러간다는 걸 느낍니다.

    - 스레드 하나가 있기 때문.

- 멀티 프로그래밍 환경의 꽃

- 정의

    - 프로세스의 실행 콘텍스트(execution context)

    - 프로세스 실행 단위

    - 하나의 프로세스엔 적어도 하나의 쓰레드가 존재

- 멀티 쓰레드

    - 하나의 프로세스에 여러 개의 쓰레드
- Thread클래스와 Runnable 인터페이스

    - 차이 : 다중 상속 문제로 Runnable을 더 많이 씁니다.
    - Runnable :  '실행 가능'하도록 구현해라.
        - implements Runnable
        - public void run() 구현

        - 실행이 가능해졌으니 쓰레드로 만들기 가능

[ ] NPTL

- Native Posix Thread Library. 요즘 리눅스의 쓰레드 관리 라이브러리

- 옛날엔 프로세스랑 쓰레드 모두 커널 내부의 태스크와 1:1로 대응되는 성능 나쁜 방식이었다.

- 그러다 M:N방식의 NGPT 와 1:1방식을 개선한 NPTL이 각자 싸우게 됨 ㄷㄷ

- 그런데 리눅스 2.6에서 잉고 몰라가 0(1) 스케쥴러라는 엄청난걸 만들어버림

    - 스케쥴링 오버헤드가 0(1)이라 그런이름.

    - 덕분에 NPTL이 대세가 됨

    - 리눅스의 약점을 극복하게 된 계기.->자바는 스레드를 사용하기 때문에 자바의 성능 향상됨(기존에 있었던 쓰레드 생성, 소멸의 오버헤드가 메우 작아짐)

[ ] 프로세스의 추가 생성

- fork()시스템 콜을 통해 추가 생성이 됨.

- 생성하는 쪽이 부모, 생성되는 쪽이 자식 프로세스가 됨.

- 최초에 부모와 자식은 완전히 동일한 두 개의 프로세스.

- 일반적으로 자식 프로세스는 바로 exec()을 통해 부모와 다른 코드로 바뀌게 됨.

[ ] 스레드의 추가 생성

- 처음 자바 프로그램을 시작하면 JVM이 스레드를 하나 만든다.

    - 그리고 main()메소드를 실행
- Thread인스턴스의  start()메서드를 실행하면 추가 스레드가 생성됨

    - 그리고 run()메서드를 실행함.

- 정리 :

    - 메인스레드 : main() 실행

    - 추가로만든스레드 : run()실행

[ ] 자바는?

- 자바의 기본 작업 단위는 메소드.

- 그리고 쓰레드를 이용해 메서드를 실행.

[ ] 동기화

- 정확한 결과를 위해선 동기화를 보장해줘야 합니다.

    - 자바에선 메서드 동기화와 클래스 동기화 두 가지 방법을 제공.

    - 그런데 동기화를 지나치게 적용하면 성능 좋지 않음.

        - 한 번에 하나씩 하니까.

- 동기화 방법

    - 메서드 동기화 : 메서드 앞에 synchronized를 붙인다: 해당 메서드는 절대 두 개가 동시에 실행되지 않는다.

        - 해당 메서드 안의 공유 변수에 대해 동기화를 보장.

    - 클래스 동기화 : 동기화 블록이라고도 함. 동기화가 필요한 클래스가 있을 때 사용.

<강이의 자바 강좌 정리>
출처 : http://alecture.blogspot.kr/2011/05/thread.html

[ ] 자바의 쓰레드(Thread)

- 자바의 스레드 : in 동시 프로그래밍의 영역

    - 스레드 & 프로세스 : 동시 프로그래밍이 가능하도록 만들어주는 기본 단위. (대부분 쓰레드가 차지)

- 자바 공부하는 사람들이 쓰레드 어려워한다. 그러지말쟈 ^^

- 프로세스 : 컴퓨터에서 연속적으로 실행되고 있는 프로그램.

    - 멀티프로세싱 : 여러 개의 프로세서 사용

    - 멀티태스킹 : 여러 개의 프로그램을 같은 시간에 시분할방식으로 돌리는거.

- 쓰레드 : 프로세스 내에서 실행되는 흐름의 단위.

    - 하나의 프로그램은 최소한 하나의 쓰레드(main thread)를 가짐.

    - 멀티쓰레드 : 프로그램에 따라 둘 이상의 쓰레드 실행 가능

    - 컴으로 웹서핑하면서 음악듣기 ~ 쓰레드 사용.

    - 프로세스보다 리소스도 덜 잡아먹고 효율적이다.

    - 자바 클래스 내부에 보편저긍로 쓰레드 기능이 적용되고 있어서 눈으로 확인 못했을 뿐 자바가 알아서 처리해주고 있었다!!

    - 우리가 흔히 써왔던 메인메서드를 메인쓰레드라 생각하면 됨.

[ ] 쓰레드 사용법

- run() : 쓰레드 만들고 실행시키기 위해 오버라이드 해야하는 메서드.

    - 인터페이스로 구현해서 간접적으로 Thread클래스 사용.
    - Thread클래스는 java.lang 패키지에 들어있다.

    - 인터페이스라 다른 클래스 상속받을 수 있음. 일반적으로 이거 씀.

-
    - Thread라는 클래스 직접 상속받아 쓰레드 만들기

    - 단점 : 자바는 다중상속이 안되서 이 클래스는 더이상 다른 클래스 상속받을 수 없음.

[ ] sleep()메서드

- 뭔가 하다가 일시중지하는 명령어
- 1/1000초 (millisecond)로 세팅됨. 인자에 값 넣어주면 넣어준 값만큼 시간 지연.

- 직접 해보면 초신기해!

- 근데 예외처리 해야함. throws InterruptedException

[ ] join()메서드

-  쓰레드가 끝날때까지 친절하게 기다려준다. 끝나고 다음 명령 실행.

- 예외처리 필요. throw InterruptedException
- isAlive() : 쓰레드가 살아있는지 확인하는 메서드

- 쓰레드를 이용하면 동시다발적인 현상이 발생 ->join은 이런 걸 제어해줄때 사용.
- join(long millis) 안에 숫자 넣으면, 쓰레드를 1/1000로만큼 기다린다.

[ ] 다중스레드

- 각 쓰레드에 대한 명령을 일정시간 돌아가면서 실행 =>사용자는 동시에 실행되는걸로 보임 ㅋ

- 작업을 쓰레드별로 쪼개서 담당 처리한다 생각해도 ㄱㅊ

[ ] 파일 시스템

- 저장장치 : 데이터를 물리적으로 저잦ㅇ하기 위한 장치

    - 하드디스크, USB메모리, 시디롬, 네트워크 장치…

- 파일시스템

    - 실제 물리적 저장장치에 데이터를 저장하기 위한 계층

    - 파일에 대한 일관적인 논리적 관점을 제공

    - 서로 종류도 특성도 완전히 다른 물리적 저장장치지만 사용자에게는 동일하게 파일을 저장하고 관리하는 장치로 보임

- 마운트

    - 물리적인 저장장치를 특정 논리적인 접근지점과 연결하는 행동
        - ex)윈도우의 디스크 마운트
        - c:/    <-하드디스크
        - e:/    <-시디롬

        - 윈도우의 경우는 대부분 자동으로 마운트가 됨

    - 리눅스의 경우는 일반적으로 최상위 디렉토리인 /(root)에 메인 드라이브가 마운트됨
- gdb사용법

    - $ gdb <실행파일이름>

    - $ gdb <실행파일이름> <pid> : 실행중인 프로그램을 디버깅할때

    - $ gdb <실행파일이름> <코어덤프이름> : 덤프만 남기고 죽은 프로세스를 디버깅할때
    - (gdb) q 아니면 ctrl_d : 종료

    - 소스코드 보기 :
        - (gdb) l [줄번호] | [함수이름]    (l은 리스트의 약자)

- 엔터 : 가장 중요한 명령!

    - 엔터만 치면 앞 명령을 반복수행
- (gdb) run [매개변수] : 불러온 프로그램을 실행. 매개변수는 옵션

- 브레이크 포인트
    - (gdb) b <줄번호> | <함수이름> : 브렉포인트 설정
    - (gdb) b [파일이름]:<함수이름>
    - (gdb) info b : 설정된 브뤸포인트의 번호를 볼 수 있음
    - s : 스텝. 한 줄 지나가기. 함수만나면 들어감 s6 하면 6줄 지나감
    - n : 넥스트. 한줄 지나가기. 함수만나면 통과
    - c :  컨티뉴. 다음 브렉포인트까지 계속
    - u : 루프를 빠져나감
    - finish : 현재 함수를 빠져나감
    - info b : 브렉포인트 고유번호 보기
    - d <고유번호> : 브렉포인트 삭제

    - 브렉포인트에 조건걸기 (유용함)
        - b <라인번호> if <조건식>
        - b 19 if n>100
        - condition <고유번호> <조건식>    이런 식으로도 할 수 있다.

- 와치 포인트

    - 특정 변수의 값이 바뀌면 멈춤
    - gdb) watch <변수명>
    - gdb) b 19
    - gdb) run
    - gdb) watch n if n>9000

- 변수값 출력

    - 간단하게 변수값 볼 수 있다
    - gdb) p <변수명>
    - gdb) display <변수명>  : 매번 자동으로 변수값 출력. 해제는 underplay

- 스택 정보 보기
    -   gdb) info f

    - 중요한데 어려움
- backtrace 보기
    -  gdb) backtrace

- 코어 덤프

    - 죽기전에 남기는 파일

    - 키보드로 종료 명령 내리거나, 잘못된 명령 수행하거나, 기타 오류상황일때 생김

- 실행중인 프로그램 디버깅하기
    - sudo gdb <프로그램명> <pid>
