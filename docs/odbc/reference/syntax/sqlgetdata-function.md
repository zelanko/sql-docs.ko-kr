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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ac11505b8e47dae8df53af27c64a7ee6372b3f28
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81285509"
---
# <a name="sqlgetdata-function"></a>SQLGetData 함수(SQLGetData Function)
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLGetData** 는 결과 집합의 단일 열에 대 한 데이터를 검색 하거나 **sqlparamdata** 가 SQL_PARAM_DATA_AVAILABLE를 반환한 후 단일 매개 변수를 검색 합니다. 여러 번 호출 하 여 파트에서 가변 길이 데이터를 검색할 수 있습니다.  
  
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
 입력 문 핸들입니다.  
  
 *Col_or_Param_Num*  
 입력 열 데이터를 검색 하는 경우 데이터를 반환할 열 번호입니다. 결과 집합 열의 번호는 1부터 시작 하 여 열 순서를 늘립니다. 책갈피 열은 열 번호 0입니다. 책갈피를 사용 하는 경우에만 지정할 수 있습니다.  
  
 매개 변수 데이터를 검색 하는 경우 1에서 시작 하는 매개 변수의 서 수입니다.  
  
 *TargetType*  
 입력 **Targetvalueptr* 버퍼의 C 데이터 형식에 대 한 형식 식별자입니다. 유효한 C 데이터 형식 및 형식 식별자 목록은 부록 D: 데이터 형식의 [c 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) 섹션을 참조 하세요.  
  
 *TargetType* 이 SQL_ARD_TYPE 경우 드라이버는 사용 중인 SQL_DESC_CONCISE_TYPE 필드에 지정 된 형식 식별자를 사용 합니다. *TargetType* 이 SQL_APD_TYPE 되 면 **SQLGetData** 는 **SQLBindParameter**에 지정 된 것과 동일한 C 데이터 형식을 사용 합니다. 그렇지 않으면 **SQLGetData** 에 지정 된 c 데이터 형식이 **SQLBindParameter**에 지정 된 c 데이터 형식을 재정의 합니다. SQL_C_DEFAULT 경우 드라이버는 원본의 SQL 데이터 형식에 따라 기본 C 데이터 형식을 선택 합니다.  
  
 확장 된 C 데이터 형식을 지정할 수도 있습니다. 자세한 내용은 [ODBC의 C 데이터 형식](../../../odbc/reference/develop-app/c-data-types-in-odbc.md)을 참조 하세요.  
  
 *TargetValuePtr*  
 출력 데이터를 반환할 버퍼에 대 한 포인터입니다.  
  
 *Targetvalueptr* 은 NULL 일 수 없습니다.  
  
 *BufferLength*  
 입력 **Targetvalueptr* 버퍼의 길이 (바이트)입니다.  
  
 드라이버는 문자 또는 이진 데이터와 같은 가변 길이 데이터를 반환할 \*때 *targetvalueptr* 버퍼의 끝을 지나서 쓰기를 방지 하기 위해 *bufferlength* 를 사용 합니다. 드라이버는 문자 데이터를 \* *targetvalueptr*으로 반환할 때 null 종료 문자를 계산 합니다. *따라서 *Targetvalueptr* 은 null 종료 문자에 대 한 공간을 포함 해야 합니다. 그렇지 않으면 드라이버에서 데이터를 자릅니다.  
  
 드라이버가 정수 또는 날짜 구조와 같은 고정 길이 데이터를 반환 하는 경우 드라이버는 *Bufferlength* 를 무시 하 고 버퍼가 데이터를 저장할 수 있을 만큼 충분히 큰지 가정 합니다. 따라서 응용 프로그램은 고정 길이 데이터에 충분 한 크기의 버퍼를 할당 하는 것이 중요 합니다. 그렇지 않으면 드라이버가 버퍼의 끝을 넘어 기록 됩니다.  
  
 **SQLGetData** 는 *bufferlength* 가 0 보다 작지만 *bufferlength* 가 0 일 때가 아닌 경우 SQLSTATE HY090 (잘못 된 문자열 또는 버퍼 길이)를 반환 합니다.  
  
 *StrLen_or_IndPtr*  
 출력 길이 또는 표시기 값을 반환할 버퍼에 대 한 포인터입니다. Null 포인터인 경우 길이 또는 표시기 값이 반환 되지 않습니다. 인출 되는 데이터가 NULL 이면 오류가 반환 됩니다.  
  
 **SQLGetData** 는 길이/표시기 버퍼에서 다음 값을 반환할 수 있습니다.  
  
-   반환할 수 있는 데이터의 길이입니다.  
  
-   SQL_NO_TOTAL  
  
-   SQL_NULL_DATA  
  
 자세한 내용은이 항목의 [Length/지표로 Values](../../../odbc/reference/develop-app/using-length-and-indicator-values.md) 및 "Comments" 사용을 참조 하십시오.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_NO_DATA, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLGetData** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 하는 경우 HandleType SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLGetData** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|지정 된 열 *Col_or_Param_Num*에 대 한 모든 데이터는 함수에 대 한 단일 호출에서 검색할 수 없습니다. \* *StrLen_or_IndPtr*에서 **SQLGetData** 를 호출 하기 전에 지정 된 열에 남아 있는 데이터의 길이를 SQL_NO_TOTAL 하거나 반환 합니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.<br /><br /> 단일 열에 대해 **SQLGetData** 를 여러 번 호출 하는 방법에 대 한 자세한 내용은 "설명"을 참조 하십시오.|  
|01S07|소수 잘림|하나 이상의 열에 대해 반환 된 데이터가 잘렸습니다. 숫자 데이터 형식의 경우 숫자의 소수 부분이 잘렸습니다. 시간 구성 요소를 포함 하는 time, timestamp 및 interval 데이터 형식의 경우 시간의 소수 부분이 잘렸습니다.<br /><br /> 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07006|제한 된 데이터 형식 특성 위반|결과 집합에 있는 열의 데이터 값을 인수 *TargetType*에 지정 된 C 데이터 형식으로 변환할 수 없습니다.|  
|07009|잘못 된 설명자 인덱스|인수 *Col_or_Param_Num* 에 지정 된 값이 0이 고 SQL_ATTR_USE_BOOKMARKS statement 특성이 SQL_UB_OFF로 설정 되었습니다.<br /><br /> 인수 *Col_or_Param_Num* 에 지정 된 값이 결과 집합의 열 수보다 큽니다.<br /><br /> *Col_or_Param_Num* 값이 사용 가능한 매개 변수의 서 수와 같지 않은 경우<br /><br /> (DM) 지정한 열이 바인딩 되었습니다. 이 설명은 **SQLGetInfo**의 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_BOUND 비트 마스크를 반환 하는 드라이버에는 적용 되지 않습니다.<br /><br /> (DM) 지정 된 열의 번호가 가장 높은 바인딩 열의 숫자 보다 작거나 같습니다. 이 설명은 **SQLGetInfo**의 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_ANY_COLUMN 비트 마스크를 반환 하는 드라이버에는 적용 되지 않습니다.<br /><br /> (DM) 응용 프로그램이 이미 현재 행에 대 한 **SQLGetData** 를 호출 했습니다. 현재 호출에 지정 된 열 번호가 앞의 호출에 지정 된 열 수보다 작은 경우 그리고 드라이버는 **SQLGetInfo**의 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_ANY_ORDER 비트 마스크를 반환 하지 않습니다.<br /><br /> (DM) *TargetType* 인수가 SQL_ARD_TYPE 되었으며, 그에 대 한 *Col_or_Param_Num* 설명자 레코드가 일관성 확인에 실패 했습니다.<br /><br /> (DM) *TargetType* 인수가 SQL_ARD_TYPE 되었으며, SQL_DESC_COUNT 필드의 값이 *Col_or_Param_Num* 인수 보다 낮습니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|22002|표시기 변수가 필요한 데 제공 되지 않았습니다.|*StrLen_or_IndPtr* null 포인터이 고 null 데이터가 검색 되었습니다.|  
|22003|숫자 값이 범위를 벗어났습니다.|열에 대 한 숫자 값 (숫자 또는 문자열)을 반환 하면 잘릴 수 있는 전체 (소수 자릿수가 아닌) 부분이 발생 합니다.<br /><br /> 자세한 내용은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.|  
|22007|날짜/시간 형식이 잘못 되었습니다.|결과 집합의 문자 열이 C 날짜, 시간 또는 타임 스탬프 구조에 바인딩되고 열의 값은 각각 잘못 된 날짜, 시간 또는 타임 스탬프입니다. 자세한 내용은 [부록 D: 데이터 형식](../../../odbc/reference/appendixes/appendix-d-data-types.md)을 참조 하세요.|  
|22012|0으로 나누었습니다.|0으로 나누는 산술 식의 값이 반환 되었습니다.|  
|22015|간격 필드 오버플로입니다.|정확한 숫자 또는 간격 SQL 형식을 interval C 형식으로 할당 하면 선행 필드에 유효 자릿수가 손실 됩니다.<br /><br /> 데이터를 interval C 유형에 서 반환 하는 경우 간격 C 유형에 서 SQL 유형의 값을 표시 하지 않았습니다.|  
|22018|캐스트 사양에 대 한 문자 값이 잘못 되었습니다.|결과 집합의 문자 열이 문자 C 버퍼로 반환 되었으며 버퍼의 문자 집합에 표시 되지 않은 문자가 열에 포함 되어 있습니다.<br /><br /> C 형식은 정확한 수치 또는 근사치, datetime 또는 interval 데이터 형식입니다. 열의 SQL 형식이 문자 데이터 형식입니다. 열에 있는 값이 바인딩된 C 형식의 올바른 리터럴이 아닙니다.|  
|24000|잘못된 커서 상태|(DM) 먼저 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하 여 필요한 데이터 행에 커서를 배치 하지 않고 함수를 호출 했습니다.<br /><br /> (DM) *StatementHandle* 가 실행 된 상태 이지만 *StatementHandle*과 연결 된 결과 집합이 없습니다.<br /><br /> *StatementHandle* 에서 커서가 열려 있지만 **Sqlfetch** 또는 **sqlfetchscroll** 이 호출 되었지만 결과 집합의 시작 위치 앞 이나 결과 집합의 끝 뒤에 커서가 있습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. *MessageText* 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다.|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY003|프로그램 유형이 범위를 벗어났습니다.|(DM) 인수 *TargetType* 은 올바른 데이터 형식, SQL_C_DEFAULT SQL_ARD_TYPE (열 데이터를 검색 하는 경우) 또는 SQL_APD_TYPE (매개 변수 데이터를 검색 하는 경우)가 아닙니다.<br /><br /> (DM) 인수 *Col_or_Param_Num* 0이 고, 인수 *TargetType* 이 고정 길이 책갈피 또는 가변 길이 책갈피에 대 한 SQL_C_VARBOOKMARK SQL_C_BOOKMARK 되지 않았습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 *StatementHandle*에서 **Sqlcancel** 또는 **Sqlcancelhandle** 이 호출 되 고 *StatementHandle*에서 함수가 다시 호출 되었습니다.<br /><br /> 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 에서 호출 된 다음 *StatementHandle*에 대해 함수가 다시 호출 되었습니다.|  
|HY009|Null 포인터 사용이 잘못 되었습니다.|(DM) 인수 *Targetvalueptr* 은 null 포인터입니다.|  
|HY010|함수 시퀀스 오류|(DM) 지정한 *StatementHandle* 가 실행 된 상태가 아닙니다. 함수가 먼저 **Sqlexecdirect**, **sqlexecute** 또는 catalog 함수를 호출 하지 않고 호출 되었습니다.<br /><br /> (DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLGetData** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 가 실행 된 상태 이지만 *StatementHandle*과 연결 된 결과 집합이 없습니다.<br /><br /> **SQLExeceute**, **Sqlexecdirect**또는 **SQLMoreResults** SQL_PARAM_DATA_AVAILABLE 반환 했지만 **sqlexecdirect**대신 **SQLGetData** 가 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *Bufferlength* 에 지정 된 값이 0 보다 작은 경우<br /><br /> 인수 *Bufferlength* 에 지정 된 값이 4 보다 작고 *Col_or_Param_Num* 인수가 0으로 설정 되었고 드라이버가 ODBC*2.x 드라이버 였습니다.*|  
|HY109|커서 위치가 잘못 되었습니다.|삭제 되었거나 인출할 수 없는 행의 **SQLSetPos**, **sqlfetch**, **sqlfetchscroll**또는 **SQLBulkOperations**에 의해 커서가 배치 되었습니다.<br /><br /> 커서가 앞 으로만 이동 가능한 커서이 고 행 집합 크기가 1 보다 큽니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYC00|선택적 기능이 구현 되지 않음|드라이버 또는 데이터 원본은 **Sqlfetchscroll**에서 여러 행이 포함 된 **SQLGetData** 사용을 지원 하지 않습니다. 이 설명은 **SQLGetInfo**의 SQL_GETDATA_EXTENSIONS 옵션에 대 한 SQL_GD_BLOCK 비트 마스크를 반환 하는 드라이버에는 적용 되지 않습니다.<br /><br /> 드라이버 또는 데이터 원본은 해당 열의 *TargetType* 인수와 SQL 데이터 형식의 조합으로 지정 된 변환을 지원 하지 않습니다. 이 오류는 열의 SQL 데이터 형식이 드라이버별 SQL 데이터 형식에 매핑된 경우에만 적용 됩니다.<br /><br /> 드라이버는 ODBC 2.x만 지원 하 고 인수 *TargetType* 은 다음 중 하나*였습니다.*<br /><br /> SQL_C_NUMERIC SQL_C_SBIGINT SQL_C_UBIGINT<br /><br /> 및 부록 D의 [c 데이터 형식](../../../odbc/reference/appendixes/c-data-types.md) : 데이터 형식에 나열 된 간격 c 데이터 형식입니다.<br /><br /> 드라이버는 3.50 이전 버전의 ODBC 버전만 지원 하 고 인수 *TargetType* 은 SQL_C_GUID 되었습니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 에 해당 하는 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
## <a name="comments"></a>주석  
 **SQLGetData** 는 지정 된 열에 있는 데이터를 반환 합니다. **SQLGetData** 는 **sqlfetch**, **Sqlfetchscroll**또는 **sqlextendedfetch**를 통해 결과 집합에서 하나 이상의 행을 가져온 후에만 호출할 수 있습니다. 응용 프로그램의 제한으로 인해 **sqlgetdata** 에 대 한 단일 호출에서 가변 길이 데이터가 너무 커서 응용 프로그램의 제한에 의해 반환 될 수 없는 경우 **sqlgetdata** 에서 파트를 검색할 수 있습니다. 몇 가지 제한 사항이 적용 되지만 행의 일부 열을 바인딩하고 다른 열에 대해 **SQLGetData** 를 호출할 수 있습니다. 자세한 내용은 [Long 데이터 가져오기](../../../odbc/reference/develop-app/getting-long-data.md)를 참조 하세요.  
  
 스트리밍된 출력 매개 변수와 함께 **sqlgetdata** 를 사용 하는 방법은 [Sqlgetdata를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.  
  
## <a name="using-sqlgetdata"></a>SQLGetData 사용  
 드라이버가 **SQLGetData**에 대 한 확장을 지원 하지 않는 경우 함수는 마지막으로 바인딩된 열의 숫자가 보다 큰 바인딩되지 않은 열에 대해서만 데이터를 반환할 수 있습니다. 또한 데이터 행 내에서 **SQLGetData** 에 대 한 각 호출의 *Col_or_Param_Num* 인수 값은 이전 호출에서 *Col_or_Param_Num* 값 보다 크거나 같아야 합니다. 즉, 데이터는 열 번호 오름차순으로 검색 되어야 합니다. 마지막으로 지원 되는 확장이 없는 경우 행 집합 크기가 1 보다 크면 **SQLGetData** 를 호출할 수 없습니다.  
  
 드라이버는 이러한 제한 사항을 완화할 수 있습니다. 드라이버 완화 제한 사항을 확인 하기 위해 응용 프로그램은 다음 SQL_GETDATA_EXTENSIONS 옵션 중 하나를 사용 하 여 **SQLGetInfo** 를 호출 합니다.  
  
-   SQL_GD_OUTPUT_PARAMS = **SQLGetData** 를 호출 하 여 출력 매개 변수 값을 반환할 수 있습니다. 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.  
  
-   SQL_GD_ANY_COLUMN. 이 옵션이 반환 되는 경우 마지막으로 바인딩된 열 앞에 있는 열을 포함 하 여 모든 바인딩되지 않은 열에 대해 **SQLGetData** 를 호출할 수 있습니다.  
  
-   SQL_GD_ANY_ORDER. 이 옵션을 반환 하는 경우에는 바인딩되지 않은 열에 대해 임의 순서로 **SQLGetData** 를 호출할 수 있습니다.  
  
-   SQL_GD_BLOCK. SQL_GETDATA_EXTENSIONS InfoType에 대해 **SQLGetInfo** 에서이 옵션을 반환 하는 경우 드라이버는 행 집합 크기가 1 보다 클 때 **sqlgetdata** 호출을 지원 하 고, sqlgetdata를 호출 하기 전에 응용 프로그램이 SQL_POSITION 옵션을 사용 하 여 **SQLSetPos** 를 호출 하 여 커서를 올바른 행에 배치할 수 있습니다 **.**  
  
-   SQL_GD_BOUND. 이 옵션을 반환 하는 경우 바인딩된 열 뿐만 아니라 바인딩되지 않은 열에 대해서도 **SQLGetData** 를 호출할 수 있습니다.  
  
 이러한 제한 사항에는 두 가지 예외가 있으며 드라이버를 완화 하는 기능도 있습니다. 첫째, 행 집합 크기가 1 보다 크면 앞 으로만 이동 가능한 커서에 대해 **SQLGetData** 를 호출 하면 안 됩니다. 둘째, 드라이버가 책갈피를 지 원하는 경우 응용 프로그램에서 마지막으로 바인딩된 열 앞의 다른 열에 대해 **sqlgetdata** 를 호출할 수 없는 경우에도 항상 열 0에 대해 **sqlgetdata** 를 호출 하는 기능을 지원 해야 합니다. 응용 프로그램에서 ODBC 2를 사용 하 여 작업 하는 경우 sqlfetch를 호출한 후 **sqlfetch** 가 SQL_FETCH_NEXT의 *fetchorientation* 를 사용 하 여 **sqlextendedfetch** 에 매핑되고, *Col_or_Param_Num* 0 인 **sqlgetdata** 가 SQL_GET_BOOKMARK의 *foption* 을 사용 하 여 **SQLGetStmtOption** 에 매핑되는 **경우,** *x* *드라이버는* **sqlfetch**를 호출한 후에 0과 같은 *Col_or_Param_Num* 로 호출 될 때 책갈피를 성공적으로 반환*합니다.*  
  
 SQLBulkOperations 옵션을 SQL_ADD 사용 하 여 **SQLBulkOperations** 를 호출 하 여 삽입 한 행에 대 한 책갈피를 검색 하는 데는 줄이 행에 배치 되지 않으므로 **SQLGetData** 를 사용할 수 없습니다. 응용 프로그램은 SQL_ADD를 사용 하 여 **SQLBulkOperations** 를 호출 하기 전에 열 0을 바인딩하여 이러한 행에 대 한 책갈피를 검색할 수 있습니다 .이 경우 **SQLBulkOperations** 는 바인딩된 버퍼에서 책갈피를 반환 합니다. 그런 다음 SQL_FETCH_BOOKMARK로 **Sqlfetchscroll** 을 호출 하 여 해당 행에서 커서의 위치를 변경할 수 있습니다.  
  
 *TargetType* 인수가 interval 데이터 형식인 경우에는 데이터에 대 한 기본 간격 선행 전체 자릿수 (2)와 기본 간격 초 전체 자릿수 (6)가 각각의 SQL_DESC_DATETIME_INTERVAL_PRECISION 및 SQL_DESC_PRECISION 필드에 설정 됩니다. *TargetType* 인수가 SQL_C_NUMERIC 데이터 형식이 면 데이터에 사용 되는 SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 설정 된 기본 전체 자릿수 (드라이버 정의) 및 기본 소수 자릿수 (0)가 사용 됩니다. 기본 전체 자릿수 또는 소수 자릿수가 적절 하지 않은 경우 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 적절 한 설명자 필드를 명시적으로 설정 해야 합니다. SQL_DESC_CONCISE_TYPE 필드를 SQL_C_NUMERIC로 설정 하 고 SQL_ARD_TYPE의 *TargetType* 인수로 **SQLGetData** 를 호출 하 여 설명자 필드의 전체 자릿수 및 소수 자릿수 값이 사용 되도록 할 수 있습니다.  
  
> [!NOTE]
>  ODBC 2.x에서 *.x*응용 프로그램은 *TargetType* 을 SQL_C_DATE, SQL_C_TIME 또는 SQL_C_TIMESTAMP로 설정 하 여 \* *targetvalueptr* 이 날짜, 시간 또는 타임 스탬프 구조 임을 나타내야 합니다. ODBC 3.x에서 응용 프로그램은 *TargetType* *을 SQL_C_TYPE_DATE*, SQL_C_TYPE_TIME 또는 SQL_C_TYPE_TIMESTAMP로 설정 합니다. 드라이버 관리자는 필요한 경우 응용 프로그램 및 드라이버 버전에 따라 적절 한 매핑을 수행 합니다.  
  
## <a name="retrieving-variable-length-data-in-parts"></a>부분에서 가변 길이 데이터 검색  
 **SQLGetData** 를 사용 하 여 부분에 가변 길이 데이터가 포함 된 열에서 데이터를 검색할 수 있습니다. 즉, 열의 SQL 데이터 형식 식별자가 SQL_CHAR, SQL_VARCHAR, SQL_LONGVARCHAR, SQL_WCHAR, SQL_WVARCHAR, SQL_WLONGVARCHAR, SQL_BINARY, SQL_VARBINARY, SQL_LONGVARBINARY 또는 가변 길이 형식의 드라이버별 식별자 인 경우입니다.  
  
 파트의 열에서 데이터를 검색 하기 위해 응용 프로그램은 동일한 열에 대해 연속 해 서 **SQLGetData** 를 여러 번 호출 합니다. 각 호출에서 **SQLGetData** 는 데이터의 다음 부분을 반환 합니다. 응용 프로그램은 파트를 다시 구성 하 여 문자 데이터의 중간 부분에서 null 종료 문자를 제거 하는 작업을 수행 합니다. 반환할 데이터가 더 있거나 종료 문자에 할당 된 버퍼가 충분 하지 않은 경우 **SQLGetData** 는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004 (데이터가 잘렸습니다)을 반환 합니다. 데이터의 마지막 부분이 반환 될 때 **SQLGetData** 는 SQL_SUCCESS을 반환 합니다. 응용 프로그램은 응용 프로그램 버퍼에 있는 데이터의 양을 알 수 없기 때문에 열에서 데이터를 검색 하기 위해 마지막으로 유효한 호출에는 SQL_NO_TOTAL 및 0을 반환할 수 없습니다. 이 이후에 **SQLGetData** 를 호출 하면 SQL_NO_DATA 반환 됩니다. 자세한 내용은 다음 섹션인 "SQLGetData를 사용 하 여 데이터 검색" 섹션을 참조 하세요.  
  
 가변 길이 책갈피는 **SQLGetData**로 파트에서 반환 될 수 있습니다. 다른 데이터와 마찬가지로 **SQLGetData** 를 호출 하 여 파트에서 가변 길이 책갈피를 반환 하는 경우 SQLSTATE 01004 (문자열 데이터, 오른쪽 잘림)을 반환 하 고 반환할 데이터가 더 있는 경우 SQL_SUCCESS_WITH_INFO 합니다. 이는 **Sqlfetch** 또는 **sqlfetchscroll**에 대 한 호출로 가변 길이 책갈피를 잘라내는 경우와 다릅니다 .이 경우 SQL_ERROR 및 SQLSTATE 22001 (문자열 데이터, 오른쪽 잘림)가 반환 됩니다.  
  
 **SQLGetData** 는 고정 길이 데이터를 파트로 반환 하는 데 사용할 수 없습니다. 고정 길이 데이터를 포함 하는 열에 대 한 행에서 **SQLGetData** 를 두 번 이상 호출 하는 경우 첫 번째 이후의 모든 호출에 대 한 SQL_NO_DATA를 반환 합니다.  
  
## <a name="retrieving-streamed-output-parameters"></a>스트리밍된 출력 매개 변수 검색  
 드라이버가 스트리밍된 출력 매개 변수를 지 원하는 경우 응용 프로그램은 작은 버퍼를 사용 하 여 **SQLGetData** 를 여러 번 호출 하 여 많은 매개 변수 값을 검색할 수 있습니다. 스트리밍된 출력 매개 변수에 대 한 자세한 내용은 [SQLGetData를 사용 하 여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)을 참조 하세요.  
  
## <a name="retrieving-data-with-sqlgetdata"></a>SQLGetData를 사용 하 여 데이터 검색  
 지정 된 열에 대 한 데이터를 반환 하려면 **SQLGetData** 는 다음과 같은 일련의 단계를 수행 합니다.  
  
1.  열에 대 한 모든 데이터를 이미 반환한 경우 SQL_NO_DATA를 반환 합니다.  
  
2.  데이터가 \*NULL 인 경우 *StrLen_or_IndPtr* 를 SQL_NULL_DATA로 설정 합니다. 데이터가 NULL이 고 *StrLen_or_IndPtr* null 포인터인 경우 **SQLGetData** 는 SQLSTATE 22002 (표시기 변수 필요 하지만 제공 되지 않음)을 반환 합니다.  
  
     열에 대 한 데이터가 NULL이 아닌 경우 **SQLGetData** 는 3 단계로 진행 됩니다.  
  
3.  SQL_ATTR_MAX_LENGTH statement 특성을 0이 아닌 값으로 설정 하 고 열에 문자 또는 이진 데이터가 포함 되어 있는 경우이 열에 대해 이전에 **SQLGetData** 를 호출 하지 않은 경우에는 데이터가 SQL_ATTR_MAX_LENGTH 바이트로 잘립니다.  
  
    > [!NOTE]  
    >  SQL_ATTR_MAX_LENGTH statement 특성은 네트워크 트래픽을 줄이기 위한 것입니다. 일반적으로 데이터 원본에 의해 구현 되며, 네트워크를 통해 데이터를 반환 하기 전에 데이터를 자릅니다. 드라이버 및 데이터 원본은이를 지 원하는 데 필요 하지 않습니다. 따라서 데이터가 특정 크기로 잘리지 않도록 하기 위해 응용 프로그램은 해당 크기의 버퍼를 할당 하 고 *Bufferlength* 인수의 크기를 지정 해야 합니다.  
  
4.  데이터를 *TargetType*에 지정 된 형식으로 변환 합니다. 데이터는 해당 데이터 형식에 대 한 기본 전체 자릿수 및 소수 자릿수를 제공 합니다. *TargetType* 이 SQL_ARD_TYPE 되 면 사용의 SQL_DESC_CONCISE_TYPE 필드에 있는 데이터 형식이 사용 됩니다. *TargetType* 이 SQL_ARD_TYPE 경우 SQL_DESC_CONCISE_TYPE 필드의 데이터 형식에 따라 데이터의 전체 자릿수와 소수 자릿수는 해당 데이터의 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION 및 SQL_DESC_SCALE 필드에 제공 됩니다. 기본 전체 자릿수 또는 소수 자릿수가 적절 하지 않은 경우 응용 프로그램에서 **SQLSetDescField** 또는 **SQLSetDescRec**를 호출 하 여 적절 한 설명자 필드를 명시적으로 설정 해야 합니다.  
  
5.  데이터가 문자 또는 이진 등의 가변 길이 데이터 형식으로 변환 된 경우 **SQLGetData** 는 데이터 길이가 *bufferlength*를 초과 하는지 여부를 확인 합니다. 문자 데이터의 길이 (null 종결 문자 포함)가 *Bufferlength*를 초과 하는 경우 **SQLGetData** 는 데이터를 null 종료 문자 길이 보다 작은 *bufferlength* 로 자릅니다. 그런 다음 데이터를 null로 종료 합니다. 이진 데이터의 길이가 데이터 버퍼의 길이를 초과 하는 경우 **SQLGetData** 는 버퍼를 *bufferlength* 바이트로 자릅니다.  
  
     제공 된 데이터 버퍼가 너무 작아서 null 종료 문자를 저장할 수 없는 경우 **SQLGetData** 는 SQL_SUCCESS_WITH_INFO 및 SQLSTATE 01004을 반환 합니다.  
  
     **SQLGetData** 는 고정 길이 데이터 형식으로 변환 된 데이터를 잘리지 않습니다. 항상 **Targetvalueptr* 의 길이가 데이터 형식의 크기 라고 가정 합니다.  
  
6.  변환 되 고 잘린 데이터를 \* *targetvalueptr*에 배치 합니다. **SQLGetData** 는 데이터를 아웃오브 라인으로 반환할 수 없습니다.  
  
7.  데이터의 길이를 \* *StrLen_or_IndPtr*에 배치 합니다. *StrLen_or_IndPtr* null 포인터인 경우 **SQLGetData** 는 길이를 반환 하지 않습니다.  
  
    -   문자 또는 이진 데이터의 경우 변환 후의 데이터 길이 및 *Bufferlength*로 인 한 잘림 전의 데이터 길이입니다. 변환 후 드라이버에서 데이터 길이를 확인할 수 없는 경우, 경우에 따라 긴 데이터를 사용 하는 경우에는 SQL_SUCCESS_WITH_INFO을 반환 하 고 SQL_NO_TOTAL 길이를 설정 합니다. **SQLGetData** 에 대 한 마지막 호출은 항상 0 또는 SQL_NO_TOTAL이 아닌 데이터의 길이를 반환 해야 합니다. SQL_ATTR_MAX_LENGTH statement 특성으로 인해 데이터가 잘린 경우 실제 길이와는 달리이 특성의 값은 \* *StrLen_or_IndPtr*에 배치 됩니다. 이 특성은 변환 전에 서버에서 데이터를 잘라내는 것 이므로 드라이버에서 실제 길이를 확인할 수 있는 방법이 없기 때문입니다. 동일한 열에 대해 **SQLGetData** 를 연속 해 서 여러 번 호출 하는 경우 현재 호출을 시작할 때 사용할 수 있는 데이터의 길이입니다. 즉, 각 후속 호출에서 길이가 줄어듭니다.  
  
    -   다른 모든 데이터 형식의 경우 변환 후의 데이터 길이입니다. 즉, 데이터가 변환 된 형식의 크기입니다.  
  
8.  변환 중에 중요 한 값의 손실을 방지 하 고 (예: 정수 1로 변환 될 때 실수 1.234가 잘렸습니다.) *Bufferlength* 가 너무 작기 때문에 (예: "abcdef" 문자열이 4 바이트 버퍼에 배치 되는 경우) **SQLGetData** 는 SQLSTATE 01004 (데이터가 잘렸습니다) 및 SQL_SUCCESS_WITH_INFO을 반환 합니다. SQL_ATTR_MAX_LENGTH statement 특성 때문에 중요 한 손실을 제외 하 고 데이터가 잘린 경우 **SQLGetData** 는 SQL_SUCCESS를 반환 하 고 SQLSTATE 01004 (데이터가 잘렸습니다.)을 반환 하지 않습니다.  
  
 인바운드 데이터 버퍼의 콘텐츠 ( **sqlgetdata** 가 바인딩된 열에서 호출 되는 경우) 및 **sqlgetdata** 가 SQL_SUCCESS 또는 SQL_SUCCESS_WITH_INFO를 반환 하지 않는 경우 길이/표시기 버퍼가 정의 되지 않습니다.  
  
 **SQLGetData** 를 연속 해 서 호출 하면 요청 된 마지막 열에서 데이터를 검색 합니다. 이전 오프셋이 유효 하지 않게 됩니다. 예를 들어 다음 시퀀스를 수행 합니다.  
  
```cpp  
SQLGetData(icol=n), SQLGetData(icol=m), SQLGetData(icol=n)  
```  
  
 SQLGetData (icol = n)에 대 한 두 번째 호출에서는 n 열의 시작 부분에서 데이터를 검색 합니다. 이전에 열에 대 한 **SQLGetData** 호출로 인 한 데이터의 모든 오프셋이 더 이상 유효 하지 않습니다.  
  
## <a name="descriptors-and-sqlgetdata"></a>설명자 및 SQLGetData  
 **SQLGetData** 는 모든 설명자 필드와 직접 상호 작용 하지 않습니다.  
  
 *TargetType* 이 SQL_ARD_TYPE 되 면 사용의 SQL_DESC_CONCISE_TYPE 필드에 있는 데이터 형식이 사용 됩니다. *TargetType* 이 SQL_ARD_TYPE 또는 SQL_C_DEFAULT 이면 SQL_DESC_SCALE 필드의 데이터 형식에 따라 데이터의 전체 자릿수와 소수 자릿수는 해당 데이터의 SQL_DESC_DATETIME_INTERVAL_PRECISION, SQL_DESC_PRECISION 및 SQL_DESC_CONCISE_TYPE 필드에 제공 됩니다.  
  
## <a name="code-example"></a>코드 예  
 다음 예제에서 응용 프로그램은 **SELECT** 문을 실행 하 여 이름, id 및 전화 번호를 기준으로 정렬 된 고객 id, 이름 및 전화 번호의 결과 집합을 반환 합니다. 데이터의 각 행에 대해 **Sqlfetch** 를 호출 하 여 커서를 다음 행에 배치 합니다. **SQLGetData** 를 호출 하 여 인출 된 데이터를 검색 합니다. 데이터의 버퍼와 반환 된 바이트 수는 **SQLGetData**호출에 지정 됩니다. 마지막으로, 각 직원의 이름, ID 및 전화 번호를 인쇄 합니다.  
  
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
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 저장소 할당|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|블록 커서 위치와 관련이 없는 대량 작업 수행|[SQLBulkOperations](../../../odbc/reference/syntax/sqlbulkoperations-function.md)|  
|문 처리 취소|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|SQL 문 실행|[SQLExecDirect](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|정방향 전용 방향으로 단일 데이터 행 또는 데이터 블록 페치|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|실행 시 매개 변수 데이터 보내기|[SQLPutData](../../../odbc/reference/syntax/sqlputdata-function.md)|  
|커서 위치 지정, 행 집합의 데이터 새로 고침 또는 행 집합의 데이터 업데이트 또는 삭제|[SQLSetPos](../../../odbc/reference/syntax/sqlsetpos-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)   
 [SQLGetData를 사용하여 출력 매개 변수 검색](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)
