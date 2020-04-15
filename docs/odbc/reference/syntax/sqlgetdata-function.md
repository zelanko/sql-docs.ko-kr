---
title: SQLGetData 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLGetData
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLGetData
helpviewer_keywords:
- SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac11505b8e47dae8df53af27c64a7ee6372b3f28
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81285509"
---
# <a name="sqlgetdata-function"></a>SQLGetData 함수(SQLGetData Function)
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLGetData는** 결과 집합의 단일 열 또는 **SQLParamData가** SQL_PARAM_DATA_AVAILABLE 반환한 후 단일 매개 변수에 대한 데이터를 검색합니다. 부품의 가변 길이 데이터를 검색하기 위해 여러 번 호출할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLGetData(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   Col_or_Param_Num,  
      SQLSMALLINT    TargetType,  
      SQLPOINTER     TargetValuePtr,  
      SQLLEN         BufferLength,  
      SQLLEN *       StrLen_or_IndPtr);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *Col_or_Param_Num*  
 [입력] 열 데이터를 검색하는 경우 데이터를 반환할 열의 수입니다. 결과 집합 열은 1부터 시작하는 증가열 순서로 번호가 매겨져 있습니다. 책갈피 열은 열 번호 0입니다. 책갈피를 사용하도록 설정한 경우에만 지정할 수 있습니다.  
  
 매개 변수 데이터를 검색하는 경우 1에서 시작하는 매개 변수의 서수입니다.  
  
 *Targettype*  
 [입력] **TargetValuePtr* 버퍼의 C 데이터 형식의 형식 식별자입니다. 유효한 C 데이터 유형 및 유형 식별자 목록은 부록 D: 데이터 [형식의 C 데이터 유형](../../../odbc/reference/appendixes/c-data-types.md) 섹션을 참조하십시오.  
  
 *TargetType이* SQL_ARD_TYPE 경우 드라이버는 ARD의 SQL_DESC_CONCISE_TYPE 필드에 지정된 형식 식별자를 사용합니다. *TargetType이* SQL_APD_TYPE 경우 **SQLGetData는** **SQLBindParameter**에 지정된 것과 동일한 C 데이터 형식을 사용합니다. 그렇지 않으면 **SQLGetData에** 지정된 C 데이터 형식은 **SQLBindParameter**에 지정된 C 데이터 형식을 재정의합니다. SQL_C_DEFAULT 경우 드라이버는 원본의 SQL 데이터 형식에 따라 기본 C 데이터 형식을 선택합니다.  
  
 확장 된 C 데이터 형식을 지정할 수도 있습니다. 자세한 내용은 [ODBC의 C 데이터 유형을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)참조하십시오.  
  
 *대상 밸류프트*  
 [출력] 데이터를 반환할 버퍼에 대한 포인터입니다.  
  
 *대상 값 Ptr* NULL 수 없습니다.  
  
 *버퍼 길이*  
 [입력] **TargetValuePtr* 버퍼의 길이(바이트)입니다.  
  
 드라이버는 *BufferLength를* 사용하여 문자 또는 이진 데이터와 같은 가변 길이 데이터를 반환할 때 \* *TargetValuePtr* 버퍼의 끝을 지나서 쓰지 않도록 합니다. 드라이버는 \* *TargetValuePtr*에 문자 데이터를 반환할 때 null 종료 문자를 계산합니다. *따라서 *TargetValuePtr은* null 종료 문자에 대한 공간을 포함해야 하거나 드라이버가 데이터를 트렁킨다.  
  
 드라이버가 정수 또는 날짜 구조와 같은 고정 길이 데이터를 반환하면 드라이버는 *BufferLength를* 무시하고 버퍼가 데이터를 보유할 수 있을 만큼 충분히 크다고 가정합니다. 따라서 응용 프로그램이 고정 길이 데이터에 대해 충분히 큰 버퍼를 할당하거나 드라이버가 버퍼의 끝을 지나 서 작성하는 것이 중요합니다.  
  
 **SQLGetData는** *버퍼 길이가* 0보다 작지만 *버퍼* 길이가 0일 때는 SQLSTATE HY090(잘못된 문자열 또는 버퍼 길이)을 반환합니다.  
  
 *StrLen_or_IndPtr*  
 [출력] 길이 또는 표시기 값을 반환할 버퍼에 대한 포인터입니다. null 포인터인 경우 길이 또는 표시기 값이 반환되지 않습니다. 이렇게 하면 가져오는 데이터가 NULL인 경우 오류가 반환됩니다.  
  
 **SQLGetData** 길이/표시기 버퍼에서 다음 값을 반환할 수 있습니다.  
  
-   반환할 수 있는 데이터의 길이  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 자세한 내용은 이 항목의 [길이/표시기 값 및 "주석" 사용을](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) 참조하십시오.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 SQL_HANDLE_STMT *핸들 SQL_HANDLE_STMT* 핸들 *핸들을* **호출** 하 여 가져올 수 있습니다. *Handle* 다음 표에서는 **SQLGetData에서** 일반적으로 반환되는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|지정된 열에 대한 모든 데이터 *Col_or_Param_Num*함수에 대한 단일 호출에서 검색할 수 없습니다. SQL_NO_TOTAL 또는 **SQLGetData에** 대 한 현재 호출 하기 전에 지정된된 \*열에 남아 있는 데이터의 길이 *StrLen_or_IndPtr*반환 됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)<br /><br /> 단일 열에 **대해 SQLGetData에** 대한 여러 호출을 사용하는 방법에 대한 자세한 내용은 "주석"을 참조하십시오.|  
|01S07|분수 잘림|하나 이상의 열에 대해 반환된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함하는 시간, 타임스탬프 및 간격 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07006|제한된 데이터 형식 특성 위반|결과 집합에 있는 열의 데이터 값은 *TargetType 인수TargetType에*의해 지정된 C 데이터 유형으로 변환할 수 없습니다.|  
|07009|잘못된 설명자 인덱스|인수 *Col_or_Param_Num* 지정된 값이 0이고 SQL_ATTR_USE_BOOKMARKS 문 특성이 SQL_UB_OFF 설정되었습니다.<br /><br /> *인수 Col_or_Param_Num* 지정된 값이 결과 집합의 열 수보다 큽합니다.<br /><br /> *Col_or_Param_Num* 값은 사용 가능한 매개 변수의 서수와 같지 않았습니다.<br /><br /> (DM) 지정된 열이 바인딩되었습니다. 이 설명은 **SQLGetInfo**에서 SQL_GETDATA_EXTENSIONS 옵션에 대한 SQL_GD_BOUND 비트 마스크를 반환하는 드라이버에는 적용되지 않습니다.<br /><br /> (DM) 지정된 열의 수가 가장 높은 바운드 열의 수보다 적거나 같습니다. 이 설명은 **SQLGetInfo**에서 SQL_GETDATA_EXTENSIONS 옵션에 대한 SQL_GD_ANY_COLUMN 비트 마스크를 반환하는 드라이버에는 적용되지 않습니다.<br /><br /> (DM) 응용 프로그램이 이미 현재 행에 대해 **SQLGetData를** 호출했습니다. 현재 호출에 지정된 열 수가 이전 호출에 지정된 열 수보다 적습니다. 및 드라이버는 **SQLGetInfo에서**SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_ANY_ORDER 비트 마스크를 반환 하지 않습니다.<br /><br /> (DM) *TargetType* 인수가 SQL_ARD_TYPE ARD의 *Col_or_Param_Num* 설명자 레코드가 일관성 검사에 실패했습니다.<br /><br /> (DM) *TargetType* 인수가 SQL_ARD_TYPE ARD의 SQL_DESC_COUNT 필드의 값이 *Col_or_Param_Num* 인수보다 적습니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|22002|표시기 변수가 필요하지만 제공되지 않음|*StrLen_or_IndPtr* null 포인터이고 NULL 데이터가 검색되었습니다.|  
|22003|범위를 벗어난 숫자 값|열에 대한 숫자 값(숫자 또는 문자열)을 반환하면 숫자의 전체(소수와 반대)가 잘리게 됩니다.<br /><br /> 자세한 내용은 [부록 D: 데이터 유형을](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조하십시오.|  
|22007|잘못된 날짜 시간 형식|결과 집합의 문자 열은 C 날짜, 시간 또는 타임스탬프 구조에 바인딩되었으며 열의 값은 각각 잘못된 날짜, 시간 또는 타임스탬프입니다. 자세한 내용은 [부록 D: 데이터 유형을](../../../odbc/reference/appendixes/appendix-d-data-types.md)참조하십시오.|  
|22012|0으로 나누기|0으로 분할된 산술 식의 값이 반환되었습니다.|  
|22015|간격 필드 오버플로|정확한 숫자 또는 간격 SQL 형식에서 간격 C 유형으로 할당하면 선행 필드에서 상당한 자릿수가 손실되었습니다.<br /><br /> 간격 C 유형으로 데이터를 반환할 때 간격 C 형식에서 SQL 형식의 값을 표현할 수 없었습니다.|  
|22018|캐스트 사양에 대해 잘못된 문자 값|결과 집합의 문자 열이 문자 C 버퍼로 반환되고 열에는 버퍼의 문자 집합에 표현이 없는 문자가 포함되어 있습니다.<br /><br /> C 형식은 정확하거나 대략적인 숫자, 날짜 시간 또는 간격 데이터 형식이었습니다. 열의 SQL 형식은 문자 데이터 형식입니다. 열의 값이 바인딩된 C 형식의 유효한 리터럴이 아닙니다.|  
|24000|잘못된 커서 상태|(DM) 이 함수는 필요한 데이터 행에 커서를 배치하기 위해 **SQLFetch** 또는 **SQLFetchScroll를** 먼저 호출하지 않고 호출되었습니다.<br /><br /> (DM) *명령문 핸들이* 실행된 상태였지만 명령문 *핸들*과 연관된 결과 집합이 없습니다.<br /><br /> *명령문 핸들에* 커서가 열려 있고 **SQLFetch** 또는 **SQLFetchScroll가** 호출되었지만 결과 집합이 시작되기 전이나 결과 집합이 끝난 후에 커서가 배치되었습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. *MessageText* 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다.|  
|HY01|메모리 할당 오류|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|프로그램 유형 범위를 벗어난 경우|(DM) *인수 TargetType(열* 데이터를 검색하는 경우) SQL_ARD_TYPE 또는 SQL_APD_TYPE(매개 변수 데이터를 검색하는 경우)SQL_C_DEFAULT 유효한 데이터 형식이 아닙니다.<br /><br /> (DM) *인수 Col_or_Param_Num* 0이고 *TargetType* 인수가 고정 길이 책갈피 또는 가변 길이 책갈피의 SQL_C_VARBOOKMARK SQL_C_BOOKMARK 않았습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *StatementHandle에서*호출된 다음 *명령문 핸들*에서 함수가 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출된 다음 *명령문 핸들*에서 함수가 다시 호출되었습니다.|  
|HY09|null 포인터의 잘못된 사용|(DM) 인수 *TargetValuePtr는* null 포인터였습니다.|  
|HY010|함수 시퀀스 오류|(DM) 지정된 *명령문핸들이* 실행된 상태가 아닙니다. 이 함수는 **SQLExecDirect,** **SQLExecute** 또는 카탈로그 함수를 먼저 호출하지 않고 호출되었습니다.<br /><br /> (DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. 이 비동기 함수는 **SQLGetData** 함수가 호출될 때 계속 실행 중이었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.<br /><br /> (DM) *명령문 핸들이* 실행된 상태였지만 명령문 *핸들*과 연관된 결과 집합이 없습니다.<br /><br /> **SQLExeceute,** **SQLExecDirect**또는 **SQLMoreResults에** 대한 호출은 SQL_PARAM_DATA_AVAILABLE 반환되었지만 **SQLGetData** 대신 **SQLParamData가**호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 인수 *BufferLength에* 대해 지정된 값이 0보다 적습니다.<br /><br /> *인수 BufferLength에* 대해 지정된 값이 4보다 적고 *Col_or_Param_Num* 인수가 0으로 설정되었으며 드라이버가 ODBC 2 *.x* 드라이버였습니다.|  
|HY109|잘못된 커서 위치|커서는 삭제되었거나 가져올 수 없는 행에 **(SQLSetPos,** **SQLFetch,** **SQLFetchScroll**또는 **SQLBulkOperations)에**위치했습니다.<br /><br /> 커서는 정방향 전용 커서였으며 행 집합 크기가 1개보다 큽했습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|하이크00|구현되지 않은 선택적 기능|드라이버 또는 데이터 원본은 **SQLFetchScroll**에서 여러 행이 있는 **SQLGetData** 사용을 지원하지 않습니다. 이 설명은 **SQLGetInfo**에서 SQL_GETDATA_EXTENSIONS 옵션에 대한 SQL_GD_BLOCK 비트 마스크를 반환하는 드라이버에는 적용되지 않습니다.<br /><br /> 드라이버 또는 데이터 원본은 *TargetType* 인수와 해당 열의 SQL 데이터 형식의 조합으로 지정된 변환을 지원하지 않습니다. 이 오류는 열의 SQL 데이터 형식이 드라이버 별 SQL 데이터 형식에 매핑된 경우에만 적용됩니다.<br /><br /> 드라이버는 ODBC 2 *.x만*지원하며 *TargetType* 인수는 다음 중 하나입니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 부록 D: 데이터 형식의 [C 데이터 형식에](../../../odbc/reference/appendixes/c-data-types.md) 나열된 간격 C 데이터 형식중 어느 쪽도 해당합니다.<br /><br /> 드라이버는 3.50 이전의 ODBC 버전만 지원하며 *TargetType* 인수가 SQL_C_GUID.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle에* 해당하는 드라이버는 기능을 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetData** 지정된 열에서 데이터를 반환합니다. **SQLGetData는** **SQLFetch, SQLFetchScroll**또는 **SQLExtendedFetch**에 의해 설정된 **SQLFetchScroll**결과집합에서 하나 이상의 행을 가져온 후에만 호출할 수 있습니다. 가변 길이 데이터가 너무 커서 **SQLGetData를** 한 번 호출하여 반환할 수 없는 경우(응용 프로그램의 제한으로 인해) **SQLGetData는** 부분적으로 검색할 수 있습니다. 일부 열을 행에 바인딩하고 **SQLGetData를** 호출할 수 있지만 일부 제한 사항이 적용됩니다. 자세한 내용은 [긴 데이터 얻기](../../../odbc/reference/develop-app/getting-long-data.md)를 참조하십시오.  
  
 스트리밍된 출력 매개 변수를 사용하여 **SQLGetData를** 사용하는 자세한 내용은 [SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)를 사용하여 출력 매개 변수 검색을 참조하십시오.  
  
## <a name="using-sqlgetdata"></a>SQLGetData 사용  
 드라이버가 **SQLGetData에**대한 확장을 지원하지 않는 경우 함수는 마지막 바인딩된 열보다 큰 숫자가 있는 언바운드 열에 대해서만 데이터를 반환할 수 있습니다. 또한 데이터 행 내에서 **SQLGetData에** 대한 각 호출의 *Col_or_Param_Num* 인수 값은 이전 호출의 *Col_or_Param_Num* 값보다 크거나 같아야 합니다. 즉, 데이터는 열 번호 순서를 증가시켜 검색해야 합니다. 마지막으로 확장이 지원되지 않으면 행 집합 크기가 1보다 큰 경우 **SQLGetData를** 호출할 수 없습니다.  
  
 운전자는 이러한 제한 사항을 완화할 수 있습니다. 드라이버가 완화하는 제한을 결정하기 위해 응용 프로그램은 다음과 같은 SQL_GETDATA_EXTENSIONS 옵션 중 한 가지로 **SQLGetInfo를** 호출합니다.  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** 출력 매개 변수 값을 반환 하기 위해 호출할 수 있습니다. 자세한 내용은 [SQLGetData를 사용하여 출력 매개 변수 검색을](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)참조하십시오.  
  
-   SQL_GD_ANY_COLUMN. 이 옵션이 반환되면 마지막 바인딩된 열 이전의 열을 포함하여 모든 언바운드 열에 대해 **SQLGetData를** 호출할 수 있습니다.  
  
-   SQL_GD_ANY_ORDER. 이 옵션이 반환되면 **SQLGetData는** 임의의 순서로 언바운드 열을 호출할 수 있습니다.  
  
-   SQL_GD_BLOCK. SQL_GETDATA_EXTENSIONS InfoType에 대해 **SQLGetInfo에서** 이 옵션을 반환하는 경우 드라이버는 행 집합 크기가 1보다 클 때 **SQLGetData** 호출을 지원하며 응용 프로그램은 **SQLGetData를** 호출하기 전에 올바른 행에 커서를 배치하는 SQL_POSITION 옵션으로 **SQLSetPos를** 호출할 수 있습니다.  
  
-   SQL_GD_BOUND. 이 옵션이 반환되면 **SQLGetData는** 바인딩된 열과 언바운드 열에 대해 호출할 수 있습니다.  
  
 이러한 제한 사항에는 두 가지 예외가 있으며 운전자가 이완할 수 있는 기능이 있습니다. 첫째, 행 집합 크기가 1보다 큰 경우 **SQLGetData는** 정방향 전용 커서에 대해 호출해서는 안 됩니다. 둘째, 드라이버가 책갈피를 지원하는 경우 응용 프로그램이 마지막 바인딩된 열 앞에 다른 열에 대해 **SQLGetData를** 호출할 수 없는 경우에도 항상 **SQLGetData를** 열 0에 호출하는 기능을 지원해야 합니다. (응용 프로그램이 ODBC 2 .x 드라이버로 작업하는 경우 **SQLGetData는** **SQLFetch를**호출한 후 Col_or_Param_Num 0으로 호출될 때 책갈피를 *.x* 성공적으로 반환합니다. **SQLFetch는** SQL_FETCH_NEXT *FetchOrientation을* 사용하여 **SQLExtendedFetch에 매핑되고** Col_or_Param_Num 0이 있는 **SQLGetData는** odBC *Col_or_Param_Num* 3 *Col_or_Param_Num* *fOption* *.x* 드라이버 관리자 *.x* **SQLSqlst.SQL_GET_BOOKMARK.)**  
  
 **SQLGetData** 커서가 행에 배치되지 않았기 때문에 **SQLBulkOperations를** SQL_ADD 옵션으로 호출하여 삽입된 행에 대한 책갈피를 검색하는 데 사용할 수 없습니다. 응용 프로그램은 **SQL_ADD 함께 SQLBulkOperations를** 호출하기 전에 열 0을 바인딩하여 이러한 행에 대한 책갈피를 검색할 수 있으며, 이 경우 **SQLBulkOperations는** 바인딩된 버퍼에서 책갈피를 반환합니다. 그런 다음 **SQLFetchScroll를** SQL_FETCH_BOOKMARK 호출하여 해당 행의 커서를 재배치할 수 있습니다.  
  
 *TargetType* 인수가 간격 데이터 형식인 경우 ARD의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정된 기본 간격 정밀도(2)와 기본 간격 초 정밀도(6)가 각각 데이터에 사용됩니다. *TargetType* 인수가 SQL_C_NUMERIC 데이터 형식인 경우 ARD의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정된 기본 정밀도(드라이버 정의) 및 기본 눈금(0)이 데이터에 사용됩니다. 기본 정밀도 또는 배율이 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**을 호출하여 적절한 설명자 필드를 명시적으로 설정해야 합니다. SQL_DESC_CONCISE_TYPE 필드를 SQL_C_NUMERIC 호출하고 *SQL_ARD_TYPE TargetType* 인수를 사용하여 **SQLGetData를** 호출할 수 있으며, 이로 인해 설명자 필드의 정밀도와 배율 값이 사용됩니다.  
  
> [!NOTE]
>  ODBC 2 *.x에서*응용 프로그램은 *TargetType을 SQL_C_DATE,* SQL_C_TIME \*또는 SQL_C_TIMESTAMP 설정하여 *TargetValuePtr이* 날짜, 시간 또는 타임스탬프 구조임을 나타냅니다. ODBC 3 *.x에서*응용 프로그램은 *TargetType을* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME 또는 SQL_C_TYPE_TIMESTAMP 설정합니다. 드라이버 관리자는 응용 프로그램 및 드라이버 버전에 따라 필요한 경우 적절한 매핑을 만듭니다.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>파트에서 가변 길이 데이터 검색  
 **SQLGetData는** 부분적으로 가변 길이 데이터가 포함된 열에서 데이터를 검색하는 데 사용할 수 있습니다 SQL_LONGVARBINARY SQL_VARBINARY SQL_BINARY SQL_WLONGVARCHAR SQL_WVARCHAR SQL_WCHAR SQL_LONGVARCHAR SQL_VARCHAR SQL_CHAR.  
  
 부분적으로 열에서 데이터를 검색하기 위해 응용 프로그램은 동일한 열에 대해 **SQLGetData를** 여러 번 연속으로 호출합니다. 각 호출에서 **SQLGetData는** 데이터의 다음 부분을 반환합니다. 문자 데이터의 중간 부분에서 null 종료 문자를 제거하는 데 주의를 기울여 부품을 다시 어셈블하는 것은 응용 프로그램에 달려 있습니다. 반환할 데이터가 더 많거나 종료 문자에 대해 충분한 버퍼가 할당되지 않은 경우 **SQLGetData는** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004(데이터가 잘린 데이터)를 반환합니다. 데이터의 마지막 부분을 반환하면 **SQLGetData가** SQL_SUCCESS 반환합니다. 응용 프로그램이 응용 프로그램 버퍼의 데이터 양을 알 수 없기 때문에 SQL_NO_TOTAL 또는 0은 열에서 데이터를 검색하기 위해 마지막 유효한 호출에서 반환될 수 없습니다. 이후에 **SQLGetData가** 호출되면 SQL_NO_DATA 반환됩니다. 자세한 내용은 다음 섹션 "SQLGetData로 데이터 검색"을 참조하십시오.  
  
 가변 길이 책갈피는 **SQLGetData에**의해 부분적으로 반환될 수 있습니다. 다른 데이터와 마찬가지로 **SQLGetData를** 호출하여 부분적으로 가변 길이 책갈피를 반환하면 SQLSTATE 01004(문자열 데이터, 오른쪽 잘린)가 반환되고 반환할 데이터가 더 있을 때 SQL_SUCCESS_WITH_INFO 반환됩니다. 이는 SQL_ERROR 및 SQLSTATE 22001(문자열 데이터, 오른쪽 잘린)을 반환하는 **SQLFetch** 또는 **SQLFetchScroll**호출에 의해 가변 길이 책갈피를 잘린 경우와 다릅니다.  
  
 **SQLGetData는** 부분적으로 고정 길이 데이터를 반환하는 데 사용할 수 없습니다. **SQLGetData** 고정 길이 데이터를 포함 하는 열에 대 한 행에서 두 번 이상 호출 하는 경우 첫 번째 후 모든 호출에 대 한 SQL_NO_DATA 반환 합니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색  
 드라이버가 스트리밍된 출력 매개 변수를 지원하는 경우 응용 프로그램은 작은 버퍼로 **SQLGetData를** 여러 번 호출하여 큰 매개 변수 값을 검색할 수 있습니다. 스트리밍된 출력 매개 변수에 대한 자세한 내용은 [SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)를 사용하여 출력 매개 변수 검색을 참조하십시오.  
  
## <a name="retrieving-data-with-sqlgetdata"></a>SQLGetData를 사용하여 데이터 검색  
 지정된 열에 대한 데이터를 반환하기 위해 **SQLGetData는** 다음 단계 순서를 수행합니다.  
  
1.  열에 대한 모든 데이터를 이미 반환한 경우 SQL_NO_DATA 반환합니다.  
  
2.  데이터가 \*NULL인 경우 *StrLen_or_IndPtr* SQL_NULL_DATA 설정합니다. 데이터가 null이고 *StrLen_or_IndPtr* null 포인터인 경우 **SQLGetData는** SQLSTATE 22002를 반환합니다(표시기 변수는 필요하지만 제공되지 않음).  
  
     열의 데이터가 NULL이 아닌 경우 **SQLGetData는** 3단계로 진행됩니다.  
  
3.  SQL_ATTR_MAX_LENGTH 문 특성이 영하지 않은 값으로 설정된 경우 열에 문자 또는 이진 데이터가 포함되어 있고 **SQLGetData가** 이전에 열에 대해 호출되지 않은 경우 데이터가 SQL_ATTR_MAX_LENGTH 바이트로 잘립니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 명령문 특성은 네트워크 트래픽을 줄이기 위한 것입니다. 일반적으로 네트워크를 통해 데이터를 반환하기 전에 데이터를 트렁크로 하는 데이터 원본에 의해 구현됩니다. 드라이버와 데이터 원본을 지원하기 위해 필요하지 않습니다. 따라서 데이터가 특정 크기로 잘리도록 하려면 응용 프로그램은 해당 크기의 버퍼를 할당하고 *BufferLength* 인수의 크기를 지정해야 합니다.  
  
4.  데이터를 *TargetType*에 지정된 유형으로 변환합니다. 데이터에는 해당 데이터 형식에 대한 기본 정밀도와 배율이 지정됩니다. *TargetType이* SQL_ARD_TYPE 경우 ARD의 SQL_DESC_CONCISE_TYPE 필드에 있는 데이터 형식이 사용됩니다. *TargetType이* SQL_ARD_TYPE 경우 SQL_DESC_CONCISE_TYPE 필드의 데이터 형식에 따라 ARD의 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드의 정밀도와 배율이 데이터에 부여됩니다. 기본 정밀도 또는 배율이 적절하지 않은 경우 응용 프로그램은 **SQLSetDescField** 또는 **SQLSetDescRec**을 호출하여 적절한 설명자 필드를 명시적으로 설정해야 합니다.  
  
5.  데이터가 문자 또는 바이너리와 같은 가변 길이 데이터 유형으로 변환된 경우 **SQLGetData는** 데이터의 길이가 *BufferLength를*초과하는지 여부를 확인합니다. 문자 데이터의 길이(null-종료 문자 포함)가 *BufferLength를*초과하는 경우 **SQLGetData는** 데이터를 *BufferLength로* 트렁킨다. 그런 다음 데이터를 null-종료합니다. 이진 데이터의 길이가 데이터 버퍼의 길이를 초과하는 경우 **SQLGetData는** *이를 BufferLength* 바이트로 연결합니다.  
  
     제공된 데이터 버퍼가 너무 작아서 null 종료 문자를 보유할 수 없습니다 **SQL_SUCCESS_WITH_INFO.**  
  
     **SQLGetData는** 고정 길이 데이터 유형으로 변환된 데이터를 트렁킨다. 항상 **TargetValuePtr의* 길이가 데이터 형식의 크기라고 가정합니다.  
  
6.  \* *TargetValuePtr*에서 변환된(및 잘린) 데이터를 배치합니다. **SQLGetData는** 데이터를 줄바에서 반환할 수 없습니다.  
  
7.  StrLen_or_IndPtr. \* *StrLen_or_IndPtr* *StrLen_or_IndPtr* null 포인터인 경우 **SQLGetData는** 길이를 반환하지 않습니다.  
  
    -   문자 또는 이진 데이터의 경우 변환 후 *BufferLength로*인해 잘림하기 전의 데이터 길이입니다. 드라이버가 변환 후 데이터의 길이를 확인할 수 없는 경우(예: 긴 데이터의 경우)는 SQL_SUCCESS_WITH_INFO 반환하고 길이를 SQL_NO_TOTAL 설정합니다. **SQLGetData에** 대한 마지막 호출은 항상 0 또는 SQL_NO_TOTAL 아니라 데이터의 길이를 반환해야 합니다. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 데이터가 잘린 경우 실제 길이가 아닌 이 특성의 값은 \* *StrLen_or_IndPtr.* 이 특성은 변환 하기 전에 서버에서 데이터를 트러닝 하도록 설계 되었습니다 때문에 드라이버는 실제 길이 알아낼 수 없습니다. **SQLGetData가** 동일한 열에 대해 여러 번 연속으로 호출되는 경우 현재 호출이 시작될 때 사용할 수 있는 데이터의 길이입니다. 즉, 각 후속 호출에 따라 길이가 줄어듭니다.  
  
    -   다른 모든 데이터 형식의 경우 변환 후 데이터의 길이입니다. 즉, 데이터가 변환된 형식의 크기입니다.  
  
8.  변환 하는 동안 중요 도 없이 데이터가 잘린 경우 (예: 실제 숫자 1.234 정수 1로 변환 될 때 잘립니다) 또는 *BufferLength너무* 작기 때문에 (예를 들어, 문자열 "abcdef" 4 바이트 버퍼에 배치 됩니다), **SQLGetData** 반환 SQLSTATE 01004 (데이터 잘린) 및 SQL_SUCCESS_WITH_INFO. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 데이터가 손실 없이 잘린 경우 **SQLGetData는** SQL_SUCCESS 반환하고 SQLSTATE 01004(데이터가 잘린 데이터)를 반환하지 않습니다.  
  
 바인딩된 데이터 버퍼의 내용(바인딩된 열에서 **SQLGetData가** 호출되는 경우) 및 길이/표시기 버퍼는 **SQLGetData가** SQL_SUCCESS 반환하지 않거나 SQL_SUCCESS_WITH_INFO 경우 정의되지 않습니다.  
  
 **SQLGetData에** 대한 연속 호출은 요청된 마지막 열에서 데이터를 검색합니다. 이전 오프셋이 유효하지 않게 됩니다. 예를 들어 다음 시퀀스가 수행되는 경우:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 SQLGetData (icol=n)에 대한 두 번째 호출은 n 열의 시작부터 데이터를 검색합니다. 열에 대한 **SQLGetData에** 대한 이전 호출로 인한 데이터의 오프셋은 더 이상 유효하지 않습니다.  
  
## <a name="descriptors-and-sqlgetdata"></a>설명자 및 SQLGetData  
 **SQLGetData는** 설명자 필드와 직접 상호 작용하지 않습니다.  
  
 *TargetType이* SQL_ARD_TYPE 경우 ARD의 SQL_DESC_CONCISE_TYPE 필드에 있는 데이터 형식이 사용됩니다. *TargetType이* SQL_ARD_TYPE 또는 SQL_C_DEFAULT 경우 SQL_DESC_CONCISE_TYPE 필드의 데이터 형식에 따라 ARD의 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드의 정밀도와 배율이 데이터에 부여됩니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 **SELECT** 문을 실행하여 이름, ID 및 전화 번호로 정렬된 고객 ID, 이름 및 전화 번호의 결과 집합을 반환합니다. 각 데이터 행에 대해 **SQLFetch를** 호출하여 커서를 다음 행에 배치합니다. 가져온 데이터를 검색하기 위해 **SQLGetData를** 호출합니다. 데이터에 대한 버퍼와 반환된 바이트 수는 **SQLGetData**에 대한 호출에 지정됩니다. 마지막으로 각 직원의 이름, ID 및 전화 번호를 인쇄합니다.  
  
```cpp  
#define NAME_LEN 50  
#define PHONE_LEN 50  
  
SQLCHAR      szName[NAME_LEN], szPhone[PHONE_LEN];  
SQLINTEGER   sCustID, cbName, cbAge, cbBirthday;  
SQLRETURN    retcode;  
SQLHSTMT     hstmt;  
  
retcode = SQLExecDirect(hstmt,  
   "SELECT CUSTID, NAME, PHONE FROM CUSTOMERS ORDER BY 2, 1, 3",  
   SQL_NTS);  
  
if (retcode == SQL_SUCCESS) {  
   while (TRUE) {  
      retcode = SQLFetch(hstmt);  
      if (retcode == SQL_ERROR || retcode == SQL_SUCCESS_WITH_INFO) {  
         show_error();  
      }  
      if (retcode == SQL_SUCCESS || retcode == SQL_SUCCESS_WITH_INFO){  
  
         /* Get data for columns 1, 2, and 3 */  
  
         SQLGetData(hstmt, 1, SQL_C_ULONG, &sCustID, 0, &cbCustID);  
         SQLGetData(hstmt, 2, SQL_C_CHAR, szName, NAME_LEN, &cbName);  
         SQLGetData(hstmt, 3, SQL_C_CHAR, szPhone, PHONE_LEN,  
            &cbPhone);  
  
         /* Print the row of data */  
  
         fprintf(out, "%-5d %-*s %*s", sCustID, NAME_LEN-1, szName,   
            PHONE_LEN-1, szPhone);  
      } else {  
         break;  
      }  
   }  
}  
```  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 대한 저장소 할당|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|블록 커서 위치와 관련이 없는 대량 작업 수행|[SQLBulk운영](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|명령문 처리 취소|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문 실행|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비된 SQL 문 실행|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록 가져오기 또는 결과 집합 스크롤|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|단일 데이터 행 또는 정방향 전용 방향으로 데이터 블록 가져오기|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|커서 위치 지정, 행 집합의 데이터 새로 고침 또는 행 집합의 데이터 업데이트 또는 삭제|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
