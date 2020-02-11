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
ms.openlocfilehash: a8cd46fbc8f633ef31f00fa60ced885f9455f185
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68062723"
---
# <a name="catalog-functions-in-odbc"></a>ODBC의 카탈로그 함수
ODBC에는 다음 카탈로그 함수가 포함 되어 있습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**SQLTables**|데이터 원본의 카탈로그, 스키마, 테이블 또는 테이블 형식 목록을 반환 합니다.|  
|**SQLColumns**|하나 이상의 테이블에 있는 열의 목록을 반환 합니다.|  
|**SQLStatistics**|단일 테이블에 대 한 통계 목록을 반환 합니다. 는 해당 테이블과 연결 된 인덱스의 목록도 반환 합니다.|  
|**SQLSpecialColumns**|단일 테이블의 행을 고유 하 게 식별 하는 열 목록을 반환 합니다. 또한 자동으로 업데이트 되는 해당 테이블의 열 목록을 반환 합니다.|  
|**SQLPrimaryKeys**|단일 테이블의 기본 키를 구성 하는 열 목록을 반환 합니다.|  
|**SQLForeignKeys**|단일 테이블의 외래 키 목록과 단일 테이블을 참조 하는 다른 테이블의 외래 키 목록을 반환 합니다.|  
|**SQLTablePrivileges**|하나 이상의 테이블과 연결 된 권한 목록을 반환 합니다.|  
|**SQLColumnPrivileges**|단일 테이블에서 하나 이상의 열과 연결 된 권한 목록을 반환 합니다.|  
|**SQLProcedures**|데이터 원본에 있는 프로시저의 목록을 반환 합니다.|  
|**SQLProcedureColumns**|단일 프로시저의 결과 집합에 있는 입력 및 출력 매개 변수, 반환 값 및 열의 목록을 반환 합니다.|  
|**SQLGetTypeInfo**|데이터 원본에서 지원 되는 SQL 데이터 형식의 목록을 반환 합니다. 이러한 데이터 형식은 일반적으로 **CREATE TABLE** 및 **ALTER TABLE** 문에 사용 됩니다.|  
  
 **Sqltables**, **sqltables**, **SQLStatistics**및 **SQLSpecialColumns** 는 Open GROUP cli를 준수 하 고 **SQLGetTypeInfo** 는 ISO 92 cli를 준수 하기 때문에 대부분의 드라이버에 의해 구현 됩니다. 나머지 카탈로그 함수는 ODBC 규칙 수준에 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 함수에 의해 반환된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [스키마 보기](../../../odbc/reference/develop-app/schema-views.md)
