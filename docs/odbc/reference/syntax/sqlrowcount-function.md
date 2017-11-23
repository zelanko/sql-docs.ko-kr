---
title: "SQLRowCount 함수 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
apiname: SQLRowCount
apilocation: sqlsrv32.dll
apitype: dllExport
f1_keywords: SQLRowCount
helpviewer_keywords: SQLRowCount function [ODBC]
ms.assetid: 61e00a8a-9b3b-45b9-b397-7fe818822416
caps.latest.revision: "22"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c46515b464ea694cfa6184072efb95e2459b1d00
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="sqlrowcount-function"></a>SQLRowCount 함수(SQLRowCount Function)
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLRowCount** 영향을 받는 행 수를 반환 된 **업데이트**, **삽입**, 또는 **삭제** 문;는 SQL_ADD SQL_UPDATE_BY_BOOKMARK, 또는 SQL_ DELETE_BY_BOOKMARK 작업 **SQLBulkOperations**; 또는에서 SQL_UPDATE 또는 SQL_DELETE 작업 **SQLSetPos**합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLRowCount(  
      SQLHSTMT   StatementHandle,  
      SQLLEN *   RowCountPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *RowCountPtr*  
 [출력] 반환할 행 수를 버퍼를 가리킵니다. 에 대 한 **업데이트**, **삽입**, 및 **삭제** 에 SQL_ADD, SQL_UPDATE_BY_BOOKMARK, 및 SQL_DELETE_BY_BOOKMARK 작업에 대 한 문을  **SQLBulkOperations**, 및에서 SQL_UPDATE 또는 SQL_DELETE 작업 **SQLSetPos**에 반환 된 값 **RowCountPtr* 영향을 받는 행 수는 요청 또는 영향을 받는 행 수를 사용할 수 없는 경우-1입니다.  
  
 때 **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, **SQLSetPos 또는 SQLMoreResults** 호출 되는 SQL_DIAG_ROW_COUNT 진단 데이터 구조의 필드를 행 수로 설정 하 고 행 개수를 종속 구현 방식으로 캐시 됩니다. **SQLRowCount** 캐시 된 행 개수 값을 반환 합니다. 문 핸들을 준비 또는 할당 된 상태로 다시 설정할 때까지 캐시 된 행 개수 값이 올바른지, 문을 다시 실행은, 또는 **SQLCloseCursor** 호출 됩니다. SQL_DIAG_ROW_COUNT 필드가 설정 된 이후 함수 호출 된 경우 값을 반환 하 여 참고 **SQLRowCount** SQL_DIAG_ROW_COUNT 필드는으로 다시 설정 하기 때문에 SQL_DIAG_ROW_COUNT 필드의 값과에서 다를 수 있습니다 모든 함수 호출에 의해 0입니다.  
  
 다른 문 및 함수에 대 한 드라이버에서 반환 된 값을 정의할 수 있습니다 \* *RowCountPtr*합니다. 예를 들어 일부 데이터 원본 수에서 반환 된 행의 수를 반환 하는 **선택** 문 또는 행을 인출 하기 전에 카탈로그 함수입니다.  
  
> [!NOTE]  
>  여러 데이터 소스 결과 변하면를 인출 하기 전에 집합에 행의 수를 반환할 수 없습니다. 상호 운용성을 극대화 응용 프로그램은이 동작에 의존 하지 해야 합니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLRowCount** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* SQL_의 HANDLE_STMT 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLRowCount** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLRowCount** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> (DM) 함수가 호출 하기 전에 호출 된 **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 는 에대한 *StatementHandle*합니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
  
## <a name="comments"></a>설명  
 문 핸들에서 실행 된 마지막 SQL 문이 없는 복제본이 경우는 **업데이트**, **삽입**, 또는 **삭제** 문 또는 경우에는 *작업* 에 대 한 이전 호출에서 인수 **SQLBulkOperations** 되지 않았거나 SQL_ADD, SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK, 또는 경우에는 *작업* 에대한이전호출에서인수 **SQLSetPos** 되지 않았거나 SQL_UPDATE SQL_DELETE, 값 **RowCountPtr* 는 드라이버 정의입니다. 자세한 내용은 참조 [영향을 받는 행 개수 확인](../../../odbc/reference/develop-app/determining-the-number-of-affected-rows.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
