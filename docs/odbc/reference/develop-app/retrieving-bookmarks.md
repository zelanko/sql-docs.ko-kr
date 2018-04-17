---
title: 책갈피를 검색 합니다. | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 0d31e012efba212b1acbac0d4127459147508fd1
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/16/2018
---
# <a name="retrieving-bookmarks"></a>책갈피를 검색합니다.
응용 프로그램 책갈피를 사용할 경우를 준비 하거나 문을 실행 하기 전에 SQL_UB_VARIABLE로 SQL_ATTR_USE_BOOKMARKS 문 특성을 설정 합니다. 빌드 및 응용 프로그램 좋은 보장할 수 있는 경우에 책갈피를 사용할 수 해야 하므로 책갈피는 비용이 많이 드는 작업 수를 유지 관리 중 사용 되므로이 작업이 필요 합니다.  
  
 책갈피 결과 집합의 열 0으로 반환 됩니다. 세 가지 방법으로 응용 프로그램에서 검색할 수 있습니다.  
  
-   0은 결과 집합의 열을 바인딩하십시오. **SQLFetch** 또는 **SQLFetchScroll** 각 행의 다른 데이터와 함께 행 집합의 바인딩된 열에 대 한 책갈피를 반환 합니다.  
  
-   호출 **SQLSetPos** 행 집합의 행에 위치를 지정 하 여 호출 **SQLGetData** 0 열에 대 한 합니다. 호출 하는 기능 항상 지원 해야 하는 드라이버에서 책갈피를 지 원하는 경우 **SQLGetData** 0, 응용 프로그램 호출을 허용 하지 않는 경우에 열에 대 한 **SQLGetData** 마지막 바인딩 하기 전에 다른 열에 대 한 열입니다.  
  
-   호출 **SQLBulkOperations** 와 *작업* SQL_ADD로 설정 하는 인수 및 바인딩된 열 0입니다. 커서 행을 삽입 하 고 바운드 버퍼의 행에 대 한 책갈피를 반환 합니다.
