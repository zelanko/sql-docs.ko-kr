---
title: 책갈피 검색 | 마이크로 소프트 문서
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d146b2fb9bfc0e7294709e971f1b6752dc99ab3
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300073"
---
# <a name="retrieving-bookmarks"></a>책갈피 검색
응용 프로그램이 책갈피를 사용하는 경우 문을 준비하거나 실행하기 전에 SQL_ATTR_USE_BOOKMARKS 명령문 특성을 SQL_UB_VARIABLE 설정해야 합니다. 책갈피를 만들고 유지 관리하는 것은 비용이 많이 드는 작업일 수 있으므로 응용 프로그램에서 책갈피를 잘 사용할 수 있는 경우에만 책갈피를 사용하도록 설정해야 합니다.  
  
 책갈피는 결과 집합의 열 0으로 반환됩니다. 응용 프로그램에서 검색할 수 있는 방법에는 세 가지가 있습니다.  
  
-   결과 집합의 열 0을 바인딩합니다. **SQLFetch** 또는 **SQLFetchScroll는** 행 집합의 각 행에 대한 책갈피를 다른 바인딩된 열에 대한 데이터와 함께 반환합니다.  
  
-   **SQLSetPos를** 호출하여 행 집합의 행에 배치한 다음 **SQLGetData를** 열 0에 호출합니다. 드라이버가 책갈피를 지원하는 경우 응용 프로그램이 마지막 바인딩된 열 앞에 다른 열에 대해 **SQLGetData를** 호출할 수 없는 경우에도 항상 **SQLGetData를** 열 0에 대해 호출하는 기능을 지원해야 합니다.  
  
-   *작업* 인수를 SQL_ADD 설정 하 고 열 0 바인딩된 **SQLBulkOperations를** 호출 합니다. 커서는 행을 삽입하고 바인딩된 버퍼의 행에 대한 책갈피를 반환합니다.
