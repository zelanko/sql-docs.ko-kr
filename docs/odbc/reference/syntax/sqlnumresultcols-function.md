---
title: SQLNumResultCols 함수 | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2019
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
apiname:
- SQLNumResultCols
apilocation:
- sqlsrv32.dll
- odbc32.dll
apitype: dllExport
f1_keywords:
- SQLNumResultCols
helpviewer_keywords:
- SQLNumResultCols function [ODBC]
ms.assetid: d863179f-12a9-4b55-ac6b-7d84202d3da3
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 43c7f72869cf46fa12f942a3d31399cf3e316520
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68343552"
---
# <a name="sqlnumresultcols-function"></a>SQLNumResultCols 함수
**규칙**  
 소개 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **Sqlnumresultcols** 는 결과 집합의 열 수를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```cpp  
  
SQLRETURN SQLNumResultCols(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ColumnCountPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 입력 문 핸들입니다.  
  
 *ColumnCountPtr*  
 출력 결과 집합의 열 수를 반환할 버퍼에 대 한 포인터입니다. 이 개수는 바인딩된 책갈피 열을 포함 하지 않습니다.  
  
## <a name="returns"></a>반환  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE입니다.  
  
## <a name="diagnostics"></a>진단  
 **Sqlnumresultcols** 가 SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 반환할 때 SQL_HANDLE_STMT의 *HandleType* 및 *StatementHandle* *핸들* 을 사용 하 여 **SQLGetDiagRec** 를 호출 하면 연결 된 SQLSTATE 값을 얻을 수 있습니다. 다음 표에서는 일반적으로 **Sqlnumresultcols** 에서 반환 하는 SQLSTATE 값을 나열 하 고이 함수의 컨텍스트에서 각 항목에 대해 설명 합니다. "(DM)" 표기법은 드라이버 관리자에서 반환 된 SQLSTATEs의 설명 보다 앞에 나옵니다. 다른 설명이 없는 한 각 SQLSTATE 값과 연결 된 반환 코드는 SQL_ERROR 됩니다.  
  
|SQLSTATE|Error|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. 함수는 SQL_SUCCESS_WITH_INFO를 반환 합니다.|  
|08S01|통신 연결 오류|드라이버가 연결 된 드라이버와 데이터 원본 간의 통신 연결이 함수 처리를 완료 하기 전에 실패 했습니다.|  
|HY000|일반 오류|특정 SQLSTATE가 없고 구현 별 SQLSTATE가 정의 되지 않은 오류가 발생 했습니다. MessageText 버퍼에서 **SQLGetDiagRec** 에 의해 반환 되는 오류 메시지는 오류 및 해당 원인을 설명 합니다. * \**|  
|HY001|메모리 할당 오류|드라이버에서 함수 실행 또는 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업 취소됨|*StatementHandle*에 대해 비동기 처리를 사용 하도록 설정 했습니다. 함수가 호출 되었으며 실행이 완료 되기 전에 **sqlcancel** 또는 **Sqlcancelhandle** 이 *StatementHandle*에 대해 호출 되었습니다. 그런 다음 *StatementHandle*에서 함수를 다시 호출 했습니다.<br /><br /> 함수가 호출 되 고 실행이 완료 되기 전에 **sqlcancel** 또는 **sqlcancelhandle** 이 다중 스레드 응용 프로그램의 다른 스레드에서 *StatementHandle* 호출 되었습니다.|  
|HY010|함수 시퀀스 오류|(DM) *StatementHandle*연결 된 연결 핸들에 대해 비동기적으로 실행 되는 함수가 호출 되었습니다. **SQLNumResultsCols** 함수가 호출 될 때이 비동기 함수는 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**또는 **SQLMoreResults** 가 *StatementHandle* 에 대해 호출 되 고 SQL_PARAM_DATA_AVAILABLE 반환 되었습니다. 이 함수는 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에 호출 되었습니다.<br /><br /> (DM) *StatementHandle*에 대해 **Sqlprepare** 또는 **sqlexecdirect** 를 호출 하기 전에 함수가 호출 되었습니다.<br /><br /> (DM) *StatementHandle* 에 대해 비동기적으로 실행 되는 함수 (이 함수 아님)가 호출 되었으며이 함수가 호출 될 때 계속 실행 중입니다.<br /><br /> (DM) **Sqlexecute**, **sqlexecdirect**, **SQLBulkOperations**또는 **SQLSetPos** 가 *StatementHandle* 에 대해 호출 되 고 SQL_NEED_DATA 반환 되었습니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대해 데이터를 보내기 전에 호출 되었습니다.<br /><br /> 문 핸들을 해제할 수 있는 경우에 대 한 자세한 내용은 [Sqlprepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md) 를 참조 하세요.|  
|HY013|메모리 관리 오류|메모리 부족 상태로 인해 기본 메모리 개체에 액세스할 수 없기 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|알 수 없는 트랜잭션 상태로 인해 연결이 일시 중단 되었습니다. 연결 끊기 및 읽기 전용 함수만 허용 됩니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 [Sqlendtran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)를 참조 하세요.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 원본이 요청에 응답 하기 전에 연결 제한 시간이 만료 되었습니다. 연결 제한 시간은 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT을 통해 설정 됩니다.|  
|IM001|드라이버가이 기능을 지원 하지 않습니다.|(DM) *StatementHandle* 연결 된 드라이버는 함수를 지원 하지 않습니다.|  
|IM017|비동기 알림 모드에서는 폴링을 사용할 수 없습니다.|알림 모델을 사용할 때마다 폴링은 사용 하지 않도록 설정 됩니다.|  
|IM018|이 핸들에서 이전 비동기 작업을 완료 하기 위해 **SQLCompleteAsync** 가 호출 되지 않았습니다.|핸들에 대 한 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드가 설정 된 경우에는 핸들에 대해 **SQLCompleteAsync** 를 호출 하 여 사후 처리를 수행 하 고 작업을 완료 해야 합니다.|  
  
 **Sqlnumresultcols** 는 데이터 원본이 문과 연결 된 SQL 문을 평가 하는 시점에 따라 sqlprepare 및 **sqlexecute** **이전에 호출** 될 때 **sqlprepare** 또는 **sqlexecute** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 있습니다.  
  
## <a name="comments"></a>주석  
 **Sqlnumresultcols** 는 문이 준비, 실행 또는 배치 된 상태에 있는 경우에만 성공적으로 호출할 수 있습니다.  
  
 *StatementHandle* 와 연결 된 문이 열을 반환 하지 않는 경우 **Sqlnumresultcols** 는 **columncountptr* 을 0으로 설정 합니다.  
  
 **Sqlnumresultcols** 에서 반환 하는 열 수는 IRD의 SQL_DESC_COUNT 필드와 동일한 값입니다.  
  
 자세한 내용은 [생성 된 결과 집합](../../../odbc/reference/develop-app/was-a-result-set-created.md) 및 [메타 데이터를 사용 하는 방법](../../../odbc/reference/develop-app/how-is-metadata-used.md)을 참조 하세요.  
  
## <a name="related-functions"></a>관련 함수  
  
|원하는 정보|참조 항목|  
|---------------------------|---------|  
|결과 집합의 열에 버퍼 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리 취소|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLColAttribute 함수(SQLColAttribute Function)](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|결과 집합의 열에 대 한 정보 반환|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문 실행|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록 가져오기 또는 결과 집합을 통한 스크롤|[SQLFetchScroll 함수(SQLFetchScroll Function)](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|정방향 전용 방향으로 단일 행 또는 데이터 블록 페치|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|데이터 열의 일부 또는 전체를 가져오는 중|[SQLGetData 함수(SQLGetData Function)](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|실행할 SQL 문 준비|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|커서 스크롤 옵션 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>참고 항목  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
