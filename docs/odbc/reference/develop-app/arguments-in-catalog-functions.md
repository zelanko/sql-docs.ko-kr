---
title: 카탈로그 함수의 인수 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- arguments in catalog functions [ODBC]
- catalog functions [ODBC], arguments
- arguments in catalog functions [ODBC], about arguments
- functions [ODBC], catalog functions
ms.assetid: f5e0abec-8f24-42e0-b94f-16dd1f2004fd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5dd36e82b71ff862a543bfa38cda4b4a660738a8
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63287752"
---
# <a name="arguments-in-catalog-functions"></a>카탈로그 함수의 인수
모든 카탈로그 함수 인수는 응용 프로그램 반환 되는 데이터의 범위를 제한할 수 있습니다. 예를 들어, 첫 번째 및 두 번째 호출 **SQLTables** 다음 코드에서 세 번째 호출은 Orders 테이블에 대 한 정보를 반환 하는 동안에 모든 테이블에 대 한 정보를 포함 하는 집합 결과 반환 합니다.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 카탈로그 함수 문자열 인수가 네 가지 서로 다른 형식에 속합니다: 일반 인수 (OA), 패턴 값 인수 (PV), 식별자 (ID), 인수 및 값 목록 인수 (VL). 대부분의 문자열 인수는 SQL_ATTR_METADATA_ID 문 특성 값에 따라 두 가지 형식의 중 하나일 수 있습니다. 다음 표에서 각 카탈로그 함수에 대 한 인수를 나열 하 고 SQL_ATTR_METADATA_ID는 SQL_TRUE 또는 SQL_FALSE 값에 대 한 인수의 형식에 설명 합니다.  
  
|기능|인수|입력 하는 경우 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|입력 하는 경우 SQL_<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA OA OA PV|ID ID ID ID|  
|**SQLColumns**|*CatalogName* *SchemaName* *TableName* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLForeignKeys**|*PKCatalogName* *PKSchemaName* *PKTableName* *FKCatalogName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*CatalogName* *SchemaName* *ProcName* *ColumnName*|OA PV PV PV|ID ID ID ID|  
|**SQLProcedures**|*CatalogName* *SchemaName* *ProcName*|OA PV PV|ID ID ID|  
|**SQLSpecialColumns**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*CatalogName* *SchemaName* *TableName*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*CatalogName* *SchemaName* *TableName*|OA PV PV|ID ID ID|  
|**SQLTables**|*CatalogName* *SchemaName* *TableName* *TableType*|PV PV PV VL|ID ID ID  VL|  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [일반 인수](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [식별자 인수](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [값 목록 인수](../../../odbc/reference/develop-app/value-list-arguments.md)
