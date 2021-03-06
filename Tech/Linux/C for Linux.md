## 1. 리눅스의 특징

개발자인 필자의 입장에서 리눅스는 **또 다른 Unix 운영체제**다. 여기에 소개된 리눅스의 특징은 거의 대부분이 Unix의 특징 그대로이다. Linux의 특징을 배우면서 덤으로 Unix의 특징까지 배우게 되니 **일석이조**라 할 수 있겠다.

리눅스의 특징을 자세히 다루는 것은 이 문서의 범위를 완전히 벗어난다. 여기에서는 개발환경을 이해할 수 있는 수준에서의 최소한의 내용만 다룰 것이다.

유닉스가 모든 리눅스의 특징을 가지고 있으므로, 설명에서는 Unix로 통일하도록 하겠다.

#### 다중 사용자

개인이 사용하는 PC(:12)의 운영체제로 만들어졌던 DOS(:12), Windows(:12)와는 달리 Unix는 처음부터 중대형의 컴퓨터를 제어할 목적으로 만들어진 운영체제다. 그런이유로 처음부터 다중사용자 지원을 고려해서 설계가 되었다.

이런 다중 사용자는 대부분의 경우 물리적으로 컴퓨터에서 멀리 떨어져 있으며, NetWork(:12)를 이용해서 접속 하게 된다. Unix는 접속이 유효한 접속인지 아닌지(불법적인 사용자나 크래커)를 판단하기 위해서 ID:Password 방식의 Login(:12) 시스템을 지원한다.

#### 다중 프로세스

프로세스란 운영체제위에서 주어진일을 하는 프로그램의 실행 이미지다. Unix는 다중의 사용자를 지원하고 있으므로, 동시에 여러개의 프로세스를 지원 할 수 있도록 만들어졌다. **A**사용자가 웹 브라우진을 하는 동안 **B**사용자는 DataBase(:12)작업을 하면서 동시에 mp3(:12)를 감상할 수 있다.

#### 높은 이식성

Unix는 운영체제의 80% 이상이 C언어로 만들어졌다. 이는 다른 종류의 컴퓨터에 쉽게 이식할 수 있음을 말한다. Unix는 거의 대부분의 중대형 컴퓨터와 PC/임베디드기기 - Linux -에 설치되어 있다.

#### 단순함

추상적이긴 하지만 유닉스의 **단순함**은 유닉스의 대표적인 특징이다. 윈도우 사용자가 Unix를 제일 접하면 느끼는게 단순함에서 오는 황당함이다. 도스시절을 보는 것과 같이 컴은 바탕화면에 프롬프트만 깜빡이고 있는걸 보면서 절망을 느낀 사용자도 꽤나 있었을 것이다.

게다가 프로그램역시 너무나 무성의 하기 그지 없다. 아기자기한 아이콘과 다양한 부가기능을 제공하며 마우스 클릭으로 필요한 일을 해결할 수 있는 윈도우와는 달리 Unix의 프로그램은 직접 타이핑을 하고 옵션을 줘서 일을 수행해야 한다. 유닉스 환경에 매우 익숙한 개발자라고 하더라도 파일의 목록을 보여주는 **ls**의 옵션을 완벽하게 이해하고 사용하는 사람은 아마도 없을 것이다.

그러나 모순되게도 이러한 단순함이 유닉스를 강력하게 만들어준다. 유닉스의 대부분의 기능과 프로그램들은 자기에게 주어진 일만 하며, 복잡한 작업은 철저히 분업화 함으로써 수행을 한다. 텍스트 파일의 내용을 읽어서 Linux가 포함된 라인을 따로 저장하는 일을 하고 싶다고 가정해보자. 간단한 작업같지만 윈도우에서 이러한 일은 **원하는 프로그램**을 찾아야 하는 지루한 과정을 거쳐야 한다. 유닉스는 아래와 같이 간단하게 해결할 수 있다.

```
# cat sample.txt | grep "Linux" > Linux.txt
```

파일의 내용을 출력하는 **cat**을 이용해서 내용을 읽어오고, 읽어온 내용을 문자열을 비교할 수 있는 기능을 가진 **grep**에 보내어서 Linux를 포함한 라인을 Linux.txt에 저장하는 방식이다. 철저히 분업화 되어있음을 알 수 있다.

이러한 **단순함**은 파이프(:12)와 재지향(:12)이라는 기술을 통해서 얻어지는 특징이다. 파이프와 재지향에 대해서는 따로 다루게 될 것이다.



## 2.리눅스 환경

리눅스의 환경을 개발에 필요한 최소한의 수준에서 알아보도록 하겠다.

#### Shell

우리가 컴퓨터를 사용하는데 있어서, 컴퓨터와 운영체제의 복잡한 구성을 이해하고 있을 필요는 없다. 그래야 한다면 컴퓨터는 단지 전문가의 전유물이 되었을 것이다. Shell(:12)은 조개껍질이 내부를 감추는 것처럼 컴퓨터와 운영체제를 내부로 숨긴다. Shell을 이용하는 사용자는 운영체제가 어떻게 명령을 수행하는지 등의 복잡한 것에 신경 쓸필요 없이 shell에 간단히 명령을 내림으로써 필요한 작업을 할 수 있도록 만들어준다.

attachment:shell.gif

shell은 이를테면 운영체제와 사용자를 연결해주는 일을 하는 프로그램이라고 할 수 있다. 여러종류의 게임이 있듯이 shell도 여러종류의 쉘이 있다. **ksh**, **csh**, **bash**, **zshell**등이 있으며 리눅스 환경에서는 bash(:12)쉘이 가장 널리 사용된다. 쉘 프로그램이라고 부르기도 한다.

쉘은 프롬프트라는 것을 통해서 사용자의 입력을 받아들여서 필요한 일을 수행한다.

attachment:prompt.jpg

윈도우즈에서도 **cmd**라고 불리우는 쉘을 띄울 수는 있지만, 유닉스의 쉘은 윈도우즈의 쉘과는 다른 차원의 것이다. GUI화면에서 마우스 클릭으로 거의 대부분의 일을 처리하는 윈도우즈와는 달리 유닉스는 거의 모든 작업이 쉘에서 이루어진다. 비록 KDE(:12)와 Gnome(:12)와 같은 데스크탑 환경이 나오긴 했지만, 여전히 많은 유닉스 유저들이 데스크탑환경을 단지 많은 **쉘 창**을 띄우기 위한 용도로 사용할 뿐이다.

#### 모든 것은 파일이다

유닉스는 모든걸 파일(:12)로 취급한다. 위에 잠깐 언급되었던 것처럼 디렉토리(:12)도 (특수한 형태)의 파일로 취급할 뿐만 아니라, 하드디스크, 이더넷카드, 프린터, 각종 입출력 포트(USB, PS/2, Serial)등 모든 장치까지 파일로 취급한다. 예를 들자면 하드디스크는 **/dev/hda1**, **/dev/hda2**, 플로피디스크 드라이브는 **/dev/fd0**이름의 파일로 관리한다.

윈도우즈유저라면 이러한 환경이 낯설게 느껴지겠지만, 이는 적어도 개발자의 입장에서 봤을 때는 매우 합리적인 구조다. 모든 걸 파일이라는 동일한 객체로 보게 됨으로써, 동일한 프로그래밍 방식을 적용할 수 있기 때문이다. 각각의 장치를 위한 프로토콜은 제외하더라도, 장치에 읽고/쓰는데 있어서 동일한 프로그래밍 기법을 사용할 수 있으므로 개발 시간을 크게 단축시킬 수 있다.

이러한 장치와 관련된 특수한 파일들은 **/dev**밑에 위치한다.

#### 파이프와 재지향

Pipe(파이프)는 한쪽 객체에서 다른쪽 객체로 어떤 물건을 보내기 위한 통로로 사용된다. 상하수도관이 대표적인 경우가 될것이다. 컨테이너벨트역시 형태는 다르지만 물건을 보내기 위한 통로로 사용된다는 점에서 일종의 파이프라고 할 수 있다.

Unix(:12)역시 객체 사이의 물건을 전달하기 위한 목적으로 **파이프**를 사용한다. 여기에서 객체는 운영체제(:12)에서 어떤 작업을 수행하는 최소단위인 **프로세스**가되며, 물건은 일련의 연속된 bit로 이루어진 **데이터**가 된다.

```
  +------------+        PIPE       +------------+
  | Process A  | --------||------> | Process B  |
  +------------+                   +------------+
```



파이프는 유닉스 시스템에서 프로세스간 데이터를 전달하기 위해서 가장널리 필수적으로 사용되는 설비다. 다음은 유닉스에서 파이프를 통해서 작업을 하는 일반적인 예다. 파이프없는 유닉스는 앙꼬 없는 찐빵이라 할 수 있다. 쉘에서는 **|**를 이용해서 파이프를 이용할 수 있다.

```
// 프로세스 중에서 vi의 정보를 얻어온다. 
# ps -ef | grep vi 

// file.txt를 읽어서 몇라인으로 구성되어 있는지 확인한다. 
# cat file.txt | wc -l 

// 확장자가 .txt인 모든 파일을 읽어서 "joinc"문자열을 가진 파일을 얻어온다.
# cat *.txt | grep "joinc"

// 프로세스 중에서 root유저가 실행한 vi의 정보를 얻어온다.
# ps -ef | grep vi | grep root
```

**재지향**은 **다른 곳으로 향하게 한다**라는 뜻을 가지고 있다. 예를 들자면 화면에 출력되는 데이터를 **파일**이나 **프린터**등으로 보내기 위한 용도로 사용할 수 있는데, 이 경우 데이터를 **파일로 재지향**한다. 데이터를 **프린터**로 재지향 한다. 라고 말한다. 쉘에서는 **>**를 이용해서 재지향 할 수 있다.

```
// 프로세스 중에서 root유저가 실행한 vi의 정보를 화면이 아닌  
// rootvi.txt 파일로 재지향한다. 
# ps -ef | grep vi | grep root >  rootvi.txt 

// rootvi.txt 파일의 내용을 프린터로 재지향 한다.
// 프린터가 설정되어 있다면 출력이 될 것이다.
# cat rootvi.txt > lp0
```

**>**를 이용해서 재지향 할경우 동일한 이름의 파일이 없다면 새로 생성될 것이다. 만약 동일한 이름의 이름의 파일이 있다면, 덮어써버리게 된다. 덮어쓰지 않고 마지막부터 추가되게 할려면 **>>**를 이용하면 된다.

```
// newaddr.txt를 읽어서 addr.txt 파일에 추가한다. 
# cat newaddr.txt >> addr.txt
```

#### 표준입력,표준출력,표준에러

컴퓨터로 우리가 하는 일은 결국 **입력**과 **출력** 두가지 작업으로 요약될 수 있다. 우리가 입력을 통해서 컴퓨터로 명령을 전달하면, 그 결과는 출력의 형태로 우리에게 전달된다. 입력은 키보드로 출력은 모니터를 통해서 이루어진다.



키보드로 통해서 이루어지는 입력을 **표준입력(:12)**이라고 하며, 모니터를 통해서 이루어지는 출력을 **표준출력(:12)**이라고 한다. 그렇다면 **표준에러**란 무엇인가. 입력은 무조건 하나가 되겠지만, 출력은 한가지 이상이 될 수 있다. 작업을 제대로 마쳤을 경우의 출력결과가 있을 수 있지만 작업을 실패했을 경우의 출력결과가 있을 수도 있기 때문이다. **표준에러**는 작업에 실패했다라는 것을 사용자에게 알려주기 위해서 사용한다.



Unix에서는 이러한 입력과 출력까지도 파일로 관리를 한다. 이 파일들은 다음과 같이 입력과 출력에 대응되는 숫자로된 이름을 가지고 있다.

| 표준입력 | 0    |
| -------- | ---- |
| 표준출력 | 1    |
| 표준에러 | 2    |

이를 이용해서 재지향을 시킬 때, 표준에러와 표준에러를 따로 저장할 수도 있다.

```
// 표준출력을 suessvalue.txt로 재지향 한다. 
# ./prog 1> suessvalue.txt

// 표준에러를 error.txt 파일로 저장한다.
# ./prog 2> error.txt
```

다음과 같은 방법으로 표준에러를 표준출력으로 재지향 시킬 수도 있다.

```
#./prog 2>&1
```



#### 계정

리눅스 역시 다른 유닉스들과 마찬가지로 다중사용자 운영체제이다. 이렇다 보니 시스템 자원에 대한 접근권한이 매우 중요해 진다. 예를 들어 특정 유저의 개인 신상정보를 가진 파일은 결코 다른 유저들이 볼 수 있어서는 안될 것이며 shutdown(:12)과 같은 시스템 다운 명령은 특수한 유저(슈퍼유저)만이 제한적으로 실행 가능 해야 할것이다. 아무튼 네트워크장치, 파일, 프로세스, 장치(디스크, CD-ROM, 프린터등)의 모든 시스템 자원에 대해서 사용자 계정수준에서의 접근제어와 관련된 제한이 필요하게 될 것이다. 회사의 직책과 관련된 시스템과 동일하다고 보면 된다. 일반 사원인지, 대리인지, 과장인지, 사장인지에 따라서 접근할수 있는 회사자원의 레벨이 결정되는 것과 마찬가지다. 일반 공지사항이야 전직원이 볼 수 있지만 경영과 관련된 중요 문건은 최고경영진만 볼수 있어야 할것이다.

##### 유저

회사로 치면 사원 개개인이다. 리눅스 시스템 관점에서 보자면 시스템에 접근할 수 있는 최소단위 객체가 된다. 유저는 접근을 위해서 자신의 ID와 패스워드를 가지며, 이외에도 시스템에서의 원할한 활동을 위한 "사용자 홈디렉토리", "사용자 쉘", "포함되는 그룹"과 같은 각종 부가적인 정보들을 가지게 된다. 리눅스에서 유저는 크게 2개로 나누게 된다. 절대적인 권한을 가지는 슈퍼유저와 일반유저 유저다.

**슈퍼유저**는 보통 ID로 **root**를 가지며 시스템에서 절대적인 영향력을 행사한다. 시스템의 셧다운, 리부팅, 장치의 제어, 유저제어, 파일제어에 있어서 전혀 제한이 없다. 마음만 먹는다면 **rm -rf /**로 시스템의 모든 파일을 날려버릴 수도 있는 절대 권한자이다. 워낙에 막강한 권한을 가지고 있기 때문에 운영체제 자체를 파괴해 버리는 어처구니 없는 실수를 할 수도 있다. 해서 몇몇 상용운영체제들은 슈퍼유저라도 파워에 제한을 두기도 한다.

일반 유저는 슈퍼유저를 제외한 나머지 유저를 가리킨다. 일반유저는 슈퍼유저가 정하는 바에 따라서 시스템내에서의 권한과 활동영역에 있어서 제한을 받게 된다.

##### 그룹

회사에서는 인적자원관리의 효율성을 높이기 위해서 개인별로 직책과 직급을 두고 이를 다시 묶어서 부서(팀)를 만들어서 관리한다. 기술개발팀, 경영지원팀, 회계팀, 인사팀등인데, 한명의 직원은 하나 혹은 그 이상의 팀에 소속될 수 있을 것이고 팀의 특징에 따라서 권한이 재조정 될것이다.

회사와 같이 부서(팀)을 만들어서 조직을 효율적으로 만드는것과 같은 구조는 다른 모든 집단에서 (이름만 약간 바꾸어서) 공통적으로 나타나며 운영체제역시 예외없이 이러한 구조를 따른다.

리눅스에서는 이를 그룹이라고 한다. 리눅스에서의 그룹역시 유저자원을 효율적으로 관리하기 위한 장치다. 하나의 유저는 하나이상의 그룹에 포함될 수 있다.

##### 권한

유저와 그룹은 고유의 권한이 있으며, 이러한 권한은 주로 파일에 적용된다. 즉 파일일 읽을수 있는지 (r), 쓸수 있는지 (w), 실행할 수 있는지 (x)에 대해 정의 하는 것으로 이루어진다. 리눅스에서 모든 것은 파일로 다루어지므로 파일에 대해서 권한을 설정한다는 것은 결국 시스템 전체에 대한 권한을 설정하는 것과 동일한 효과를 가진다.

이러한 권한은 유저(User)와 그룹(Group), Other(어디에도 속하지 않은)에 대해서 각각 정의 할 수 있다.

```
 유저     그룹     Other
+-+-+-+  +-+-+-+  +-+-+-+
|R|W|X|  |R|W|X|  |R|W|X|
+-+-+-+  +-+-+-+  +-+-+-+
 4 2 1    4 2 1    4 2 1
```

예를 들어 **test.txt**파일을 유저 **yundream**에 대해서 읽기/쓰기/실행 권한을 그룹 **develop**와 Other에는 읽기/쓰기 권한이 부여되어 있다면 ls(:12)결과는 다음과 같을 것이다.

```
$ ls -al
-rw-r--r--   1 yundream develop     5632 2006-04-19 18:09 uname.c
-rwxr-xr-x   1 yundream develop     5632 2006-04-19 18:09 yundream.txt 
```

이해하는데 별로 어려움없을 것이다. ls는 권한을 7개의 필터로 나타낸다. 처음 9개 필드가 3개씩 끊어서 유저/그룹/Otehr에 대한 권한을 설정한다. 마지막 필드는 stiky bit와 같은 특수한 정의를 위해서 사용된다.



## 3. C

### 필요한 요소

개발환경을 위해서는 최소한 아래의 툴들이 필요하다. 아래의 툴들은 완전히 공개되었으며 GPL(:12)을 따르는 소프트웨어들이다.

1. 에디터 : 코드를 짤려면 당연히 에디터가 준비되어 있어야 한다.
2. 컴파일러 : C언어에 의해서 짜여진 코드는 **인간**이 쉽게 이해할 수 있는 코드이다. 기계는 이 코드를 이해할 수 없으므로, 기계가 이해할 수 있는 **기계어**로 변경해줘야 한다. 컴파일러는 인간이 인지할 수 있는 C로 작성된 코드를 컴퓨터가 인지 **기계어**된 실행파일로 만들어준다. 번역기라고 생각하면 된다.

기본적으로 위의 2개의 툴만 설치되면 C(:12)언어를 배우는데, 전혀 문제가 없다. 그러나 C언어를 이용해서 그럴듯한 프로그램을 만들려면 몇가지 툴들이 더 갖추어진 환경을 만들 필요가 있다.

1. 디버거 : C언어가 아무리 인간이 이해하기 쉽도록 만들어졌다고는 하지만, 여전히 기계(컴퓨터)의 입장에서 생각을 해야 한다. 그러다 보니 많은 실수가 생길 수 밖에 없다. 어떤 실수는 쉽게 찾아낼 수 있지만 어떤 실수는 찾아내기 매우 어렵다. 디버거를 이용하면, 잘못된 부분을 좀더 쉽게 찾아서 수정할 수 있다.
2. Make툴 : 아주 작은 프로그램이 아닌 이상, 관리나 유지보수의 목적으로 여러개의 코드파일로 구성이 된다. make를 이용하면 이들 코드를 좀더 쉽게 유지할 수 있다. 프로젝트 관리를 위한 툴이라고 보면된다.
3. 형상관리(:12)도구 : cvs(:12), svn(:12)등으로 공동작업을 할때, 코드 파일이 꼬이지 않도록 도와주며, 버젼을 관리할 수 있도록 해준다. 여기에서는 형상관리툴에 대해서는 다루지 않을 것이다. 아마도 꽤 큰 규모의 프로젝트를 하기전엔 필요없긴 하겠지만, 관심이 있다면 링크를 따라가서 읽어보기 바란다.

### 개발 환경 만들기

#### 에디터 준비

코드를 만들려면 일단 에디터가 필요하다. Linux(:12)에도 다양한 에디터가 준비되어 있는데, 개인적으로 vi(:12)나 emacs(:12)를 사용할 것을 권장한다. 이들 에디터는 윈도우 사용자라면 익숙하지 않은 터미널 환경을 가지고 있다는 단점이 있다. 이들 에디터에 적응하기가 곤란하다면, 익숙해지기 전까지 울트라에디터와 같은 kate(:12)와 Visual C++과 같은 통합개발환경(:12)인 kdevelop(:12)등도 활용할 수 있다.

특히 kdevelop(:12)는 높은 수준의 통합개발환경을 제공한다. 그러나 kdevelop를 제대로 사용하기 위해서는, C언어 뿐만 아니라, 디버깅, 프로젝트/형상관리에 대한 내용을 알고 있어야 하기 때문에 지금 다루지는 않을 것이다. 혹시 자바언어를 사용했다면 eclipse(:12)에서 사용하능한 CDT(:12)라는 C/C++개발 환경도 제공한다. 역시 자세히 다루지는 않을 것이다.

여기에서는 vi를 사용하도록 할 것이다. vi를 사용하는 이유는 에디터로써의 필요한 기능만을 가지고 있기 때문에, 다른 부가적인 것에 신경쓰지 않고 학습에만 신경쓰면 되기 때문이다. 게다가 원격으로 연결해서 사용하기에도 전혀 문제가 없다 - GUI(:12) 방식의 에디터로도 원격작업을 할 수 있긴하지만.. 하지 않느니만 못한 경우가 대부분이다 -. 생소한 입력방식 때문에 처음에 적응하기 약간 까다롭겠지만, 눈 딱감고 한두시간 정도만 연습삼아 사용해 보기 바란다. 얼마안되어 **vi**마니아가 되어 있는 자신을 발견하게 될것이다.

#### 컴파일러 준비

컴파일러는 인간의 언어에 가까운 C로된 코드를 번역해서 기계어(:12)로 만들어주는 일을 한다. 우리가 만든 코드를 실행가능한 프로그램으로 만들려면 반드시 컴파일러(:12)를 이용해서 컴파일 과정을 거쳐야 한다. Linux(:12)에는 강력한 gcc(:12)라는 컴파일러를 제공한다. gcc(:12)는 GNU 프로젝트의 결과물로 완전히 공개되어 있으며, 리눅스는 물론이고 거의 대부분의 상용 유닉스(:12)와 맥(:12) 윈도우즈에서도 사용할 수 있다. 때때로 gcc의 성능에 대해서 의문을 표하기도 하고 실제, 해당 벤더가 제공하는 전용의 컴파일러에 비해서 성능이 떨어지기도 하지만, 대부분의 경우 사용하는데 문제가 없다.



아뭏든 이 문서는 **gcc**를 기준으로 내용을 채워갈 것이다. 버젼은 3.x 이상으로 하겠다. 최근의 Linux에 설치된 gcc는 최소 3.x에서 4.x 버젼이니 사용하는데 큰 문제가 없을 것이다. 아래와 같은 방법으로 gcc가 설치되어 있는지 확인해 보도록 하자. 만약 gcc가 설치되어 있지 않다면, 배포판에 맞는 패키지 관리자를 통해서 설치해야 한다. 방법은 배포판에 따라서 다르기 때문에 별도로 설명하지 않도록 하겠다. 메뉴얼을 천천히 읽어보기 바란다.

```
# gcc --version
gcc (GCC) 3.2.2 20030222 (Red Hat Linux 3.2.2-5)
Copyright (C) 2002 Free Software Foundation, Inc.
This is free software; see the source for copying conditions.  There is NO
warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```



#### 첫번째 C 프로그램의 작성

C 프로그램이란 C언어를 이용해서 만들어진 프로그램을 뜻한다.



그럼 첫번째 프로그램을 작성해보도록 하자. 유명한 **hello world**프로그램으로, 실행시키면 화면에 **hello world**를 출력하는 일을 한다. 에디터로 아래의 코드를 입력해보자. 파일이름은 hello.c로 하자.

```
#include <stdio.h>

int main(int argc, char **argv)
{
    printf("Hello World\n");
    return 0;
}
```



간단히 설명을 하도록 하겠다. C언어 학습에 들어가기전에 맛보기 식으로 하는 거니, 이해가 안가더라도 그러려니 하고 넘어가도록 하자. 어차피 나중에 자세히 알아보게 될 것이다.

1. **#include** : 외부 함수를 사용하기 위해서 함수가 선언되어 있는 파일을 포함시킬려고 사용한다. stdio.h는 표준입력/표준출력/표준에러와 관련된 함수들이 선언되어 있다.
2. main 함수 : 프로그램의 본문이다. 프로그램이 실행되기 위해서는 반드시 하나의 main함수가 포함되어 있어야 한다.
3. printf 함수 : 표준출력을위한 함수로 "Hello World\n"를 모니터 화면에 출력한다.
4. return : 함수의 결과를 넘겨주기 위해서 사용한다.

이제 **gcc 컴파일러**를 이용해서 실행가능한 파일로 만들어 보도록 하자.

```
# gcc -o hello hello.c
```

hello.c를 컴파일 해서 hello라는 실행파일로 만들어라는 명령이다. 이제 hello를 실행하면 다음과 같이 주어진 일을하는 것을 볼 수 있을 것이다.

```
# ./hello
Hello World
#
```

현재 디렉토리에서 명령을 찾도록하기 위해서 **./**를 이용했다.





#### C 프로그램의 구조

모든 프로그램은 특유의 구조를 가지게 된다. 앞 절에서 예로 들었던 **hello.c**를 이용해서 C 프로그램의 구조에 대해서 알아보도록 하겠다.

1. 프로그램은 하나 이상의 함수로 이루어진다.
2. 반드시 하나의 **main**함수를 포함해야 한다.
3. 함수는 서로 독립적인 관계에 있다.

##### 함수

함수는 주어진 일을 수행하는 **코드조각**으로 개념적으로 매우 간단하다.

```
    입력 데이터
    +--\ /--------------+
    |                   |
    |                   |
    +-----------/ \-----+
             출력결과
```

위의 이미지는 함수의 개념을 전형적으로 설명해주고 있다. 이미 초등학교때 소개된 개념이므로 함수를 이해하는데에는 전혀 문제 없으리라 생각된다.



함수는 **어떤 데이터 셋**을 집어 넣으면 필요한 연산을 해서 **출력 결과**를 되돌려준다. 함수는 다음과 같은 구조를 가진다.

```
return type function_name(argument)
{
   // 코드
}
```

1. return type : 출력 데이터의 형(type)를 지정해 준다.
2. function_name : 함수의 이름으로 각 함수는 이름으로 구분되며, 이름으로 사용할 수 있다.
3. argument(인자) : 함수에 넘겨지는 값이다.
4. 함수 코드 : 함수의 본체부분으로 인자를 받아서 **연산**을 하고 결과값을 되돌려준다.

다음은 두개의 숫자를 입력받아서 **더하기**연산을 한 후 되돌려주는 가장 간단한 형식의 함수다. 가장 간단한 함수이긴 하지만 모든 함수는 결국 아래의 예와 동일한 구조를 가진다.

```
int plus(int a, int b) 
{
    return a+b;
}
```



하나의 프로그램은 하나 이상의 함수로 구성되어있다. 이 함수들은 입력값과 출력의 형식으로 다른 함수들에게 값을 넘기는 식의 데이터의 흐름으로 주어진 일을 수행한다. 분업화된 컨테이너 벨트를 생각하면 될거 같다.



attachment:function.png

##### main 함수

**main 함수**는 특별한 종류의 함수이며, 프로그램이 시작되는 지점이다. 모든 C 프로그램은 반드시 하나의 main 함수를 포함하고 있어야만 한다. 다른 함수와 마찬가지로 return type, function name, argument의 3요소로 이루어져 있다.

attachment:function2.png

다음은 **덧셈**연산을 하는 sum이라는 함수를 포함한 프로그램이다.

```
#include <stdio.h>

int sum(int a, int b)
{
    return a+b;
}
int main(int argc, char **argv)
{
    int result;
    result = sum(4, 5);
    return result;
}
```

완전한 프로그램이 되기 위해서 하나의 main함수를 가지고 있으며, main함수는 내부에서 sum이라는 함수를 호출해서 4와 5를 더하고 결과값을 리턴하고 프로그램을 종료한다. 프로그램이 종료되었으면 어떻게 리턴값을 확인할 수 있을까 ? 다음과 같이 쉘에서 확인 가능하다.

```
# ./sum
# echo $?
9
```

echo(1)는 화면에 출력을 하기 위해서 사용하는 쉘내부명령어이다. **$?**는 가장 최근 실행시킨 프로그램이 리턴한 값이 저장되는 쉘의 특별한 변수다. 어떻게 이런일이 가능한지는 아직은 몰라도 된다. 차차 알아나가게 될 것이다.



#####  주석

주석(:12)은 부가적인 정보를 알려주기 위해서 사용되는 C언어의 요소다. C언어가 인간의 언어와 상당히 유사하긴 하지만, 여전히 이해하기 힘든면이 있다. 그러다 보니 다른 사람이 코드를 이해하기 힘들며, 심지어 프로그램을 만든 당사자 조차도, 시간이 지나면 왜 이코드를 작성했는지 잊어버리는 경우가 생긴다. 이는 프로그램의 유지보수를 힘들게 만드는 요인이 된다.

주석을 사용하면 이해하기 쉬운 코드를 만들 수 있다. 특히 여러명과 협력해서 작업해야 할경우 주석은 필수적인 요소다. 당연하지만 주석은 기계어로 번역이 되지 않는다. 다음은 주석의 예이다.

```
#include <stdio.h>

/*
 * 만든사람 : yundream
 * 하는일 : 두개의 인자를 더한 결과를 리턴한다.
 * 인자 : int a, int b
 */
int sum(int a, int b)
{
    return a+b;
}

// Main 함수 시작 
int main(int argc, char **argv)
{
    int result;
    result = sum(4, 5); // 두개의 인자를 더한다.
    return result;
}
```

주석은 "/* */"과 "//" 두개를 이용해서 작성할 수 있다. "/* */"는 블럭단위의 주석을 만들기 위해서 사용하며, *//*는 라인단위의 주석을 만들기 위해서 사용한다. 함수 전체에 대한 상세설명등은 **/\* \*/**를 코드 중간중간 간단한 설명을 위해서 **//**를 사용한다.



### C 프로그램이 만들어지는 과정

인간이 이해하기 쉬운 C언어를 이용해서 **프로그램**을 만들었다면, 이를 컴퓨터가 이해할 수 있는 기계어 파일로 번역해서 컴퓨터가 실행할 수 있는 **실행파일**의 형태로 만들어야 한다. 이러한 일을 하는 프로그램을 **컴파일러**라고 한다. 이미 우리는 hello world 프로그램 예제를 통해서, **컴파일러**를 이용해서 실행파일을 만들고 이를 실행시키는 방법에 대해서 알아보았다. 여기에서는 어떠한 과정을 거쳐서 실행파일이 만들어지는지에 대해서 알아보도록 하겠다.

**소스 코드 생성**

인간이 이해할 수 있는 언어로 프로그램을 작성한다. 이것을 소스코드라고 하는데, 여기에는 컴퓨터에게 내릴 명령들이 포함되어 있다. 소스코드는 인간이 쉽게 이해할 수 있지만, 컴퓨터는 이해할 수 없기 때문에 컴퓨터가 이해할 수 있도록 번역하는 과정이 필요하다.

**Pre processor**

컴파일러를 실행시키면 가장 먼저 **pre compile**를 수행한다. 프로그래머가 생성한 소스코드는 인간이 보다 쉽게 읽을 수 있도록 하기 위해서 include나 **매크로**등을 이용해서 코드가 축약되어 있다. pre compile는 축약된 내용을 컴파일러가 쉽게 해석할 수 있도록 풀어쓰는 과정이다.

**Assembly 코드의 생성**

이제 풀어쓴 코드를 가장 원시적인 언어의 형태인 Assembly(:12)코드로 만들어준다. 어셈블리코드는 기계어와 1:1로 대응되기 때문에 일단 어셈블리코드로 성공적으로 만들어낸다면 쉽게 기계어형태로 변환할 수 있다.

**Object 파일의 생성**

Assembly 코드가 만들어졌다면, 이제 이걸 기계어로 변환한다. 이렇게 해서 만들어진 파일을 object파일이라고 한다.

**linker**

그러나 object파일이 생겼다고 바로 실행될 수 있는게 아니다. 프로그램으로써 실행하기 위해서는 운영체제가 제공하는 다른 여러가지 객체(기능)들과 연결(link)되어야 한다. link과정을 거치면 비로서 실행가능한 완전한 프로그램이 만들어지게 된다.