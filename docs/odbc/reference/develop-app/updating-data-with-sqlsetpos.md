---
title: SQLSetPos로 데이터 업데이트 | 마이크로 소프트 문서
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81286163"
---
# <a name="updating-data-with-sqlsetpos"></a>SQLSetPos를 사용하여 데이터 업데이트
응용 프로그램은 **SQLSetPos**를 사용 하 고 행 집합의 행을 업데이트 하거나 삭제할 수 있습니다. **SQLSetPos호출은** SQL 문을 생성하고 실행하는 대신 편리한 대안입니다. 데이터 원본이 위치 가 있는 SQL 문을 지원하지 않는 경우에도 ODBC 드라이버가 위치 지정 업데이트를 지원할 수 있습니다. 함수 호출을 통해 완전한 데이터베이스 액세스를 달성하는 패러다임의 일부입니다.  
  
 **SQLSetPos는** 현재 행 집합에서 작동하며 **SQLFetchScroll**을 호출한 후에만 사용할 수 있습니다. 응용 프로그램은 업데이트, 삭제 또는 삽입할 행 수를 지정하고 드라이버는 행 집합 버퍼에서 해당 행에 대한 새 데이터를 검색합니다. **SQLSetPos는** 지정된 행을 현재 행으로 지정하거나 데이터 원본에서 행 집합의 특정 행을 새로 고치는 데 사용할 수도 있습니다.  
  
 행 집합 크기는 SQL_ATTR_ROW_ARRAY_SIZE *특성* 인수를 사용하여 **SQLSetStmtAttr에** 대한 호출로 설정됩니다. **그러나 SQLSetPos는** **SQLFetch** 또는 **SQLFetchScroll**를 호출한 후에만 새 행 집합 크기를 사용합니다. 예를 들어 행 집합 크기가 변경되면 **SQLSetPos가** 호출된 다음 **SQLFetch** 또는 **SQLFetchScroll가** 호출되고 **SQLSetPos호출은** 이전 행 집합 크기를 사용하고 **SQLFetch또는** **SQLFetchScroll는** 새 행 집합 크기를 사용합니다.  
  
 행 집합의 첫 번째 행 번호는 1입니다. **SQLSetPos의** *RowNumber* 인수는 행 집합에서 행을 식별해야 합니다. 즉, 해당 값은 가장 최근에 가져온 행 수(행 집합 크기보다 작을 수 있음) 사이의 범위여야 합니다. *RowNumber가* 0이면 행 집합의 모든 행에 작업이 적용됩니다.  
  
 관계형 데이터베이스와의 대부분의 상호 작용은 SQL을 통해 수행되므로 **SQLSetPos는** 널리 지원되지 않습니다. 그러나 드라이버는 **UPDATE** 또는 **DELETE** 문을 생성하고 실행하여 쉽게 에뮬레이트할 수 있습니다.  
  
 **SQLSetPos가** 지원하는 작업을 결정하기 위해 응용 프로그램은 SQL_DYNAMIC_CURSOR_ATTRIBUTES1, SQL_FORWARD_ONLY_CURSOR_ATTRIBUTES1, SQL_KEYSET_CURSOR_ATTRIBUTES1 또는 SQL_STATIC_CURSOR_ATTRIBUTES1 정보 옵션(커서의 유형에 따라 다름)을 사용하여 **SQLGetInfo를** 호출합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [SQLSetPos를 사용하여 행 집합의 행 업데이트](../../../odbc/reference/develop-app/updating-rows-in-the-rowset-with-sqlsetpos.md)  
  
-   [SQLSetPos를 사용하여 행 집합에서 행 삭제](../../../odbc/reference/develop-app/deleting-rows-in-the-rowset-with-sqlsetpos.md)
