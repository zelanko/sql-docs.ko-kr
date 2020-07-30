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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3f1882172bb3f300c50820db642443ec0d1583f4
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363478"
---
# <a name="unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver"></a>지원되지 않는 Visual FoxPro 명령 및 함수(Visual FoxPro ODBC 드라이버)
다음 표에서는 Visual FoxPro ODBC 드라이버에서 지원 되지 않지만 Microsoft® Visual FoxPro®에서 지원 되는 FoxPro 명령 및 함수를 보여 줍니다.  
  
 응용 프로그램이 규칙, 트리거, 기본값 또는 저장 프로시저가 이러한 Visual FoxPro 명령이 나 함수를 호출 하는 데이터와 상호 작용 하는 경우 드라이버에서 오류를 생성할 수 있습니다.  
  
## <a name="unsupported-visual-foxpro-commands-and-functions"></a>지원 되지 않는 Visual FoxPro 명령 및 함수  

:::row:::
    :::column:::
        !명령 (실행 &#124;!을 참조 하세요.명령  
        #<a name="defineundef"></a>정의 ... #UNDEF  
        #<a name="ifendifpreprocessordirective"></a>IF ... #ENDIF 전처리기 지시문  
        #<a name="ifdef124ifndef"></a>IFDEF &#124; #IFNDEF  
        #<a name="includepreprocessordirective"></a>전처리기 지시문 포함  
        :: 범위 결정 연산자  
        ?&#124;?명령  
    :::column-end:::
    :::column:::
        ???명령  
        @ ... BOX 명령  
        @ ... 클래스 명령  
        @ ... CLEAR 명령  
        @ ... 편집 편집 상자 명령  
        @ ... FILL 명령  
        @ ... 가져오기  
    :::column-end:::
    :::column:::
        @ ... 메뉴 명령  
        @ ... PROMPT 명령  
        @ ... 말 명령  
        @ ... SCROLL 명령  
        @ ... TO 명령  
        \ &#124; \\ \ 명령  
    :::column-end:::
:::row-end:::

## <a name="a"></a>A  

:::row:::
    :::column:::
        ACCEPT 명령  
        ACLASS () 함수  
        메뉴 명령 활성화  
        팝업 명령 활성화  
        화면 활성화 명령  
        창 활성화 명령  
    :::column-end:::
    :::column:::
        ActivateCell 메서드  
        클래스 추가 명령  
        ADIR () 함수  
        AFONT () 함수  
        AINSTANCE () 함수  
        _ALIGNMENT 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        AMEMBERS () 함수  
        ANSIT기념일 EM () 함수  
        APRINTERS () 함수  
        ASELOBJ () 함수  
        지원 명령  
    :::column-end:::
:::row-end:::

## <a name="b"></a>b  

:::row:::
    :::column:::
        BAR () 함수  
        바 COUNT () 함수  
        바 프롬프트 () 함수  
        _BEAUTIFY 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        _BOX 시스템 메모리 변수  
        찾아보기 명령  
        _BROWSER 시스템 메모리 변수  
        응용 프로그램 빌드 명령  
    :::column-end:::
    :::column:::
        빌드 EXE 명령  
        프로젝트 빌드 명령  
        _BUILDER 시스템 메모리 변수  
    :::column-end:::
:::row-end:::

## <a name="c"></a>C  

:::row:::
    :::column:::
        _CALCVALUE 시스템 메모리 변수  
        CALL 명령  
        취소 명령  
        CAPSLOCK () 함수  
        CD 명령  
        명령 변경  
        CHDIR 명령  
        CHRSAW () 함수  
        _CLIPTEXT 시스템 메모리 변수  
        메모 닫기 명령  
        CNTBAR () 함수  
        CNTPAD () 함수  
        COL () 함수  
        COMPILE 명령  
    :::column-end:::
    :::column:::
        데이터베이스 컴파일 명령  
        FORM 컴파일 명령  
        COMPOBJ () 함수  
        컨테이너 개체  
        컨트롤 개체  
        _CONVERTER 시스템 메모리 변수  
        파일 복사 명령  
        메모 복사 명령  
        CREATE 명령  
        클래스 만들기 명령  
        CLASSLIB 명령 만들기  
        색 집합 만들기 명령  
        연결 명령 만들기  
        데이터베이스 만들기 명령  
    :::column-end:::
    :::column:::
        양식 만들기 명령  
        다음에서 만들기 명령  
        레이블 만들기 명령  
        메뉴 명령 만들기  
        프로젝트 만들기 명령  
        쿼리 명령 만들기  
        보고서 만들기 명령  
        화면 만들기 명령  
        SQL 보기 만들기 명령  
        트리거 명령 만들기  
        뷰 만들기 명령  
        CREATEOBJECT () 함수  
        CURDIR () 함수  
        _CUROBJ 시스템 메모리 변수  
    :::column-end:::
:::row-end:::

## <a name="d"></a>D  

:::row:::
    :::column:::
        _DBLCLICK 시스템 메모리 변수  
        DBSETPROP () 함수  
        DDE 함수  
        메뉴 명령 비활성화  
        비활성화 팝업 명령  
        창 비활성화 명령  
        DECLARE 명령  
        DECLARE-DLL 명령  
        모음 정의 명령  
        상자 정의 명령  
        클래스 정의 명령  
        메뉴 명령 정의  
    :::column-end:::
    :::column:::
        PAD 명령 정의  
        POPUP 명령 정의  
        창 정의 명령  
        연결 삭제 명령  
        데이터베이스 삭제 명령  
        파일 삭제 명령  
        트리거 삭제 명령  
        뷰 삭제 명령  
        _DIARYDATE 시스템 메모리 변수  
        DIR 명령  
        디렉터리 명령  
        표시 명령  
    :::column-end:::
    :::column:::
        연결 표시 명령  
        데이터베이스 명령 표시  
        DLL 명령 표시  
        파일 표시 명령  
        메모리 표시 명령  
        개체 표시 명령  
        프로시저 표시 명령  
        상태 표시 명령  
        표시 구조 명령  
        테이블 표시 명령  
        보기 표시 명령  
        양식 실행 명령  
    :::column-end:::
:::row-end:::

## <a name="e"></a>E  

:::row:::
    :::column:::
        명령 편집  
        배출 명령  
        페이지 꺼내기 명령  
    :::column-end:::
    :::column:::
        ERASE 명령  
        오류 명령  
        내보내기 명령  
    :::column-end:::
    :::column:::
        외부 명령  
    :::column-end:::
:::row-end:::

## <a name="f"></a>F  

:::row:::
    :::column:::
        FCHSIZE () 함수  
        FCLOSE () 함수  
        FCREATE () 함수  
        FEOF () 함수  
        FERROR () 함수  
        FFLUSH () 함수  
        FGETS () 함수  
    :::column-end:::
    :::column:::
        필터 명령  
        찾기 명령  
        FKLABEL () 함수  
        FKMAX () 함수  
        글꼴 메트릭 () 함수  
        FOPEN () 함수  
        _FOXDOC 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        _FOXGRAPH 시스템 메모리 변수  
        FPUTS () 함수  
        FREAD () 함수  
        FSEEK () 함수  
        FWRITE () 함수  
    :::column-end:::
:::row-end:::

## <a name="g"></a>G  

:::row:::
    :::column:::
        _GENGRAPH 시스템 메모리 변수  
        _GENMENU 시스템 메모리 변수  
        _GENPD 시스템 메모리 변수  
        _GENSCRN 시스템 메모리 변수  
        _GENXTAB 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        GETBAR () 함수  
        GETCOLOR () 함수  
        GETDIR () 함수  
        GETEXPR 명령  
        GETFILE () 함수  
    :::column-end:::
    :::column:::
        GETFONT () 함수  
        GETOBJECT () 함수  
        GETPAD () 함수  
        GETPICT () 함수  
        GETPRINTER () 함수  
    :::column-end:::
:::row-end:::

## <a name="h"></a>H  

:::row:::
    :::column:::
        HELP 명령  
        메뉴 명령 숨기기  
    :::column-end:::
    :::column:::
        팝업 명령 숨기기  
        창 숨기기 명령  
    :::column-end:::
    :::column:::
        HOME () 함수  
    :::column-end:::
:::row-end:::

## <a name="i"></a>I  

:::row:::
    :::column:::
        IMESTATUS () 함수  
        IMPORT 명령  
        _INDENT 시스템 메모리 변수  
        인덱스 켜기 명령  
    :::column-end:::
    :::column:::
        INKEY () 함수  
        입력 명령  
        명령 삽입  
        INSMODE () 함수  
    :::column-end:::
    :::column:::
        ISCOLOR () 함수  
        ISMOUSE () 함수  
    :::column-end:::
:::row-end:::

## <a name="j"></a>J  

조인 명령

## <a name="k"></a>K  

키보드 명령

## <a name="l"></a>L  

:::row:::
    :::column:::
        레이블 명령  
        LASTKEY () 함수  
        LINENO () 함수  
    :::column-end:::
    :::column:::
        명령 나열  
        연결 나열 명령  
        _LMARGIN 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        로드 명령  
        LOCFILE () 함수  
    :::column-end:::
:::row-end:::

## <a name="m"></a>M  

:::row:::
    :::column:::
        MCOL () 함수  
        MD 명령  
        MDOWN () 함수  
        MEMORY () 함수  
        메뉴 명령  
        MENU () 함수  
        명령 메뉴  
        MESSAGEBOX () 함수  
        MKDIR 명령  
        클래스 수정 명령  
        명령 수정 명령  
        연결 수정 명령  
    :::column-end:::
    :::column:::
        데이터베이스 수정 명령  
        파일 수정 명령  
        양식 수정 명령  
        일반 명령 수정  
        레이블 수정 명령  
        메모 수정 명령  
        메뉴 명령 수정  
        프로시저 수정 명령  
        프로젝트 수정 명령  
        쿼리 명령 수정  
        보고서 수정 명령  
        화면 수정 명령  
    :::column-end:::
    :::column:::
        구조 수정 명령  
        뷰 수정 명령  
        창 수정 명령  
        마우스 명령  
        팝업 명령 이동  
        창 이동 명령  
        MRKBAR () 함수  
        MRKPAD () 함수  
        MROW () 함수  
        MWINDOW () 함수  
    :::column-end:::
:::row-end:::

## <a name="n"></a>N  

NUMLOCK () 함수

## <a name="o"></a>O  

:::row:::
    :::column:::
        OBJNUM () 함수  
        OBJTOCLIENT () 함수  
        OBJVAR () 함수  
        OEMTOANSI () 함수  
        APLABOUT 명령  
        가로 막대형 명령  
        ON ESCAPE 명령  
        끝내기 표시줄 명령  
    :::column-end:::
    :::column:::
        종료 메뉴 명령  
        PAD 끝내기 명령  
        ON EXIT POPUP 명령  
        ON KEY = 명령  
        ON KEY LABEL 명령  
        ON MACHELP 명령  
        채움 명령  
        페이지 명령  
    :::column-end:::
    :::column:::
        ON READERROR 명령  
        선택 막대에서 명령  
        선택 항목 메뉴 명령  
        선택 채움 패드 명령  
        선택 영역 팝업 명령  
        종료 시 명령  
    :::column-end:::
:::row-end:::

## <a name="p"></a>P  

:::row:::
    :::column:::
        PACK 데이터베이스 명령  
        PAD () 함수  
        _PADVANCE 시스템 메모리 변수  
        _PAGENO 시스템 메모리 변수  
        _PBPAGE 시스템 메모리 변수  
        PCOL () 함수  
        _PCOLNO 시스템 메모리 변수  
        _PCOPIES 시스템 메모리 변수  
        _PDRIVER 시스템 메모리 변수  
        _PDSETUP 시스템 메모리 변수  
        _PECODE 시스템 메모리 변수  
        _PEJECT 시스템 메모리 변수  
        PEMSTATUS () 함수  
    :::column-end:::
    :::column:::
        _PEPAGE 시스템 메모리 변수  
        매크로 재생 명령  
        _PLENGTH 시스템 메모리 변수  
        _PLINENO 시스템 메모리 변수  
        _PLOFFSET 시스템 메모리 변수  
        POP 키 명령  
        POP 메뉴 명령  
        POP POPUP 명령  
        POPUP () 함수  
        _PPITCH 시스템 메모리 변수  
        _PQUALITY 시스템 메모리 변수  
        _PRETEXT 시스템 메모리 변수  
        PRINTJOB ... ENDPRINTJOB 명령  
    :::column-end:::
    :::column:::
        PRINTSTATUS () 함수  
        PRMBAR () 함수  
        PRMPAD () 함수  
        PROMPT () 함수  
        PROW () 함수  
        PRTINFO () 함수  
        _PSCODE 시스템 메모리 변수  
        _PSPACING 시스템 메모리 변수  
        키 푸시 명령  
        밀어넣기 메뉴 명령  
        PUSH POPUP 명령  
        PUTFILE () 함수  
        _PWAIT 시스템 메모리 변수  
    :::column-end:::
:::row-end:::

## <a name="q"></a>Q  

QUIT 명령

## <a name="r"></a>R  

:::row:::
    :::column:::
        RD 명령  
        RDLEVEL () 함수  
        읽기 명령  
        읽기 메뉴 명령  
        READKEY () 함수  
        REFRESH () 함수  
        명령 인덱스  
        RELEASE 명령  
        릴리스 표시줄 명령  
        RELEASE CLASSLIB 명령  
        RELEASE LIBRARY 명령  
        메뉴 해제 명령  
        RELEASE 모듈 명령  
    :::column-end:::
    :::column:::
        RELEASE PAD 명령  
        팝업 릴리스 명령  
        릴리스 프로시저 명령  
        WINDOWS 명령 해제  
        클래스 제거 명령  
        명령 이름 바꾸기  
        클래스 이름 바꾸기 명령  
        연결 이름 바꾸기 명령  
        테이블 이름 바꾸기 명령  
        뷰 이름 바꾸기 명령  
        보고서 명령  
        REQUERY () 함수  
        복원 명령  
    :::column-end:::
    :::column:::
        매크로 복원 명령  
        복원 화면 명령  
        창 복원 명령  
        RESUME 명령  
        RGB () 함수  
        RGBSCHEME () 함수  
        _RMARGIN 시스템 메모리 변수  
        RMDIR 명령  
        ROW () 함수  
        &#124;를 실행 합니다.명령  
        RUNSCRIPT가 명령  
    :::column-end:::
:::row-end:::

## <a name="s"></a>S  

:::row:::
    :::column:::
        매크로 저장 명령  
        화면 저장 명령  
        저장 명령  
        WINDOWS 명령 저장  
        SCHEME () 함수  
        SCOLS () 함수  
        _SCREEN 시스템 메모리 변수  
        SCROLL 명령  
        SET 명령  
        대체 명령 설정  
        SET ANSI 명령  
        APLABOUT 명령 설정  
        자동 저장 명령 설정  
        종 모양 설정 명령  
        BLINK 명령 설정  
        BORDER 명령 설정  
        SET BRSTATUS 명령  
        SET CLASSLIB 명령  
        CLEAR 명령 설정  
        클록 명령 설정  
        명령 색 설정  
        구성표 색 설정 명령  
        색 집합 명령 설정  
        색을 명령으로 설정  
        호환 명령 설정  
        CONFIRM 명령 설정  
        콘솔 명령 설정  
        CPCOMPILE 설정  
        CPDIALOG 설정  
        통화 설정 명령  
        커서 설정 명령  
        DATASESSION 설정 명령  
        디버그 명령 설정  
        DECIMALS 명령 설정  
        구분 기호 설정 명령  
        개발 명령 설정  
        장치 설정 명령  
    :::column-end:::
    :::column:::
        표시 명령 설정  
        DOHISTORY 명령 설정  
        ECHO 명령 설정  
        이스케이프 명령 설정  
        FORMAT 명령 설정  
        SET FUNCTION 명령  
        머리글 설정 명령  
        도움말 명령 설정  
        HELPFILTER 명령 설정  
        강도 설정 명령  
        SET KEY 명령  
        SET KEYCOMP 명령  
        LOGERRORS 명령 설정  
        MACDESKTOP 명령 설정  
        SET MACHELP 명령  
        MACKEY 명령 설정  
        MARGIN 명령 설정  
        명령 표시 설정  
        표시를 명령으로 설정  
        MEMOWIDTH 명령 설정  
        메시지 명령 설정  
        마우스 설정 명령  
        SET ODOMETER 명령  
        SET OLEOBJECT 명령  
        색상표 설정 명령  
        SET 설정 명령  
        POINT 명령 설정  
        프린터 명령 설정  
        READBORDER 명령 설정  
        새로 고침 명령 설정  
        리소스 명령 설정  
        SAFETY 명령 설정  
        스코어 보드 명령 설정  
        SECONDS 명령 설정  
        구분 기호 설정 명령  
        SHADOWS 명령 설정  
        명령 건너뛰기 설정  
    :::column-end:::
    :::column:::
        공간 설정 명령  
        상태 설정 명령  
        상태 표시줄 설정 명령  
        STEP 명령 설정  
        고정 명령 설정  
        SYSFORMATS 명령 설정  
        SYSMENU 명령 설정  
        대화 명령 설정  
        SET TEXTMERGE 명령  
        SET TEXTMERGE 구분 기호 명령  
        항목 설정 명령  
        항목 ID 명령 설정  
        TRBETWEEN 명령 설정  
        형식 미리 설정 명령  
        보기 명령 설정  
        MEMO 명령의 창 설정  
        XCMDFILE 명령 설정  
        _SHELL 시스템 메모리 변수  
        GET 명령 표시  
        SHOW 명령을 표시 합니다.  
        메뉴 명령 표시  
        개체 명령 표시  
        팝업 명령 표시  
        창 표시 명령  
        크기 팝업 명령  
        크기 창 명령  
        기능 없는 PBAR () 함수  
        SKPPAD () 함수  
        SOUNDEX () 함수  
        _SPELLCHK 시스템 메모리 변수  
        SQL 함수  
        SROWS () 함수  
        _STARTUP 시스템 메모리 변수  
        SUSPEND 명령  
        Sys () 함수 (2011) 제외  
        SYSMETRIC () 함수  
    :::column-end:::
:::row-end:::

## <a name="t"></a>T  

:::row:::
    :::column:::
        _TABS 시스템 메모리 변수  
        텍스트 ... ENDTEXT 명령  
        _THROTTLE 시스템 메모리 변수  
    :::column-end:::
    :::column:::
        TRANSFORM () 함수  
        _TRANSPORT 시스템 메모리 변수  
        TXTWIDTH () 함수  
    :::column-end:::
    :::column:::
        유형 명령  
    :::column-end:::
:::row-end:::

## <a name="u"></a>U  

:::row:::
    :::column:::
        UPDATED () 함수  
    :::column-end:::
    :::column:::
        명령 사용  
    :::column-end:::
:::row-end:::

## <a name="v"></a>V  

:::row:::
    :::column:::
        데이터베이스 유효성 검사 명령  
    :::column-end:::
    :::column:::
        VARREAD () 함수  
    :::column-end:::
    :::column:::
        VERSION () 함수  
    :::column-end:::
:::row-end:::

## <a name="w"></a>W  

:::row:::
    :::column:::
        WAIT 명령  
        WBORDER () 함수  
        WCHILD () 함수  
        WCOLS () 함수  
        WEXIST () 함수  
        WFONT () 함수  
        _WINDOWS 시스템 메모리 변수  
        ... ENDWITH 명령  
    :::column-end:::
    :::column:::
        _WIZARD 시스템 메모리 변수  
        WLAST () 함수  
        WLCOL () 함수  
        WLROW () 함수  
        WMAXIMUM () 함수  
        WMINIMUM () 함수  
        WONTOP () 함수  
        WOUTPUT () 함수  
    :::column-end:::
    :::column:::
        WPARENT () 함수  
        _WRAP 시스템 메모리 변수  
        WREAD () 함수  
        WROWS () 함수  
        WTITLE () 함수  
        WVISIBLE () 함수  
    :::column-end:::
:::row-end:::

## <a name="z"></a>Z  

창 확대/축소 명령
