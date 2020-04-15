---
title: 더 이상 사용되지 이상 함수 매핑 | 마이크로 소프트 문서
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
ms.openlocfilehash: a4e89cd9281520e70ec5fb289c6050e77ec6194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299883"
---
# <a name="mapping-deprecated-functions"></a>사용되지 않는 함수 매핑
이 섹션에서는 ODBC 2.x *응용* 프로그램과 함께 사용되는 ODBC *3.x* 드라이버의 이전 버전과의 호환성을 보장하기 위해 ODBC *3.x* 드라이버 관리자에서 더 이상 사용되지 않는 함수를 매핑하는 방법을 설명합니다. 드라이버 관리자는 응용 프로그램의 버전에 관계없이 이 매핑을 수행합니다. 다음 목록의 각 ODBC *2.x* 함수는 ODBC *3.x* 드라이버에서 호출될 때 해당 ODBC *3.x* 함수에 매핑되므로 ODBC *3.x* 드라이버는 ODBC *2.x* 함수를 구현할 필요가 없습니다.  
  
 드라이버가 ODBC *3.x* 드라이버이고 드라이버가 매핑되는 기능을 지원하지 않을 때 목록의 매핑이 트리거됩니다.  
  
 다음 표에는 ODBC *3.x에*도입된 모든 중복 된 기능이 나열됩니다.  
  
|ODBC *2.x* 기능|ODBC *3.x* 기능|  
|-------------------------|-------------------------|  
|**SQLAllocConnect**|**SQLAlloc핸들**|  
|**SQLAllocEnv**|**SQLAlloc핸들**|  
|**SQLAllocStmt**|**SQLAlloc핸들**|  
|**SQLBindParam**[1]|**SQLBindParameter**|  
|**SQLCol속성**|**SQLColAttribute**|  
|**SQL오류**|**SQLGetDiagRec**|  
|**SQLFreeConnect**|**SQLFreeHandle**|  
|**SQL프리엔프**|**SQLFreeHandle**|  
|SQL_DROP *옵션이* 있는 **SQLFreeStmt**|**SQLFreeHandle**|  
|**SQLGet연결 옵션**|**SQLGetConnectAttr**|  
|**SQLGetStmt옵션**|**SQLGetStmtAttr**|  
|**SQLParam옵션**|**SQLSetStmtAttr**|  
|**SQLSet연결옵션**|**SQLSetConnectAttr**|  
|**SQLSetParam**[2]|**SQLBindParameter**|  
|**SQLSet스크롤 옵션**|**SQLSetStmtAttr**|  
|**SQLSetStmt옵션**|**SQLSetStmtAttr**|  
|**SQLTransact**|**SQLEndTran**|  
  
 [1] 이 함수는 ODBC *2.x에*존재하지 않았지만 오픈 그룹 및 ISO 표준에 있습니다.  
  
 [2] ODBC 1.0 기능입니다.  
  
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
