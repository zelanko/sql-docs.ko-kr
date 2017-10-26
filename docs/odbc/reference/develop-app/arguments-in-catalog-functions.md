---
title: "카탈로그 함수에서 인수 | Microsoft Docs"
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
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2f8939b2e1ae81c3eb171e78753e7fc3b6cc17ae
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="arguments-in-catalog-functions"></a>카탈로그 함수에서 인수
모든 카탈로그 함수는 응용 프로그램 반환 되는 데이터의 범위를 제한 하는 데 수 있는 인수를 수락 합니다. 예를 들어 첫 번째 및 두 번째에 대 한 호출 **SQLTables** 다음 코드에서 세 번째 호출은 Orders 테이블에 대 한 정보를 반환 하는 동안 모든 테이블에 대 한 정보를 포함 한 결과 집합을 반환 합니다.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 카탈로그 함수 문자열 인수는 네 가지 종류에 속하는: 일반 인수 (OA), 패턴 값 인수 (pv 준), 식별자 (ID), 인수 및 값 목록 인수 (VL). 대부분의 문자열 인수는 SQL_ATTR_METADATA_ID 문 특성의 값에 따라 두 가지 종류 중 하나의 수 있습니다. 다음 표에서 각 카탈로그 함수에 대 한 인수 목록과 SQL_ATTR_METADATA_ID는 SQL_TRUE 또는 SQL_FALSE 값에 대 한 인수의 형식을 설명 합니다.  
  
|함수|인수|유형에 사용할 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|유형에 사용할 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *열 이름*|OA OA OA PV|ID ID ID ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *열 이름*|OA PV PV PV|ID ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* * FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *열 이름*|OA PV PV PV|ID ID ID ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID ID ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID ID ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|ID ID ID VL|  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [일반 인수](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [식별자 인수](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [값 목록 인수](../../../odbc/reference/develop-app/value-list-arguments.md)

