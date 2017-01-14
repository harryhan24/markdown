# Linux Command Part1


## 기본명령어

### sudo && su
다른 유저의 권한으로 명령할때 실행하며 -u 인자를 통해서  유저를 설정하는게 가능하다. 생략할경우 superuser 권한 su 와 sudo 차이점은 sudo의 경우 새로운 쉘로 전환되지 않는다.

### 유틸리티
#### cal
달력
#### date 날짜

### cd

1. cd 홈디렉토리
2. cd - 이전 작업 디렉토리
3. cd -username 해당 사용자의 홈 디렉토리

###  ls

1. -l 자세히
2. -ls 자세하고 시간순
3. -lsr 자세하게 시간역순
4. -s 파일크기순
5. -h 파일크기 사람 친화적
6. -d  현재 디렉토리 내용 (주로 -ld)

-rw-r--r--/1/dongsuhan/staff/3.0K/12 17 00:36/source-install.log
권한/하드링크수/소유자/그룹/크기/수정날짜/파일명


| -rw-r--r-- | 1 | dongsuhan | staff | 3.0K | 12 17 00:36 | source-install.log |
|----------|-------------|---|---|---|---|------:|
| 권한 | 하드링크수 | 소유자 | 그룹 | 크기 | 수정날짜 | 파일명 |

## 복사 및 삭제
### cp
- -a 소유자 상태 정보까지 복사
- -i 덮어쓸 경우 물어봄
- -r 디렉토리 복사
- -u 업데이트
- -v (verbose) 끝나고 알려줌

### mv
moving
cp와 인자값이 대체로 비슷

### rm
- -r 재귀적 디렉토리까지 전부 삭제합니다.
- -f
rf -rf file file2 에서 file1이 존재하지 않아도 삭제명령 진행


### ln
- -s 소프트링크
- -h 하드링크


## 입출력

### alias
명령어 약속어
ex) alias foo='cd /usr;ls;cd;';
### type command
명령어 타입 확인
### which 명령어 위치

### ">"
출력 방향
date > a.txt

 ### ">>"
이어쓰기

### "2>"
표준오류 아웃풋

### 오류출력 분기
```shell
ls -R / > a.txt 2> error.log
```

### cat
파일을 읽어내서 내보냄
- cat<lazt_dob.txt 파일읽어서 출력
- cat>lazt_dob.txt 텍스트를 입력받아 txt생성

### 파이프라인

"|" 를 통한 체이닝

- ls /bin /usr/bin | sort | less (분류 후 less로 실행)

- ls /bin /usr/bin | sort | uniq| less (분류 후 중복 거른 후 less로 실행)

### tail, head

```
head -n 5 a.txt
tail -n 5 a.txt

ls /usr/bin | tail -n 5

```

### tee
표준 입력을 읽어 표준 출력과 파일에 출력
ls /usr/bin | tee a.txt | grep zip
a.txt에 저장하고 zip이 들어가는 파일만 또 출력

### echo


- echo * = 전체파일명
- echo \*s = s로 끝나는 모든
- echo [[:upper:]]* = 대문자로 모든.
- echo $(( 2 + 2 )) 계산식
- echo ~ 현재 사용자 홈디렉토리
- echo ~foo foo라는 사용자 홈디렉토리
- echo 4 is = $(( 2 + 2 ))  확장 문법
echo number_{{1..5}}
= number1 number2 number3 number4 number5


### printenv
모든 매개변수 출력

### hisotry
입력한 명령어 리스트

- !number == 해당 명령어 실행.
- !! 마지막 명령어 반복실행
- !string = 이 문자열로 시작하는 가장 최근 입력 항목 선택



## 퍼미션

### id
사용자 id
###  chmod
권한변경
###  umask  
기본 퍼밋션 마스크 설정
###  chown
소유권 변경
bob to bob
bob:user //bob으로 바꾸고 그룹유저 user로
:admin = 그룹유저만
bob: bob으로 바꾸고 그룹유저도 bob 으로

###  chgrp 그룹 소유자 변경
### passwd 사용자 비밀번호 변경



## 프로세스

### ps aux
자세한 프로세스 상태
### top
동적인 상태 프로세스 모니터링
### kill
kill -15 종료하라고 명령함
kill -9 강제종료
killall xlogo = xlogo 이름 들어간 프로그램 다 종료

pstress = 프로세스 간 자식관계

### jobs
현재 실행중인 작업 목록

### fg
중지된 포어그라운드 프로세스를 보여주거나 하나뿐이 없을경우 해당 프로세스 실행
fg %2, fg %3 과 같은 형식으로 프로세스를 실행함

### bg
실행을 시킬 때 끝에 &를 넣어줄경우 백그라운드 앱으로 실행
