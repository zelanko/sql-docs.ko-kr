---
title: "SQLGetData 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLGetData
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLGetData
helpviewer_keywords: SQLGetData function [ODBC]
ms.assetid: e3c1356a-5db7-4186-85fd-8b74633317e8
caps.latest.revision: "46"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 0a23ddb9ee932b67bddd35edfcc9d64228b36f18
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqlgetdata-function"></a>SQLGetData 함수(SQLGetData Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetData** 후 단일 매개 변수 또는 결과 집합의 단일 열에 대 한 데이터를 검색 **SQLParamData** SQL_PARAM_DATA_AVAILABLE를 반환 합니다. 여러 번 부분에 가변 길이 데이터를 검색 하려면 호출할 수 있습니다 것입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 [입력] 열 데이터를 검색 하는 것에 대 한 데이터를 반환할 대상이 되는 열의 개수 이기 합니다. 결과 집합 열은 1부터 시작 하는 증가 열 순서 번호가 매겨집니다. 책갈피 열은 열 번호는 0; 이 수 책갈피를 사용할 경우에 지정 합니다.  
  
 매개 변수 데이터를 검색 하는 1부터 시작 하는 매개 변수의 서 수입니다.  
  
 *TargetType*  
 [입력] 유형 식별자의 C 데이터 형식에는 **TargetValuePtr* 버퍼입니다. 유효한 C 데이터 형식 및 유형 식별자의 목록에 대 한 참조는 [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식에는 섹션입니다.  
  
 경우 *TargetType* SQL_ARD_TYPE, 형식 식별자는 카드가의 SQL_DESC_CONCISE_TYPE 필드에 지정 된 드라이버 사용 됩니다. 경우 *TargetType* SQL_APD_TYPE은 **SQLGetData** 에서에 지정 된 동일한 C 데이터 형식을 사용 **SQLBindParameter**합니다. C 데이터 형식을 지정 하는 그렇지 않은 경우 **SQLGetData** C 데이터 형식에 지정 된 재정의 **SQLBindParameter**합니다. SQL_C_DEFAULT 이면 드라이버 원본의 SQL 데이터 형식에 따라 기본 C 데이터 형식을 선택 합니다.  
  
 또한 확장된 C 데이터 형식을 지정할 수 있습니다. 자세한 내용은 참조 [odbc에서 C 데이터 형식을](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)합니다.  
  
 *TargetValuePtr*  
 [출력] 반환할 데이터 버퍼에 대 한 포인터입니다.  
  
 *TargetValuePtr* NULL 일 수 없습니다.  
  
 *BufferLength*  
 [입력] 길이 **TargetValuePtr* 버퍼의 바이트입니다.  
  
 드라이버를 사용 하 여 *BufferLength* 의 끝을 지난 않도록 하기 위하여는 \* *TargetValuePtr* 문자 또는 이진 데이터와 같은 가변 길이 데이터를 반환할 때 버퍼입니다. 문자 데이터를 반환 하는 경우 드라이버는 null 종료 문자 할 계산 \* *TargetValuePtr*합니다. **TargetValuePtr* 따라서 null 종료 문자에 대 한 공간을 포함 해야 합니다 또는 드라이버는 데이터를 자릅니다.  
  
 드라이버는 정수 또는 날짜 구조와 같은 고정 길이 데이터를 반환 하는 경우 드라이버에서 무시 *BufferLength* 데이터를 저장할 수 있을 만큼 큰 버퍼를 가정 합니다. 고정 길이 데이터에 대해 너무 큰 버퍼를 할당할 응용 프로그램에 대 한 중요 한 되므로 또는 드라이버는 버퍼의 끝을 지나서 작성 합니다.  
  
 **SQLGetData** SQLSTATE HY090 반환 (잘못 된 문자열 또는 버퍼 길이) 때 *BufferLength* 0 보다 작지 않음은 때가 아니라 *BufferLength* 은 0입니다.  
  
 *StrLen_or_IndPtr*  
 [출력] 길이 또는 표시기 값을 반환 하는 버퍼에 대 한 포인터입니다. Null 포인터 이면 길이 또는 표시기 값이 반환 됩니다. 이 인출 되 고 데이터가 NULL 경우 오류가 반환 됩니다.  
  
 **SQLGetData** 길이/표시기 버퍼의 다음 값을 반환할 수 있습니다.  
  
-   반환할 수 있는 데이터의 길이  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 자세한 내용은 참조 [길이/표시기 값을 사용 하 여](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) 이 항목의 "설명"입니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLGetData** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 여는 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLGetData** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|지정된 된 열에 대 한 데이터의 일부만 *Col_or_Param_Num*, 단일 함수 호출에서 검색할 수 없습니다. SQL_NO_TOTAL 또는 현재 호출 하기 전에 지정된 된 열에서 남아 있는 데이터의 길이로 **SQLGetData** 에 반환 \* *StrLen_or_IndPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)<br /><br /> 에 대 한 여러 호출을 사용 하 여 대 한 자세한 내용은 **SQLGetData** 단일 열, "설명"을 참조 하십시오.|  
|01S07|일부가 잘렸습니다.|하나 이상의 열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식에 대 한 수의 소수 부분이 잘렸습니다. 시간, 타임 스탬프 및 interval 데이터 형식을 시간 구성 요소가 포함 된 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07006|제한 된 데이터 형식 특성 위반|결과 집합에 있는 열의 데이터 값을 인수로 지정 된 C 데이터 형식을 변환할 수 없습니다 *TargetType*합니다.|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 대해 지정 된 값 *Col_or_Param_Num* 0, 였으며 SQL_ATTR_USE_BOOKMARKS 문 특성 SQL_UB_OFF로 설정 되었습니다.<br /><br /> 인수에 대해 지정 된 값 *Col_or_Param_Num* 결과 집합의 열 개수 보다 큽니다.<br /><br /> *Col_or_Param_Num* 값을 사용할 수 있는 매개 변수의 서 수와 같지 없습니다.<br /><br /> (DM) 지정된 된 열에 바인딩 되었습니다. 이 설명은에서 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_BOUND 비트 마스크를 반환 하는 드라이버에 적용 되지 않습니다 **SQLGetInfo**합니다.<br /><br /> (DM) 지정된 된 열의 수가 가장 높은 바인딩된 열 개수 보다 작거나 합니다. 이 설명은에서 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_ANY_COLUMN 비트 마스크를 반환 하는 드라이버에 적용 되지 않습니다 **SQLGetInfo**합니다.<br /><br /> (DM) 응용 프로그램이 이미 호출 **SQLGetData** 는 현재 행에 대 한 현재 호출에 지정 된 열의 수가 이전 호출;에 지정 된 열의 개수 보다 작으면 였으며 드라이버는 SQL_ 반환 하지 않습니다 SQL_GETDATA_EXTENSIONS 옵션에 대 한 비트 마스크 GD_ANY_ORDER **SQLGetInfo**합니다.<br /><br /> DM ()는 *TargetType* SQL_ARD_TYPE, 되었습니다 및 *Col_or_Param_Num* 설명자 레코드는 카드가에 일관성 검사에 실패 합니다.<br /><br /> DM ()는 *TargetType* 인수 SQL_ARD_TYPE, 이며는 카드가의 SQL_DESC_COUNT 필드의 값 보다 작은 *Col_or_Param_Num* 인수입니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|22002|지표 변수가 필요 하지만 제공 되지 않았습니다.|*StrLen_or_IndPtr* 는 null 포인터 및 NULL 데이터를 검색 합니다.|  
|22003|숫자 값 범위를 벗어났습니다.|열에 대 한 숫자 값 (숫자 또는 문자열)으로 반환 것 발생할 (소수) 대비 전체 부분의 잘릴 수 있습니다.<br /><br /> 자세한 내용은 참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.|  
|22007|잘못 된 날짜/시간 형식|C 날짜, 시간 또는 타임 스탬프 구조에는 문자는 결과 집합 열에에서 바인딩된 되었으며 값 열에는 잘못 된 날짜, 시간 또는 타임 스탬프, 각각. 자세한 내용은 참조 [부록 d: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)합니다.|  
|22012|0으로 나누기|0으로 나누기에서 발생 하는 산술 식의 값이 반환 되었습니다.|  
|22015|간격 필드 오버플로|정확한 수치 또는 간격 SQL 형식에서 C 간격 유형으로 할당 선행 필드에 유효 자릿수 손실이 발생 합니다.<br /><br /> C 간격 유형으로 데이터를 반환할 때 C 간격 유형에서 SQL 형식의 값으로 표시 되지 했습니다.|  
|22018|캐스트 사양의 문자 값|C 문자 버퍼에 반환 된 결과 집합의 문자 열 및 열 버퍼의 문자 집합에 없는 표현 된 문자를 포함 합니다.<br /><br /> 정확한 수 또는 대략적인 숫자, datetime, 또는 간격 데이터 형식;가 C 유형은 열의 SQL 형식을 문자 데이터 형식. 및 열에 값이 바인딩된 C 형식의 올바른 리터럴.|  
|24000|잘못된 커서 상태|(DM) 함수가 먼저 호출 하지 않고 호출 된 **SQLFetch** 또는 **SQLFetchScroll** 필요한 데이터의 행에 커서를 놓습니다.<br /><br /> DM ()는 *StatementHandle* 된 실행된 상태에 있지만 결과 집합이 연관 된는 *StatementHandle*합니다.<br /><br /> 에 커서가 열린는 *StatementHandle* 및 **SQLFetch** 또는 **SQLFetchScroll** 마치 호출 된 후 또는 결과 집합의 시작 되기 전에 커서가 있었기 하지만 결과 집합의 끝입니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에 *MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|프로그램 유형 범위를 벗어났습니다.|(DM) 인수 *TargetType* 되지 않았거나 올바른 데이터 형식, SQL_C_DEFAULT, 열 데이터 검색), (경우 SQL_ARD_TYPE SQL_APD_TYPE (발생할 경우 매개 변수 데이터 검색).<br /><br /> (DM) 인수 *Col_or_Param_Num* 0이 고 인수를 *TargetType* 하지 못한 SQL_C_BOOKMARK 고정 길이의 책갈피나 SQL_C_VARBOOKMARK 가변 길이 책갈피에 대 한 합니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*, 함수가 호출 후 및 다시는 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램 및 함수에서 다시 호출 된는 *StatementHandle*합니다.|  
|HY009|Null 포인터를 잘못 사용 했습니다.|(DM) 인수 *TargetValuePtr* 는 null 포인터입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM) 지정 된 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 호출 하지 않고 호출 된 **SQLExecDirect**, **SQLExecute** 또는 카탈로그 함수입니다.<br /><br /> DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLGetData** 함수를 호출 했습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> DM ()는 *StatementHandle* 된 실행된 상태에 있지만 결과 집합이 연관 된는 *StatementHandle*합니다.<br /><br /> 에 대 한 호출 **SQLExeceute**, **SQLExecDirect**, 또는 **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE를 반환 하지만 **SQLGetData** 호출한 를 대신 **SQLParamData**합니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대해 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.<br /><br /> 인수에 지정 된 값 *BufferLength* 보다 작거나 4는 *Col_or_Param_Num* 인수는 0으로 설정 된 되었으며 드라이버는 ODBC 2*.x* 드라이버입니다.|  
|HY109|잘못 된 커서 위치|커서가 있었기 (여 **SQLSetPos**, **SQLFetch**, **SQLFetchScroll**, 또는 **SQLBulkOperations**)에 삭제 된 행에 대해 또는 가져올 수 없습니다.<br /><br /> 커서는 정방향 전용 커서 였으며 행 집합 크기가 1 보다 큽니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYC00|선택적 기능이 구현 되지 않았습니다|드라이버 또는 데이터 원본 사용을 지원 하지 않습니다 **SQLGetData** 에 여러 행이 있는 **SQLFetchScroll**합니다. 이 설명은에서 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_BLOCK 비트 마스크를 반환 하는 드라이버에 적용 되지 않습니다 **SQLGetInfo**합니다.<br /><br /> 드라이버 또는 데이터 원본 변환의 조합으로 지정 하는 지원 하지 않습니다는 *TargetType* 인수 및 해당 열의 SQL 데이터 형식입니다. 이 오류는 SQL 데이터 형식 열의 드라이버별 SQL 데이터 형식에 매핑된 경우에 적용 됩니다.<br /><br /> 드라이버는 ODBC 2만 지원*.x*, 인수 및 *TargetType* 다음 중 하나 였습니다.<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 에 나열 된 모든 C interval 데이터 형식 및 [C 데이터 형식을](../../../odbc/reference/appendixes/c-data-types.md) 부록 d: 데이터 형식에서입니다.<br /><br /> 드라이버 지원 3.50, 및 인수는 이전 ODBC 버전 *TargetType* SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)에 해당 하는 드라이버는 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetData** 지정된 된 열에 데이터를 반환 합니다. **SQLGetData** 하나 이상의 행으로 결과 집합에서 인출 된 후에 호출할 수 있습니다 **SQLFetch**, **SQLFetchScroll**, 또는 **SQLExtendedFetch** . 가변 길이 데이터를 한 번 호출에서 반환 될 너무 크면 **SQLGetData** (제한으로 인해 응용 프로그램에), **SQLGetData** 부분에서 검색할 수 있습니다. 행과 호출의 일부 열에 바인딩할 수 **SQLGetData** 다른 사용자에 대 한 몇 가지 제한 사항이 적용 되는 아니지만 합니다. 자세한 내용은 참조 [긴 데이터를 가져오는](../../../odbc/reference/develop-app/getting-long-data.md)합니다.  
  
 사용에 대 한 내용은 **SQLGetData** 스트리밍된 출력 매개 변수를 가진 참조 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="using-sqlgetdata"></a>SQLGetData를 사용 하 여  
 드라이버에 대 한 확장을 지원 하지 않는 경우 **SQLGetData**, 함수는 마지막 바인딩된 열 보다 큰 숫자로 바인딩되지 않은 열에 대해서만 데이터를 반환할 수 있습니다. 또한 데이터의 값의 행 내의 *Col_or_Param_Num* 인수를 호출할 때마다 **SQLGetData** 보다 크거나 같은 값 이어야 합니다 *Col_or_Param_Num*; 이전 호출에서 즉, 열 번호 오름차순으로 데이터를 검색 해야 합니다. 마지막으로 확장 없음 지원 되 면, **SQLGetData** 행 집합 크기가 1 보다 큰 경우에 호출할 수 없습니다.  
  
 드라이버는 이러한 모든 제한 완화할 수 있습니다. 응용 프로그램이 호출 드라이버를 완화 하는 제한 사항를 확인 하려면 **SQLGetInfo** 와 다음 SQL_GETDATA_EXTENSIONS 옵션 중 하나:  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** 출력 매개 변수 값을 반환 하기 위해 호출 될 수 있습니다. 자세한 내용은 참조 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
-   SQL_GD_ANY_COLUMN 합니다. 이 옵션은 반환 되 면 **SQLGetData** 바인딩된 마지막 열 전에 포함 하 여 모든 바인딩되지 않은 열에 대해 호출할 수 있습니다.  
  
-   SQL_GD_ANY_ORDER 합니다. 이 옵션은 반환 되 면 **SQLGetData** 에 바인딩되지 않은 열 순서에 관계 없이 호출할 수 있습니다.  
  
-   SQL_GD_BLOCK 합니다. 이 옵션에서 반환 되 면 **SQLGetInfo** SQL_GETDATA_EXTENSIONS 정보 항목에 대 한 드라이버 지원에 대 한 호출 **SQLGetData** 행 집합 크기가 1 보다 크면 응용 프로그램 를호출할수시점과**SQLSetPos** 호출 하기 전에 올바른 행에 커서를 배치 하는 SQL_POSITION 옵션과 함께 **SQLGetData 합니다.**  
  
-   SQL_GD_BOUND 합니다. 이 옵션은 반환 되 면 **SQLGetData** 바인딩되지 않은 열 뿐만 아니라 바인딩된 열에 대해 호출할 수 있습니다.  
  
 이러한 제한 사항 및 이러한 완화 하는 드라이버의 기능을 두 가지 예외가 있습니다. 첫째, **SQLGetData** 호출 되 면 안 정방향 전용 커서에 대 한 행 집합 크기가 1 보다 큰 경우. 둘째, 드라이버 책갈피를 지 원하는 경우 지원 해야 합니다 항상 호출 하는 기능 **SQLGetData** 0, 응용 프로그램 호출을 허용 하지 않는 경우에 열에 대 한 **SQLGetData** 마지막 하기 전에 다른 열에 대 한 바인딩된 열입니다. (ODBC 2를 응용 프로그램은 사용 하는 경우*.x* 드라이버 **SQLGetData** 책갈피를 사용 하 여 호출을 반환 하는 *Col_or_Param_Num* 을 호출한 후에 0 **SQLFetch**때문에, **SQLFetch** ODBC 3 매핑할*.x* 드라이버 관리자를 **SQLExtendedFetch** 는 와 *FetchOrientation* 는 SQL_FETCH_NEXT, 및 **SQLGetData** 와 *Col_or_Param_Num* ODBC 3 0 매핑할*.x* 드라이버 관리자를 **SQLGetStmtOption** 와 *fOption* SQL_GET_BOOKMARK입니다.)  
  
 **SQLGetData** 호출 하 여 방금 삽입 한 행에 대 한 책갈피를 검색 하는 데 사용할 수 없습니다 **SQLBulkOperations** SQL_ADD 옵션을 사용 하므로 커서는 행에 위치 하지 않습니다. 응용 프로그램 호출 하기 전에 바인딩 열 0 하 여 이러한 행에 대 한 책갈피를 검색할 수 **SQLBulkOperations** 경우에서 SQL_ADD와 **SQLBulkOperations** 바인딩된 버퍼에 책갈피를 반환 합니다. **SQLFetchScroll** 해당 행에서 커서 위치를 변경 하려면 SQL_FETCH_BOOKMARK로 호출할 수 있습니다.  
  
 경우는 *TargetType* 인수가의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정 된 대로 기본 간격 선행 자릿수 (2)와 기본 간격 초 자릿수 (6), 간격 데이터 형식 각각의 카드가 데이터에 사용 됩니다. 경우는 *TargetType* 인수는 SQL_C_NUMERIC 데이터 형식, 기본 전체 자릿수 (드라이버 정의 됨) 및 기본 크기 (0)는 카드가의 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정 된 대로, 데이터에 사용 됩니다. 모든 기본 전체 자릿수 또는 소수 자릿수를 적절 한 없으면 응용 프로그램이 명시적으로 설정 해야 적절 한 설명자 필드를 호출 하 여 **SQLSetDescField** 또는 **SQLSetDescRec**합니다. SQL_DESC_CONCISE_TYPE 필드 SQL_C_NUMERIC 및 호출을 설정할 수 있습니다 **SQLGetData** 와 *TargetType* 로 인해 전체 자릿수 및 소수 자릿수 값의 설명자 필드는 SQL_ARD_TYPE의 인수 사용할 수 있습니다.  
  
> [!NOTE]  
>  ODBC 2에서*.x*, 응용 프로그램 집합 *TargetType* SQL_C_DATE, SQL_C_TIME, 또는 SQL_C_TIMESTAMP 임을 나타내는 \* *TargetValuePtr* 날짜, 시간, 또는 타임 스탬프 구조입니다. ODBC 3에서*.x*, 응용 프로그램 집합 *TargetType* SQL_C_TYPE_DATE, SQL_C_TYPE_TIME, 또는 SQL_C_TYPE_TIMESTAMP 합니다. 드라이버 관리자를 통해 적절 한 매핑을 필요한을 기반으로 하는 경우 응용 프로그램 및 드라이버 버전에 있습니다.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>가변 길이 데이터 부분에서 검색  
 **SQLGetData** 부분에 가변 길이 데이터를 포함 하는 열에서 데이터를 검색 하는 데 사용 될-때 SQL 데이터 형식의 열 식별자 즉, SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_ WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY, 또는 가변 길이 유형에 대 한 드라이버 관련 식별자입니다.  
  
 파트의 열에서 데이터를 검색 하려면 응용 프로그램 호출 **SQLGetData** 동일한 열에 대 한 연속 해 서 여러 번입니다. 각 호출에서 **SQLGetData** 데이터의 다음 부분이 반환 합니다. 것은 문자 데이터의 중간 부분에서 null 종료 문자를 제거 하도록 부품이를 다시 응용 프로그램입니다. 더 많은 데이터가 종결 문자에 대 한 충분 한 버퍼를 할당할 지 여부를 반환 하는 경우 **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (데이터 잘림)를 반환 합니다. 데이터의 마지막 부분을 반환 하는 경우 **SQLGetData** 관계 없이 SQL_SUCCESS를 반환 합니다. 0이 아니고 SQL_NO_TOTAL 때문에 응용 프로그램은 다음 응용 프로그램 버퍼에 있는 데이터의 양을 올바른지 알 수 없습니다 데이터를 검색 하는 열에서 유효한 마지막 호출에서 반환할 수 있습니다. 경우 **SQLGetData** 라고 이후 부터는 SQL_NO_DATA를 반환 합니다. 자세한 내용은 다음 섹션인 "데이터를 가져오는 SQLGetData 사용 합니다."를 참조 하십시오.  
  
 가변 길이 책갈피 부품으로 반환 될 수 있습니다 **SQLGetData**합니다. 에 대 한 호출, 다른 데이터와 마찬가지로 **SQLGetData** 반환할 더 많은 데이터가 반환 될 때 부분에 가변 길이 책갈피 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (문자열 데이터, 오른쪽이 잘렸습니다)를 반환 합니다. 이것이 다른 경우 보다 다양 한 길이의 책갈피를 호출 하 여 잘리면 **SQLFetch** 또는 **SQLFetchScroll**, SQLSTATE 22001 (문자열 데이터, 오른쪽이 잘렸습니다) 및 SQL_ERROR를 반환 하는 합니다.  
  
 **SQLGetData** 고정 길이 데이터 부분의 반환을 사용할 수 없습니다. 경우 **SQLGetData** 은 고정 길이 데이터를 포함 하는 열에 대 한 행에 한 번 이상 호출 sql_no_data가 반환 될 모든 호출에 대 한 첫 번째 후 합니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색  
 응용 프로그램을 호출할 수는 드라이버 스트리밍된 출력 매개 변수를 지 원하는 경우 **SQLGetData** 소문자로 큰 매개 변수 값을 검색 하려면 여러 번을 버퍼링 합니다. 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 참조 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)합니다.  
  
## <a name="retrieving-data-with-sqlgetdata"></a>SQLGetData로 데이터 검색  
 지정된 된 열에 대 한 데이터를 반환할 **SQLGetData** 다음과 같은 일련의 단계를 수행 합니다.  
  
1.  가 이미 반환 되 면 모든 열에 대 한 데이터 SQL_NO_DATA를 반환 합니다.  
  
2.  집합 \* *StrLen_or_IndPtr* 을 sql_null_data로 데이터가 NULL입니다. 데이터가 NULL이 있으면 및 *StrLen_or_IndPtr* 는 null 포인터 **SQLGetData** SQLSTATE 22002 (지표 변수가 필요 하지만 제공 되지 않은)을 반환 합니다.  
  
     열에 대 한 데이터 매개 변수가 NULL 이면 **SQLGetData** 3 단계로 진행 됩니다.  
  
3.  SQL_ATTR_MAX_LENGTH 문 특성은 문자 또는 이진 데이터 열에 있는 경우 0이 아닌 값으로 설정 되 고 경우 **SQLGetData** 이전에 호출 되지 않은 열에 대 한 SQL_ATTR_MAX_LENGTH로 데이터가 잘립니다 바이트 수입니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH 문 특성은 네트워크 트래픽이 감소 하는 데 사용 됩니다. 일반적으로 네트워크를 통해 반환 하기 전에 데이터를 자릅니다 하는 데이터 원본에 의해 구현 됩니다. 드라이버 및 데이터 원본 지원 하기 위한 필요 하지 않습니다. 따라서 특정 크기로 데이터가 잘리고 있는지를 보장 하려면 응용 프로그램 해야 해당 크기의 버퍼를 할당 하 고 크기를 지정 된 *BufferLength* 인수입니다.  
  
4.  데이터에 지정 된 형식으로 변환 *TargetType*합니다. 데이터는 해당 데이터 형식에 대 한 기본 전체 자릿수 및 소수 자릿수 제공 됩니다. 경우 *TargetType* SQL_ARD_TYPE, 데이터는 사용 되 고 카드가의 SQL_DESC_CONCISE_TYPE 필드의 형식입니다. 경우 *TargetType* SQL_ARD_TYPE 되며 데이터는에 지정 된 전체 자릿수와 소수 자릿수가 SQL_DESC_PRECISION, SQL_DESC_DATETIME_INTERVAL_PRECISION는 SQL_DESC_CONCISE에 입력 데이터에 따라 카드가의 자릿수가 SQL_DESC_SCALE 필드 입력 (_t) 필드입니다. 모든 기본 전체 자릿수 또는 소수 자릿수를 적절 한 없으면 응용 프로그램이 명시적으로 설정 해야 적절 한 설명자 필드를 호출 하 여 **SQLSetDescField** 또는 **SQLSetDescRec**합니다.  
  
5.  데이터를 문자 또는 이진, 같은 가변 길이 데이터 형식으로 변환 된 경우 **SQLGetData** 데이터의 길이 초과 하는지 확인 *BufferLength*합니다. (Null 종결 문자 포함)는 문자 데이터의 길이 초과 하는 경우 *BufferLength*, **SQLGetData** 데이터를 자릅니다 *BufferLength* 길이 덜 null 종료 문자입니다. 그 다음 null-데이터를 종료 합니다. 이진 데이터의 길이 데이터 버퍼의 길이 초과 하는 경우 **SQLGetData** 로 자릅니다 *BufferLength* 바이트입니다.  
  
     제공 된 데이터 버퍼가 너무 작아서 null 종료 문자를 저장할 경우 **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 반환 합니다.  
  
     **SQLGetData** 되지 자릅니다 데이터를 변환할 고정 길이 데이터 형식; 항상 있다고 가정 길이의 **TargetValuePtr* 데이터 형식의 크기입니다.  
  
6.  에 변환 된 (및 가능한 잘린) 데이터 \* *TargetValuePtr*합니다. **SQLGetData** 아웃오브 라인 데이터를 반환할 수 없습니다.  
  
7.  에 있는 데이터의 길이 배치 \* *StrLen_or_IndPtr*합니다. 경우 *StrLen_or_IndPtr* 는 null 포인터 **SQLGetData** 길이 반환 하지 않습니다.  
  
    -   문자 또는 이진 데이터에 대 한이 데이터의 길이로 인해 잘림 전과 변환 후 *BufferLength*합니다. 드라이버 때 긴 데이터의 경우 변환 후 데이터의 길이 확인할 수 없으면, SQL_SUCCESS_WITH_INFO를 반환 하 고 길이 SQL_NO_TOTAL 설정 합니다. (마지막으로 호출한 **SQLGetData** 항상 0 또는 SQL_NO_TOTAL 아닌지 데이터의 길이 반환 해야 합니다.) SQL_ATTR_MAX_LENGTH 문으로 인해 데이터가 잘렸습니다 경우 특성을이 특성의 값-실제 길이 달리-에 위치한 \* *StrLen_or_IndPtr*합니다. 이 특성은 드라이버에, 실제 길이 사항을 알아내는 수 있는 방법이 있으므로 변환 하기 전에 서버에서 데이터를 자르는 데 설계 때문입니다. 때 **SQLGetData** 이 현재 호출의 시작 부분에 사용할 수 있는 데이터의 길이 동일한 열에 대 한 연속으로 여러 번 호출 이며 길이 각 후속 호출에 반비례 하는, 즉 합니다.  
  
    -   다른 모든 데이터 형식 변환; 후 데이터의 길이입니다. 즉, 데이터가 변환 된 형식의 크기를입니다.  
  
8.  변환 하는 동안 데이터가 significance의 손실 없이 잘립니다 경우 (예를 들어 실수 1.234 잘립니다 정수 1로 변환 하는 경우)에 게 없거나 *BufferLength* 너무 작습니다 (예를 들어 문자열 "abcdef"를 배치 4 바이트 버퍼의 경우)에서 **SQLGetData** SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (데이터 잘림)를 반환 합니다. SQL_ATTR_MAX_LENGTH 문 특성으로 인해 significance의 손실 없이 데이터가 잘립니다 경우 **SQLGetData** 관계 없이 SQL_SUCCESS를 반환 하 고 SQLSTATE 01004 (데이터 잘림)를 반환 하지 않습니다.  
  
 바인딩된 데이터 버퍼의 내용이 (경우 **SQLGetData** 바인딩된 열에 호출 됨) 및 경우에 길이/표시기 버퍼 정의 되지 않습니다 **SQLGetData** SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않습니다.  
  
 에 대 한 연속 호출은 **SQLGetData** 이전 오프셋 유효 하지 않게; 요청한 마지막 열에서 데이터를 검색 합니다. 예를 들어 다음 순서 대로 수행 될 때:  
  
```  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 두 번째 호출 SQLGetData(icol=n) n 열의 시작 부분부터 데이터를 검색합니다. 에 대 한 이전 호출으로 인해 데이터에 대 한 오프셋 **SQLGetData** 입니다 열은 더 이상 유효 합니다.  
  
## <a name="descriptors-and-sqlgetdata"></a>설명자 및 SQLGetData  
 **SQLGetData** 모든 설명자 필드와 직접 상호 작용 하지 않습니다.  
  
 경우 *TargetType* SQL_ARD_TYPE, 데이터는 사용 되 고 카드가의 SQL_DESC_CONCISE_TYPE 필드의 형식입니다. 경우 *TargetType* SQL_ARD_TYPE 또는 SQL_C_DEFAULT, 데이터는에 지정 된 전체 자릿수와 소수 자릿수가 SQL_DESC_PRECISION, SQL_DESC_DATETIME_INTERVAL_PRECISION 이며 데이터에 따라 카드가의 자릿수가 SQL_DESC_SCALE 필드 입력 SQL_DESC_CONCISE_TYPE 필드입니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서는 응용 프로그램 실행을 **선택** Id, 이름, 고객의 결과 집합을 반환 하 고 전화 번호를 기준으로 이름, ID 및 전화 번호 정렬 문을 합니다. 데이터의 각 행에 대 한 호출 **SQLFetch** 다음 행으로 커서를 놓습니다. 호출 **SQLGetData** 에 대 한 호출에 인출된 된 데이터, 데이터 및 반환 된 바이트 수에 대 한 버퍼를 검색 지정 **SQLGetData**합니다. 마지막으로, 각 직원의 이름, ID 및 전화 번호를 인쇄 합니다.  
  
```  
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
|결과 집합의 열에 대 한 저장소를 할당합니다.|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|블록 커서 위치와 관련이 없으며 대량 작업 수행|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리를 취소합니다.|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문 실행|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|데이터의 단일 행 이나 앞 으로만 이동 가능한 방향의 데이터 블록을 인출합니다.|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|커서를 놓고, 행 집합에서 데이터 새로 고침 또는 업데이트 또는 행 집합의 데이터 삭제|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
