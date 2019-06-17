---
title: SQLGetData 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0dc0e57356c972797cbd72fa4ce3427a0e473dad
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65537998"
---
# <a name="sqlgetdata-function"></a>SQLGetData 함수(SQLGetData Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLGetData** 한 후 단일 매개 변수 또는 결과 집합의 단일 열에 대 한 데이터를 검색 **SQLParamData** SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 여러 번 부분에서 가변 길이 데이터를 검색할 호출할 수 있습니다 것입니다.  
  
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
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *Col_or_Param_Num*  
 [입력] 열 데이터를 검색 하는 것에 대 한 것이 데이터를 반환 하는 열 번호입니다. 결과 집합 열은 1부터 증가 열 순서 대로 번호가 지정 됩니다. 책갈피 열은 열 번호는 0입니다. 이 수 책갈피를 사용할 경우에 지정 합니다.  
  
 매개 변수 데이터를 검색, 1부터 시작 하는 매개 변수의 서 수입니다.  
  
 *TargetType*  
 [입력] C 데이터 형식의 형식 식별자는 **TargetValuePtr* 버퍼입니다. 유효한 C 데이터 형식 및 형식 식별자의 목록을 참조 하세요. 합니다 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션의 부록 d: 데이터 형식입니다.  
  
 하는 경우 *TargetType* SQL_ARD_TYPE, 형식 식별자는 카드가 SQL_DESC_CONCISE_TYPE 필드에 지정 된 드라이버 사용 됩니다. 하는 경우 *TargetType* SQL_APD_TYPE, 됩니다 **SQLGetData** 에 지정 된 동일한 C 데이터 형식을 사용 합니다 **SQLBindParameter**합니다. C 데이터 형식을 지정 하는 고, 그렇지 **SQLGetData** C 데이터 형식에 지정 된 재정의 **SQLBindParameter**합니다. SQL_C_DEFAULT 인 경우 드라이버 원본의 SQL 데이터 형식에 따라 기본 C 데이터 형식을 선택 합니다.  
  
 또한 확장된 C 데이터 유형을 지정할 수 있습니다. 자세한 내용은 [odbc에서 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.  
  
 *TargetValuePtr*  
 [출력] 데이터를 반환 하는 버퍼에 대 한 포인터입니다.  
  
 *TargetValuePtr* NULL 일 수 없습니다.  
  
 *BufferLength*  
 [입력] 길이 **TargetValuePtr* 바이트 버퍼입니다.  
  
 드라이버를 사용 하 여 *BufferLength* 끝 쓰기를 방지 하려면 합니다 \* *TargetValuePtr* 문자 또는 이진 데이터와 같은 가변 길이 데이터를 반환 하는 경우 버퍼입니다. 문자 데이터를 반환 하는 경우 드라이버는 null 종료 문자를 세는 유의 \* *TargetValuePtr*합니다. **TargetValuePtr* null 종료 문자에 대 한 공간이 있어야 하므로 또는 드라이버는 데이터를 자릅니다.  
  
 드라이버는 정수 또는 날짜 구조와 같은 고정 길이 데이터를 반환 하는 경우 드라이버 무시 *BufferLength* 버퍼 데이터를 저장 하기에 충분히 큰지 가정 합니다. 고정 길이 데이터에 대해 충분히 큰 버퍼를 할당할 응용 프로그램에 대 한 중요 한 되므로 또는 드라이버는 버퍼의 끝을 넘어 작성 합니다.  
  
 **SQLGetData** SQLSTATE HY090 반환 (잘못 된 문자열 또는 버퍼 길이) 때 *BufferLength* 0 보다 작은 하지만 때가 아니라 *BufferLength* 은 0입니다.  
  
 *StrLen_or_IndPtr*  
 [출력] 길이 또는 표시기 값을 반환 하는 버퍼에 대 한 포인터입니다. Null 포인터 이면 길이 또는 표시기 값이 반환 됩니다. 이 인출 되 고 데이터가 NULL 하는 경우 오류를 반환 합니다.  
  
 **SQLGetData** 길이/표시기 버퍼의 다음 값을 반환할 수 있습니다.  
  
-   반환할 사용 가능한 데이터의 길이  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 자세한 내용은 [길이/표시기 값을 사용 하 여](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) 이 항목의 "설명"입니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 사용 하 여는 *HandleType* 의 호출 및 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLGetData** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|지정된 된 열에 대 한 데이터의 일부만 *Col_or_Param_Num*, 단일 함수 호출에서 검색할 수 없습니다. SQL_NO_TOTAL 또는 현재 호출 하기 전에 지정된 된 열에서 남아 있는 데이터의 길이로 **SQLGetData** 반환 됩니다 \* *StrLen_or_IndPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> 여러 번 호출 하는 방법은 **SQLGetData** 단일 열을 "주석입니다."을 참조 하세요.|  
|01S07|소수 잘림|하나 이상의 열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 시간 구성 요소를 포함 하는 간격 데이터 형식에 대 한 시간의 소수 부분을 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성을 위반 했습니다.|결과 집합에 있는 열의 데이터 값을 인수로 지정한 C 데이터 형식으로 변환할 수 없습니다 *TargetType*합니다.|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 지정 된 값 *Col_or_Param_Num* 0 되었으며 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.<br /><br /> 인수에 지정 된 값 *Col_or_Param_Num* 결과 집합의 열 수보다 큽니다.<br /><br /> 합니다 *Col_or_Param_Num* 값을 사용할 수 있는 매개 변수의 서 수와 같지 없습니다.<br /><br /> (DM) 지정된 된 열에 바인딩 되었습니다. 이 설명은 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_BOUND 비트 마스크를 반환 하는 드라이버에 적용 되지 않습니다 **SQLGetInfo**합니다.<br /><br /> (DM) 지정 된 열의 숫자가 가장 높은 바인딩된 열의 개수 보다 작거나 합니다. 이 설명은 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_ANY_COLUMN 비트 마스크를 반환 하는 드라이버에 적용 되지 않습니다 **SQLGetInfo**합니다.<br /><br /> (DM) 응용 프로그램에 이미 호출 **SQLGetData** 현재 행에 대 한 현재 호출에 지정 된 열의 숫자가, 이전 호출에서 지정 된 열의 수보다 작 및 드라이버를 SQL_ 반환 하지 않습니다 SQL_GETDATA_EXTENSIONS 옵션에 대 한 비트 마스크 GD_ANY_ORDER **SQLGetInfo**합니다.<br /><br /> (DM)는 *TargetType* 인수가 SQL_ARD_TYPE, 및 *Col_or_Param_Num* 설명자 레코드는 카드가 일관성 검사에 실패 합니다.<br /><br /> (DM)는 *TargetType* 인수가 SQL_ARD_TYPE, 및는 카드가 SQL_DESC_COUNT 필드에 값이 보다 작은 *Col_or_Param_Num* 인수입니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지|*StrLen_or_IndPtr* 가 null 포인터 및 NULL 데이터를 검색 합니다.|  
|22003|숫자 값 범위를 벗어났습니다.|열에 대 한 숫자 값 (숫자 또는 문자열)으로 반환 되 었어야 하지만 (소수) 대신 전체 부분 숫자를 자를 수입니다.<br /><br /> 자세한 내용은 참조 하세요. [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.|  
|22007|잘못 된 날짜/시간 형식|결과 집합의 문자 열 C 날짜, 시간 또는 타임 스탬프 구조에 바인딩 되었습니다 및 각각 열에 값이는 잘못 된 날짜, 시간 또는 타임 스탬프입니다. 자세한 내용은 참조 하세요. [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.|  
|22012|0으로 나누기|0으로 나누기에서 발생 하는 산술 식의 값이 반환 되었습니다.|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형을 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> 간격 C 형식으로 데이터를 반환 하는 경우 C 간격 유형으로 SQL 형식의 값 표현 방식이 없기 있었습니다.|  
|22018|캐스트 사양의 문자 값|C 문자 버퍼에 반환 된 결과 집합의 문자 열 및 열 버퍼의 문자 집합에 표현이 없는 된 문자를 포함 합니다.<br /><br /> C 형식이는 정확 하거나 대략적인 숫자, datetime, 또는 간격 데이터 형식 열의 SQL 형식이 된 문자 데이터 형식입니다. 하는 열에 값을 바인딩된 C 형식의 유효한 리터럴이 없습니다.|  
|24000|잘못된 커서 상태|(DM) 함수가 먼저 호출 하지 않고 호출 된 **SQLFetch** 하거나 **SQLFetchScroll** 필요한 데이터의 행에 커서를 놓습니다.<br /><br /> (DM)는 *StatementHandle* 실행 상태가 되었지만 결과 집합이 연관 된 합니다 *StatementHandle*합니다.<br /><br /> 커서가 열린 합니다 *StatementHandle* 및 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 된 후 또는 결과 집합의 시작 하기 전에 커서가 있었기 있지만 결과 집합의 끝입니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 *MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|프로그램 유형 범위를 벗어났습니다.|(DM) 인수 *TargetType* 올바른 데이터 형식, SQL_C_DEFAULT, SQL_ARD_TYPE (의 경우 열 데이터 검색) 또는 SQL_APD_TYPE (의 경우 매개 변수 데이터를 검색).<br /><br /> (DM) 인수 *Col_or_Param_Num* 가 0이 고 인수가 *TargetType* 없습니다 SQL_C_BOOKMARK 고정 길이 책갈피 또는 SQL_C_VARBOOKMARK 가변 길이 책갈피에 대 한 합니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle*, 및 함수를 호출한 다음 다시 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램 및 기능에서 다시 호출 된 합니다 *StatementHandle*합니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) 인수 *TargetValuePtr* 가 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 지정 된 *StatementHandle* 실행 상태가 없습니다. 첫 번째 호출 하지 않고 함수를 호출한 **SQLExecDirect**를 **SQLExecute** 또는 카탈로그 함수입니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 여전히 실행 시기를 **SQLGetData** 함수를 호출 했습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.<br /><br /> (DM)는 *StatementHandle* 실행 상태가 되었지만 결과 집합이 연관 된 합니다 *StatementHandle*합니다.<br /><br /> 에 대 한 호출 **SQLExeceute**를 **SQLExecDirect**, 또는 **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE를 반환 하지만 **SQLGetData** 호출한 를 대신 **SQLParamData**합니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대 한 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.<br /><br /> 인수에 대 한 지정 된 값 *BufferLength* 보다 작은 4 합니다 *Col_or_Param_Num* 인수를 0으로 설정 된 했는데 드라이버는 ODBC 2 *.x* 드라이버입니다.|  
|HY109|잘못 된 커서 위치|커서가 있었기 (하 여 **SQLSetPos**, **SQLFetch**를 **SQLFetchScroll**, 또는 **SQLBulkOperations**)는 삭제 된 행 또는 가져올 수 없습니다.<br /><br /> 커서는 정방향 전용 커서 되었으며 행 집합 크기가 1 보다 큰 것입니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 사용을 지원 하지 않습니다 **SQLGetData** 에서 여러 행을 갖는 **SQLFetchScroll**합니다. 이 설명은 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_BLOCK 비트 마스크를 반환 하는 드라이버에 적용 되지 않습니다 **SQLGetInfo**합니다.<br /><br /> 드라이버 또는 데이터 원본 조합에 의해 지정 된 변환을 지원 하지 않습니다 합니다 *TargetType* 인수 및 해당 열의 SQL 데이터 형식입니다. 이 오류는 SQL 데이터 형식의 열 드라이버별 SQL 데이터 형식에 매핑한 경우에 적용 됩니다.<br /><br /> 드라이버는 ODBC 2만 지원 *.x*, 및 인수 *TargetType* 다음 중 하나 였습니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> C 간격 데이터 형식 중 하나에 나열 [C 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식입니다.<br /><br /> 드라이버 3.50, 및 인수 이전 ODBC 버전 지원 *TargetType* SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetData** 지정된 된 열에 데이터를 반환 합니다. **SQLGetData** 하 여 결과 집합에서 하나 이상의 행 인출 된 후에 호출할 수 있습니다 **SQLFetch**하십시오 **SQLFetchScroll**, 또는 **SQLExtendedFetch**합니다. 가변 길이 데이터에 대 한 단일 호출에서 반환할 너무 크면 **SQLGetData** (제한으로 인해 응용 프로그램에서), **SQLGetData** 부분에서 검색할 수 있습니다. 행 및 호출의 일부 열에 바인딩할 수 **SQLGetData** 다른 사용자에 대 한 몇 가지 제한 사항이 적용은 아니지만 합니다. 자세한 내용은 [긴 데이터를 가져오는](../../../odbc/reference/develop-app/getting-long-data.md)합니다.  
  
 에 대 한 내용은 **SQLGetData** 스트리밍된 출력 매개 변수를 사용 하 여 참조 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="using-sqlgetdata"></a>SQLGetData를 사용 하 여  
 드라이버에 대 한 확장을 지원 하지 않는 경우 **SQLGetData**, 함수는 마지막 바인딩된 열 보다 큰 숫자로 바인딩되지 않은 열에 대해서만 데이터를 반환할 수 있습니다. 또한 데이터 값의 행 내의 합니다 *Col_or_Param_Num* 각 호출에서 인수 **SQLGetData** 보다 크거나 같은 값 이어야 합니다 *Col_or_Param_Num*; 이전 호출에서 즉, 열 번호 순서 높이기 위한 과정에서 데이터를 검색 해야 합니다. 마지막으로 확장 없음 지 원하는 경우, **SQLGetData** 행 집합 크기가 1 보다 큰 경우에 호출할 수 없습니다.  
  
 드라이버는 이러한 제한 중 하나를 완화할 수 있습니다. 제한 완화 하는 드라이버를 확인 하려면 응용 프로그램 호출 **SQLGetInfo** 다음 SQL_GETDATA_EXTENSIONS 옵션 중 하나를 사용 하 여:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** 출력 매개 변수 값을 반환 하도록 호출 될 수 있습니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
-   SQL_GD_ANY_COLUMN. 이 옵션은 반환 되 면 **SQLGetData** 바인딩된 마지막 열 전에 포함 하 여 모든 바인딩되지 않은 열에 대해 호출할 수 있습니다.  
  
-   SQL_GD_ANY_ORDER. 이 옵션은 반환 되 면 **SQLGetData** 순서에 관계 없이 바인딩되지 않은 열에 대해 호출할 수 있습니다.  
  
-   SQL_GD_BLOCK. 이 옵션에서 반환 되 면 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 정보 항목을 드라이버 지원에 대 한 호출 **SQLGetData** 행 집합 크기가 1 보다 큰 응용 프로그램 호출할수시점과**SQLSetPos** SQL_POSITION 옵션을 호출 하기 전에 올바른 행에 커서를 놓고 **SQLGetData 합니다.**  
  
-   SQL_GD_BOUND. 이 옵션은 반환 되 면 **SQLGetData** 바인딩되지 않은 열 뿐만 아니라 바인딩된 열에 대해 호출할 수 있습니다.  
  
 이러한 제한을 완화 하는 드라이버의 기능을 두 가지 예외가 있습니다. 먼저 **SQLGetData** 호출 되 면 안 정방향 전용 커서에 대 한 행 집합 크기가 1 보다 큰 경우. 둘째, 드라이버 책갈피를 지 원하는 경우 지원 해야 합니다 항상 호출 하는 기능도 **SQLGetData** 0, 응용 프로그램이 호출할 수 없도록 하는 경우에 열에 대 한 **SQLGetData** 지난 기간 이전에 다른 열에 대 한 바인딩된 열입니다. (경우 응용 프로그램이 사용 되는 ODBC 2 *.x* 드라이버 **SQLGetData** 호출 된 경우 책갈피를 성공적으로 반환 됩니다 *Col_or_Param_Num* 을 호출한 후에 0 **SQLFetch**이므로 **SQLFetch** ODBC 3으로 매핑되어 *.x* 드라이버 관리자를 **SQLExtendedFetch** 를사용하여 *FetchOrientation* sql_fetch_next, 및 **SQLGetData** 사용 하 여를 *Col_or_Param_Num* ODBC 3으로 매핑된 0 *.x* 드라이버 관리자 **SQLGetStmtOption** 사용 하 여는 *fOption* SQL_GET_BOOKMARK입니다.)  
  
 **SQLGetData** 를 호출 하 여 방금 삽입 행에 대 한 책갈피를 검색 하려면 사용할 수 없습니다 **SQLBulkOperations** 에 SQL_ADD 옵션을 사용 하 여 커서가 행에 위치 하지는 때문입니다. 응용 프로그램 바인딩 앞에 열 0 호출 하 여 이러한 행에 대 한 책갈피를 검색할 수 있습니다 **SQLBulkOperations** 경우에 SQL_ADD를 사용 하 여 **SQLBulkOperations** 바인딩된 버퍼에 책갈피를 반환 합니다. **SQLFetchScroll** SQL_FETCH_BOOKMARK 해당 행에서 커서 위치를 변경 하려면를 사용 하 여 호출할 수 있습니다.  
  
 경우는 *TargetType* 인수가 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 자릿수가 SQL_DESC_PRECISION 필드에 설정 된 대로 기본 간격 선행 정밀도 (2) 및 기본 간격 초 전체 자릿수 (6) 간격 데이터 형식 각각은 카드가 데이터에 사용 됩니다. 경우는 *TargetType* 인수는 SQL_C_NUMERIC 데이터 형식, 기본 전체 자릿수 (드라이버 정의 됨) 및 (0), 확장 된 카드가의 SQL_DESC_PRECISION 및 자릿수가 SQL_DESC_SCALE 필드에 설정 된 대로 기본, 데이터에 사용 됩니다. 모든 기본 전체 자릿수 또는 소수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 적절 한 설명자 필드를 호출한 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다. SQL_DESC_CONCISE_TYPE 필드 SQL_C_NUMERIC 호출을 설정할 수 있습니다 **SQLGetData** 사용 하 여를 *TargetType* 설명자 필드에 전체 자릿수 및 소수 자릿수 값이 그러면 SQL_ARD_TYPE의 인수 사용할 수 있습니다.  
  
> [!NOTE]
>  ODBC 2에서 *.x*, 응용 프로그램 집합 *TargetType* SQL_C_DATE, SQL_C_TIME, 또는 SQL_C_TIMESTAMP 나타내는 \* *TargetValuePtr* 날짜, 시간 또는 타임 스탬프 구조입니다. ODBC 3에서 *.x*, 응용 프로그램 집합 *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME, 또는 SQL_C_TYPE_TIMESTAMP 합니다. 드라이버 관리자를 사용 하면 적절 한 매핑이 필요한 경우 기반 응용 프로그램 및 드라이버 버전에 있습니다.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>파트의 가변 길이 데이터를 검색합니다.  
 **SQLGetData** 가변 길이 데이터가 들어 있는 파트 즉, SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_ 식별자는 SQL 데이터 형식 열의 경우 열에서 데이터를 검색할 수 WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY, 또는 가변 길이 유형에 대 한 드라이버 관련 식별자입니다.  
  
 일부 열에서 데이터를 검색할 응용 프로그램 호출 **SQLGetData** 여러 번의 연속 해 서 동일한 열에 대 한 합니다. 호출할 때마다 **SQLGetData** 데이터의 다음 부분을 반환 합니다. 것은 문자 데이터의 중간 부분에서 null 종료 문자를 제거 하도록 파트를 어셈블해야 하기 때문에 응용 프로그램입니다. 종결 문자에 대 한 충분 한 버퍼를 할당할 지 여부를 반환 하려면 더 많은 데이터가 있으면 **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (데이터 잘림)를 반환 합니다. 데이터의 마지막 부분을 반환할 때 **SQLGetData** 관계 없이 SQL_SUCCESS를 반환 합니다. SQL_NO_TOTAL 아니고 0 있으므로 응용 프로그램은 다음 응용 프로그램 버퍼에 데이터의 양을 유효 알 수 없습니다 열에서 데이터를 검색할 유효한 마지막 호출에서 반환할 수 있습니다. 하는 경우 **SQLGetData** 라고 그러면 SQL_NO_DATA를 반환할 합니다. 자세한 내용은 다음 섹션에서는 "SQLGetData 사용 하 여 검색 데이터입니다."을 참조 하세요.  
  
 파트의 가변 길이 책갈피를 반환할 수 있습니다 **SQLGetData**합니다. 다른 데이터에 대 한 호출 처럼 **SQLGetData** 반환할 추가 데이터가 반환 될 때 부분에서 가변 길이 책갈피 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (문자열 데이터, 오른쪽이 잘렸습니다)를 반환 합니다. 이 가변 길이 책갈피를 호출 하 여 잘리면 경우 다릅니다 **SQLFetch** 또는 **SQLFetchScroll**, SQLSTATE 22001 (문자열 데이터, 오른쪽이 잘렸습니다) 및 SQL_ERROR를 반환 하는 합니다.  
  
 **SQLGetData** 부분에서 고정 길이 데이터를 반환 하려면 사용할 수 없습니다. 하는 경우 **SQLGetData** 은 고정 길이 데이터를 포함 하는 열에 대 한 행에 한 번 이상 호출 sql_no_data가 반환 될 모든 호출에 대 한 시작 합니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색  
 드라이버 스트리밍된 출력 매개 변수를 지 원하는 경우 응용 프로그램이 호출할 수 있습니다 **SQLGetData** 작은 사용 하 여 큰 매개 변수 값을 검색 하는 횟수를 버퍼링 합니다. 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 참조 하세요. [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="retrieving-data-with-sqlgetdata"></a>SQLGetData 사용 하 여 데이터를 검색합니다.  
 지정된 된 열에 대 한 데이터를 반환할 **SQLGetData** 다음 일련의 단계를 수행 합니다.  
  
1.  에 이미 반환 되 면 모든 열에 대 한 데이터에서 SQL_NO_DATA를 반환 합니다.  
  
2.  집합 \* *StrLen_or_IndPtr* 를 sql_null_data로 데이터가 NULL 인 경우. 데이터가 NULL 인 경우와 *StrLen_or_IndPtr* 가 null 포인터 **SQLGetData** SQLSTATE 22002 (지표 변수가 필요 하지만 제공 되지)를 반환 합니다.  
  
     열에 대 한 데이터를 NULL이 아닌 경우 **SQLGetData** 3 단계로 진행 됩니다.  
  
3.  SQL_ATTR_MAX_LENGTH 문 특성 문자 또는 이진 데이터 열이 있으면 0이 아닌 값으로 설정 되어 있는 경우 **SQLGetData** 이전에 호출 되지 않은 열에 대 한 SQL_ATTR_MAX_LENGTH로 데이터가 잘립니다 바이트 수입니다.  
  
    > [!NOTE]  
    >  네트워크 트래픽을 줄이기 위해 SQL_ATTR_MAX_LENGTH 문 특성을 것입니다. 일반적으로 네트워크를 통해 반환 하기 전에 데이터를 자릅니다 되는 데이터 원본에 의해 구현 됩니다. 드라이버 및 데이터 원본 지원 하도록 않아도 됩니다. 따라서 특정 크기로 데이터가 잘리고 있는지을 보장 하기 위해 응용 프로그램은 해당 크기의 버퍼를 할당 및 크기를 지정 합니다 *BufferLength* 인수입니다.  
  
4.  지정 된 형식으로 데이터를 변환할 *TargetType*합니다. 데이터는 해당 데이터 형식에 대 한 기본 전체 자릿수 및 규모 지정 됩니다. 하는 경우 *TargetType* SQL_ARD_TYPE, 데이터는 사용 되는 카드가의 SQL_DESC_CONCISE_TYPE 필드의 형식입니다. 하는 경우 *TargetType* SQL_ARD_TYPE, 데이터는에 지정 된 전체 자릿수 및 소수 자릿수가 SQL_DESC_PRECISION, SQL_DESC_DATETIME_INTERVAL_PRECISION, 및 데이터에 따라는 카드가의 자릿수가 SQL_DESC_SCALE 필드는 SQL_DESC_CONCISE 입력 형식 (_t) 필드입니다. 모든 기본 전체 자릿수 또는 소수 적합 하지 않은 경우 응용 프로그램이 명시적으로 설정 해야 적절 한 설명자 필드를 호출한 **SQLSetDescField** 하거나 **SQLSetDescRec**합니다.  
  
5.  데이터는 문자 또는 이진 같은 가변 길이 데이터 형식으로 변환 된 경우 **SQLGetData** 데이터의 길이 초과 하는지 여부를 확인 합니다. *BufferLength*합니다. (Null 종결 문자 포함)는 문자 데이터의 길이 초과 하는 경우 *BufferLength*하십시오 **SQLGetData** 데이터를 자릅니다 *BufferLength* 길이 덜 null 종료 문자입니다. 그런 다음 null-종료 될 데이터입니다. 이진 데이터의 길이 데이터 버퍼의 길이 초과 하는 경우 **SQLGetData** 되도록 자릅니다 *BufferLength* 바이트입니다.  
  
     제공 된 데이터 버퍼가 너무 작아서 null 종료 문자를 저장할 수 있으면 **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 반환 합니다.  
  
     **SQLGetData** 자릅니다 되지 데이터 형식이 고정 길이 데이터를 변환, 항상 있다고 가정 길이 **TargetValuePtr* 데이터 형식의 크기입니다.  
  
6.  변환 (및 가능한 경우) 데이터 배치 \* *TargetValuePtr*합니다. 사실은 **SQLGetData** 아웃오브 라인 데이터를 반환할 수 없습니다.  
  
7.  배치에 있는 데이터의 길이 \* *StrLen_or_IndPtr*합니다. 하는 경우 *StrLen_or_IndPtr* 가 null 포인터 **SQLGetData** 길이 반환 하지 않습니다.  
  
    -   문자 또는 이진 데이터에 대 한이 값은 길이 데이터의 변환 후로 인해 자르기 전에 *BufferLength*합니다. 드라이버는 경우에 따라 긴 데이터의 경우 변환 후 데이터의 길이 확인할 수 없으면, SQL_SUCCESS_WITH_INFO를 반환 하 고 길이 SQL_NO_TOTAL를 설정 합니다. (마지막 호출 **SQLGetData** 항상 0 또는 SQL_NO_TOTAL 아니라 데이터의 길이 반환 해야 합니다.) 데이터가 SQL_ATTR_MAX_LENGTH 문 특성으로 인해 잘렸습니다,--실제 길이 달리이 특성의 값에 배치 됩니다 \* *StrLen_or_IndPtr*합니다. 드라이버가 어떤 실제 길이 알아내는 방법이 아니므로 변환 하기 전에 서버에서 데이터를 자를이 특성은 때문입니다. 때 **SQLGetData** 현재 호출의 시작 부분에 사용할 수 있는 데이터의 길이 동일한 열에 대 한 연속 해 서에서 여러 번 호출 이며, 길이 줄입니다 각 후속 호출을 사용 하 여 합니다.  
  
    -   다른 모든 데이터 형식에 대 한이 값은 길이 데이터의 변환 후 즉, 해당 데이터를 변환 하는 형식의 크기입니다.  
  
8.  변환 하는 동안 데이터가 significance의 손실 없이 잘립니다 경우 (예를 들어 실수 1.234 잘립니다 정수 1로 변환 하는 경우) 되거나 *BufferLength* 너무 작습니다 (예를 들어 문자열 "abcdef"를 배치 4 바이트 버퍼의 경우)에서 **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (데이터 잘림)를 반환 합니다. 데이터 SQL_ATTR_MAX_LENGTH 문 특성으로 인해 significance의 손실 없이 잘리면 **SQLGetData** 관계 없이 SQL_SUCCESS를 반환 하 고 SQLSTATE 01004 (데이터 잘림)를 반환 하지 않습니다.  
  
 바인딩된 데이터 버퍼의 내용을 (경우 **SQLGetData** 바인딩된 열에 라고) 및 경우에 길이/표시기 버퍼 정의 되지 않습니다 **SQLGetData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않습니다.  
  
 에 대 한 연속 호출 **SQLGetData** 요청한 마지막 열에서 데이터를 검색 하는, 이전 오프셋 유효 하지 않게 됩니다. 예를 들어, 다음 순서 대로 수행 될 때:  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 두 번째 호출은 SQLGetData(icol=n) n 열의 시작 부분에서 데이터를 검색합니다. 에 대 한 이전 호출으로 인해 데이터의 임의 오프셋 **SQLGetData** 입니다 열은 더 이상 유효 합니다.  
  
## <a name="descriptors-and-sqlgetdata"></a>설명자 및 SQLGetData  
 **SQLGetData** 설명자 필드와 직접 상호 작용 하지 않습니다.  
  
 하는 경우 *TargetType* SQL_ARD_TYPE, 데이터는 사용 되는 카드가의 SQL_DESC_CONCISE_TYPE 필드의 형식입니다. 하는 경우 *TargetType* SQL_ARD_TYPE 또는 SQL_C_DEFAULT, 데이터는에 지정 된 전체 자릿수 및 소수 자릿수가 SQL_DESC_PRECISION, SQL_DESC_DATETIME_INTERVAL_PRECISION, 및 데이터에 따라는 카드가의 자릿수가 SQL_DESC_SCALE 필드 입력 SQL_DESC_CONCISE_TYPE 필드입니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램 실행을 **선택** Id, 이름, 고객의 결과 집합을 반환 하 고 전화 번호를 이름, ID 및 전화 번호를 정렬할 문을 합니다. 호출 데이터의 각 행에 대해 **SQLFetch** 다음 행으로 커서를 놓습니다. 호출한 **SQLGetData** 검색할 인출된 된 데이터, 데이터 및 반환 된 바이트 수에 대 한 버퍼에에서 지정 된 호출 **SQLGetData**합니다. 마지막으로, 각 직원의 이름, ID 및 전화 번호 인쇄 합니다.  
  
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
  
|내용|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 대 한 저장소 할당|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|블록 커서 위치에는 대량 작업 수행|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리를 취소합니다.|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문을 실행합니다.|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록을 인출 또는 결과 통해 스크롤 설정|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|데이터의 단일 행 이나 앞 으로만 이동 가능한 방향에서 데이터 블록을 가져오는 중|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|실행 시 매개 변수 데이터 전송|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|커서를 놓고, 행 집합에서 데이터 새로 고침, 업데이트 또는 행 집합의 데이터 삭제|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
