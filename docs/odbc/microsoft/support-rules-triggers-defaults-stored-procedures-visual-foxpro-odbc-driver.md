---
title: 규칙, 트리거, 기본값 및 저장 프로시저에 대 한 지원 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2fcf8e7c80b2712313cba81199489dc7cb06dce0
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301140"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>규칙, 트리거, 기본값 및 저장 프로시저 지원(Visual FoxPro ODBC 드라이버)
Visual foxpro 규칙, 트리거, 기본값 또는 저장 프로시저는 Visual FoxPro ODBC 드라이버를 사용 하 여 만들 수 없습니다. 그러나 응용 프로그램은 데이터베이스에 저장 된 Visual FoxPro 데이터를 삽입, 업데이트 또는 삭제할 때 기존 규칙, 트리거, 기본값 또는 저장 프로시저와 상호 작용할 수 있습니다.  
  
 다음 표에서는 명령 또는 함수가 규칙, 트리거, 기본값 또는 저장 프로시저에 있는 경우 Visual FoxPro ODBC 드라이버에서 지 원하는 Visual FoxPro 명령 및 함수를 나열 합니다.  
  
 응용 프로그램이 규칙, 트리거, 기본값 또는 저장 프로시저가 다른 Visual FoxPro 명령이 나 함수를 호출 하는 데이터와 상호 작용 하는 경우 드라이버에서 오류를 생성 합니다. 드라이버에서 지원 하지 않는 명령 및 함수 목록은 [지원 되지 않는 Visual FoxPro 명령 및 함수](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) 를 참조 하세요.  
  
> [!TIP]  
>  드라이버에서 호출할 때 실행할 명령을 결정 하는 조건부 코드를 규칙, 트리거 또는 저장 프로시저에 삽입 하려는 경우 **VERSION ()** 함수를 사용할 수 있습니다. **VERSION ()** 함수는 드라이버에서 호출 될 때 "Visual FoxPro ODBC 드라이버 * \<버전>*"을 반환 합니다.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>규칙, 트리거, 기본값 및 저장 프로시저에서 지원 되는 Visual FoxPro 명령 및 함수  
  
||||  
|-|-|-|  
|$ 연산자|% 연산자|& 명령|  
|&& 명령|* 명령|= 명령|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS () 함수|ACOPY () 함수|테이블 추가 명령|  
|ADATABASES () 함수|ADBOBJECTS () 함수|AERROR () 함수|  
|ADEL () 함수|AELEMENT () 함수|ALEN () 함수|  
|AFIELDS () 함수|AINS () 함수|ALTER TABLE - SQL 명령|  
|ALIAS () 함수|ALLTRIM () 함수|배열에서 추가 명령|  
|AND 연산자|추가 명령|메모 추가 명령|  
|명령에서 추가|일반 명령 추가|ASCAN () 함수|  
|프로시저 추가 명령|ASC () 함수|ASUBSCRIPT () 함수|  
|ASIN () 함수|ASORT () 함수|ATAN () 함수|  
|AT () 함수|AT_C () 함수|ATCLINE () 함수|  
|ATC () 함수|ATCC () 함수|AUSED () 함수|  
|ATLINE () 함수|ATN2 () 함수||  
|평균 명령|ACOS () 함수||  
  
## <a name="b"></a>b  
  
||||  
|-|-|-|  
|BEGIN TRANSACTION 명령|BETWEEN () 함수|BITNOT () 함수|  
|BITCLEAR () 함수|BITLSHIFT () 함수|BITSET () 함수|  
|BITOR () 함수|BITRSHIFT () 함수|빈 명령|  
|BITTEST () 함수|BITXOR () 함수||  
|BOF () 함수|BITAND () 함수||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|CALCULATE 명령|후보 () 함수|CHR () 함수|  
|CDX () 함수|천장 () 함수|닫기 명령|  
|CHRTRAN () 함수|CHRTRANC () 함수|인덱스 복사 명령|  
|CMONTH () 함수|CONTINUE 명령|구조 복사 확장 명령|  
|프로시저 복사 명령|구조 복사 명령|복사 명령|  
|태그 복사 명령|배열에 복사 명령|CPCONVERT () 함수|  
|COS () 함수|COUNT 명령|CTOD () 함수|  
|CPCURRENT () 함수|CPDBF () 함수|CURSORSETPROP () 함수|  
|CTOT () 함수|CURSORGETPROP () 함수||  
|CURVAL () 함수|CDOW () 함수||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|DATE () 함수|DATETIME () 함수|DAY () 함수|  
|DBC () 함수|DBF () 함수|DBGETPROP () 함수|  
|DBUSED () 함수|DELETE - SQL 명령|DELETE 명령|  
|DELETE TAG 명령|DELETED () 함수|내림차순 () 함수|  
|차 () 함수|차원 명령|DISKSPACE () 함수|  
|AMY () 함수|DO CASE ... ENDCASE 명령|DO 명령|  
|수행 하는 동안 ... ENDDO 명령|DOW () 함수|ETOC () 함수|  
|DTOR () 함수|DTO () 함수|DTOT () 함수|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|EMPTY () 함수|EVALUATE () 함수|끝내기 명령|  
|ERROR () 함수|EXP () 함수||  
|END TRANSACTION 명령|EOF () 함수||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT () 함수|FDATE () 함수|FIELD () 함수|  
|FILE () 함수|FILTER () 함수|FLDLIST () 함수|  
|FLOCK () 함수|FLOOR () 함수|플러시 명령|  
|... ENDFOR 명령|FOR () 함수|FOUND () 함수|  
|FREE 테이블 명령|FSIZE () 함수|FTIME () 함수|  
|FULLPATH () 함수|함수 명령|FV () 함수|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|수집 명령|GETNEXTMODIFIED () 함수|GO/GOTO 명령|  
|GETFLDSTATE () 함수|GOMONTH () 함수||  
|GETCP () 함수|GETENV () 함수||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|HEADER () 함수|HOUR () 함수|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE () 함수|... ENDIF 명령|IIF () 함수|  
|INDBC () 함수|INDEX 명령|INLIST () 함수|  
|SQL 명령 삽입|INT () 함수|ISALPHA () 함수|  
|ISBLANK () 함수|ISDIGIT () 함수|ISEXCLUSIVE () 함수|  
|ISLEADBYTE () 함수|ISLOWER () 함수|ISNULL () 함수|  
|ISREADONLY () 함수|ISUPPER () 함수||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|KEY () 함수|KEYMATCH () 함수||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|LEFT () 함수|왼쪽 c () 함수|LIKEC () 함수|  
|LENC () 함수|LIKE () 함수|LOCK () 함수|  
|LOCAL 명령|찾기 명령|LOOKUP () 함수|  
|LOG () 함수|LOG10 () 함수|LTRIM () 함수|  
|LOWER () 함수|LPARAMETERS 명령||  
|LUPDATE () 함수|LEN () 함수||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE 시스템 메모리 변수|MAX () 함수|MDX () 함수|  
|MDY () 함수|MEMLINES () 함수|MESSAGE () 함수|  
|MIN () 함수|MINUTE () 함수|MLINE () 함수|  
|MOD () 함수|MONTH () 함수|MTON () 함수|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX () 함수|정규화 () 함수|NOT 연산자|  
|NOTE 명령|NTOM () 함수|NVL () 함수|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|Occurs () 함수|OLDVAL () 함수|ON ERROR 명령|  
|ON KEY 명령|ON () 함수|데이터베이스 열기 명령|  
|OR 연산자|ORDER () 함수|OS () 함수|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|PACK 명령|PARAMETERS () 함수|결제 () 함수|  
|PARAMETERS 명령|PRIMARY () 함수|PRIVATE 명령|  
|PI () 함수|PROGRAM () 함수|적절 한 () 함수|  
|프로시저 명령|PV () 함수||  
|공용 명령|PADL () &#124; PADR () &#124; PADC () 함수||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND () 함수|RAT () 함수|RATC () 함수|  
|RATLINE () 함수|회수 명령|RECCOUNT () 함수|  
|-NO () 함수|고 크기 () 함수|국가별 명령|  
|RELATION () 함수|테이블 제거 명령|REPLACE 명령|  
|배열에서 바꾸기 명령|복제 () 함수|RETRY 명령|  
|반환 명령|RIGHT () 함수|RIGHTC () 함수|  
|RLOCK () 함수|ROLLBACK 명령|ROUND () 함수|  
|RTOD () 함수|RTRIM () 함수||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|검색 ... ENDSCAN 명령|분산형 명령|SEC () 함수|  
|SECONDS () 함수|SEEK 명령|SEEK () 함수|  
|명령 선택|SELECT () 함수|SELECT-SQL 명령|  
|SET BLOCKSIZE 명령|SET 운반 명령|세기 명령 설정|  
|SET COLLATE 명령|데이터베이스 명령 설정|날짜 설정 명령|  
|기본 명령 설정|SET DELETED 명령|SET EXACT 명령|  
|SET EXCLUSIVE 명령|SET FDOW 명령|SET FIELDS 명령|  
|필터 명령 설정|고정 명령 설정|SET FULLPATH 명령|  
|FWEEK 명령 설정|시간 설정 명령|인덱스 설정 명령|  
|잠금 명령 설정|SET MULTILOCKS 명령|NEAR 명령 설정|  
|NOCPTRANS 명령 설정|알림 설정 명령|SET NULL 명령|  
|최적화 명령 설정|SET ORDER 명령|SET PATH 명령|  
|SET PROCEDURE 명령|RELATION 명령 설정|관계 해제 명령 설정|  
|SET REPROCESS 명령|SKIP 명령 설정|SET UDFPARMS 명령|  
|SET UNIQUE 명령|볼륨 설정 명령|SET () 함수|  
|SETFLDSTATE () 함수|SIGN () 함수|SIN () 함수|  
|SKIP 명령|정렬 명령|SPACE () 함수|  
|SQRT () 함수|저장 명령|STR () 함수|  
|STRCONV () 함수|STRTRAN () 함수|사물 () 함수|  
|STUFFC () 함수|SUBSTR () 함수|SUBSTRC () 함수|  
|SUM 명령|SYS (2011) 함수||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|_TALLY 시스템 메모리 변수|_TRIGGERLEVEL 시스템 메모리 변수|TAGCOUNT () 함수|  
|TABLEUPDATE () 함수|TAG () 함수|TARGET () 함수|  
|TAGNO () 함수|TAN () 함수|TRIM () 함수|  
|TIME () 함수|TOTAL 명령|TXNLEVEL () 함수|  
|TTOC () 함수|TTOD () 함수||  
|TYPE () 함수|TABLEREVERT () 함수||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|UNIQUE () 함수|잠금 해제 명령|명령 사용|  
|UPDATE 명령|UPPER () 함수||  
|USED () 함수|UPDATE - SQL 명령||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL () 함수|VERSION () 함수||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|WEEK () 함수|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|YEAR () 함수|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 명령|||
