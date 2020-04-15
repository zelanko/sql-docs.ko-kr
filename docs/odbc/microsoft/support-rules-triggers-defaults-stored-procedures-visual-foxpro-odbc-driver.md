---
title: 규칙, 트리거, 기본값 및 저장 프로시저 지원 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301140"
---
# <a name="support-for-rules-triggers-default-values-and-stored-procedures-visual-foxpro-odbc-driver"></a>규칙, 트리거, 기본값 및 저장 프로시저 지원(Visual FoxPro ODBC 드라이버)
Visual FoxPro ODBC 드라이버를 사용하여 Visual FoxPro 규칙, 트리거, 기본값 또는 저장 프로시저를 만들 수 없습니다. 그러나 응용 프로그램은 데이터베이스에 저장된 Visual FoxPro 데이터를 삽입, 업데이트 또는 삭제할 때 기존 규칙, 트리거, 기본값 또는 저장 프로시저와 상호 작용할 수 있습니다.  
  
 다음 표에는 명령또는 함수가 규칙, 트리거, 기본값 또는 저장 프로시저에 있을 때 Visual FoxPro ODBC 드라이버에서 지원하는 Visual FoxPro 명령 및 함수가 나열됩니다.  
  
 응용 프로그램이 규칙, 트리거, 기본값 또는 저장 프로시저가 다른 Visual FoxPro 명령 또는 함수를 호출하는 데이터와 상호 작용하는 경우 드라이버는 오류를 생성합니다. 지원되지 [않는 Visual FoxPro 명령 및 기능은](../../odbc/microsoft/unsupported-visual-foxpro-commands-and-functions-visual-foxpro-odbc-driver.md) 드라이버에서 지원하지 않는 명령 및 함수 목록을 참조하십시오.  
  
> [!TIP]  
>  드라이버에서 호출할 때 실행할 명령을 결정하는 조건부 코드를 규칙, 트리거 또는 저장 프로시저에 삽입하려면 **VERSION()** 함수를 사용할 수 있습니다. **버전()** 함수는 드라이버에서 호출할 * \< *때 "Visual FoxPro ODBC 드라이버 버전>"을 반환합니다.  
  
## <a name="visual-foxpro-commands-and-functions-supported-in-rules-triggers-default-values-and-stored-procedures"></a>규칙, 트리거, 기본값 및 저장 프로시저에서 지원되는 Visual FoxPro 명령 및 기능  
  
||||  
|-|-|-|  
|$ 연산자|% 연산자|& 명령|  
|&& 명령|* 명령|= 명령|  
  
## <a name="a"></a>A  
  
||||  
|-|-|-|  
|ABS () 기능|ACOPY () 기능|테이블 명령 추가|  
|A데이터베이스() 기능|ADBOBJECTS() 기능|AERROR() 함수|  
|ADEL () 기능|AELEMENT () 함수|알렌 () 기능|  
|AFIELDS () 함수|AINS() 기능|ALTER TABLE - SQL 명령|  
|별칭 () 기능|올트림() 기능|배열 명령에서 부속|  
|및 연산자|부속 명령|메모 명령 부속|  
|명령에서 부속|일반 명령 부속|ASCAN () 기능|  
|프로시저 명령 부속|ASC () 기능|서브스크립트() 기능|  
|아신() 기능|ASORT () 함수|아탄 () 기능|  
|AT ( ) 기능|AT_C() 기능|ATCLINE() 기능|  
|ATC() 기능|ATCC () 기능|AUSED() 함수|  
|ATLINE() 기능|ATN2 () 기능||  
|평균 명령|ACOS () 기능||  
  
## <a name="b"></a>b  
  
||||  
|-|-|-|  
|트랜잭션 명령 시작|사이 () 기능|비트노() 기능|  
|비트 클리어 () 기능|BITLSHIFT () 기능|비트 세트 () 기능|  
|비트 () 기능|비트시프트() 기능|빈 명령|  
|비트 테스트 () 기능|비트소르() 기능||  
|BOF () 기능|비트 앤드 () 기능||  
  
## <a name="c"></a>C  
  
||||  
|-|-|-|  
|명령 계산|후보() 기능|CHR () 기능|  
|CDX () 기능|천장 () 기능|명령 닫기|  
|크트란 () 기능|CHRTRANC () 기능|복사 인덱스 명령|  
|CMONTH () 기능|계속 명령|복사 구조 확장 명령|  
|프로시저 커맨드 복사|복사 구조 명령|명령에 복사|  
|태그 복사 명령|배열 명령에 복사|CPCONVERT () 기능|  
|코스 () 기능|카운트 명령|CTOD () 기능|  
|CPCURRENT () 함수|CPDBF () 기능|커서셋프롭() 기능|  
|CTO () 기능|커서게프롭() 기능||  
|CURVAL () 기능|CDOW () 함수||  
  
## <a name="d"></a>D  
  
||||  
|-|-|-|  
|날짜 ( ) 기능|날짜 시간() 기능|일 () 기능|  
|DBC () 기능|DBF () 기능|DBGETPROP () 기능|  
|DBUSED() 기능|DELETE - SQL 명령|명령 삭제|  
|DELETE TAG 명령|삭제됨() 함수|내림차순() 기능|  
|차이 () 기능|차원 명령|디스크 스페이스 () 기능|  
|DMY() 기능|케이스를 수행 ... 끝 케이스 명령|DO 명령|  
|하는 동안 ... ENDDO 명령|다우 () 함수|DTOC () 기능|  
|DTOR () 기능|DTOS () 기능|DTOT () 기능|  
  
## <a name="e"></a>E  
  
||||  
|-|-|-|  
|빈 () 기능|평가() 기능|종료 명령|  
|오류() 기능|EXP() 기능||  
|트랜잭션 종료 명령|EOF() 기능||  
  
## <a name="f"></a>F  
  
||||  
|-|-|-|  
|FCOUNT () 기능|FDATE ( ) 기능|필드() 기능|  
|FILE ( ) 기능|필터() 기능|FLDLIST () 기능|  
|FLOCK () 기능|바닥 () 기능|플러시 명령|  
|에 대 한 ... 엔드포 명령|FOR () 기능|FOUND () 기능|  
|무료 테이블 명령|FSIZE () 기능|FTIME () 기능|  
|풀패스() 기능|함수 명령|FV () 기능|  
  
## <a name="g"></a>G  
  
||||  
|-|-|-|  
|명령 수집|GETNEXT수정() 기능|이동/고토 명령|  
|겟플드스테이트() 기능|GOMONTH () 기능||  
|GETCP () 기능|게텐프 () 기능||  
  
## <a name="h"></a>H  
  
|||  
|-|-|  
|헤더() 기능|시간 () 기능|  
  
## <a name="i"></a>I  
  
||||  
|-|-|-|  
|IDXCOLLATE () 기능|경우... ENDIF 명령|IIF() 함수|  
|INDBC () 기능|INDEX 명령|인리스트 () 기능|  
|삽입 SQL 명령|INT () 기능|ISALPHA () 기능|  
|ISBLANK() 기능|ISDIGIT () 기능|ISEXCLUSIVE() 기능|  
|이세리드바이트() 기능|ISLOWER() 기능|ISNULL() 함수|  
|ISREADONLY () 기능|ISUPPER () 기능||  
  
## <a name="k"></a>K  
  
||||  
|-|-|-|  
|키() 기능|키매치() 기능||  
  
## <a name="l"></a>L  
  
||||  
|-|-|-|  
|왼쪽() 함수|왼쪽() 함수|LIKEC () 기능|  
|LENC () 기능|LIKE () 기능|잠금() 기능|  
|로컬 명령|명령 찾기|조회() 기능|  
|로그() 기능|LOG10 () 기능|LTRIM () 기능|  
|LOWER () 기능|LPARAMETERS 명령||  
|LUPDATE () 기능|LEN () 기능||  
  
## <a name="m"></a>M  
  
||||  
|-|-|-|  
|_MLINE 시스템 메모리 변수|MAX () 기능|MDX () 기능|  
|MDY() 기능|MEMLINES() 기능|메시지() 기능|  
|최소() 기능|분() 기능|MLINE() 기능|  
|MOD ( ) 기능|월() 기능|MTON () 기능|  
  
## <a name="n"></a>N  
  
||||  
|-|-|-|  
|NDX () 기능|정규화() 기능|운영자가 아님|  
|참고 명령|NTOM () 기능|NVL () 기능|  
  
## <a name="o"></a>O  
  
||||  
|-|-|-|  
|발생() 기능|올드발 () 기능|오류 명령 켜기|  
|키 명령시|ON () 기능|데이터베이스 명령 열기|  
|OR 연산자|순서 () 기능|OS() 기능|  
  
## <a name="p"></a>P  
  
||||  
|-|-|-|  
|팩 명령|매개 변수 () 함수|지불 () 기능|  
|매개 변수 명령|기본() 함수|개인 명령|  
|PI() 기능|프로그램() 기능|적절한() 기능|  
|프로시저 명령|태양광 발전() 기능||  
|공용 명령|PADL () &#124; PADR () &#124; PADC () 기능||  
  
## <a name="r"></a>R  
  
||||  
|-|-|-|  
|RAND () 기능|RAT () 기능|RATC () 기능|  
|RATLINE() 기능|리콜 명령|RECCOUNT () 기능|  
|RECNO () 기능|RECSIZE () 기능|지역 사령부|  
|관계() 함수|테이블 명령 제거|바꾸기 명령|  
|배열 명령에서 바꾸기|복제( ) 함수|명령 다시 시도|  
|Return 명령|오른쪽() 기능|오른쪽() 기능|  
|RLOCK() 기능|롤백 명령|원형() 기능|  
|RTOD () 기능|RTRIM() 기능||  
  
## <a name="s"></a>S  
  
||||  
|-|-|-|  
|스캔... ENDSCAN 명령|분산 명령|SEC ( ) 기능|  
|초() 기능|검색 명령|SEEK () 기능|  
|명령 선택|SELECT ( ) 기능|선택-SQL 명령|  
|SET BLOCKSIZE 명령|캐리 커맨드 설정|세기 명령 설정|  
|SET COLLATE 명령|데이터베이스 명령 설정|날짜 명령 설정|  
|기본 명령 설정|SET DELETED 명령|SET EXACT 명령|  
|SET EXCLUSIVE 명령|FDOW 명령 설정|필드 명령 설정|  
|필터 명령 설정|고정 명령 설정|전체 경로 명령 설정|  
|FWEEK 명령 설정|시간 설정 명령|인덱스 명령 설정|  
|잠금 명령 설정|멀티록스 명령 설정|명령 근처 설정|  
|NOCPTRANS 명령 설정|알림 명령 설정|SET NULL 명령|  
|최적화 명령 설정|주문 설정 명령|SET PATH 명령|  
|프로시저 명령 설정|관계 명령 설정|관계 끄기 명령 설정|  
|SET REPROCESS 명령|건너뛰기 명령 설정|UDFPARMS 명령 설정|  
|SET UNIQUE 명령|볼륨 명령 설정|SET ( ) 기능|  
|SETFLDSTATE () 기능|기호 () 기능|SIN() 기능|  
|건너뛰기 명령|정렬 명령|공간 () 기능|  
|SQRT () 기능|저장 명령|STR () 기능|  
|STRCONV () 기능|스트트란 () 기능|물건 () 기능|  
|STUFFC () 기능|SUBSTR () 기능|SUBSTRC () 기능|  
|SUM 명령|SYS (2011) 기능||  
  
## <a name="t"></a>T  
  
||||  
|-|-|-|  
|시스템 메모리 변수 _TALLY|시스템 메모리 변수 _TRIGGERLEVEL|태그카운트() 기능|  
|테이블 업데이트 () 기능|태그() 기능|대상() 기능|  
|타그노() 기능|TAN () 기능|트림 () 기능|  
|시간() 기능|총 명령|TXNLEVEL () 기능|  
|TTOC () 기능|TTOD () 기능||  
|유형 () 기능|테이블 버트 () 기능||  
  
## <a name="u"></a>U  
  
||||  
|-|-|-|  
|고유() 기능|명령 잠금 해제|사용 명령|  
|업데이트 명령|어퍼() 기능||  
|USED () 기능|UPDATE - SQL 명령||  
  
## <a name="v"></a>V  
  
||||  
|-|-|-|  
|VAL ( ) 기능|버전 () 기능||  
  
## <a name="w"></a>W  
  
||||  
|-|-|-|  
|주간 () 기능|||  
  
## <a name="y"></a>Y  
  
||||  
|-|-|-|  
|연도() 기능|||  
  
## <a name="z"></a>Z  
  
||||  
|-|-|-|  
|ZAP 명령|||
