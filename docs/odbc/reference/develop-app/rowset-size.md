---
title: "행 집합 크기 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- rowset size [ODBC]
- cursors [ODBC], block
- result sets [ODBC], rowset size
- block cursors [ODBC]
- result sets [ODBC], block cursors
ms.assetid: 60366ae8-175c-456a-ae5e-bdd860786911
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: e693a799c737baf8a11064c5bd50c2618cd1e29a
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="rowset-size"></a>행 집합 크기
응용 프로그램에 사용 하는 행 집합 크기에 따라 다릅니다. 일반적으로 화면 기반 응용 프로그램 두 가지 전략 중 하나를 수행 합니다. 첫 번째 화면에 표시 되는 행의 수는 행 집합 크기를 설정 하는 사용자가 화면을 응용 프로그램에 따라 행 집합 크기를 변경 합니다. 두 번째에 더 큰 숫자를 100, 데이터 원본에 대 한 호출 수를 줄일 수 있는를 행 집합 크기를 설정 하는 것입니다. 응용 프로그램이 로컬로 가능 하면 행 집합 내의 스크롤하고 행 집합 외부 스크롤 하는 경우에 새 행을 인출 합니다.  
  
 응용 프로그램 합리적으로 처리할 수는 행의 가장 큰 수로 행 집합 크기 설정 하는 경향이 보고서와 같은 다른 응용 프로그램-보다 큰 행 집합으로 행 마다 오버 헤드 네트워크 경우에 따라 줄어듭니다. 정확 하 게 크기는 행 집합 수는 사용 가능한 메모리의 양과 각 행의 크기에 따라 달라 집니다.  
  
 호출 하 여 행 집합 크기 설정 되어 **SQLSetStmtAttr** 와 *특성* SQL_ATTR_ROW_ARRAY_SIZE의 인수입니다. 행 집합 크기를 변경, 새 행 집합 버퍼를 바인딩할 수 응용 프로그램이 (호출 하 여 **SQLBindCol** 바인딩 오프셋을 지정 하거나) 인출 된 행의 한 후에 또는 둘 다 합니다. 행 집합 크기를 변경의 의미는 함수에 따라 달라 집니다.  
  
-   **SQLFetch** 및 **SQLFetchScroll** 메서드를 호출할 때에는 행 집합 크기를 사용 하 여 행 인출 수를 결정 합니다. 그러나 **SQLFetchScroll** 와 *FetchOrientation* SQL_FETCH_NEXT 간격의 커서 기반 이전 인출 및 다음 인출의 행 집합에는 현재 행 집합 크기를 기준으로 행 집합입니다.  
  
-   **SQLSetPos** 에 대 한 이전 호출을 기준으로 적용 되는 행 집합 크기를 사용 하 여 **SQLFetch** 또는 **SQLFetchScroll**때문에, **SQLSetPos** 에서 작동 하는 이미 설정 된 행 집합입니다. **SQLSetPos** 도 선택 됩니다 새 행 집합 크기가 경우 **SQLBulkOperations** 를 호출한 후 행 집합 크기가 변경 되었습니다.  
  
-   **SQLBulkOperations** 사용 하 여 행 집합 크기가 적용 호출의 시간에 관계 없이 모든 인출 된 행 집합의 테이블에 대 한 작업을 수행 하기 때문에 있습니다.
