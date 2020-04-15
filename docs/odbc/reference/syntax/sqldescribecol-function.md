---
title: SQLDescribeCol 함수 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLDescribeCol
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLDescribeCol
helpviewer_keywords:
- SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c727f6b36930b0d2ad0d5a61592b83bcd4995426
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301173"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 함수
**규칙**  
 버전 출시: ODBC 1.0 표준 규정 준수: ISO 92  
  
 **요약**  
 **SQLDescribeCol은** 결과 집합의 한 열에 대해 열 이름, 유형, 열 크기, 소수 자릿수 및 nullability와 같은 결과 설명자(결과 설명자)를 반환합니다. 이 정보는 IRD 의 필드에서도 사용할 수 있습니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLDescribeCol(  
      SQLHSTMT       StatementHandle,  
      SQLUSMALLINT   ColumnNumber,  
      SQLCHAR *      ColumnName,  
      SQLSMALLINT    BufferLength,  
      SQLSMALLINT *  NameLengthPtr,  
      SQLSMALLINT *  DataTypePtr,  
      SQLULEN *      ColumnSizePtr,  
      SQLSMALLINT *  DecimalDigitsPtr,  
      SQLSMALLINT *  NullablePtr);  
```  
  
## <a name="arguments"></a>인수  
 *명령문 핸들*  
 [입력] 명령문 핸들입니다.  
  
 *ColumnNumber*  
 [입력] 결과 데이터의 열 수, 1부터 시작하여 열 순서를 증가시켜 순차적으로 정렬됩니다. *ColumnNumber* 인수를 책갈피 열을 설명하기 위해 0으로 설정할 수도 있습니다.  
  
 *ColumnName*  
 [출력] 열 이름을 반환할 null 종료 버퍼에 대한 포인터입니다. 이 값은 IRD의 SQL_DESC_NAME 필드에서 읽습니다. 열의 이름이 없거나 열 이름을 확인할 수 없는 경우 드라이버는 빈 문자열을 반환합니다.  
  
 *ColumnName이* NULL인 경우 *NameLengthPtr은* *ColumnName*로 가리키는 버퍼에서 반환할 수 있는 총 문자 수(문자 데이터에 대한 null-termination 문자 제외)를 반환합니다.  
  
 *버퍼 길이*  
 [입력] **ColumnName* 버퍼의 길이입니다.  
  
 *이름길이Ptr*  
 [출력] \* *ColumnName에서*반환할 수 있는 총 문자 수(null 종료 제외)를 반환하는 버퍼에 대한 포인터입니다. 반환할 수 있는 문자 수가 *BufferLength보다*크거나 같으면 \* *ColumnName의* 열 이름이 *BufferLength에* 잘려null 종료 문자의 길이를 뺀 값입니다.  
  
 *데이터 타이핑 Ptr*  
 [출력] 열의 SQL 데이터 형식을 반환할 버퍼에 대한 포인터입니다. 이 값은 IRD의 SQL_DESC_CONCISE_TYPE 필드에서 읽습니다. 이 값은 [SQL 데이터 형식의](../../../odbc/reference/appendixes/sql-data-types.md)값 중 하나또는 드라이버별 SQL 데이터 형식입니다. 데이터 형식을 확인할 수 없는 경우 드라이버는 SQL_UNKNOWN_TYPE 반환합니다.  
  
 ODBC 3. *x,* 날짜, 시간 또는 타임스탬프 데이터에 대해 * \*dataTypePtr에서* 각각 반환되는 SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP ODBC 2에서. *x,* SQL_DATE, SQL_TIME 또는 SQL_TIMESTAMP 반환됩니다. 드라이버 관리자는 ODBC 2때 필요한 매핑을 수행합니다. *x* 응용 프로그램이 ODBC 3로 작동합니다. *x* 드라이버 또는 ODBC 3. *x* 응용 프로그램이 ODBC 2로 작동합니다. *x* 드라이버.  
  
 *ColumnNumber가* 책갈피 열의 경우 0이면 SQL_BINARY 가변 길이 책갈피의 * \*경우 DataTypePtr에서* 반환됩니다. (odBC 3에서 책갈피를 사용하는 경우 SQL_INTEGER 반환됩니다. *x* 응용 프로그램은 ODBC 2로 작업합니다. *x* 드라이버 또는 ODBC 2에 의해. *x* 응용 프로그램은 ODBC 3로 작업합니다. *x* 드라이버.)  
  
 이러한 데이터 형식에 대한 자세한 내용은 부록 D: 데이터 [형식의 SQL 데이터 유형을](../../../odbc/reference/appendixes/sql-data-types.md) 참조하십시오. 드라이버 별 SQL 데이터 형식에 대한 자세한 내용은 드라이버 설명서를 참조하십시오.  
  
 *열크기Ptr*  
 [출력] 데이터 원본에서 열의 크기(문자)를 반환할 버퍼를 포인터로 지정합니다. 열 크기를 확인할 수 없는 경우 드라이버는 0을 반환합니다. 열 크기에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.  
  
 *소수 자릿수Ptr*  
 [출력] 데이터 원본에서 열의 소수 자릿수를 반환할 버퍼를 포인터로 지정합니다. 소수 자릿수를 확인할 수 없거나 적용할 수 없는 경우 드라이버는 0을 반환합니다. 소수 자릿수에 대한 자세한 내용은 [열 크기, 소수 자릿수, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 유형의 표시 크기를 참조하십시오.  
  
 *널러블 Ptr*  
 [출력] 열이 NULL 값을 허용하는지 여부를 나타내는 값을 반환하는 버퍼에 대한 포인터입니다. 이 값은 IRD의 SQL_DESC_NULLABLE 필드에서 읽습니다. 값은 다음 중 하나입니다.  
  
 SQL_NO_NULLS: 열에서 NULL 값을 허용하지 않습니다.  
  
 SQL_NULLABLE: 열은 NULL 값을 허용합니다.  
  
 SQL_NULLABLE_UNKNOWN: 드라이버는 열이 NULL 값을 허용하는지 확인할 수 없습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE.  
  
## <a name="diagnostics"></a>진단  
 **SQLDescribeCol** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO 반환 하는 경우 관련 된 SQLSTATE 값 *SQL_HANDLE_STMT 핸들 유형* 및 문 *핸들*핸들을 호출 하 여 가져올 수 있습니다. **SQLGetDiagRec** *Handle* 다음 표에서는 **SQLDescribeCol에서** 일반적으로 반환하는 SQLSTATE 값을 나열하고 이 함수의 컨텍스트에서 각 값을 설명합니다. "(DM)"는 드라이버 관리자가 반환하는 SQLSTATEs의 설명 앞에 옵니다. 별도로 명시되지 않는 한 각 SQLSTATE 값과 연결된 반환 코드는 SQL_ERROR.  
  
|SQLSTATE|Error|설명|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|01004|문자열 데이터, 오른쪽 잘린|버퍼 \* *ColumnName* 전체 열 이름을 반환할 만큼 충분히 크지 않았기 때문에 열 이름이 잘렸습니다. 잘린 열 이름의 길이는 **NameLengthPtr에서*반환됩니다. (함수는 SQL_SUCCESS_WITH_INFO 반환합니다.)|  
|07005|*커서 사양이* 아닌 준비된 문|*StatementHandle과* 연결된 명령문이 결과 집합을 반환하지 않았습니다. 설명할 열이 없습니다.|  
|07009|잘못된 설명자 인덱스|(DM) *인수 ColumnNumber에* 대해 지정된 값이 0이고 SQL_ATTR_USE_BOOKMARKS 문 옵션이 SQL_UB_OFF.<br /><br /> *ColumnNumber* 인수에 대해 지정된 값은 결과 집합의 열 수보다 큽합니다.|  
|08S01|통신 링크 오류|함수 처리가 완료되기 전에 드라이버와 드라이버가 연결된 데이터 원본 간의 통신 링크가 실패했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현별 SQLSTATE가 정의되지 않은 오류가 발생했습니다. MessageText 버퍼에서 **SQLGetDiagRec에서** 반환 된 오류 메시지는 오류 및 그 원인을 설명 합니다. * \**|  
|HY01|메모리 할당 실패|드라이버가 함수의 실행 또는 완료를 지원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY08|작업 취소됨|*명령문 핸들*에 대해 비동기 처리가 활성화되었습니다. 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** *명령문 핸들*에서 호출되었습니다. 그런 다음 *함수가 StatementHandle*에서 다시 호출되었습니다.<br /><br /> 함수가 호출되었고 실행을 완료하기 전에 **SQLCancel** 또는 **SQLCancelHandle이** 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle에서* 호출되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*와 연결된 연결 핸들에 대해 비동기적으로 실행되는 함수가 호출되었습니다. **SQLDescribeCol이** 호출될 때 이 비동기 함수는 여전히 실행 중이었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**또는 **SQLMoreResults는** *명령문 핸들에* 대해 호출되고 SQL_PARAM_DATA_AVAILABLE 반환되었습니다. 이 함수는 스트리밍된 모든 매개 변수에 대해 데이터를 검색하기 전에 호출되었습니다.<br /><br /> (DM) 비동기적으로 실행 되는 함수 (이 하나) *StatementHandle에* 대 한 호출 하 고이 함수를 호출 될 때 여전히 실행 되 고.<br /><br /> (DM) **SQLPrepare,** **SQLExecute**또는 문 핸들의 카탈로그 함수를 호출하기 전에 함수가 호출되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**및 **SQLSetPos는** *문 핸들에* 대해 호출되고 SQL_NEED_DATA 반환되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 조건으로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|유효하지 않은 문자열 또는 버퍼 길이|(DM) 인수 *BufferLength에* 대해 지정된 값이 0보다 적습니다.|  
|HY17|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단됩니다. 분리 및 읽기 전용 함수만 허용됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [SQLEndTran 함수를](../../../odbc/reference/syntax/sqlendtran-function.md)참조 하십시오.|  
|HYT01|연결 시간 시간이 만료되었습니다.|데이터 원본이 요청에 응답하기 전에 연결 시간 시간 만료 기간이 만료되었습니다. 연결 시간 설정 기간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 통해 설정됩니다.|  
|IM001|드라이버가 이 기능을 지원하지 않습니다.|(DM) *StatementHandle와* 연결된 드라이버는 함수를 지원하지 않습니다.|  
|IM017|비동기 알림 모드에서 폴링이 비활성화됨|알림 모델을 사용할 때마다 폴링이 비활성화됩니다.|  
|IM018|**SQLCompleteAsync이** 핸들에 이전 비동기 작업을 완료 하기 위해 호출 되지 않았습니다.|핸들의 이전 함수 호출이 SQL_STILL_EXECUTING 반환하고 알림 모드가 활성화된 경우 **SQLCompleteAsync를** 호출하여 사후 처리를 수행하여 작업을 완료해야 합니다.|  
  
 **SQLDescribeCol은** 데이터 원본이 문 핸들과 관련된 SQL 문을 평가하는 시기에 **SQLExecute**따라 **SQLPrepare** 또는 **SQLExecute에서** 반환할 수 있는 **SQLState를** 반환할 수 있습니다.  
  
 성능상의 이유로 응용 프로그램은 문을 실행하기 전에 **SQLDescribeCol을** 호출해서는 안 됩니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램은 일반적으로 SQLPrepare를 호출한 후 **SQLExecute에**대한 연결된 호출 전후에 **SQLDescribeCol을** 호출합니다. **SQLPrepare** 응용 프로그램은 **SQLExecDirect**를 호출한 후 **SQLDescribeCol을** 호출할 수도 있습니다. 자세한 내용은 [결과 집합 메타데이터](../../../odbc/reference/develop-app/result-set-metadata.md)를 참조하십시오.  
  
 **SQLDescribeCol** **SELECT** 문에 의해 생성 된 열 이름, 유형 및 길이를 검색 합니다. 열이 식인 경우 **ColumnName은* 빈 문자열 또는 드라이버 정의 이름입니다.  
  
> [!NOTE]  
>  ODBC는 열린 그룹 및 SQL 액세스 그룹 호출 수준 인터페이스 사양이 **SQLDescribeCol**에 대한 옵션을 지정하지 않더라도 SQL_NULLABLE_UNKNOWN 확장으로 지원합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|명령문 처리 취소|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대한 정보 반환|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|여러 데이터 행 가져오기|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행을 위한 명령문 준비|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
