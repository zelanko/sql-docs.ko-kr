---
title: SQLSetPos를 사용 하 여 데이터를 업데이트 하는 중 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d1c31ef622281b4f52f62ca3867c5afa7dcae8ca
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47680791"
---
# <a name="updating-data-with-sqlsetpos"></a>SQLSetPos를 사용하여 데이터 업데이트
응용 프로그램을 업데이트 하거나 사용 하 여 행 집합의 모든 행을 삭제 **SQLSetPos**합니다. 호출 **SQLSetPos** 작성 하 고 SQL 문을 실행 하는 편리한 대체 방법입니다. 데이터 원본 위치 지정된 된 SQL 문을 지원 하지 않는 하는 경우에 위치 지정된 업데이트를 지 원하는 ODBC 드라이버를 수 있습니다. 함수 호출을 사용 하 여 전체 데이터베이스 액세스를 달성 하는 패러다임의 일부입니다.  
  
 **SQLSetPos** 현재 행 집합에서 작동 하 고 호출 후에 사용할 수 있습니다 **SQLFetchScroll**합니다. 업데이트, 삭제 또는 삽입 행의 수를 지정 하는 응용 프로그램 및 드라이버는 행 집합 버퍼에서 해당 행에 대 한 새 데이터를 검색 합니다. **SQLSetPos** 현재 행으로 지정된 된 행을 지정 하거나 데이터 원본의 행 집합의 특정 행을 새로도 사용할 수 있습니다.  
  
 호출 하 여 행 집합 크기 설정 되어 **SQLSetStmtAttr** 사용 하 여는 *특성* SQL_ATTR_ROW_ARRAY_SIZE의 인수입니다. **그러나 SQLSetPos** 를 호출한 후에 새 행 집합 크기를 사용 하 여 **SQLFetch** 하거나 **SQLFetchScroll**합니다. 예를 들어 행 집합 크기가 변경 되 면 **SQLSetPos** 이라고 차례로 **SQLFetch** 또는 **SQLFetchScroll** 가 호출 및 호출 **SQLSetPos** 하는 동안 이전 행 집합 크기를 사용 하 여 **SQLFetch** 하거나 **SQLFetchScroll** 새 행 집합 크기를 사용 합니다.  
  
 행 집합의 첫 번째 행 번호는 1입니다. *RowNumber* 에서 인수 **SQLSetPos** ; 행 집합의 행을 식별 해야 1 및 가장 최근에 인출 된 행의 번호 사이의 범위에 해당 값 즉, 이어야 합니다 (일 수 있는 보다 작은 행 집합 크기)입니다. 하는 경우 *RowNumber* 0 인 작업은 행 집합의 모든 행에 적용 됩니다.  
  
 관계형 데이터베이스를 사용 하 여 대부분의 상호 작용은 SQL을 통해 수행 되므로 **SQLSetPos** 광범위 하 게 지원 되지 않습니다. 그러나 드라이버를 쉽게 여 에뮬레이트할 수 있습니다이 작성 하 고 실행을 **업데이트** 또는 **삭제** 문입니다.  
  
 작업을 결정할 **SQLSetPos** 지 원하는 응용 프로그램 호출 **SQLGetInfo** SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ 특성을 1 또는 (커서 유형)에 따라 다름 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSetPos를 사용하여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [SQLSetPos를 사용하여 행 집합에서 행 삭제](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
