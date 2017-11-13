---
title: "매핑 사용 되지 않는 함수와 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 61d05017039673989e1477501feb17b3da6d7220
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="mapping-deprecated-functions"></a>사용 되지 않는 함수와 매핑
이 섹션에서는 어떻게 사용 되지 않는 함수를 설명 ODBC 3으로 매핑되는*.x* ODBC 3의 이전 버전과 호환성을 보장 하기 위해 드라이버 관리자*.x* 드라이버는 ODBC 2와 함께 사용 됩니다. *x* 응용 프로그램입니다. 드라이버 관리자는 응용 프로그램의 버전에 관계 없이이 매핑이 수행합니다. 때문에 각 ODBC 2. *x* 함수는 다음 목록에는 해당 ODBC 3에 매핑된*.x* ODBC 3에서 호출 된 경우 작동*.x* 드라이버에서 ODBC 3*.x*드라이버는 ODBC 2를 구현 하지 않아도 됩니다. *x* 함수입니다.  
  
 매핑 목록에는 드라이버는 ODBC 3 때 트리거되는*.x* 드라이버 및 드라이버 매핑 중인 함수를 지원 하지 않습니다.  
  
 다음 표에서 ODBC 3에 도입 된 모든 중복 된 기능*.x*합니다.  
  
|ODBC 2입니다. *x* 함수|ODBC 3*.x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** 와 *옵션* SQL_DROP의|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 하지만이 함수는 ODBC 2에 존재 하지 않기*.x*, Open Group 및 ISO 표준에 있습니다.  
  
 [2] ODBC 1.0 함수입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLAllocConnect 매핑](../../../odbc/reference/appendixes/sqlallocconnect-mapping.md)  
  
-   [SQLAllocEnv 매핑](../../../odbc/reference/appendixes/sqlallocenv-mapping.md)  
  
-   [SQLAllocStmt 매핑](../../../odbc/reference/appendixes/sqlallocstmt-mapping.md)  
  
-   [SQLBindParam 매핑](../../../odbc/reference/appendixes/sqlbindparam-mapping.md)  
  
-   [SQLColAttributes 매핑](../../../odbc/reference/appendixes/sqlcolattributes-mapping.md)  
  
-   [SQLError 매핑](../../../odbc/reference/appendixes/sqlerror-mapping.md)  
  
-   [SQLFreeConnect 매핑](../../../odbc/reference/appendixes/sqlfreeconnect-mapping.md)  
  
-   [SQLFreeEnv 매핑](../../../odbc/reference/appendixes/sqlfreeenv-mapping.md)  
  
-   [SQLFreeStmt 매핑](../../../odbc/reference/appendixes/sqlfreestmt-mapping.md)  
  
-   [SQLGetConnectOption 매핑](../../../odbc/reference/appendixes/sqlgetconnectoption-mapping.md)  
  
-   [SQLGetStmtOption 매핑](../../../odbc/reference/appendixes/sqlgetstmtoption-mapping.md)  
  
-   [SQLInstallTranslator 매핑](../../../odbc/reference/appendixes/sqlinstalltranslator-mapping.md)  
  
-   [SQLParamOptions 매핑](../../../odbc/reference/appendixes/sqlparamoptions-mapping.md)  
  
-   [SQLSetConnectOption 매핑](../../../odbc/reference/appendixes/sqlsetconnectoption-mapping.md)  
  
-   [SQLSetParam 매핑](../../../odbc/reference/appendixes/sqlsetparam-mapping.md)  
  
-   [SQLSetScrollOptions 매핑](../../../odbc/reference/appendixes/sqlsetscrolloptions-mapping.md)  
  
-   [SQLSetStmtOption 매핑](../../../odbc/reference/appendixes/sqlsetstmtoption-mapping.md)  
  
-   [SQLTransact 매핑](../../../odbc/reference/appendixes/sqltransact-mapping.md)

