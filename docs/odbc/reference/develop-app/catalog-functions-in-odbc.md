---
title: ODBC의 카탈로그 기능 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c6731018b99f2f3043e48ee7c174a08cb9ef71fc
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306234"
---
# <a name="catalog-functions-in-odbc"></a>ODBC의 카탈로그 함수
ODBC에는 다음 카탈로그 함수가 포함되어 있습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**SQLTables**|데이터 원본에서 카탈로그, 스키마, 테이블 또는 테이블 유형 목록을 반환합니다.|  
|**SQLColumns**|하나 이상의 테이블에서 열 목록을 반환합니다.|  
|**SQLStatistics**|단일 테이블에 대한 통계 목록을 반환합니다. 또한 해당 테이블과 연결된 인덱스 목록을 반환합니다.|  
|**SQLSpecialColumns**|단일 테이블에서 행을 고유하게 식별하는 열 목록을 반환합니다. 또한 자동으로 업데이트되는 해당 테이블의 열 목록을 반환합니다.|  
|**SQLPrimaryKeys**|단일 테이블의 기본 키를 구성하는 열 목록을 반환합니다.|  
|**SQLForeignKeys**|단일 테이블의 외래 키 목록 또는 단일 테이블을 참조하는 다른 테이블의 외래 키 목록을 반환합니다.|  
|**SQLTablePrivileges**|하나 이상의 테이블과 연결된 권한 목록을 반환합니다.|  
|**SQLColumnPrivileges**|단일 테이블에서 하나 이상의 열과 연결된 권한 목록을 반환합니다.|  
|**SQLProcedures**|데이터 원본의 프로시저 목록을 반환합니다.|  
|**SQLProcedureColumns**|단일 프로시저의 결과 집합에서 입력 및 출력 매개 변수 목록, 반환 값 및 열을 반환합니다.|  
|**SQLGetTypeInfo**|데이터 원본에서 지원하는 SQL 데이터 형식 목록을 반환합니다. 이러한 데이터 형식은 일반적으로 **CREATE 테이블** 및 **ALTER TABLE** 문에서 사용됩니다.|  
  
 **SQLTable,** **SQLColumns,** **SQLStatistics**및 **SQLSpecialColumns는** 오픈 그룹 CLI를 준수하고 **SQLGetTypeInfo는** ISO 92 CLI를 준수하므로 대부분의 드라이버에서 구현됩니다. 나머지 카탈로그 함수는 ODBC 준수 수준에 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 함수에 의해 반환된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [스키마 보기](../../../odbc/reference/develop-app/schema-views.md)
