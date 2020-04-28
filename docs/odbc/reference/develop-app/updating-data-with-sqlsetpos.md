---
title: SQLSetPos를 사용 하 여 데이터 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 16476a1e1007905f34ec2e70ce6032eb8d81fe7a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81286163"
---
# <a name="updating-data-with-sqlsetpos"></a>SQLSetPos를 사용하여 데이터 업데이트
응용 프로그램은 **SQLSetPos**를 사용 하 여 행 집합의 모든 행을 업데이트 하거나 삭제할 수 있습니다. **SQLSetPos** 호출은 SQL 문을 생성 하 고 실행 하는 편리한 대안입니다. 데이터 원본에서 위치가 지정 된 SQL 문을 지원 하지 않는 경우에도 ODBC 드라이버에서 위치 지정 업데이트를 지원할 수 있습니다. 함수 호출을 통해 전체 데이터베이스 액세스를 달성 하는 패러다임의 일부입니다.  
  
 **SQLSetPos** 는 현재 행 집합에서 작동 하며 **sqlfetchscroll**을 호출한 후에만 사용할 수 있습니다. 응용 프로그램은 update, delete 또는 insert 행의 번호를 지정 하 고, 드라이버는 행 집합 버퍼에서 해당 행에 대 한 새 데이터를 검색 합니다. **SQLSetPos** 를 사용 하 여 지정 된 행을 현재 행으로 지정 하거나 데이터 원본에서 행 집합의 특정 행을 새로 고칠 수도 있습니다.  
  
 행 집합 크기는 SQL_ATTR_ROW_ARRAY_SIZE *특성* 인수를 사용 하 여 **SQLSetStmtAttr** 에 대 한 호출로 설정 됩니다. 그러나 **SQLSetPos** 는 **Sqlfetch** 또는 **sqlfetchscroll**을 호출한 후에만 새 행 집합 크기를 사용 합니다. 예를 들어 행 집합 크기가 변경 되 면 **sqlsetpos** 를 호출 하 고 **Sqlfetch** 또는 **sqlfetchscroll** 을 호출 하 고, **sqlsetpos** 호출에서 이전 행 집합 크기를 사용 하는 반면, **sqlfetch** 또는 **sqlfetchscroll** 은 새 행 집합 크기를 사용 합니다.  
  
 행 집합의 첫 번째 행 번호는 1입니다. **SQLSetPos** 의 *RowNumber* 인수는 행 집합에서 행을 식별 해야 합니다. 즉, 해당 값은 1에서 가장 최근에 인출 된 행 수 (행 집합 크기 보다 낮을 수 있음)의 범위에 있어야 합니다. *RowNumber* 가 0 이면 행 집합의 모든 행에 작업이 적용 됩니다.  
  
 관계형 데이터베이스와의 상호 작용은 대부분 SQL을 통해 수행 되기 때문에 **SQLSetPos** 는 광범위 하 게 지원 되지 않습니다. 그러나 **UPDATE** 또는 **DELETE** 문을 생성 하 고 실행 하 여 드라이버에서 쉽게 에뮬레이트할 수 있습니다.  
  
 **SQLSetPos** 에서 지 원하는 작업을 확인 하기 위해 응용 프로그램은 커서의 유형에 따라 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션을 사용 하 여 **SQLGetInfo** 를 호출 합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSetPos를 사용하여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [SQLSetPos를 사용하여 행 집합에서 행 삭제](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
