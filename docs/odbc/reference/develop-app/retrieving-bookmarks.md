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
ms.openlocfilehash: f18b87adf31f19d2a93bb3af3e14c265ae3940af
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68020567"
---
# <a name="retrieving-bookmarks"></a>책갈피 검색
응용 프로그램에서 책갈피를 사용 하는 경우 문을 준비 하거나 실행 하기 전에 SQL_ATTR_USE_BOOKMARKS statement 특성을 SQL_UB_VARIABLE으로 설정 해야 합니다. 책갈피를 빌드하고 유지 관리 하는 작업은 비용이 많이 들 수 있으므로 응용 프로그램에서 적절 하 게 사용할 수 있는 경우에만 책갈피를 사용 하도록 설정 해야 합니다.  
  
 책갈피는 결과 집합의 열 0으로 반환 됩니다. 응용 프로그램에서 검색할 수 있는 방법에는 세 가지가 있습니다.  
  
-   결과 집합의 열 0을 바인딩합니다. **Sqlfetch** 또는 **sqlfetchscroll** 은 다른 바인딩된 열의 데이터와 함께 행 집합의 각 행에 대 한 책갈피를 반환 합니다.  
  
-   **SQLSetPos** 를 호출 하 여 행 집합의 행에 위치를 지정한 다음 열 0에 대해 **SQLGetData** 를 호출 합니다. 드라이버가 책갈피를 지 원하는 경우 응용 프로그램에서 마지막으로 바인딩된 열 앞의 다른 열에 대해 **sqlgetdata** 를 호출할 수 없는 경우에도 항상 열 0에 대해 **sqlgetdata** 를 호출 하는 기능을 지원 해야 합니다.  
  
-   SQL_ADD 및 열 0으로 설정 된 *작업* 인수를 사용 하 여 **SQLBulkOperations** 를 호출 합니다. 커서는 행을 삽입 하 고 바인딩된 버퍼의 행에 대 한 책갈피를 반환 합니다.
