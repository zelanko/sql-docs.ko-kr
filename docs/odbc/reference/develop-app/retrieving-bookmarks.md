---
title: 책갈피 검색 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- retrieving bookmarks [ODBC]
- result sets [ODBC], bookmarks
- bookmarks [ODBC]
ms.assetid: a34c8f09-b786-4835-a44b-b7294c970aff
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9d7d4bd52a5f6e5b03a084cef4402e0a9044f97d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62861403"
---
# <a name="retrieving-bookmarks"></a>책갈피 검색
응용 프로그램에서 책갈피에 사용 하면 SQL_ATTR_USE_BOOKMARKS 문 특성 준비 하거나 문을 실행 하기 전에 SQL_UB_VARIABLE로 설정 합니다. 그 중 빌드 및 책갈피를 만들 수 있으므로 좋은 경우에 책갈피를 사용 해야 하므로 비용이 많이 드는 작업 수를 유지 관리에 사용 하기 때문에 이것이 필요한입니다.  
  
 책갈피는 결과 집합의 열 0으로 반환 됩니다. 세 가지 방법으로 응용 프로그램을 검색할 수 있습니다.  
  
-   0은 결과 집합의 열을 바인딩하십시오. **SQLFetch** 나 **SQLFetchScroll** 다른 데이터와 함께 행 집합의 각 행 바인딩된 열에 대 한 책갈피를 반환 합니다.  
  
-   호출 **SQLSetPos** 행 집합의 행에 배치 하 고 호출 하 **SQLGetData** 0 열에 대 한 합니다. 호출 하는 기능은 드라이버 책갈피를 지 원하는 경우 항상 지원 해야 합니다 **SQLGetData** 0, 응용 프로그램이 호출할 수 없도록 하는 경우에 열에 대 한 **SQLGetData** 마지막 바인딩 전에 다른 열에 대 한 열입니다.  
  
-   호출 **SQLBulkOperations** 사용 하 여 합니다 *작업* SQL_ADD로 설정 하는 인수 및 바인딩된 열 0입니다. 커서는 행을 삽입 하 고 바인딩된 버퍼에 행에 대 한 책갈피를 반환 합니다.
