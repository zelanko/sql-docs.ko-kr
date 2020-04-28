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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c727f6b36930b0d2ad0d5a61592b83bcd4995426
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301173"
---
# <a name="sqldescribecol-function"></a>SQLDescribeCol 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLDescribeCol** 결과 집합의 한 열에 대해 결과 설명자-열 이름, 형식, 열 크기, 10 진수 숫자 및 null 허용 여부를 반환 합니다. 이 정보는 IRD의 필드 에서도 사용할 수 있습니다.  
  
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
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *ColumnNumber*  
 입력 열 순서에서 1부터 시작 하 여 순차적으로 정렬 된 결과 데이터의 열 수입니다. 또한 *Columnnumber* 인수를 0으로 설정 하 여 책갈피 열을 설명할 수 있습니다.  
  
 *ColumnName*  
 출력 열 이름을 반환할 null로 끝나는 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_NAME 필드에서이 값을 읽습니다. 열이 명명 되지 않았거나 열 이름을 확인할 수 없는 경우 드라이버는 빈 문자열을 반환 합니다.  
  
 *Columnname* 이 NULL 인 경우 *NameLengthPtr* 는 *columnname*이 가리키는 버퍼에서 반환 하는 데 사용할 수 있는 문자 데이터의 NULL 종료 문자를 제외한 총 문자 수를 반환 합니다.  
  
 *BufferLength*  
 입력 **ColumnName* 버퍼의 길이 (문자)입니다.  
  
 *NameLengthPtr*  
 출력 \* *ColumnName*에서 반환 하는 데 사용할 수 있는 총 문자 수 (null 종료 제외)를 반환할 버퍼에 대 한 포인터입니다. 반환할 수 있는 문자 수가 *bufferlength*보다 크거나 같은 경우 \* *ColumnName* 의 열 이름은 *bufferlength* 에서 null 종료 문자의 길이를 뺀 값으로 잘립니다.  
  
 *DataTypePtr*  
 출력 열의 SQL 데이터 형식을 반환할 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_CONCISE_TYPE 필드에서이 값을 읽습니다. 이 값은 [Sql 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md)또는 드라이버별 sql 데이터 형식의 값 중 하나입니다. 데이터 형식을 확인할 수 없는 경우 드라이버는 SQL_UNKNOWN_TYPE을 반환 합니다.  
  
 ODBC 3. *x*, SQL_TYPE_DATE, SQL_TYPE_TIME 또는 SQL_TYPE_TIMESTAMP는 각각 날짜, 시간 또는 타임 스탬프 데이터에 대해 * \*DataTypePtr* 로 반환 됩니다. ODBC 2. *x*, SQL_DATE, SQL_TIME 또는 SQL_TIMESTAMP 반환 됩니다. 드라이버 관리자는 ODBC 2를 사용할 때 필요한 매핑을 수행 합니다. *x* 응용 프로그램이 ODBC 3에서 작동 하 고 있습니다. *x* 드라이버 또는 ODBC 3 인 경우 *x* 응용 프로그램에서 ODBC 2를 사용 하 고 있습니다. *x* 드라이버.  
  
 *Columnnumber* 가 0과 같을 때 (책갈피 열) SQL_BINARY 가변 길이 책갈피에 대 한 * \*DataTypePtr* 에서 반환 됩니다. ODBC 3에서 책갈피를 사용 하는 경우 SQL_INTEGER 반환 됩니다. ODBC 2를 사용 하 여 작동 하는 *x* 응용 프로그램 *x* 드라이버 또는 ODBC 2. ODBC 3에서 작동 하는 *x* 응용 프로그램입니다. *x* 드라이버)  
  
 이러한 데이터 형식에 대 한 자세한 내용은 부록 D: 데이터 형식에서 [SQL 데이터 형식](../../../odbc/reference/appendixes/sql-data-types.md) 을 참조 하세요. 드라이버별 SQL 데이터 형식에 대 한 자세한 내용은 드라이버 설명서를 참조 하십시오.  
  
 *ColumnSizePtr*  
 출력 데이터 원본에 있는 열의 크기 (문자 수)를 반환할 버퍼에 대 한 포인터입니다. 열 크기를 확인할 수 없는 경우 드라이버는 0을 반환 합니다. 열 크기에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.  
  
 *DecimalDigitsPtr*  
 출력 데이터 원본에 있는 열의 소수 자릿수를 반환할 버퍼에 대 한 포인터입니다. 10 진수의 수를 확인할 수 없거나 해당 사항이 적용 되지 않는 경우 드라이버는 0을 반환 합니다. 10 진수에 대 한 자세한 내용은 [열 크기, 10 진수 숫자, 전송 옥텟 길이 및](../../../odbc/reference/appendixes/column-size-decimal-digits-transfer-octet-length-and-display-size.md) 부록 D: 데이터 형식의 표시 크기를 참조 하세요.  
  
 *NullablePtr*  
 출력 열이 NULL 값을 허용 하는지 여부를 나타내는 값을 반환할 버퍼에 대 한 포인터입니다. IRD의 SQL_DESC_NULLABLE 필드에서이 값을 읽습니다. 값은 다음 중 하나입니다.  
  
 SQL_NO_NULLS: 열은 NULL 값을 허용 하지 않습니다.  
  
 SQL_NULLABLE: 열은 NULL 값을 허용 합니다.  
  
 SQL_NULLABLE_UNKNOWN: 드라이버에서 열이 NULL 값을 허용 하는지 여부를 확인할 수 없습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **SQLDescribeCol** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하 여 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **SQLDescribeCol** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|01004|문자열 데이터, 오른쪽이 잘렸습니다.|버퍼 \* *ColumnName* 이 전체 열 이름을 반환 하기에 충분히 크지 않아 열 이름이 잘렸습니다. 잘린 열 이름의 길이가 **NameLengthPtr*에서 반환 됩니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|07005|준비 된 문이 *커서 사양이* 아닙니다.|*StatementHandle* 와 연결 된 문에서 결과 집합을 반환 하지 않았습니다. 설명 하는 열이 없습니다.|  
|07009|잘못 된 설명자 인덱스|(DM) 인수 *Columnnumber* 에 지정 된 값이 0이 고 SQL_ATTR_USE_BOOKMARKS 문 옵션이 SQL_UB_OFF 되었습니다.<br /><br /> 인수 *Columnnumber* 에 지정 된 값이 결과 집합의 열 수보다 큽니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 실패|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLDescribeCol** 가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) 함수는 문 핸들에서 **Sqlprepare**, **sqlprepare**또는 catalog 함수를 호출 하기 전에 호출 되었습니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY090|잘못 된 문자열 또는 버퍼 길이입니다.|(DM) 인수 *Bufferlength* 에 지정 된 값이 0 보다 작은 경우|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
 **SQLDescribeCol** 는 데이터 원본에서 문 핸들과 연결 된 SQL 문을 평가 하는 시점에 따라 sqlprepare 및 **sqlprepare** **이전에 호출** 될 때 **sqlprepare** 또는 **sqlprepare** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
 성능상의 이유로 응용 프로그램은 문을 실행 하기 전에 **SQLDescribeCol** 를 호출 하면 안 됩니다.  
  
## <a name="comments"></a>주석  
 응용 프로그램은 일반적으로 **Sqlprepare** 를 호출한 후 **sqlprepare**에 연결 된 호출 전후에 **SQLDescribeCol** 를 호출 합니다. 응용 프로그램은 **Sqlexecdirect**를 호출한 후에도 **SQLDescribeCol** 를 호출할 수 있습니다. 자세한 내용은 [결과 집합 메타 데이터](../../../odbc/reference/develop-app/result-set-metadata.md)를 참조 하세요.  
  
 **SQLDescribeCol** 는 **SELECT** 문에 의해 생성 된 열 이름, 유형 및 길이를 검색 합니다. 열이 식인 경우 **ColumnName* 은 빈 문자열 또는 드라이버 정의 이름 중 하나입니다.  
  
> [!NOTE]  
>  Open Group 및 SQL 액세스 그룹 호출 수준 인터페이스 사양은 **SQLDescribeCol**에 대 한 옵션을 지정 하지 않더라도 ODBC는 SQL_NULLABLE_UNKNOWN 확장으로 지원 합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLColAttribute](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|여러 행의 데이터 페치|[SQLFetch](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|결과 집합 열 수 반환|[SQLNumResultCols](../../../odbc/reference/syntax/sqlnumresultcols-function.md)|  
|실행을 위한 문 준비|[SQLPrepare](../../../odbc/reference/syntax/sqlprepare-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
