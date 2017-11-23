---
title: "검색 결과 (고급) | Microsoft Docs"
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
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 0f669180407ed626ae9235bd666068b6889060b8
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/20/2017
---
# <a name="retrieving-results-advanced"></a>검색 결과 (고급)
응용 프로그램에서 오프셋 바인딩된 데이터 버퍼 주소 및 해당 길이/표시기 추가 되어 있는지를 지정할 수 때 버퍼 주소 **SQLBulkOperations**, **SQLFetch**,  **SQLFetchScroll**, 또는 **SQLSetPos** 호출 됩니다. 추가 하는이 코드의 결과 이러한 작업에 사용 되는 주소를 결정 합니다.  
  
 바인딩 오프셋 하면 응용 프로그램 바인딩을 호출 하지 않고 변경할 **SQLBindCol** 이전에 바인딩된 열에 대 한 합니다. 에 대 한 호출 **SQLBindCol** 버퍼 주소 및 길이/표시기 포인터 변경 데이터를 다시 바인딩해야 합니다. 기존 바인딩된 데이터 버퍼 주소 및 길이/표시기 버퍼 주소 오프셋을 단순히 추가 반면에 리바인딩, 오프셋을 사용 합니다. 오프셋을 사용 하는 바인딩이 지 응용 프로그램 버퍼 레이아웃 하는 방법의 "템플릿" 않으며 응용 프로그램 오프셋을 변경 하 여 메모리의 다른 영역 "템플릿"이 이동할 수 있습니다. 새 오프셋 언제 든 지 지정할 수 있으며은 항상 원래 바인딩된 값에 추가 합니다.  
  
 바인딩 오프셋을 지정 하려면 응용 프로그램 SQLINTEGER 버퍼의 주소를 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성을 설정 합니다. 응용 프로그램 같은 바인딩을 사용 하는 함수 호출 전에 **SQLBulkOperations**, **SQLFetch**, **SQLFetchScroll**, 또는 **SQLSetPos**, 데이터 버퍼 주소 아니고 길이/표시기 버퍼 주소는 0, 및 바인딩된 열은 결과 집합에서으로 오프셋이이 버퍼의 바이트에 배치 합니다. 주소와 오프셋의 합계에는 유효한 주소 여야 합니다. (이 좀 더 중 하나 또는 모두 오프셋 및 오프셋을 추가한 주소 수 있습니다 하지 유효 합계는 유효한 주소입니다.) SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 오프셋된 값을 하나의 오프셋된 값을 변경 하 여 변경할 수 있는 모든 데이터를 바인딩 하나 이상의 집합에 적용할 수 있도록 포인터입니다. 응용 프로그램은 커서를 닫을 때까지 포인터가 유효 유지 되는지 확인 해야 합니다.  
  
> [!NOTE]  
>  바인딩 오프셋 ODBC 2에서 지원 되지 않습니다. *x* 드라이버입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 커서 라이브러리](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)
