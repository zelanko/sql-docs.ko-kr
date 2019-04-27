---
title: 지원 되지 않는 Visual FoxPro 명령 및 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- FoxPro ODBC driver [ODBC], commands and functions
- functions [ODBC], Visual FoxPro
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro commands and functions
- FoxPro ODBC driver
ms.assetid: afdb6b7e-738d-42ca-8053-67ae50873ca6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6b69c8bf15b4d56872c4030725638e4b61571e6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62633373"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>지원되지 않는 Visual FoxPro 명령 및 함수(Visual FoxPro ODBC 드라이버)
다음 표에서 FoxPro 명령 및 Visual FoxPro ODBC 드라이버에서 지원 되지 않지만 Microsoft® Visual FoxPro®에서 지원 되는 함수를 나열 합니다.  
  
 해당 규칙, 트리거, 기본값, 응용 프로그램 데이터와 상호 작용 또는 저장된 프로시저 이러한 Visual FoxPro 명령 또는 함수를 호출 하는 경우 드라이버는 오류를 생성할 수 있습니다.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>지원 되지 않는 Visual FoxPro 명령 및 함수  
  
||||  
|-|-|-|  
|# #UNDEF DEFINE...|... #IF #ENDIF 전처리기 지시문|#IFDEF &#124; #IFNDEF|  
|#INCLUDE 전처리기 지시문|:: 범위 결정 연산자|! 명령 (실행이 표시 &#124; ! 명령)|  
|? &#124; ?? Command|??? Command|\ &#124; \\\ Command|  
|@ ... 명령 상자|@ ... 명령 클래스|@ ... 지우기 명령|  
|@ ... 편집-상자 명령 편집|@ ... 명령 입력|@ ... 가져오기|  
|@ ... 메뉴 명령|@ ... 명령 프롬프트|@ ... 명령 예를 들어합니다|  
|@ ... 스크롤 명령|@ ... 명령||  
  
## <a name="a"></a>변수를 잠그기 위한  
  
||||  
|-|-|-|  
|허용 명령|ACLASS () 함수|메뉴 명령을 활성화합니다|  
|팝업 명령 활성화|화면 명령 활성화|명령 창 활성화|  
|ActivateCell 메서드|추가 클래스 명령|ADIR () 함수|  
|AFONT () 함수|AINSTANCE () 함수|_ALIGNMENT 시스템 메모리 변수|  
|AMEMBERS () 함수|ANSITOOEM () 함수|APRINTERS () 함수|  
|ASELOBJ () 함수|명령 지원||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|() 함수 막대|BARCOUNT () 함수|BARPROMPT () 함수|  
|_BEAUTIFY 시스템 메모리 변수|시스템 메모리 변수 상자 (_b)|명령 찾아보기|  
|_BROWSER 시스템 메모리 변수|응용 프로그램 명령 빌드하십시오|EXE 명령을 작성합니다|  
|빌드 프로젝트 명령|_BUILDER 시스템 메모리 변수||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|_CALCVALUE 시스템 메모리 변수|_CLIPTEXT 시스템 메모리 변수|_CONVERTER 시스템 메모리 변수|  
|_CUROBJ 시스템 메모리 변수|명령을 호출합니다|CANCEL 명령|  
|CAPSLOCK () 함수|CD 명령|변경 명령|  
|CHDIR 명령|CHRSAW () 함수|닫기 메모 명령|  
|CNTBAR () 함수|CNTPAD () 함수|COL () 함수|  
|컴파일 명령|데이터베이스 명령을 컴파일합니다|양식 명령을 컴파일합니다|  
|COMPOBJ () 함수|컨테이너 개체|컨트롤 개체|  
|파일 명령을 복사합니다|메모 명령 복사|클래스 명령 만들기|  
|CLASSLIB 명령 만들기|색 집합 명령 만들기|명령 만들기|  
|연결 명령 만들기|데이터베이스 명령 만들기|양식 명령을 만들려면|  
|명령에서 만들기|레이블 명령 만들기|메뉴 명령 만들기|  
|프로젝트 명령 만들기|쿼리 명령 만들기|보고서 명령 만들기|  
|화면 명령 만들기|SQL 보기 명령 만들기|트리거 명령 만들기|  
|명령 보기 만들기|CREATEOBJECT () 함수|CURDIR () 함수|  
  
## <a name="d"></a>d  
  
||||  
|-|-|-|  
|_DBLCLICK 시스템 메모리 변수|_DIARYDATE 시스템 메모리 변수|DBSETPROP () 함수|  
|DDE 함수|비활성화 메뉴 명령|팝업 명령 비활성화|  
|창 명령을 비활성화 합니다.|선언-DLL 명령|명령 선언|  
|명령 모음 정의|상자 명령 정의|클래스 명령 정의|  
|메뉴 명령 정의|패드 명령 정의|팝업 명령 정의|  
|정의 창 명령|연결 명령 삭제|데이터베이스 명령을 삭제 합니다.|  
|DELETE 명령 파일|DELETE 트리거 명령|명령 보기 삭제|  
|DIR 명령|디렉터리 명령|표시 명령|  
|디스플레이 연결 명령|데이터베이스 명령 표시|DLL 명령 표시|  
|표시 파일 명령|메모리 명령 표시|표시 개체 명령|  
|표시 프로시저 명령|표시 상태 명령|표시 구조 명령|  
|표시 테이블 명령|표시 뷰 명령|명령을 형성 하지|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|명령 편집|오류 명령입니다.||  
|지우기 명령|외부 명령|내보내기 명령|  
|꺼내기 명령|꺼내기 페이지 명령||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|_FOXDOC 시스템 메모리 변수|_FOXGRAPH 시스템 메모리 변수|FEOF () 함수|  
|FCLOSE 함수|FCREATE () 함수|FGETS 함수|  
|FERROR () 함수|FFLUSH () 함수|FKLABEL () 함수|  
|필터가 명령|찾기 명령|FOPEN () 함수|  
|FKMAX () 함수|FONTMETRIC () 함수|FSEEK () 함수|  
|FPUTS () 함수|FREAD () 함수||  
|FWRITE () 함수|FCHSIZE () 함수||  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|_GENGRAPH 시스템 메모리 변수|_GENMENU 시스템 메모리 변수|_GENPD 시스템 메모리 변수|  
|_GENSCRN 시스템 메모리 변수|_GENXTAB 시스템 메모리 변수|GETBAR () 함수|  
|GETCOLOR () 함수|GETDIR () 함수|GETEXPR 명령|  
|GETFILE () 함수|GETFONT () 함수|GETOBJECT () 함수|  
|GETPAD () 함수|GETPICT () 함수|GETPRINTER () 함수|  
  
## <a name="h"></a>H  
  
||||  
|-|-|-|  
|HELP 명령|숨기기 메뉴 명령|팝업 명령 숨기기|  
|숨기기 창 명령|홈 () 함수||  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IMESTATUS () 함수|IMPORT 명령|입력된 명령|  
|명령 인덱스|INKEY () 함수|ISCOLOR () 함수|  
|INSERT 명령|INSMODE () 함수||  
|ISMOUSE () 함수|시스템 메모리 변수 (_i)||  
  
## <a name="j"></a>J  
  
||||  
|-|-|-|  
|연결 명령|||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|키보드 명령|||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|_LMARGIN 시스템 메모리 변수|레이블 명령|LASTKEY () 함수|  
|LINENO () 함수|명령 목록|연결 목록 표시 명령|  
|로드 명령|Locfile에 둡니다 () 함수||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|MCOL () 함수|MD 명령|메뉴 명령|  
|메모리 () 함수|메뉴 명령|MKDIR 명령|  
|메뉴 () 함수|MESSAGEBOX () 함수|연결 명령 수정|  
|클래스 명령 수정|명령 수정|양식 명령을 수정합니다|  
|데이터베이스 명령 수정|명령 파일 수정|메모 명령 수정|  
|일반 명령 수정|레이블 명령 수정|프로젝트 명령 수정|  
|메뉴 명령 수정|PROCEDURE 명령을 수정 합니다.|화면 명령 수정|  
|쿼리 명령 수정|보고서 명령 수정|창 명령 수정|  
|명령 구조 수정|명령 보기 수정|이동 창 명령|  
|마우스 명령|이동 팝업 명령|MROW () 함수|  
|MRKBAR () 함수|MRKPAD () 함수||  
|MWINDOW () 함수|MDOWN () 함수||  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NUMLOCK () 함수|||  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|OBJNUM () 함수|OBJTOCLIENT () 함수|명령 모음 ON|  
|OEMTOANSI () 함수|APLABOUT 명령|ON EXIT 메뉴 명령|  
|이스케이프 명령|종료 표시줄 명령|키 = 명령|  
|ON EXIT 패드 명령|ON EXIT 팝업 명령|ON 패드 명령|  
|키 레이블이 명령|MACHELP 명령|표시줄 명령 선택|  
|페이지 명령|READERROR 명령|선택 팝업 명령|  
|메뉴 명령 선택|패드 명령 선택||  
|종료 명령|OBJVAR () 함수||  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|_PADVANCE 시스템 메모리 변수|_PAGENO 시스템 메모리 변수|_PBPAGE 시스템 메모리 변수|  
|_PCOLNO 시스템 메모리 변수|_PCOPIES 시스템 메모리 변수|_PDRIVER 시스템 메모리 변수|  
|_PDSETUP 시스템 메모리 변수|_PECODE 시스템 메모리 변수|_PEJECT 시스템 메모리 변수|  
|_PEPAGE 시스템 메모리 변수|_PLENGTH 시스템 메모리 변수|_PLINENO 시스템 메모리 변수|  
|_PLOFFSET 시스템 메모리 변수|_PPITCH 시스템 메모리 변수|_PQUALITY 시스템 메모리 변수|  
|_PRETEXT 시스템 메모리 변수|_PSCODE 시스템 메모리 변수|_PSPACING 시스템 메모리 변수|  
|_PWAIT 시스템 메모리 변수|PACK 데이터베이스 명령|패드 () 함수|  
|PCOL () 함수|PEMSTATUS () 함수|매크로 명령 실행|  
|팝업 키 명령|POP 메뉴 명령|POP 팝업 명령|  
|팝업 () 함수|PRINTJOB... ENDPRINTJOB 명령|PRINTSTATUS () 함수|  
|PRMBAR () 함수|PRMPAD () 함수|프롬프트 () 함수|  
|PROW () 함수|PRTINFO () 함수|푸시 키 명령|  
|푸시 메뉴 명령|푸시 팝업 명령|PUTFILE () 함수|  
  
## <a name="q"></a>Q  
  
||||  
|-|-|-|  
|종료 명령|||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|_RMARGIN 시스템 메모리 변수|RD 명령|READKEY () 함수|  
|명령은 읽기|메뉴 명령을 읽기|릴리스 표시줄 명령|  
|REFRESH() 함수|명령 인덱스 다시 작성|릴리스 라이브러리 명령|  
|릴리스 CLASSLIB 명령|릴리스 명령|릴리스 패드 명령|  
|릴리스 메뉴 명령|릴리스 모듈 명령|릴리스 WINDOWS 명령|  
|릴리스 팝업 명령|릴리스 PROCEDURE 명령|명령 이름 바꾸기|  
|클래스 명령 제거|명령 클래스 이름 바꾸기|명령 보기 이름 바꾸기|  
|연결 명령 이름 바꾸기|명령 테이블 이름 바꾸기|명령에서 복원|  
|보고서 명령|() 함수를 다시 쿼리|창 명령 복원|  
|복원 명령 매크로|화면 명령 복원|RGBSCHEME () 함수|  
|다시 시작 명령|RGB () 함수|실행 &AMP;#124; ! Command|  
|RMDIR 명령|ROW () 함수||  
|RUNSCRIPT 명령|RDLEVEL () 함수||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|매크로 명령을 저장 합니다.|화면 명령 저장|명령 저장|  
|WINDOWS 명령 저장|체계 () 함수|SCOLS () 함수|  
|스크롤 명령|_SCREEN 시스템 메모리 변수|SET 명령|  
|SET 대체 명령|SET ANSI 명령|SET APLABOUT 명령|  
|자동 저장 명령 집합|SET 벨 명령|SET 깜박임 명령|  
|SET 테두리 명령|SET BRSTATUS 명령|SET CLASSLIB 명령|  
|일반 명령 집합|SET 클록 명령|색 설정 명령|  
|구성표 명령의 색 설정|색 집합 명령 집합|명령에 색 설정|  
|호환 명령 집합|SET 확인 명령|SET 콘솔 명령|  
|집합 CPCOMPILE|집합 CPDIALOG|SET 통화 명령|  
|SET CURSOR 명령|SET DATASESSION 명령|디버그 명령 집합|  
|10 진수 명령 집합|구분 기호 명령 집합|SET 개발 명령|  
|장치 명령 집합|SET 표시 명령|SET DOHISTORY 명령|  
|SET ECHO 명령|SET 이스케이프 명령|집합 형식 명령|  
|SET 함수 명령입니다.|SET 머리글 명령|HELP 명령 집합|  
|SET HELPFILTER 명령|SET 강도 명령|집합 키 명령|  
|SET KEYCOMP 명령|SET LOGERRORS 명령|SET MACDESKTOP 명령|  
|SET MACHELP 명령|SET MACKEY 명령|SET 여백 명령|  
|명령 집합을 표시 합니다.|명령에 표시를 설정 합니다.|SET MEMOWIDTH 명령|  
|SET 메시지 명령|SET 마우스 명령|SET 주행 기록 계 명령|  
|SET OLEOBJECT 명령|SET 색상표 명령|SET PDSETUP 명령|  
|설정 지점 명령|SET 프린터 명령|SET READBORDER 명령|  
|REFRESH 명령 집합|SET 리소스 명령|SET 안전성 명령|  
|SET 스코어 명령|SET 초 명령|구분 기호 명령 집합|  
|SET 그림자 명령|설정 건너뛰기 명령|SET 공간 명령|  
|SET 상태 명령|상태 표시줄 명령 설정|SET 단계 명령|  
|SET 스티커 명령|SET SYSFORMATS 명령|SET SYSMENU 명령|  
|SET TALK 명령|SET TEXTMERGE 명령|SET TEXTMERGE 구분 기호 명령|  
|SET 항목 명령|항목 ID 명령 집합|SET TRBETWEEN 명령|  
|SET 미리 입력 명령|명령 집합 보기|메모 명령의 집합 창|  
|SET XCMDFILE 명령|_SHELL 시스템 메모리 변수|GET 명령 표시|  
|SHOW 명령을 가져옵니다.|표시 메뉴 명령|명령 개체를 표시 합니다.|  
|팝업 명령 표시|표시 창 명령|크기 팝업 명령|  
|크기 창 명령|SKPBAR () 함수|SKPPAD () 함수|  
|SOUNDEX () 함수|_SPELLCHK 시스템 메모리 변수|SQL 함수|  
|SROWS () 함수|_STARTUP 시스템 메모리 변수|일시 중지 명령|  
|SYS(2011) 제외한 SYS() 함수|SYSMETRIC () 함수||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TABS System Memory Variable|텍스트는 중... ENDTEXT 명령|TXTWIDTH () 함수|  
|() 함수를 변환 합니다.|_TRANSPORT 시스템 메모리 변수||  
|명령 유형|_THROTTLE 시스템 메모리 변수||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|업데이트 () 함수|명령을 사용 하 여||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|유효성 검사 데이터베이스 명령|VARREAD () 함수|버전 () 함수|  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|시스템 메모리 변수 (_w)|_WIZARD 시스템 메모리 변수|WCHILD () 함수|  
|대기 명령|WBORDER () 함수|WFONT () 함수|  
|WCOLS () 함수|WEXIST () 함수|WLROW () 함수|  
|사용 하 여는 중... ENDWITH 명령|WLAST () 함수|WONTOP () 함수|  
|WMAXIMUM () 함수|WLCOL () 함수|WREAD () 함수|  
|WOUTPUT () 함수|WMINIMUM () 함수|WVISIBLE () 함수|  
|WPARENT () 함수|WTITLE () 함수||  
|WROWS () 함수|_WRAP 시스템 메모리 변수||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|확대/축소 창 명령|||
