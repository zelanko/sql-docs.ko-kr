---
title: "SQLDescribeCol 함수 | Microsoft Docs"
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
apiname: SQLDescribeCol
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLDescribeCol
helpviewer_keywords: SQLDescribeCol function [ODBC]
ms.assetid: eddef353-83f3-4a3c-8f24-f9ed888890a4
caps.latest.revision: "35"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4967b2de98246e3ae8eedb91ecfcbf507b2afc8c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLDescribeCol** 결과 설명자를 반환-열 이름, 유형, 열 크기, 소수 자릿수 및 null 허용 여부 — 결과의 열 하나에 대 한 설정입니다. 이 정보에도 사용할 수 있는 IRD 필드에서 합니다.  
  
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
 [입력] 결과 데이터의 열 번호 1에서 시작 증가 열 순서로 순차적으로 정렬 합니다. *ColumnNumber* 인수 수 책갈피 열을 설명 하기 위해도 0으로 설정 하는 수입니다.  
  
 *열 이름*  
 [출력] 열 이름을 반환 하는 null로 끝나는 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_NAME 필드에서이 값을 읽습니다. 해당 열이 명명 된 열 이름을 확인할 수 없는 경우 드라이버는 빈 문자열을 반환 합니다.  
  
 경우 *ColumnName* 이 NULL 이면 *NameLengthPtr* 는 문자 (문자 데이터에 대 한 null 종결 문자 제외)의 총 수를 반환 여전히 가리키는 버퍼에서 반환할 수 *ColumnName*합니다.  
  
 *BufferLength*  
 [입력] 길이 **ColumnName* 문자에서 버퍼입니다.  
  
 *NameLengthPtr*  
 [출력] 문자 (null 종결 제외)의 총 수를 반환 하는 버퍼에 대 한 포인터를 반환 하려면 사용 가능한 \* *ColumnName*합니다. 반환할 수 있는 문자 수는 보다 크거나 같은 경우 *BufferLength*에 열 이름을 \* *ColumnName* 잘립니다 *BufferLength*null 종결 문자 길이 뺀 값입니다.  
  
 *DataTypePtr*  
 [출력] SQL 데이터 형식의 열을 반환 하는 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_CONCISE_TYPE 필드에서이 값을 읽습니다. 값 중 하나가이 됩니다 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md), 또는 드라이버별 SQL 데이터 형식입니다. 데이터 형식을 확인할 수 없는 경우 드라이버는 SQL_UNKNOWN_TYPE를 반환 합니다.  
  
 Odbc 3. *x*, SQL_TYPE_DATE SQL_TYPE_TIME 및 SQL_TYPE_TIMESTAMP에 반환 됩니다  *\*DataTypePtr* 날짜, 시간 또는 타임 스탬프 데이터에 대 한 ODBC 2에서 각각;. *x*, SQL_DATE, SQL_TIME, 또는 SQL_TIMESTAMP 반환 됩니다. 드라이버 관리자 때 ODBC 2 필요한 매핑을 수행 합니다. *x* 응용 프로그램이 작동 ODBC 3. *x* 드라이버 때나 ODBC 3. *x* 응용 프로그램이 작동 ODBC 2. *x* 드라이버입니다.  
  
 때 *ColumnNumber* 같은지 SQL_BINARY에 반환 됩니다 (책갈피 열)에 대해 0으로  *\*DataTypePtr* 가변 길이 책갈피에 대 한 합니다. (SQL_INTEGER는 책갈피가 ODBC 3에서 사용 되는 경우에 반환 됩니다. *x* 응용 프로그램을 사용 하는 ODBC 2. *x* 드라이버 또는 ODBC 2. *x* 응용 프로그램을 사용 하는 ODBC 3. *x* 드라이버입니다.)  
  
 이러한 데이터 형식에 대 한 자세한 내용은 참조 하십시오. [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 부록 d: 데이터 형식에서입니다. 드라이버별 SQL 데이터 형식에 대 한 내용은 드라이버의 설명서를 참조 하십시오.  
  
 *ColumnSizePtr*  
 [출력] 데이터 원본에 열 크기를 문자 단위로 반환 하는 버퍼에 대 한 포인터입니다. 열 크기를 확인할 수 없는 경우 드라이버는 0을 반환 합니다. 열 크기에 대 한 자세한 내용은 참조 하십시오. [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.  
  
 *DecimalDigitsPtr*  
 [출력] 데이터 원본에 열 10 진수의 수를 반환 하는 버퍼에 대 한 포인터입니다. 소수 자리 수가 확인할 수 없는 적용 되지 않는 경우 드라이버는 0을 반환 합니다. 10 진수 숫자에 대 한 자세한 내용은 참조 하십시오. [열 크기, 10 진수, 8 진수 길이 전송 및 표시 크기](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 d: 데이터 형식에서입니다.  
  
 *NullablePtr*  
 [출력] 열 NULL 값을 허용 하는지 여부를 나타내는 값을 반환 하는 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_NULLABLE 필드에서이 값을 읽습니다. 값은 다음 중 하나입니다.  
  
 SQL_NO_NULLS: 열의 NULL 값을 허용 하지 않습니다.  
  
 SQL_NULLABLE: 열의 NULL 값을 허용 합니다.  
  
 SQL_NULLABLE_UNKNOWN: 드라이버 열이 NULL 값을 허용 하는 경우 확인할 수 없습니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLDescribeCol** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환 합니다. 호출 하 여 관련된 된 SQLSTATE 값을 가져올 수 있습니다 **SQLGetDiagRec** 와 *HandleType*여의 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLDescribeCol** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|01004|문자열 데이터 오른쪽 잘림|버퍼 \* *ColumnName* 충분히 열 이름이 잘렸습니다 하므로 전체 열 이름을 반환할 수 없습니다. 잘리지 않은 열 이름의 길이에서 **NameLengthPtr*합니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|07005|준비 된 문의 하지는 *커서 사양이*|와 관련 된 문을 *StatementHandle* 결과 집합을 반환 하지 않았습니다. 설명 하기 위해 열 하지 않았습니다.|  
|07009|잘못 된 설명자 인덱스입니다.|인수에 대해 지정 된 값 (DM) *ColumnNumber* 0 한 SQL_ATTR_USE_BOOKMARKS 문 옵션 SQL_UB_OFF 였습니다.<br /><br /> 인수에 대해 지정 된 값 *ColumnNumber* 결과 집합의 열 개수 보다 큽니다.|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 실패|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*합니다. 함수에서 다시 호출 된 후의 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때 **SQLDescribeCol** 호출 되었습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) 함수가 호출 하기 전에 호출 된 **SQLPrepare**, **SQLExecute**, 또는 문 핸들에서 카탈로그 함수입니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|문자열 또는 버퍼 길이가 잘못 되었습니다.|인수에 대해 지정 된 값 (DM) *BufferLength* 0 보다 작습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
 **SQLDescribeCol** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 **SQLPrepare** 또는 **SQLExecute** 호출 **SQLPrepare** 하기전에 **SQLExecute**데이터 원본 문 핸들에 연결 된 SQL 문을 계산 하는 경우에 따라 합니다.  
  
 성능상의 이유로 응용 프로그램 호출 하지 않아야 **SQLDescribeCol** 문을 실행 하기 전에.  
  
## <a name="comments"></a>주석  
 응용 프로그램에서 일반적으로 호출 **SQLDescribeCol** 를 호출한 후 **SQLPrepare** 이전 또는 관련된 호출 후 및 **SQLExecute**합니다. 응용 프로그램 호출 또한 수 **SQLDescribeCol** 를 호출한 후 **SQLExecDirect**합니다. 자세한 내용은 참조 [결과 집합 메타 데이터](../../../odbc/reference/develop-app/result-set-metadata.md)합니다.  
  
 **SQLDescribeCol** 열 이름, 형식 및 길이 의해 생성 된 검색 한 **선택** 문. 열이 식 **ColumnName* 은 빈 문자열 또는 드라이버에서 정의 된 이름이 있습니다.  
  
> [!NOTE]  
>  ODBC를 확장으로 SQL_NULLABLE_UNKNOWN Open Group 및 SQL 액세스 그룹 호출 수준 인터페이스 사양에 대 한 옵션을 지정 하지 않는 경우에 지원 **SQLDescribeCol**합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|여러 데이터 행을 인출합니다.|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|열 집합 결과의 수를 반환 합니다.|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행할 문을 준비합니다.|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
