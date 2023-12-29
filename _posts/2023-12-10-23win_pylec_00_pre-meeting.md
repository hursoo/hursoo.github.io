---
layout: single
title: "[23파이썬특강] 0. 사전 모임"
author_profile: false
toc : true
---

파이썬은 데이터 분석 작업에 많이 사용되는 프로그래밍 언어이다. 파이썬을 익히려면 파이썬 설치뿐 아니라 파이썬을 활용한 분석 작업을 쉽게 만들어주는 **통합 개발 환경(IDE)**을 갖추는 것이 좋다. IDE 소프트웨어에는 여러 가지가 있지만 본 특강에서는 **주피터랩(JupyterLab)**을 사용한다. 파이썬과 주피터랩 모두 **아나콘다(Anaconda)**라는 소프트웨어를 통해 설치할 수 있다. 이와 함께 텍스트 분석 작업에 유용한 간단한 소프트웨어도 함께 설치한다. <br>
[교재: 02. 파이썬 데이터 분석 환경 만들기, pp.31-50 참조]

### 1. 텍스트 편집기와 파일찾기 툴 설치

#### 1.1 텍스트 편집기 설치
- 먼저, 텍스트 편집기를 설치한다. 텍스트 편집기는 확장자가 txt나 csv인 자료를 다룰 때 많이 사용한다. 본 특강에서는 **엠에디터(Emeditor, 윈도우 기반)**를 사용한다. 이 편집기는 옛한글과 한자를 잘 표현하므로 역사학 자료를 다룰 때 편리하다. OS가 윈도우가 아닌 경우 다른 편집기를 사용해도 파이썬 공부 단계에서는 큰 문제 없다. 
- 실행파일인 "emed32_13.0.6.exe"을 [깃허브 주소](https://github.com/hursoo/2023_winter_big-khistory01/tree/main/tools/emeditor)에서 다운로드하고 이 파일을 실행하여 엠에디터를 설치한다. <br>
- 설치 완료된 엠에디터를 실행한다. 팝업 메뉴 맨 마지막에 있는 "도움말"의 "Emeditor 소개"에 들어가서 "등록키 입력"을 클릭하고 등록키를 입력한다. 등록키는 전술한 깃허브 주소에 있는 "emed32_13.0.6_등록키.txt"의 여러 키들 중 하나를 선택하면 된다. <br>
- 엠에디터로 할 수 있는 작업 중 **[정규표현식](https://wikidocs.net/1642)**을 이용한 간단한 실습을 해 보면 다음과 같다.
- 실습 1_여러 줄의 데이터를 한 줄로 일괄 변환: 동일한 깃허브 주소의 실습자료 이용. ```실습자료_이메일주소.txt```의 내용을 복사해서 엠에디터의 새 창(ctrl-N)에 붙여 넣는다. -> '찾기'(ctrl-F) 검색창에 ```\n```을 입력 -> 우측 메뉴에서 '바꾸기'를 클릭 -> 바꾸기 창에 ```, ```(컴머와 공백 한 칸)를 입력 -> 검색창 하단의 둘째 줄 "정규식 사용"을 선택 -> 우측 메뉴의 "모두 바꾸기" 클릭 -> (결과) 한 줄씩 구분된 여러 줄 자료가 컴머와 빈칸을 경계로 한 줄로 변경되었다.
- 실습 2_한 줄의 데이터를 문장 혹은 단어 단위의 여러 줄로 일괄 변환: ```실습자료_기상청은_슈퍼컴퓨터도.txt```의 내용 복사하여 엠에디터의 새 창에 붙여 넣는다. -> (실습 1과 마찬가지 방식으로) '찾기' 창엔 ```\.```를, '바꾸기' 창엔 ```.\n```을 입력하고 "모두 바꾸기" 클릭 -> (결과) 문장 단위로 구분되었다. ---> 다시 '찾기' 창엔 ```\s```를, '바꾸기' 창엔 ```.\n```을 입력하고 "모두 바꾸기" 클릭 -> (결과) 각 단어가 한 줄씩 된 형태로 바뀌었다.

#### 1.2 파일찾기 툴 설치
- **리스터리(Listary)**라는 파일찾기 툴은 간편하게 필요한 파일을 찾을 때 유용하다. 다음 웹페이지 주소에서 다운로드 받아서 설치한다. [https://www.listary.com/](https://www.listary.com/). 
- 사용법은 간단하다. 특별히 이 툴의 아이콘 등을 클릭할 필요없이 ctrl키를 두번 누르면 검색 창이 뜬다. 여기에 찾고싶은 파일 이름의 일부를 입력하면 해당 파일이 나타난다.

### 2. 파이썬 및 주피터랩 설치
- 선택: [아나콘다 다운로드 페이지](https://www.anaconda.com/download)로 들어가서 아나콘다 설치 파일을 다운로드 받는다. 이 때 설치 파일은 pc의 운영 체제(예: 윈도우 64비트)에 맞는 것을 선택한다.
- 설치: 설치 파일을 클릭하여 아나콘다를 설치한다. 설치 후에는 자기 pc에 있는 **Anaconda3** 폴더의 **Anaconda Navigator**를 클릭해서 아나콘다를 실행한다 -- 윈도우 사용자 계정이 **한글**로 되어 있으면 설치 중에 **오류**가 발생한다. 이 경우에는 사용자 계정을 영문으로 새로 만들어 로그인한 다음 아나콘다를 다시 설치한다. (교재 34쪽 참고)
- 확인: 실행 후 열린 화면에는 주피터랩 아이콘을 볼 수 있다. 파이썬은 따로 아이콘으로 보이지 않으나 사용할 수 있는 상태이다. (현재 파이썬 버전은 3.11이다)

### 3. 주피터랩 실행
#### 3.1 프롬프트로 실행
- 아나콘다 프롬프트 실행: **아나콘다 프롬프트(Ananconda Prompt)** 아이콘을 마우스로 더블클릭해 연다. 이 프롬프트 아이콘은 윈도우 시작 메뉴를 누르면 나타나는 Anaconda3 폴더 안에 있다.
- 주피터랩 실행: 아나콘다 프롬프트에 `jupyter lab`이라고 입력하고 엔터를 누른다. 그러면 웹 브라우저에 주피터랩이 실행된다. 
- 아나콘다 프롬프트 창은 주피터랩을 사용하는 동안 열려 있어야 하니, 종료하지 않고 그냥 둔다.
- 주피터랩의 화면 구성과 기본 기능은 교재 02-2(pp.37-47) 참조

#### 3.2 바로가기로 실행
- 아나콘타 프롬프트에서 명령어를 입력하는 대신, **원하는 폴더로 바로가기**를 할 수 있는 아이콘을 만들고 이를 더블클릭해서 실행하면 편리하다. 
- 워킹 디렉터리(working directory) 복사: (1) 워킹 디렉터리는 주피터랩에서 파일을 불러오거나 저장할 때 사용하는 폴더를 말한다. 기본값은 `C:/Users/<사용자 이름>`으로 지정되어 있다. 이 기본값을 **실제 자신의 작업 디렉터리 경로**로 바꾼다. (2) 경로 주소는 모두 **영어**로 되어 있는 것이 좋다. 경로 일부에 한글이 있을 경우 오류가 생길 수 있기 때문이다. (3) 경로 주소는 다음 절차로 간단히 복사할 수 있다. 윈도우탐색기에서 해당 디렉터리로 들어간 뒤, 탐색기 상단의 해당 디렉터리 이름에 마우스 우클릭해서 **"주소를 텍스트로 복사"**를 클릭한다. 해당 주소를 텍스트 편집기 등에 붙여 놓는다.
- 워킹 디렉터리 변경: (1) activate.bat 파일(`C://Users/<사용자 이름>/anaconda3/Scripts` 소재)을 동일한 폴더 내에 복사하고, 이 복사본 파일의 이름을 `JupyterLab.bat`으로 변경한다. (2) 변경된 파일을 열어서 맨 아래에 다음 두 줄을 입력한 뒤 저장한다. 첫째 줄에는 위킹 디렉터리로 이동하라는 명령어가, 둘째 줄에는 주피터랩을 실행하는 명령어가 들어간다. ```<워킹 디렉터리로 사용할 폴더 경로>``` 부분에 조금 전 복사해 둔 워킹 디렉터리 경로를 붙인다.
```python
cd <워킹 디렉터리로 사용할 폴더 경로>
jupyter lab
```
- 주피터랩 바로가기 만들기: (1) JupyterLab.bat 파일을 마우스로 우클릭해서 바로 가기를 만들고, 이것을 바탕화면에 복사한다. (2) 바로가기를 '주피터 노트북' 로고로 바꾼다. 첫째, 주피터랩 바로가기를 마우스 우클릭한 뒤, '속성 -> 아이콘 변경 -> 찾아보기'를 클릭한다. 노트북 로고는 `C://Users/<사용자 이름>/anaconda3/Menu`에 있다. (교재: 50쪽 참조)

### 4. 기타
- 팀 편성, 팀원 인사
- 특강 운영 관련
