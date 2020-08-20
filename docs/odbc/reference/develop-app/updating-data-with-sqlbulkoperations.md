---
description: SQLBulkOperations로 데이터 업데이트
title: SQLBulkOperations를 사용 하 여 데이터 업데이트 | Microsoft Docs
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
ms.openlocfilehash: 6c8626a0925d0f30792ed92332c0f96efd23f62e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465537"
---
# <a name="updating-data-with-sqlbulkoperations"></a>SQLBulkOperations로 데이터 업데이트
응용 프로그램은 **SQLBulkOperations**를 호출 하 여 데이터 원본의 기본 테이블에서 대량 업데이트, 삭제, 페치 또는 삽입 작업을 수행할 수 있습니다. **SQLBulkOperations** 를 호출 하는 것은 SQL 문을 생성 하 고 실행 하는 편리한 방법입니다. 데이터 원본에서 위치가 지정 된 SQL 문을 지원 하지 않는 경우에도 ODBC 드라이버에서 위치 지정 업데이트를 지원할 수 있습니다. 함수 호출을 통해 전체 데이터베이스 액세스를 달성 하는 패러다임의 일부입니다.  
  
 **SQLBulkOperations** 는 현재 행 집합에서 작동 하며 **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후에만 사용할 수 있습니다. 응용 프로그램은 책갈피를 캐싱하여 업데이트, 삭제 또는 새로 고침에 대 한 행을 지정 합니다. 드라이버는 행 집합 버퍼에서 업데이트할 행 또는 기본 테이블에 삽입할 새 데이터에 대 한 새 데이터를 검색 합니다.  
  
 **SQLBulkOperations** 에서 사용할 행 집합 크기는 SQL_ATTR_ROW_ARRAY_SIZE *특성* 인수를 사용 하 여 **SQLSetStmtAttr** 에 대 한 호출로 설정 됩니다. **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후에만 새 행 집합 크기를 사용 하는 **SQLSetPos**와 달리 **SQLBulkOperations** 는 **SQLSetStmtAttr**를 호출한 후 새 행 집합 크기를 사용 합니다.  
  
 관계형 데이터베이스와의 상호 작용은 대부분 SQL을 통해 수행 되기 때문에 **SQLBulkOperations** 는 광범위 하 게 지원 되지 않습니다. 그러나 드라이버는 **UPDATE**, **DELETE**또는 **INSERT** 문을 생성 하 고 실행 하 여 쉽게 에뮬레이트할 수 있습니다.  
  
 **SQLBulkOperation** 에서 지 원하는 작업을 확인 하기 위해 응용 프로그램은 커서의 유형에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션을 사용 하 여 **SQLGetInfo** 를 호출 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLBulkOperations로 책갈피별로 행 업데이트](../../../odbc/reference/develop-app/updating-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 책갈피별로 행 삭제](../../../odbc/reference/develop-app/deleting-rows-by-bookmark-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations를 사용하여 행 삽입](../../../odbc/reference/develop-app/inserting-rows-with-sqlbulkoperations.md)  
  
-   [SQLBulkOperations로 행 페치](../../../odbc/reference/develop-app/fetching-rows-with-sqlbulkoperations.md)
