---
title: SQLBulkOperations로 데이터를 업데이트 하는 중 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBulkOperations function [ODBC], updating data
- data updates [ODBC], SQLBulkOperations
- updating data [ODBC], SQLBulkOperations
ms.assetid: 7645a704-341e-4267-adbe-061a9fda225b
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 4d1aa9b3300cba78f34e876a8501dbaaa421390a
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68091660"
---
# <a name="updating-data-with-sqlbulkoperations"></a>SQLBulkOperations로 데이터 업데이트
응용 프로그램에 대 한 호출을 사용 하 여 데이터 원본에서 기본 테이블에 대해 대량 업데이트, 삭제, fetch, 또는 삽입 작업을 수행할 수 있습니다 **SQLBulkOperations**합니다. 호출 **SQLBulkOperations** 작성 하 고 SQL 문을 실행 하는 편리한 대체 방법입니다. 데이터 원본 위치 지정된 된 SQL 문을 지원 하지 않는 하는 경우에 위치 지정된 업데이트를 지 원하는 ODBC 드라이버를 수 있습니다. 함수 호출을 사용 하 여 전체 데이터베이스 액세스를 달성 하는 패러다임의 일부입니다.  
  
 **SQLBulkOperations** 현재 행 집합에서 작동 하 고 호출 후에 사용할 수 있습니다 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 응용 프로그램에는 행 업데이트, 삭제 또는 해당 책갈피를 캐시 하 여 새로 고침을 지정 합니다. 드라이버를 업데이트 해야 하는 행에 대 한 새 데이터 또는 행 집합 버퍼에서 기본 테이블에 삽입할 새 데이터를 검색 합니다.  
  
 사용할 행 집합 크기가 **SQLBulkOperations** 를 호출 하 여 설정 됩니다 **SQLSetStmtAttr** 사용 하 여는 *특성* SQL_ATTR_ROW_ARRAY_SIZE의 인수입니다. 와 달리 **SQLSetPos**를 호출한 후에 새 행 집합 크기를 사용 하는 **SQLFetch** 또는 **SQLFetchScroll**를 **SQLBulkOperations** 사용 하는 호출한 후 새 행 집합 크기가 **SQLSetStmtAttr**합니다.  
  
 관계형 데이터베이스를 사용 하 여 대부분의 상호 작용은 SQL을 통해 수행 되므로 **SQLBulkOperations** 광범위 하 게 지원 되지 않습니다. 그러나 드라이버를 쉽게 여 에뮬레이트할 수 있습니다이 작성 하 고 실행을 **업데이트**를 **삭제**, 또는 **삽입** 문입니다.  
  
 작업을 결정할 **SQLBulkOperation** 지 원하는 응용 프로그램 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR _ATTRIBUTES1, 또는 (커서 유형)에 따라 다름 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLBulkOperations로 책갈피별로 행 업데이트](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 책갈피별로 행 삭제하기](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations를 사용하여 행 삽입](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 행 페치](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
