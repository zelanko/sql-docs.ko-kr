---
title: SQLNumResultCols 함수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
apiname:
- SQLNumResultCols
apilocation:
- sqlsrv32.dll
apitype: dllExport
f1_keywords:
- SQLNumResultCols
helpviewer_keywords:
- SQLNumResultCols function [ODBC]
ms.assetid: d863179f-12a9-4b55-ac6b-7d84202d3da3
caps.latest.revision: 22
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: cee8f6041fbd0718da6e6710df0fb89c45200c99
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlnumresultcols-function"></a>SQLNumResultCols 함수
**규칙**  
 도입 된 버전: ODBC 1.0 표준 준수: ISO 92  
  
 **요약**  
 **SQLNumResultCols** 결과 집합의 열 수를 반환 합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
SQLRETURN SQLNumResultCols(  
     SQLHSTMT        StatementHandle,  
     SQLSMALLINT *   ColumnCountPtr);  
```  
  
## <a name="arguments"></a>인수  
 *StatementHandle*  
 [입력] 문 핸들입니다.  
  
 *ColumnCountPtr*  
 [출력] 결과에서 열 수를 반환 하는 버퍼에 대 한 포인터를 설정 합니다. 이 계산에 바인딩된 책갈피 열을 포함 되지 않습니다.  
  
## <a name="returns"></a>반환 값  
 SQL_SUCCESS, SQL_SUCCESS_WITH_INFO, SQL_STILL_EXECUTING, SQL_ERROR 또는 SQL_INVALID_HANDLE 합니다.  
  
## <a name="diagnostics"></a>진단  
 때 **SQLNumResultCols** SQL_ERROR 또는 SQL_SUCCESS_WITH_INFO를 관련된 된 SQLSTATE 값 반환을 호출 하 여 얻을 수 있습니다 **SQLGetDiagRec** 와 *HandleType* 의 여는 및 *처리* 의 *StatementHandle*합니다. 다음 표에서 일반적으로 반환 하는 SQLSTATE 값 **SQLNumResultCols** 컨텍스트에서이 함수를 각각에 설명 하 고 "DM ()" 표기법 앞의 드라이버 관리자에서 반환 된 Sqlstate 설명 합니다. 각 SQLSTATE 값과 관련 된 반환 코드는 다른 설명이 없는 경우 SQL_ERROR를는 합니다.  
  
|SQLSTATE|오류|Description|  
|--------------|-----------|-----------------|  
|01000|일반 경고|드라이버 관련 정보 메시지입니다. (함수는 SQL_SUCCESS_WITH_INFO를 반환합니다.)|  
|08S01|통신 연결 오류|함수가 완료 되었습니다. 처리 하기 전에 드라이버 및 드라이버 연결 된 데이터 원본 간에 통신 링크 하지 못했습니다.|  
|HY000|일반 오류|오류가 없는 특정 SQLSTATE 했습니다는 대 한 구현 별 SQLSTATE 없는 정의 된 발생 했습니다. 반환 된 오류 메시지 **SQLGetDiagRec** 에  *\*MessageText* 버퍼에는 오류와 원인에 설명 합니다.|  
|HY001|메모리 할당 오류가 발생 했습니다.|드라이버가 실행 또는 함수 완료를 지 원하는 데 필요한 메모리를 할당할 수 없습니다.|  
|HY008|작업이 취소 됨|비동기 처리를 사용 하도록 설정할는 *StatementHandle*합니다. 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle*; 함수가에서 다시 호출 후 *StatementHandle*합니다.<br /><br /> 함수를 호출 하 고, 실행을 완료 하기 전에 **SQLCancel** 또는 **SQLCancelHandle** 에서 호출 된는 *StatementHandle* 의 서로 다른 스레드에서 다중 스레드 응용 프로그램입니다.|  
|HY010|함수 시퀀스 오류입니다.|DM ()는 비동기적으로 실행 중인 함수를 호출한 연관 된 연결 핸들에 대 한는 *StatementHandle*합니다. 이 비동기 함수 계속 실행 될 때는 **SQLNumResultsCols** 함수를 호출 했습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, 또는 **SQLMoreResults** 에 대 한 호출 된는 *StatementHandle* SQL_PARAM_DATA_ 반환 사용할 수 있습니다. 모든 스트리밍된 매개 변수에 대 한 데이터를 검색 하기 전에이 함수가 호출 되었습니다.<br /><br /> (DM) 함수가 호출 하기 전에 호출 된 **SQLPrepare** 또는 **SQLExecDirect** 에 대 한는 *StatementHandle*합니다.<br /><br /> DM ()를 비동기적으로 실행 중인 함수 (하지이 하나)에 대해 호출 되었습니다는 *StatementHandle* 호출 되었을 때 계속 실행 하 고 있습니다.<br /><br /> (DM) **SQLExecute**, **SQLExecDirect**, **SQLBulkOperations**, 또는 **SQLSetPos** 가 대 한 호출에서  *StatementHandle* SQL_NEED_DATA를 반환 합니다. 이 함수는 모든 실행 시 데이터 매개 변수 또는 열에 대 한 데이터를 보내기 전에 호출 되었습니다.<br /><br /> 참조 [SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md) 문 핸들을 해제할 수 있도록 하는 경우에 대 한 내용은 합니다.|  
|HY013|메모리 관리 오류입니다.|기본 메모리 개체에 액세스할 수 없습니다, 가능한 메모리 부족 때문에 함수 호출을 처리할 수 없습니다.|  
|HY117|연결 알 수 없는 트랜잭션 상태로 인해 일시 중단 됩니다. 만 연결을 끊고 읽기 전용 함수를 사용할 수 있습니다.|(DM) 일시 중단 된 상태에 대 한 자세한 내용은 참조 [SQLEndTran 함수](../../../odbc/reference/syntax/sqlendtran-function.md)합니다.|  
|HYT01|연결 제한 시간이 만료 되었습니다.|데이터 소스는 요청에 응답 하기 전에 연결 제한 시간에 만료 되었습니다. 연결 제한 시간을 통해 설정 됩니다 **SQLSetConnectAttr**, SQL_ATTR_CONNECTION_TIMEOUT 합니다.|  
|IM001|드라이버는이 함수를 지원 하지 않습니다.|(DM)와 관련 된 드라이버의 *StatementHandle* 함수를 지원 하지 않습니다.|  
|IM017|폴링 비동기 알림 모드 사용 불가능|알림 모델을 사용할 때마다 폴링 사용할 수 없습니다.|  
|IM018|**SQLCompleteAsync** 이 핸들에서 이전 비동기 작업을 완료 하는 호출 되지 않았습니다.|핸들에 대해 이전 함수 호출이 SQL_STILL_EXECUTING을 반환 하 고 알림 모드를 설정 하는 경우 **SQLCompleteAsync** 사후 처리를 수행 하 고 작업을 완료에 대 한 핸들에서 호출 해야 합니다.|  
  
 **SQLNumResultCols** 에서 반환 될 수 있는 모든 SQLSTATE를 반환할 수 **SQLPrepare** 또는 **SQLExecute** 호출 **SQLPrepare** 하기전에 **SQLExecute**데이터 원본 문과 연결 된 SQL 문을 계산 하는 경우에 따라 합니다.  
  
## <a name="comments"></a>설명  
 **SQLNumResultCols** 문을 준비, 실행, 또는 위치 지정 상태에 있을 때에 성공적으로 호출할 수 있습니다.  
  
 와 관련 된 문이 *StatementHandle* 열을 반환 하지 않는 **SQLNumResultCols** 설정 **ColumnCountPtr* 을 0으로 합니다.  
  
 반환 된 열 수가 **SQLNumResultCols** IRD의 SQL_DESC_COUNT 필드와 동일한 값입니다.  
  
 자세한 내용은 참조 [는 결과 집합 생성 된?](../../../odbc/reference/develop-app/was-a-result-set-created.md) 및 [메타 데이터 사용 하는 방법을?](../../../odbc/reference/develop-app/how-is-metadata-used.md)합니다.  
  
## <a name="related-functions"></a>관련 함수  
  
|내용|참조 항목|  
|---------------------------|---------|  
|버퍼를 결과 집합의 열에 바인딩|[SQLBindCol 함수](../../../odbc/reference/syntax/sqlbindcol-function.md)|  
|문 처리를 취소합니다.|[SQLCancel 함수](../../../odbc/reference/syntax/sqlcancel-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLColAttribute 함수](../../../odbc/reference/syntax/sqlcolattribute-function.md)|  
|결과 집합의 열에 대 한 정보를 반환합니다.|[SQLDescribeCol 함수](../../../odbc/reference/syntax/sqldescribecol-function.md)|  
|SQL 문 실행|[SQLExecDirect 함수](../../../odbc/reference/syntax/sqlexecdirect-function.md)|  
|준비 된 SQL 문을 실행합니다.|[SQLExecute 함수](../../../odbc/reference/syntax/sqlexecute-function.md)|  
|데이터 블록을 인출 또는 스크롤 하는 결과 집합|[SQLFetchScroll 함수](../../../odbc/reference/syntax/sqlfetchscroll-function.md)|  
|단일 행 이나 앞 으로만 이동 가능한 방향의 데이터 블록을 인출합니다.|[SQLFetch 함수](../../../odbc/reference/syntax/sqlfetch-function.md)|  
|일부 또는 전체 데이터 열을 인출합니다.|[SQLGetData 함수](../../../odbc/reference/syntax/sqlgetdata-function.md)|  
|실행에 대 한 SQL 문을 준비합니다.|[SQLPrepare 함수](../../../odbc/reference/syntax/sqlprepare-function.md)|  
|커서 스크롤 옵션 설정|[SQLSetStmtAttr 함수](../../../odbc/reference/syntax/sqlsetstmtattr-function.md)|  
  
## <a name="see-also"></a>관련 항목:  
 [ODBC API 참조](../../../odbc/reference/syntax/odbc-api-reference.md)   
 [ODBC 헤더 파일](../../../odbc/reference/install/odbc-header-files.md)
