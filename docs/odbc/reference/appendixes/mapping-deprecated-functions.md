---
title: 사용 되지 않는 함수와 매핑 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- mapping deprecated functions [ODBC], about mapping deprecated functions
- backward compatibility [ODBC], mapping deprecated functions
- deprecated functions [ODBC]
- compatibility [ODBC], mapping deprecated functions
- functions [ODBC], mapping deprecated functions
- mapping deprecated functions [ODBC]
ms.assetid: ee462617-1d79-4c88-afeb-b129cff34cc6
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 307f0f54434fdcb4ebb19c38256a7a04f4a5c46d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67990714"
---
# <a name="mapping-deprecated-functions"></a>사용되지 않는 함수 매핑
이 섹션에서는 설명 하는 방법을 사용 되지 않는 함수는 ODBC로 매핑됩니다 *3.x* ODBC의 이전 버전과 호환성을 보장 하기 위해 드라이버 관리자 *3.x* ODBC를 사용 하 여 사용 되는 드라이버 *2.x* 응용 프로그램입니다. 드라이버 관리자는 응용 프로그램의 버전에 관계 없이이 매핑을 수행합니다. 때문에 각 ODBC *2.x* 함수를 다음 목록에서 해당 ODBC에 매핑된 *3.x* ODBC에서 호출 된 경우 함수 *3.x* ODBC드라이버*3.x* 드라이버는 ODBC를 구현 하지 않아도 *2.x* 함수입니다.  
  
 드라이버는 ODBC 경우 목록에서 매핑이 트리거됩니다 *3.x* 드라이버 및 드라이버 매핑되는 함수를 지원 하지 않습니다.  
  
 다음 표에서 ODBC에 도입 된 기능을 모든 중복된 *3.x*합니다.  
  
|ODBC *2.x* 함수|ODBC *3.x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** 사용 하 여는 *옵션* SQL_DROP의|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1]에이 함수는 ODBC에 존재 하지 않았던 *2.x*, Open Group 및 ISO 표준에는 것입니다.  
  
 [2]는 ODBC 1.0 함수입니다.  
  
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
