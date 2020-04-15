---
title: SQLBulkOperations로 데이터 업데이트 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 9b96e3a43b8385910e4260cf51dea7e4ff508200
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81298487"
---
# <a name="updating-data-with-sqlbulkoperations"></a>SQLBulkOperations로 데이터 업데이트
응용 프로그램은 **SQLBulkOperations**를 호출하여 데이터 원본의 기본 테이블에서 대량 업데이트, 삭제, 가져오기 또는 삽입 작업을 수행할 수 있습니다. **SQLBulkOperations을** 호출하는 것은 SQL 문을 생성하고 실행하는 편리한 대안입니다. 데이터 원본이 위치 가 있는 SQL 문을 지원하지 않는 경우에도 ODBC 드라이버가 위치 지정 업데이트를 지원할 수 있습니다. 함수 호출을 통해 완전한 데이터베이스 액세스를 달성하는 패러다임의 일부입니다.  
  
 **SQLBulkOperations는** 현재 행 집합에서 작동하며 **SQLFetch** 또는 **SQLFetchScroll**에 대한 호출 후에만 사용할 수 있습니다. 응용 프로그램은 책갈피를 캐싱하여 업데이트, 삭제 또는 새로 고칠 행을 지정합니다. 드라이버는 업데이트할 행에 대한 새 데이터 또는 행 집합 버퍼에서 기본 테이블에 삽입할 새 데이터를 검색합니다.  
  
 **SQLBulkOperations에서** 사용할 행 집합 크기는 SQL_ATTR_ROW_ARRAY_SIZE *특성* 인수를 사용하여 **SQLSetStmtAttr에** 대한 호출로 설정됩니다. **SQLSetPos와**달리 **SQLFetch** 또는 **SQLFetchScroll에**대한 호출 후에만 새 행 집합 크기를 사용하는 **SQLBulkOperations는** **SQLSetStmtAttr**에 대한 호출 후 새 행 집합 크기를 사용합니다.  
  
 관계형 데이터베이스와의 대부분의 상호 작용은 SQL을 통해 수행되므로 **SQLBulkOperations는** 널리 지원되지 않습니다. 그러나 드라이버는 **UPDATE,** **DELETE**또는 **INSERT** 문을 생성하고 실행하여 쉽게 에뮬레이트할 수 있습니다.  
  
 **SQLBulkOperation이** 지원하는 작업을 결정하기 위해 응용 프로그램은 커서의 유형에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션을 사용하여 **SQLGetInfo를** 호출합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLBulkOperations로 책갈피별로 행 업데이트](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 책갈피별로 행 삭제](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations를 사용하여 행 삽입](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 행 페치](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
