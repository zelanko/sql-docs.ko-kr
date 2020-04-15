---
title: ODBC 3.x 드라이버 작성 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 62f2a701fd5ac94c92d41494a4fd1ab023edaf25
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300363"
---
# <a name="writing-odbc-3x-drivers"></a>ODBC 3.x 드라이버 작성
다음 표에서는 ODBC 3의 함수 지원을 보여 주며, 이에 대한 지원은 다음과 같은 것입니다. *x* 드라이버 및 ODBC 응용 프로그램 및 ODBC 3에 대해 함수가 호출될 때 드라이버 관리자가 수행하는 매핑입니다. *x* 드라이버.  
  
|함수|지원됨<br /><br /> 로<br /><br /> ODBC 3. *x*<br /><br /> 드라이버?|지원됨<br /><br /> 로<br /><br /> ODBC 3. *x*<br /><br /> 응용 프로그램?|매핑/지원<br /><br /> ODBC 3. *x*<br /><br /> 드라이버 관리자를 통해<br /><br /> ODBC 3. *X* 드라이버?|  
|--------------|----------------------------------------------------|---------------------------------------------------------|---------------------------------------------------------------------------------------------|  
|**SQLAllocConnect**|예|아니오[1]|예|  
|**SQLAllocEnv**|예|아니오[1]|예|  
|**SQLAlloc핸들**|예|예|예|  
|**SQLAllocStmt**|예|아니오[1]|예|  
|**SQLBindCol**|예|예|예|  
|**SQLBindParam**|예|예[2]|예|  
|**SQLBindParameter**|예|예|예|  
|**SQLBrowseConnect**|예|예|예|  
|**SQLBulk운영**|예|예|예|  
|**SQLCancel**|예|예|예|  
|**SQLCloseCursor**|예|예|예|  
|**SQLColAttribute**|예|예|예|  
|**SQLCol속성**|아니오[3]|예|예|  
|**SQLColumnPrivileges**|예|예|예|  
|**SQLColumns**|예|예|예|  
|**SQLConnect**|예|예|예|  
|**SQLCopyDesc**|예|예|예[4]|  
|**SQLDataSource**|예|예|예|  
|**SQLDescribeCol**|예|예|예|  
|**SQLDescribeParam**|예|예|예|  
|**SQL분리**|예|예|예|  
|**SQLDriverConnect**|예|예|예|  
|**SQLDrivers**|예|예|예|  
|**SQLEndTran**|예|예|예|  
|**SQL오류**|예|아니오[1]|예|  
|**SQLExecDirect**|예|예|예|  
|**SQLExecute**|예|예|예|  
|**SQLExtendedFetch**|예|예|예|  
|**SQLFetch**|예|예|예|  
|**SQLFetchScroll**|예|예|예|  
|**SQLForeignKeys**|예|예|예|  
|**SQLFreeConnect**|예|예[1]|예|  
|**SQL프리엔프**|예|예[1]|예|  
|**SQLFreeHandle**|예|예|예|  
|**SQLFreeStmt**|예|예|예|  
|**SQLGetConnectAttr**|예|예|예|  
|**SQLGet연결 옵션**|아니오[5]|아니오[1]|예|  
|**SQLGetCursorName**|예|예|예|  
|**SQLGetData**|예|예|예|  
|**SQLGetDescField**|예|예|예|  
|**SQLGetDescRec**|예|예|예|  
|**SQLGetDiagField**|예|예|예|  
|**SQLGetDiagRec**|예|예|예|  
|**SQLGetEnvAttr**|예|예|예|  
|**SQLGetFunctions**|아니오[6]|예|예|  
|**SQLGetInfo**|예|예|예|  
|**SQLGetStmtAttr**|예|예|예|  
|**SQLGetStmt옵션**|아니오[5]|아니오[1]|예|  
|**SQLGetTypeInfo**|예|예|예|  
|**SQLMoreResults**|예|예|예|  
|**SQLNativeSql**|예|예|예|  
|**SQLNumParams**|예|예|예|  
|**SQLNumResultCols**|예|예|예|  
|**SQLParamData**|예|예|예|  
|**SQLParam옵션**|예|예|예|  
|**SQLPrepare**|예|예|예|  
|**SQLPrimaryKeys**|예|예|예|  
|**SQLProcedureColumns**|예|예|예|  
|**SQLProcedures**|예|예|예|  
|**SQLPutData**|예|예|예|  
|**SQLRowCount**|예|예|예|  
|**SQLSetConnectAttr**|예|예|예|  
|**SQLSet연결옵션**|아니오[5]|아니오[1]|예|  
|**SQLSetCursorName**|예|예|예|  
|**SQLSetDescField**|예|예|예|  
|**SQLSetDescRec**|예|예|예|  
|**SQLSetEnvAttr**|예|예|예|  
|**SQLSetPos**|예|예|예|  
|**SQLSetParam**|예|예|예|  
|**SQLSet스크롤 옵션**|예|예|예|  
|**SQLSetStmtAttr**|예|예|예|  
|**SQLSetStmt옵션**|아니오[5]|아니오[1]|예|  
|**SQLSpecialColumns**|예|예|예|  
|**SQLStatistics**|예|예|예|  
|**SQLTablePrivileges**|예|예|예|  
|**SQLTables**|예|예|예|  
|**SQLTransact**|예|아니오[1]|예|  
  
 [1] 이 함수는 ODBC 3에서 더 이상 사용되지 않습니다. *x*. ODBC 3. *x* 응용 프로그램은 이 함수를 사용해서는 안 됩니다. 그러나 개방형 그룹 또는 ISO CLI 호환 응용 프로그램은 이 함수를 호출할 수 있습니다.  
  
 [2] ODBC 3. *x* 응용 프로그램은 SQLBindParam 대신 **SQLBind매개 변수를** 사용해야합니다. **SQLBindParam** 그러나 개방형 그룹 또는 ISO CLI 호환 응용 프로그램은 이 함수를 호출할 수 있습니다.  
  
 [3] 드라이버 작성기는 ODBC 2에 유의해야 한다. *x* 열 특성SQL_COLUMN_PRECISION, SQL_COLUMN_SCALE 및 SQL_COLUMN_LENGTH **SQLColAttribute**.  
  
 [4] **SQLCopyDesc는** 설명자가 다른 드라이버에 속하는 연결에서 복사될 때 드라이버 관리자에 의해 부분적으로 구현됩니다. 드라이버는 두 개의 자체 연결에서 **SQLCopyDesc을** 지원해야 합니다. 드라이버 관리자에서만 구현되는 **SQLDriver와**같은 함수는 이 목록에 나타나지 않습니다.  
  
 [5] 특정 상황에서 는 드라이버가 이 기능을 지원해야 할 수 있습니다. 자세한 내용은 이 함수의 참조 페이지를 참조하십시오.  
  
 [6] 드라이버가 지원하는 함수 집합이 연결마다 다른 경우 **드라이버는 SQLGetFunctions를** 지원하도록 선택할 수 있습니다.
