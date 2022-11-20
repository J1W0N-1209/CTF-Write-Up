### **Network - 번역기**

와이어샤크로 패킷파일을 열어봅니다.

File - Exports Objects - Http 를 선택해서 파일들을 추출합니다.

qjsdurrl.hwp 파일을 열어보면 다음과 같은 내용이 나옵니다.

![화면 캡처 2022-11-12 110643.png](https://s3-us-west-2.amazonaws.com/secure.notion-static.com/6d4f003a-876b-4f0f-a4f7-bd916bb11209/%ED%99%94%EB%A9%B4_%EC%BA%A1%EC%B2%98_2022-11-12_110643.png)

질문에 대한 답은 blue 이므로

플레그 포맷에 맞쳐서 제출합니다

Flag : HSOC{blue}

### Network - TimeStamp

TCP Follow Steam 기능을 이용하면 문제를 풀 수 있습니다

Stream이 3일 때 쿠키가 세팅 됩니다

이 때 Date는  Sat, 05 Nov 2022 05:27:36 GMT 입니다

Flag : HSOC{20221105}

### ****FORENSIC - isekai..!****

HxD로 HSOC을 필터링하면 HSOC{li1p4_i 라는값이 나옵니다

그리고 } 이것을 필터링하면 나머지 플레그가 뜹니다

Flag : HSOC{li1p4_i5_l3geN0}

### WEB - 개발자의 실수

개발자 도구를 열어 network 창에 들어가면

atob (SFNPQ3t5b3VfZm91bmRfdGhlX2ZsYWd9) 라는 주석이 보입니다

SFNPQ3t5b3VfZm91bmRfdGhlX2ZsYWd9 를 base64 decoding 하면 플레그가 뜹니다

Flag : HSOC{you_found_the_flag}

### SYSTEM - ㄹㅇ 창식이

real.c

```c
#include<stdio.h>
#include<stdlib.h>
#include<string.h>
#include<unistd.h>
char buf[32];
	int main() {
	int num;
	printf("What is your favorite number? : ");
	scanf("%d", &num);
	int real = num ^ 0x123ef;
	int rea1 = real ^ 0x8201;

	int fd = rea1 - 0x12345;
	int len = 0;
	len = read(fd, buf, 32);
	if(!strcmp("R3AL\n", buf)){
		printf("!!!!!!!!PERPECT!!!!!!!!\n");
		system("cat flag");
		exit(0);
	}
	printf("Good number!");
	return 0;

}
```

read(fd, buf, 32) 에서 fd를 0으로 만들어야
숫자를 입력받을 수 있습니다

rea1 = 0x12345
real ^ 0x8201 = 0x12345
real = 0x12345 ^ 0x8201
real = 0x1A144
num ^ 0x1A144 = 0x123ef
num = 0x123ef ^ 0x1A144
num = 82AB

82AB를 10진수로 고치면 33,451이다
그 다음에 R3AL을 입력해주면 플레그가 뜹니다

Flag : HSOC{R3A1_f14g}

### MISC - mic check

디스코드에 플래그가 나와 있습니다
