---
title: 결과 검색 (고급) | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- offsets [ODBC]
- result sets [ODBC], about result sets
- bind offsets [ODBC]
ms.assetid: bc00c379-71a7-407a-975c-898243f39bb6
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: ca02b4ff911c8edff06b38d5341eeaa288cc194c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81294643"
---
# <a name="retrieving-results-advanced"></a>결과 검색(고급)
응용 프로그램은 **SQLBulkOperations, SQLFetch ,** **SQLFetchScroll**또는 **SQLSetPos가** 호출될 때 **SQLFetch**오프셋이 바인딩된 데이터 버퍼 주소와 해당 길이/표시기 버퍼 주소에 추가되도록 지정할 수 있습니다. 이러한 추가 결과에 따라 이러한 작업에 사용되는 주소가 결정됩니다.  
  
 바인딩 오프셋을 사용하면 응용 프로그램이 이전에 바인딩된 열에 대해 **SQLBindCol을** 호출하지 않고 바인딩을 변경할 수 있습니다. 데이터를 다시 바인딩하기 위해 **SQLBindCol을** 호출하여 버퍼 주소와 길이/표시기 포인터를 변경합니다. 반면오프셋으로 다시 바인딩하면 기존 바인딩된 데이터 버퍼 주소와 길이/표시기 버퍼 주소에 오프셋이 추가됩니다. 오프셋을 사용할 때 바인딩은 응용 프로그램 버퍼가 배치되는 방식의 "템플릿"이며 응용 프로그램은 오프셋을 변경하여 이 "템플릿"을 다른 메모리 영역으로 이동할 수 있습니다. 새 오프셋은 언제든지 지정할 수 있으며 항상 원래 바인딩된 값에 추가됩니다.  
  
 바인드 오프셋을 지정하기 위해 응용 프로그램은 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성을 SQLINTEGER 버퍼의 주소로 설정합니다. 응용 프로그램이 **SQLBulkOperations,** **SQLFetch**, **SQLFetchScroll**또는 **SQLSetPos와**같은 바인딩을 사용하는 함수를 호출하기 전에 데이터 버퍼 주소나 길이/표시기 버퍼 주소가 0이 아니고 바인딩된 열이 결과 집합에 있는 한 이 버퍼에 바이트에 오프셋을 배치합니다. 주소와 오프셋의 합계는 유효한 주소여야 합니다. 즉, 합계가 유효한 주소인 한 오프셋과 오프셋이 추가된 주소중 하나 또는 둘 다 유효하지 않을 수 있습니다. SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성은 오프셋 값을 하나 이상의 바인딩 데이터 집합에 적용할 수 있도록 포인터이며, 모두 하나의 오프셋 값을 변경하여 변경할 수 있습니다. 응용 프로그램은 커서가 닫혀도 포인터가 유효한지 확인해야 합니다.  
  
> [!NOTE]  
>  바인딩 오프셋은 ODBC 2에서 지원되지 않습니다. *x* 드라이버.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [스크롤 가능한 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 커서 라이브러리](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)
