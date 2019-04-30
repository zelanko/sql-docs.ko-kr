---
title: ODBC의 카탈로그 함수 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 84c870d45cc487fc9ec5497e43b764bd4187d2f6
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63217623"
---
# <a name="catalog-functions-in-odbc"></a>ODBC의 카탈로그 함수
ODBC는 다음 카탈로그 함수를 포함 합니다.  
  
|기능|Description|  
|--------------|-----------------|  
|**SQLTables**|데이터 원본에서 카탈로그, 스키마, 테이블 또는 테이블 형식 목록을 반환합니다.|  
|**SQLColumns**|하나 이상의 테이블에서 열 목록을 반환합니다.|  
|**SQLStatistics**|단일 테이블에 대 한 통계의 목록을 반환합니다. 또한 해당 테이블과 연결 된 인덱스의 목록을 반환 합니다.|  
|**SQLSpecialColumns**|단일 테이블에서 행을 고유 하 게 식별 하는 열의 목록을 반환 합니다. 또한 자동으로 업데이트 되는 해당 테이블의 열 목록을 반환 합니다.|  
|**SQLPrimaryKeys**|단일 테이블의 기본 키를 구성 하는 열의 목록을 반환 합니다.|  
|**SQLForeignKeys**|단일 테이블에서 단일 테이블을 참조 하는 다른 테이블의 외래 키 목록을 외래 키 목록을 반환 합니다.|  
|**SQLTablePrivileges**|하나 이상의 테이블에 연결 된 권한 목록을 반환 합니다.|  
|**SQLColumnPrivileges**|단일 테이블에 하나 이상의 열과 연결 된 권한 목록을 반환 합니다.|  
|**SQLProcedures**|데이터 원본에 프로시저의 목록을 반환합니다.|  
|**SQLProcedureColumns**|단일 프로시저의 결과 집합의 입력 및 출력 매개 변수, 반환 값 및 열 목록을 반환합니다.|  
|**SQLGetTypeInfo**|데이터 원본에서 지 원하는 SQL 데이터 형식의 목록을 반환 합니다. 이러한 데이터 형식에 일반적으로 사용 됩니다 **CREATE TABLE** 하 고 **ALTER TABLE** 문입니다.|  
  
 때문에 **SQLTables**를 **SQLColumns**합니다 **SQLStatistics**, 및 **SQLSpecialColumns** 열기그룹CLI를준수**SQLGetTypeInfo** 92 CLI ISO 준수, 대부분의 드라이버에서 구현 됩니다. 나머지 카탈로그 함수는 ODBC 규칙 수준에서 됩니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 함수에 의해 반환된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [스키마 뷰](../../../odbc/reference/develop-app/schema-views.md)
