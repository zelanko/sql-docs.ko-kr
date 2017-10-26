---
title: "SQLBulkOperations로 데이터를 업데이트 | Microsoft Docs"
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
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 75e5f954065c0b41935aa231c85c093d5ee10226
ms.contentlocale: ko-kr
ms.lasthandoff: 09/09/2017

---
# <a name="updating-data-with-sqlbulkoperations"></a>SQLBulkOperations 사용 하 여 업데이트 데이터
응용 프로그램을 호출 하 여 데이터 원본에서 원본 테이블에 대량 업데이트, 삭제, fetch, 또는 삽입 작업을 수행할 수 **SQLBulkOperations**합니다. 호출 **SQLBulkOperations** 편리 하 게 하는 대신 하면 작성 하 고 SQL 문을 실행 합니다. 데이터 소스 위치 지정 된 SQL 문을 지원 하지 않는 경우에 위치 지정된 업데이트를 지 원하는 ODBC 드라이버를 수 있습니다. 함수 호출을 사용 하 여 완전 한 데이터베이스 액세스를 얻기 위한 패러다임의 일부인 것입니다.  
  
 **SQLBulkOperations** 현재 행 집합에서 작동 하 고에 대 한 호출 후에 사용할 수 있습니다 **SQLFetch** 또는 **SQLFetchScroll**합니다. 응용 프로그램에는 행을 업데이트, 삭제 또는 책갈피를 캐시 하 여 새로 고침을 지정 합니다. 드라이버 업데이트 될 행에 대 한 새 데이터 또는 행 집합 버퍼에서 기본 테이블에 삽입할 새 데이터를 검색 합니다.  
  
 사용할 행 집합 크기 **SQLBulkOperations** 를 호출 하 여 설정 **SQLSetStmtAttr** 와 *특성* SQL_ATTR_ROW_ARRAY_SIZE의 인수입니다. 와 달리 **SQLSetPos**, 새 행 집합 크기에 대 한 호출 후에 사용 하 여 **SQLFetch** 또는 **SQLFetchScroll**, **SQLBulkOperations** 사용 하는 호출한 후 새 행 집합 크기가 **SQLSetStmtAttr**합니다.  
  
 관계형 데이터베이스와 대부분의 상호 작용 SQL을 통해 수행 되므로 **SQLBulkOperations** 광범위 하 게 지원 되지 않습니다. 그러나 드라이버를 쉽게 여 에뮬레이트할 수 것 작성 하 고 실행 한 **업데이트**, **삭제**, 또는 **삽입** 문.  
  
 작업을 확인 하려면 **SQLBulkOperation** 지 원하는 응용 프로그램이 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR _ATTRIBUTES1, 또는 (커서 유형)에 따라 다름 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLBulkOperations로 책갈피별로 행 업데이트](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 책갈피별로 행 삭제하기](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations를 사용하여 행 삽입](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 행 페치](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)

