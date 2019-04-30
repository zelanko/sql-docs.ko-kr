---
title: SQLDescribeCol 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1b8453d76dc2af0499dc8d8af2ca1ec3024aee83
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061871"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수 합니다. ISO 92  
  
 **요약**  
 **SQLDescribeCol** 결과 집합에서 하나의 열에 대 한-열 이름, 형식, 열 크기, 소수 자릿수 및 null 허용 여부-결과 설명자를 반환 합니다. 이 정보 또한이 제품은 IRD 필드에입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
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
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *ColumnNumber*  
 [입력] 결과 데이터를 열 수는 1부터 증가 열 순서로 순차적으로 정렬 합니다. 합니다 *ColumnNumber* 인수 설정할 수도 있습니다 0 책갈피 열을 설명 합니다.  
  
 *ColumnName*  
 [출력] 열 이름을 반환 하는 null로 끝나는 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_NAME 필드에서이 값을 읽습니다. 열 이름이 또는 열 이름을 확인할 수 없는 경우 드라이버는 빈 문자열을 반환 합니다.  
  
 경우 *ColumnName* 가 null 인 경우 *NameLengthPtr* (문자 데이터에 대 한 null 종료 문자를 제외한) 문자의 총 수를 반환 여전히가 가리키는 버퍼에서 반환할 사용 가능한 *ColumnName*합니다.  
  
 *BufferLength*  
 [입력] 길이 **ColumnName* 문자에서 버퍼입니다.  
  
 *NameLengthPtr*  
 [출력] 문자 (null 종결 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *ColumnName*합니다. 반환할 사용 가능한 문자 개수 보다 크거나 같은 경우 *BufferLength*에서 열 이름을 \* *ColumnName* 잘립니다 *BufferLength*의 null 종결 문자 길이 뺀 값입니다.  
  
 *DataTypePtr*  
 [출력] SQL 데이터 형식의 열에 반환할 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_CONCISE_TYPE 필드에서이 값을 읽습니다. 에 있는 값 중 하나가이 됩니다 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md), 또는 드라이버별 SQL 데이터 형식입니다. 데이터 형식을 확인할 수 없는 경우 드라이버는 SQL_UNKNOWN_TYPE를 반환 합니다.  
  
 Odbc 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP 반환 됩니다  *\*DataTypePtr* 날짜, 시간 또는 타임 스탬프 데이터에 대 한 ODBC 2에서 각각;. *x*, SQL_DATE, SQL_TIME, 또는 SQL_TIMESTAMP 반환 됩니다. 드라이버 관리자는 ODBC 2 때 필요한 매핑을 수행 합니다. *x* 응용 프로그램이 작동을 ODBC 3. *x* 드라이버 때나는 ODBC 3. *x* 는 ODBC 2를 사용 하 여 응용 프로그램이 작동 합니다. *x* 드라이버입니다.  
  
 때 *ColumnNumber* 같은지 SQL_BINARY 반환 됩니다 (책갈피 열)에 대해 0으로  *\*DataTypePtr* 가변 길이 책갈피에 대 한 합니다. (SQL_INTEGER는 책갈피가 ODBC 3에서 사용 되는 경우에 반환 됩니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 또는 ODBC 2. *x* 응용 프로그램을 사용 하는 ODBC 3. *x* 드라이버입니다.)  
  
 이러한 데이터 유형에 대 한 자세한 내용은 참조 하세요. [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.  
  
 *ColumnSizePtr*  
 [출력] 데이터 원본에서 열의 문자 단위로 크기를 반환 하는 버퍼에 대 한 포인터입니다. 열 크기를 확인할 수 없는 경우 드라이버는 0을 반환 합니다. 열 크기에 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식입니다.  
  
 *DecimalDigitsPtr*  
 [출력] 데이터 원본에서 열의 소수 자릿수를 반환 하는 버퍼에 대 한 포인터입니다. 소수 자릿수를 확인할 수 없는 또는 적용 되지 경우 드라이버는 0을 반환 합니다. 소수 자릿수에 대 한 자세한 내용은 참조 하세요. [열 크기, 십진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식입니다.  
  
 *NullablePtr*  
 [출력] 열의 NULL 값을 허용 하는지 여부를 나타내는 값을 반환 하는 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_NULLABLE 필드에서이 값을 읽습니다. 값은 다음 중 하나입니다.  
  
 SQL_NO_NULLS: 열에서 NULL 값을 허용 하지 않습니다.  
  
 SQL_NULLABLE: 열은 NULL 값을 허용 합니다.  
  
 SQL_NULLABLE_UNKNOWN: 드라이버는 열에 NULL 값이 허용 하는 경우 확인할 수 없습니다.  
  
## <a name="returns"></a>반환 값  
 관계 없이 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR를 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDescribeCol** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 연관된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 사용 하 여를 *HandleType*호출의와 *처리할* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환한 SQLSTATE 값 **SQLDescribeCol** ;이 함수의 컨텍스트에서 각각에 설명 하 고 "(DM)" 표기법 드라이버 관리자에 의해 반환 된 Sqlstate 설명은 앞에 옵니다. 각 SQLSTATE 값과 연결 된 반환 코드를 다른 설명이 없는 경우 SQL_ERROR를 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *ColumnName* 열 이름이 잘렸습니다 하므로 전체 열 이름을 반환 하기에 충분히 없습니다. 잘리지 않은 열 이름의 길이에서 **NameLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07005|준비 된 문이 없습니다를 *커서 사양이*|관련 된 문을 합니다 *StatementHandle* 결과 집합을 반환 하지 않았습니다. 열을 설명 했습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 지정 된 값 (DM) *ColumnNumber* 0이 고 SQL_ATTR_USE_BOOKMARKS 문 옵션 SQL_UB_OFF 합니다.<br /><br /> 인수에 지정 된 값 *ColumnNumber* 결과 집합의 열 수보다 큽니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버는 연결 된 데이터 원본 간의 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 관련 SQLSTATE 했습니다는 및 없습니다 구현 별 SQLSTATE 정의 되었습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼 오류 및 해당 원인에 설명 합니다.|  
|HY001|메모리 할당 실패|드라이버 완료 함수 또는 실행을 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정 합니다 *StatementHandle*합니다. 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 가 호출 된 *StatementHandle*합니다. 함수에서 다시 호출 된 다음 합니다 *StatementHandle*합니다.<br /><br /> 함수 호출 및 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출한 합니다 *StatementHandle* 의 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|(DM)를 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한 합니다 *StatementHandle*합니다. 이 비동기 함수가 계속 실행 될 때 **SQLDescribeCol** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대해 호출 된 합니다 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM)를 비동기적으로 실행 중인 함수 (없습니다이 하나)에 대해 호출 된 합니다 *StatementHandle* 이 함수가 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) 함수를 호출한 호출 하기 전에 **SQLPrepare**를 **SQLExecute**, 또는 문 핸들에서 카탈로그 함수입니다.<br /><br /> (DM) **SQLExecute**를 **SQLExecDirect**를 **SQLBulkOperations**, 또는 **SQLSetPos** 에 대해 호출 된는  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 전송 하기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|기본 메모리 개체에 액세스할 수 없습니다, 가능한 경우 메모리 부족으로 인해 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대 한 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용으로 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 하세요. [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간 만료 됨|데이터 원본 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM) 드라이버를 사용 하 여 연결 합니다 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드로 폴링 되지|알림 모델을 사용할 때마다 폴링 비활성화 됩니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하려면 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
 **SQLDescribeCol** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다 **SQLPrepare** 하거나 **SQLExecute** 호출 **SQLPrepare** 전과 **SQLExecute**데이터 원본 문 핸들을 사용 하 여 연결 된 SQL 문을 평가 하는 경우에 따라 합니다.  
  
 성능상의 이유로 응용 프로그램 호출 하지 않아야 **SQLDescribeCol** 문을 실행 하기 전에 합니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 일반적으로 호출 **SQLDescribeCol** 을 호출한 후에 **SQLPrepare** 연결된에 대 한 호출 전후와 **SQLExecute**합니다. 응용 프로그램을 호출할 수도 있습니다 **SQLDescribeCol** 을 호출한 후에 **SQLExecDirect**합니다. 자세한 내용은 [결과 집합 메타 데이터](../../../odbc/reference/develop-app/result-set-metadata.md)입니다.  
  
 **SQLDescribeCol** 열 이름, 형식 및 길이에서 생성 된 검색을 **선택** 문입니다. 열이 식에서 **ColumnName* 는 빈 문자열 또는 드라이버에서 정의 된 이름입니다.  
  
> [!NOTE]  
>  ODBC 지원 SQL_NULLABLE_UNKNOWN 확장, Open Group 및 SQL 액세스 그룹 호출 수준 인터페이스 사양에 대 한 옵션을 지정 하지 않는 경우에 **SQLDescribeCol**합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|여러 행의 데이터를 가져오는 중|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
