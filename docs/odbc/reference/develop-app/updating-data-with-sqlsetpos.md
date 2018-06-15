---
title: SQLSetPos로 데이터를 업데이트 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- updating data [ODBC], SQLSetPos
- data updates [ODBC], SQLSetPos
- SQLSetPos function [ODBC], updating data
ms.assetid: e9625b59-06a0-4883-b155-b932ba7528d9
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3fecebb38d9e34a2a06fb0e5b70131cc57d8deff
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32916208"
---
# <a name="updating-data-with-sqlsetpos"></a>SQLSetPos 사용 하 여 업데이트 데이터
응용 프로그램을 업데이트 하거나 삭제 된 행 집합의 모든 행 **SQLSetPos**합니다. 호출 **SQLSetPos** 편리 하 게 하는 대신 하면 작성 하 고 SQL 문을 실행 합니다. 데이터 소스 위치 지정 된 SQL 문을 지원 하지 않는 경우에 위치 지정된 업데이트를 지 원하는 ODBC 드라이버를 수 있습니다. 함수 호출을 사용 하 여 완전 한 데이터베이스 액세스를 얻기 위한 패러다임의 일부인 것입니다.  
  
 **SQLSetPos** 현재 행 집합에서 작동 하 고에 대 한 호출 후에 사용할 수 있습니다 **SQLFetchScroll**합니다. 응용 프로그램 업데이트, 삭제 또는 삽입 행의 수를 지정 하 고 드라이버 행 집합 버퍼에서 해당 행에 대 한 새 데이터를 검색 합니다. **SQLSetPos** 현재 행으로 지정된 된 행을 지정 하거나 데이터 원본의 행 집합의 특정 행을 새로 고치려면 사용 수도 있습니다.  
  
 호출 하 여 행 집합 크기 설정 되어 **SQLSetStmtAttr** 와 *특성* SQL_ATTR_ROW_ARRAY_SIZE의 인수입니다. **그러나 SQLSetPos** 를 호출한 후에 새 행 집합 크기를 사용 하 여 **SQLFetch** 또는 **SQLFetchScroll**합니다. 예를 들어, 행 집합 크기가 변경 되 면 **SQLSetPos** 라고 차례로 **SQLFetch** 또는 **SQLFetchScroll** 가 호출에 대 한 호출은 **SQLSetPos** 하는 동안 오래 된 행 집합 크기를 사용 하 여 **SQLFetch** 또는 **SQLFetchScroll** 새 행 집합 크기를 사용 합니다.  
  
 행 집합의 첫 번째 행 번호는 1입니다. *RowNumber* 인수 **SQLSetPos** ; 행 집합의 행을 식별 해야 해당 값 1 및 가장 최근에 인출 된 행 수 사이의 범위에 있어야 즉, (발생할 수 있는 보다 작은 행 집합 크기)입니다. 경우 *RowNumber* 가 0 이면 행 집합의 모든 행에 작업 적용 됩니다.  
  
 관계형 데이터베이스와 대부분의 상호 작용 SQL을 통해 수행 되므로 **SQLSetPos** 광범위 하 게 지원 되지 않습니다. 그러나 드라이버를 쉽게 여 에뮬레이트할 수 것 작성 하 고 실행 한 **업데이트** 또는 **삭제** 문.  
  
 작업을 확인 하려면 **SQLSetPos** 지 원하는 응용 프로그램이 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ 특성을 1 또는 (커서 유형)에 따라 다름 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSetPos를 사용하여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [SQLSetPos를 사용하여 행 집합에서 행 삭제](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
