---
description: 사용되지 않는 함수 매핑
title: 사용 되지 않는 함수 매핑 | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9c990646c54fd0d0698482c5f8dc3f87df80fe93
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429615"
---
# <a name="mapping-deprecated-functions"></a>사용되지 않는 함수 매핑
이 섹션 *에서는 odbc 2.X 드라이버 관리자* 가 사용 되지 않는 함수를 사용 하 여 odbc 2.x 응용 프로그램에서 사용 되는 odbc *3.x 드라이버의* 이전 버전과의 호환성을 보장 하는 방법을 설명 *합니다.* 드라이버 관리자는 응용 프로그램의 버전에 관계 없이이 매핑을 수행 합니다. *Odbc 3.x 드라이버에서* 호출 하는 경우 다음 목록의 *각 odbc 2.x 함수는* 해당 odbc 2.x 함수에 *매핑되므로 odbc 2.x 드라이버는* *odbc 2.x 함수를* 구현할 필요가 없습니다. *x 함수는* 다음과 같습니다.  
  
 드라이버 *는 ODBC 3.x* 드라이버이 고 드라이버는 매핑되는 함수를 지원 하지 않는 경우 목록에 있는 매핑이 트리거됩니다.  
  
 다음 표에 *는 ODBC 3.x*에 도입 된 모든 중복 된 기능이 나열 되어 있습니다.  
  
|ODBC *2.x* 함수|ODBC *3.x* 함수|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAllocHandle**|  
|**SQLAllocEnv**|**SQLAllocHandle**|  
|**SQLAllocStmt**|**SQLAllocHandle**|  
|**Sqlbindparam 함수와**[1]|**SQLBindParameter**|  
|**SQLColAttributes**|**SQLColAttribute**|  
|**SQLError**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQLFreeEnv**|**SQLFreeHandle**|  
|**SQLFreeStmt** SQL_DROP *옵션* 을 사용 하는|**SQLFreeHandle**|  
|**SQLGetConnectOption**|**SQLGetConnectAttr**|  
|**SQLGetStmtOption**|**SQLGetStmtAttr**|  
|**SQLParamOptions**|**SQLSetStmtAttr**|  
|**SQLSetConnectOption**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSetScrollOption**|**SQLSetStmtAttr**|  
|**SQLSetStmtOption**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1]이 함수 *는 ODBC 2.x*에 존재 하지 않지만 오픈 그룹 및 ISO 표준에 포함 되어 있습니다.  
  
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
