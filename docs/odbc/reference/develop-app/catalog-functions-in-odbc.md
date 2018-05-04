---
title: 카탈로그 함수에서 ODBC | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- catalog functions [ODBC], listed
- functions [ODBC], catalog functions
ms.assetid: 4f28f557-7eca-4905-aa6d-45a6cf501a66
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7297b87ec5ce8bdbf706fa35b5ebef6ba580a49e
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="catalog-functions-in-odbc"></a>Odbc에서 카탈로그 함수
ODBC는 다음과 같은 카탈로그 함수를 포함 되어 있습니다.  
  
|함수|Description|  
|--------------|-----------------|  
|**SQLTables**|데이터 원본의 카탈로그, 스키마, 테이블 또는 테이블 형식 목록을 반환합니다.|  
|**SQLColumns**|하나 이상의 테이블에 있는 열의 목록을 반환합니다.|  
|**SQLStatistics**|단일 테이블에 대 한 통계 목록을 반환합니다. 또한 해당 테이블과 연결 된 인덱스의 목록을 반환 합니다.|  
|**SQLSpecialColumns**|단일 테이블의 행을 고유 하 게 식별 하는 열 목록을 반환 합니다. 또한 자동으로 업데이트 되는 해당 테이블의 열 목록을 반환 합니다.|  
|**SQLPrimaryKeys**|단일 테이블의 기본 키를 구성 하는 열 목록을 반환 합니다.|  
|**SQLForeignKeys**|단일 테이블을 참조 하는 다른 테이블의 외래 키의 목록 또는 단일 테이블의 외래 키 목록을 반환 합니다.|  
|**SQLTablePrivileges**|하나 이상의 테이블에 연결 된 권한 목록을 반환 합니다.|  
|**SQLColumnPrivileges**|단일 테이블에서 하나 이상의 열과 관련 된 권한 목록을 반환 합니다.|  
|**SQLProcedures**|데이터 원본에 프로시저의 목록을 반환합니다.|  
|**SQLProcedureColumns**|단일 프로시저의 결과 집합의 입력 및 출력 매개 변수, 반환 값 및 열 목록을 반환 합니다.|  
|**SQLGetTypeInfo**|데이터 원본에서 지 원하는 SQL 데이터 형식의 목록을 반환 합니다. 이러한 데이터 형식은 보통 사용 **CREATE TABLE** 및 **ALTER TABLE** 문.|  
  
 때문에 **SQLTables**, **SQLColumns**, **SQLStatistics**, 및 **SQLSpecialColumns** Open 그룹 CLI 및 준수**SQLGetTypeInfo** 92 CLI ISO에 맞는, 대부분의 드라이버에 의해 구현 됩니다. 나머지 카탈로그 함수는 ODBC 규칙 수준 있습니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [카탈로그 함수에 의해 반환된 데이터](../../../odbc/reference/develop-app/data-returned-by-catalog-functions.md)  
  
-   [카탈로그 함수의 인수](../../../odbc/reference/develop-app/arguments-in-catalog-functions.md)  
  
-   [스키마 뷰](../../../odbc/reference/develop-app/schema-views.md)
