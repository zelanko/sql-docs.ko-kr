---
title: ODBC 3.x 드라이버 작성 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- upgrading drivers [ODBC]
- ODBC drivers [ODBC], upgrading
- backward compatibility [ODBC], drivers
- compatibility [ODBC], drivers
ms.assetid: 9b75f59b-623f-4711-9ca2-e751b3622e00
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fb403cef47f901cdb43bbb32c669ba68aa34913d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68078900"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x 드라이버 작성
다음 표에서는 ODBC 3의 함수 지원을 보여 줍니다. *x* 드라이버와 odbc 응용 프로그램, 그리고 odbc 3에 대해 함수가 호출 될 때 드라이버 관리자에서 수행 하는 매핑 *x* 드라이버.  
  
|함수|지원됨<br /><br /> by<br /><br /> ODBC 3. *x*<br /><br /> 요소?|지원됨<br /><br /> by<br /><br /> ODBC 3. *x*<br /><br /> 프로그램별?|매핑/지원 됨<br /><br /> ODBC 3. *x*<br /><br /> 드라이버 관리자<br /><br /> ODBC 3. *x* 드라이버 인가요?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|예|아니요 [1]|yes|  
|**SQLAllocEnv**|예|아니요 [1]|yes|  
|**SQLAllocHandle**|yes|yes|예|  
|**SQLAllocStmt**|예|아니요 [1]|yes|  
|**SQLBindCol**|yes|yes|예|  
|**Sqlbindparam 함수와**|예|예 [2]|yes|  
|**SQLBindParameter**|yes|yes|예|  
|**SQLBrowseConnect**|yes|yes|예|  
|**SQLBulkOperations**|yes|yes|예|  
|**SQLCancel**|yes|yes|예|  
|**SQLCloseCursor**|yes|yes|예|  
|**SQLColAttribute**|yes|yes|예|  
|**SQLColAttributes**|아니요 [3]|예|yes|  
|**SQLColumnPrivileges**|yes|yes|예|  
|**SQLColumns**|yes|yes|예|  
|**SQLConnect**|yes|yes|예|  
|**SQLCopyDesc**|yes|yes|예 [4]|  
|**SQLDataSources**|예|yes|yes|  
|**SQLDescribeCol**|yes|yes|예|  
|**SQLDescribeParam**|yes|yes|예|  
|**SQLDisconnect**|yes|yes|예|  
|**SQLDriverConnect**|yes|yes|예|  
|**SQLDrivers**|예|yes|yes|  
|**SQLEndTran**|yes|yes|예|  
|**SQLError**|예|아니요 [1]|yes|  
|**SQLExecDirect**|yes|yes|예|  
|**SQLExecute**|yes|yes|예|  
|**SQLExtendedFetch**|yes|예|예|  
|**SQLFetch**|yes|yes|예|  
|**SQLFetchScroll**|yes|yes|예|  
|**SQLForeignKeys**|yes|yes|예|  
|**SQLFreeConnect**|예|예 [1]|yes|  
|**SQLFreeEnv**|예|예 [1]|yes|  
|**SQLFreeHandle**|yes|yes|예|  
|**SQLFreeStmt**|yes|yes|예|  
|**SQLGetConnectAttr**|yes|yes|예|  
|**SQLGetConnectOption**|아니요 [5]|아니요 [1]|yes|  
|**SQLGetCursorName**|yes|yes|예|  
|**SQLGetData**|yes|yes|예|  
|**SQLGetDescField**|yes|yes|예|  
|**SQLGetDescRec**|yes|yes|예|  
|**SQLGetDiagField**|yes|yes|예|  
|**SQLGetDiagRec**|yes|yes|예|  
|**SQLGetEnvAttr**|yes|yes|예|  
|**SQLGetFunctions**|아니요 [6]|yes|yes|  
|**SQLGetInfo**|yes|yes|예|  
|**SQLGetStmtAttr**|yes|yes|예|  
|**SQLGetStmtOption**|아니요 [5]|아니요 [1]|yes|  
|**SQLGetTypeInfo**|yes|yes|예|  
|**SQLMoreResults**|yes|yes|예|  
|**SQLNativeSql**|yes|yes|예|  
|**SQLNumParams**|yes|yes|예|  
|**SQLNumResultCols**|yes|yes|예|  
|**SQLParamData**|yes|yes|예|  
|**SQLParamOptions**|예|예|yes|  
|**SQLPrepare**|yes|yes|예|  
|**SQLPrimaryKeys**|yes|yes|예|  
|**SQLProcedureColumns**|yes|yes|예|  
|**SQLProcedures**|yes|yes|예|  
|**SQLPutData**|yes|yes|예|  
|**SQLRowCount**|yes|yes|예|  
|**SQLSetConnectAttr**|yes|yes|예|  
|**SQLSetConnectOption**|아니요 [5]|아니요 [1]|yes|  
|**SQLSetCursorName**|yes|yes|예|  
|**SQLSetDescField**|yes|yes|예|  
|**SQLSetDescRec**|yes|yes|예|  
|**SQLSetEnvAttr**|yes|yes|예|  
|**SQLSetPos**|yes|yes|예|  
|**SQLSetParam**|예|예|yes|  
|**SQLSetScrollOption**|yes|yes|예|  
|**SQLSetStmtAttr**|yes|yes|예|  
|**SQLSetStmtOption**|아니요 [5]|아니요 [1]|yes|  
|**SQLSpecialColumns**|yes|yes|예|  
|**SQLStatistics**|yes|yes|예|  
|**SQLTablePrivileges**|yes|yes|예|  
|**SQLTables**|yes|yes|예|  
|**SQLTransact**|예|아니요 [1]|yes|  
  
 [1]이 함수는 ODBC 3에서 더 이상 사용 되지 않습니다. *x*. ODBC 3. *x* 응용 프로그램은이 함수를 사용 하지 않아야 합니다. 그러나 개방형 그룹 또는 ISO CLI 규격 응용 프로그램은이 함수를 호출할 수 있습니다.  
  
 [2] ODBC 3. *x* 응용 프로그램은 **sqlbindparam 함수와**대신 **SQLBindParameter** 를 사용 해야 합니다. 그러나 개방형 그룹 또는 ISO CLI 규격 응용 프로그램은이 함수를 호출할 수 있습니다.  
  
 [3] 드라이버 작성자는 ODBC 2를 확인 해야 합니다. *x* 열 특성 SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE 및 SQL_COLUMN_LENGTH는 **sqlcolattribute**에서 지원 되어야 합니다.  
  
 [4] **Sqlcopydesc** 는 다른 드라이버에 속하는 연결 간에 설명자를 복사할 때 드라이버 관리자에 의해 부분적으로 구현 됩니다. 드라이버는 자체 연결의 두 연결에서 **Sqlcopydesc** 를 지 원하는 데 필요 합니다. 드라이버 관리자만이 구현 하는 **Sqldrivers**와 같은 함수는이 목록에 표시 되지 않습니다.  
  
 [5] 특정 상황에서는 드라이버가이 기능을 지원 해야 할 수 있습니다. 자세한 내용은이 함수의 참조 페이지를 참조 하세요.  
  
 [6] 드라이버에서 지 원하는 함수 집합이 연결에 따라 달라 지는 경우 **SQLGetFunctions** 지원 하도록 선택할 수 있습니다.
