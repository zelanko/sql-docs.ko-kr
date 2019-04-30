---
title: 규칙, 트리거, 기본값 및 저장된 프로시저에 대 한 지원 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], stored procedures
- FoxPro ODBC driver [ODBC], commands and functions
- commands for FoxPro ODBC driver [ODBC]
- FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], triggers
- stored procedures [ODBC], Visual FoxPro ODBC driver
- Visual FoxPro ODBC driver [ODBC], rules
- FoxPro commands and functions [ODBC]
- rules [ODBC]
- Visual FoxPro ODBC driver [ODBC], default values
- FoxPro ODBC driver [ODBC], rules
- functions [ODBC], Visual FoxPro
- default values [ODBC]
- Visual FoxPro ODBC driver [ODBC], commands and functions
- Visual FoxPro ODBC driver [ODBC], triggers
- FoxPro ODBC driver [ODBC], stored procedures
- Visual FoxPro commands and functions [ODBC]
ms.assetid: e449de20-d6ca-4902-9f8e-814eb6e86650
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 47795998b019df22b01852519f75f6e8d3d274dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63269856"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>규칙, 트리거, 기본값 및 저장 프로시저 지원(Visual FoxPro ODBC 드라이버)
Visual FoxPro 규칙, 트리거, 기본값 또는 Visual FoxPro ODBC 드라이버를 사용 하 여 저장된 프로시저를 만들 수 없습니다. 그러나 응용 프로그램은 기존 규칙, 트리거, 기본값 또는 저장된 프로시저 상호 작용할 수 있는 삽입, 업데이트 또는 삭제 Visual FoxPro 데이터를 데이터베이스에 저장 된 것 처럼 합니다.  
  
 다음 표에서 Visual FoxPro 명령 및 명령 또는 함수를 규칙, 트리거, 기본값 또는 저장된 프로시저에 있는 경우 Visual FoxPro ODBC 드라이버에서 지원 되는 함수를 나열 합니다.  
  
 드라이버 인 규칙, 트리거, 기본값, 응용 프로그램 데이터와 상호 작용 또는 다른 Visual FoxPro 명령 또는 함수 저장된 프로시저를 호출 하는 경우 오류가 발생 합니다. 참조 [지원 되지 않는 Visual FoxPro 명령 및 함수](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) 명령 목록과 드라이버에서 지원 되지 않는 함수에 대 한 합니다.  
  
> [!TIP]  
>  규칙, 트리거 또는 드라이버에 의해 호출 될 때 실행할 명령을 결정 하는 저장된 프로시저에 조건부 코드를 삽입 하려는 경우 사용할 수 있습니다 합니다 **버전 ()** 함수입니다. 합니다 **버전 ()** 함수에서 반환 "Visual FoxPro ODBC 드라이버  *\<버전 >*" 드라이버에 의해 호출 될 때입니다.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>Visual FoxPro 명령 및 규칙, 트리거, 기본값 및 저장된 프로시저에서 지원 되는 함수  
  
||||  
|-|-|-|  
|$ 연산자|% 연산자|& 명령|  
|& & 명령|* 명령|= 명령|  
  
## <a name="a"></a>변수를 잠그기 위한  
  
||||  
|-|-|-|  
|ABS () 함수|ACOPY () 함수|TABLE 명령 추가|  
|ADATABASES () 함수|ADBOBJECTS () 함수|AERROR () 함수|  
|ADEL () 함수|AELEMENT () 함수|ALEN () 함수|  
|AFIELDS () 함수|AINS () 함수|ALTER TABLE - SQL 명령|  
|별칭 () 함수|ALLTRIM () 함수|배열 명령에서 추가|  
|AND 연산자|명령 추가|메모 명령 추가|  
|명령에서 추가|일반 명령 추가|ASCAN () 함수|  
|프로시저 명령 추가|ASC () 함수|ASUBSCRIPT () 함수|  
|ASIN () 함수|ASORT () 함수|ATAN () 함수|  
|() 함수|AT_C( ) Function|ATCLINE () 함수|  
|ATC () 함수|ATCC () 함수|AUSED () 함수|  
|ATLINE () 함수|ATN2 함수||  
|평균 명령|ACOS () 함수||  
  
## <a name="b"></a>B  
  
||||  
|-|-|-|  
|트랜잭션 명령 시작|() 함수 간에|BITNOT () 함수|  
|BITCLEAR () 함수|BITLSHIFT () 함수|BITSET () 함수|  
|BITOR () 함수|BITRSHIFT () 함수|빈 명령|  
|BITTEST () 함수|BITXOR () 함수||  
|BOF () 함수|BITAND () 함수||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|명령을 계산 합니다.|후보 () 함수|CHR () 함수|  
|CDX () 함수|CEILING () 함수|닫기 명령|  
|CHRTRAN () 함수|CHRTRANC () 함수|인덱스 명령 복사|  
|CMONTH () 함수|명령을 계속합니다|구조 확장 명령 복사|  
|프로시저 명령 복사|구조 명령 복사|명령으로 복사|  
|TAG 명령 복사|명령 배열에 복사 합니다.|CPCONVERT () 함수|  
|COS () 함수|COUNT 명령이|CTOD () 함수|  
|CPCURRENT () 함수|CPDBF () 함수|CURSORSETPROP () 함수|  
|CTOT () 함수|CURSORGETPROP () 함수||  
|CURVAL () 함수|CDOW () 함수||  
  
## <a name="d"></a>d  
  
||||  
|-|-|-|  
|DATE () 함수|DATETIME () 함수|DAY () 함수|  
|Dbc입니다 () 함수|DBF () 함수|DBGETPROP () 함수|  
|DBUSED () 함수|DELETE - SQL 명령|삭제 명령|  
|DELETE TAG 명령|삭제 () 함수|내림차순 () 함수|  
|DIFFERENCE () 함수|차원 명령|디스크 공간이 () 함수|  
|DMY () 함수|대/소문자를 수행 하는 중... ENDCASE 명령|명령을 수행합니다|  
|수행 하는 동안... ENDDO 명령|DOW () 함수|DTOC () 함수|  
|DTOR () 함수|DTO () 함수|DTOT () 함수|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|빈 () 함수|() 함수를 평가 합니다.|EXIT 명령|  
|오류 () 함수|EXP () 함수||  
|최종 트랜잭션 명령|EOF () 함수||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT () 함수|FDATE () 함수|필드 () 함수|  
|파일 () 함수|FILTER () 함수|FLDLIST () 함수|  
|떼 () 함수|FLOOR () 함수|플러시 명령|  
|FOR... ENDFOR 명령|() 함수에 대 한|() 함수가 있습니다.|  
|사용 가능한 테이블 명령|FSIZE () 함수|FTIME 함수|  
|FULLPATH 함수|함수 명령입니다.|FV () 함수|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|수집 명령|GETNEXTMODIFIED () 함수|이동/이동 명령|  
|GETFLDSTATE () 함수|GOMONTH () 함수||  
|GETCP () 함수|GETENV () 함수||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|HEADER( ) Function|시간 () 함수|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE () 함수|다음과 같은 경우... ENDIF 명령|IIF () 함수|  
|INDBC () 함수|INDEX 명령|INLIST () 함수|  
|INSERT-SQL 명령|INT () 함수|ISALPHA () 함수|  
|ISBLANK 함수|ISDIGIT () 함수|ISEXCLUSIVE () 함수|  
|ISLEADBYTE 함수|ISLOWER () 함수|ISNULL () 함수|  
|ISREADONLY () 함수|ISUPPER () 함수||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|키 () 함수|KEYMATCH () 함수||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|왼쪽된 () 함수|LEFTC( ) Function|LIKEC () 함수|  
|LENC () 함수|() 함수|LOCK () 함수|  
|로컬 명령|명령 찾기|LOOKUP () 함수|  
|LOG () 함수|LOG10 함수|LTRIM () 함수|  
|LOWER () 함수|LPARAMETERS 명령||  
|LUPDATE () 함수|LEN () 함수||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE 시스템 메모리 변수|MAX () 함수|MDX () 함수|  
|MDY () 함수|MEMLINES () 함수|메시지 () 함수|  
|MIN () 함수|분 () 함수|MLINE () 함수|  
|MOD 함수|MONTH () 함수|MTON () 함수|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX () 함수|() 함수를 정규화 합니다.|NOT 연산자|  
|참고 명령|NTOM () 함수|NVL () 함수|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|() 함수를 발생합니다.|OLDVAL () 함수|오류 명령|  
|키 명령|() 함수|데이터베이스 열기 명령|  
|OR 연산자|ORDER () 함수|OS () 함수|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK 명령|매개 변수 () 함수|결제 () 함수|  
|명령 매개 변수|기본 () 함수|전용 명령|  
|PI () 함수|프로그램 () 함수|적절 한 () 함수|  
|프로시저 명령|PV () 함수||  
|공용 명령|PADL () &#124; PADR () &#124; PADC () 함수||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND () 함수|RAT () 함수|RATC () 함수|  
|RATLINE () 함수|명령 회수|RECCOUNT () 함수|  
|RECNO () 함수|RECSIZE () 함수|지역 명령|  
|관계 () 함수|TABLE 명령을 제거 합니다.|바꾸기 명령|  
|배열 명령에서 대체|REPLICATE () 함수|명령을 다시 시도|  
|명령을 반환 합니다.|오른쪽 () 함수|RIGHTC () 함수|  
|RLOCK () 함수|ROLLBACK 명령|ROUND () 함수|  
|RTOD () 함수|RTRIM () 함수||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|검색 중... ENDSCAN 명령|분산형 명령|초 () 함수|  
|시간 (초) () 함수|명령 검색|() 함수를 검색 합니다.|  
|명령 선택|선택 () 함수|SELECT-SQL 명령|  
|SET BLOCKSIZE 명령|SET 전달 명령|SET 세기 명령|  
|SET COLLATE 명령|데이터베이스 명령 집합|SET 날짜 명령|  
|집합 기본 명령|SET DELETED 명령|SET EXACT 명령|  
|SET EXCLUSIVE 명령|SET FDOW 명령|SET 필드 명령|  
|SET 필터 명령|SET 고정된 명령|SET FULLPATH 명령|  
|SET FWEEK 명령|시간 설정된 명령|INDEX 명령 집합|  
|SET LOCK 명령|SET MULTILOCKS 명령|명령 근처 설정|  
|SET NOCPTRANS 명령|알림 명령 집합|SET NULL 명령|  
|SET 최적화 명령|SET 순서 명령|SET PATH 명령|  
|SET 프로시저 명령|SET 관계 명령|집합 관계 끄기 명령|  
|SET REPROCESS 명령|설정 건너뛰기 명령|SET UDFPARMS 명령|  
|SET UNIQUE 명령|SET 볼륨 명령|SET () 함수|  
|SETFLDSTATE () 함수|SIGN () 함수|SIN () 함수|  
|SKIP 명령|정렬 명령|SPACE () 함수|  
|SQRT () 함수|저장소 명령|STR () 함수|  
|STRCONV 함수|STRTRAN () 함수|STUFF () 함수|  
|STUFFC () 함수|SUBSTR () 함수|SUBSTRC () 함수|  
|SUM 명령|SYS(2011) 함수||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY 시스템 메모리 변수|_TRIGGERLEVEL 시스템 메모리 변수|TAGCOUNT () 함수|  
|TABLEUPDATE () 함수|태그 () 함수|대상 () 함수|  
|TAGNO () 함수|TAN () 함수|TRIM () 함수|  
|TIME () 함수|총 명령|TXNLEVEL () 함수|  
|TTOC () 함수|TTOD () 함수||  
|형식 () 함수|TABLEREVERT () 함수||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|UNIQUE () 함수|UNLOCK 명령|명령을 사용 하 여|  
|업데이트 명령|위쪽 () 함수||  
|() 함수 사용|UPDATE - SQL 명령||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL () 함수|버전 () 함수||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|주 () 함수|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|YEAR () 함수|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 명령|||
