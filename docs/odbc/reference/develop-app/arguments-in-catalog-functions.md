---
title: 카탈로그 함수의 인수 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 819c10d0b137d5e0999c1e10bf22810392509f76
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81288169"
---
# <a name="arguments-in-catalog-functions"></a>카탈로그 함수의 인수
모든 카탈로그 함수는 응용 프로그램이 반환되는 데이터의 범위를 제한할 수 있는 인수를 수락합니다. 예를 들어 다음 코드에서 **SQLTables에** 대한 첫 번째 및 두 번째 호출은 모든 테이블에 대한 정보를 포함하는 결과 집합을 반환하고 세 번째 호출은 Orders 테이블에 대한 정보를 반환합니다.  
  
```  
SQLTables(hstmt1, NULL, 0, NULL, 0, NULL, 0, NULL, 0);  
SQLTables(hstmt2, NULL, 0, NULL, 0, "%", SQL_NTS, NULL, 0);  
SQLTables(hstmt3, NULL, 0, NULL, 0, "Orders", SQL_NTS, NULL, 0);  
```  
  
 카탈로그 함수 문자열 인수는 일반 인수(OA), 패턴 값 인수(PV), 식별자 인수(ID) 및 값 목록 인수(VL)의 네 가지 유형으로 나뉩니다. 대부분의 문자열 인수는 SQL_ATTR_METADATA_ID 문 특성의 값에 따라 두 가지 형식 중 하나일 수 있습니다. 다음 표는 각 카탈로그 함수에 대한 인수를 나열하고 SQL_ATTR_METADATA_ID SQL_TRUE 또는 SQL_FALSE 값에 대한 인수의 형식을 설명합니다.  
  
|함수|인수|SQL_ 때 입력<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_FALSE|SQL_ 때 입력<br /><br /> ATTR_METADATA_<br /><br /> ID = SQL_TRUE|  
|--------------|--------------|---------------------------------------------------------------|--------------------------------------------------------------|  
|**SQLColumnPrivileges**|*카탈로그이름* *스키마네임* *테이블네임* *열이름*|OA OA OA PV|ID ID ID ID|  
|**SQLColumns**|*카탈로그이름* *스키마네임* *테이블네임* *열이름*|OA PV PV PV|ID ID ID ID|  
|**SQLForeignKeys**|*PKCatalogname* *PKSchemaName* *PKtableName* *FKCatalogName FKSchemaName* *FKSchemaName* *FKTableName*|OA OA OA OA OA OA|ID ID ID ID ID ID|  
|**SQLPrimaryKeys**|*카탈로그이름* *스키마네임* *테이블네임*|OA OA OA|ID ID ID|  
|**SQLProcedureColumns**|*카탈로그 이름* *스키마네임* *ProcName* *열 이름*|OA PV PV PV|ID ID ID ID|  
|**SQLProcedures**|*카탈로그 이름* *스키마네임* *ProcName*|OA PV PV|ID ID ID|  
|**SQLSpecialColumns**|*카탈로그이름* *스키마네임* *테이블네임*|OA OA OA|ID ID ID|  
|**SQLStatistics**|*카탈로그이름* *스키마네임* *테이블네임*|OA OA OA|ID ID ID|  
|**SQLTablePrivileges**|*카탈로그이름* *스키마네임* *테이블네임*|OA PV PV|ID ID ID|  
|**SQLTables**|*카탈로그이름* *스키마네임* *테이블유형* *TableType*|PV PV PV VL|ID ID ID VL|  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [일반 인수](../../../odbc/reference/develop-app/ordinary-arguments.md)  
  
-   [패턴 값 인수](../../../odbc/reference/develop-app/pattern-value-arguments.md)  
  
-   [식별자 인수](../../../odbc/reference/develop-app/identifier-arguments.md)  
  
-   [값 목록 인수](../../../odbc/reference/develop-app/value-list-arguments.md)
