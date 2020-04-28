---
title: 결과 검색 (고급) | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81294643"
---
# <a name="retrieving-results-advanced"></a>결과 검색(고급)
응용 프로그램은 **SQLBulkOperations**, **sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos** 가 호출 될 때 바인딩된 데이터 버퍼 주소와 해당 길이/표시기 버퍼 주소에 오프셋을 추가 하도록 지정할 수 있습니다. 이러한 추가 결과에 따라 이러한 작업에 사용 되는 주소가 결정 됩니다.  
  
 바인딩 오프셋을 사용 하면 응용 프로그램에서 이전에 바인딩된 열에 대해 **SQLBindCol** 를 호출 하지 않고 바인딩을 변경할 수 있습니다. **SQLBindCol** 를 호출 하 여 데이터를 다시 바인딩하는 경우 버퍼 주소 및 길이/표시기 포인터가 변경 됩니다. 반면에 오프셋을 사용한 리바인딩은 기존 바인딩된 데이터 버퍼 주소 및 길이/표시기 버퍼 주소에 오프셋을 추가 합니다. 오프셋을 사용 하는 경우 바인딩은 응용 프로그램 버퍼가 배치 되는 방법의 "템플릿" 이며, 응용 프로그램은 오프셋을 변경 하 여이 "템플릿"을 다른 메모리 영역으로 이동할 수 있습니다. 언제 든 지 새 오프셋을 지정할 수 있으며, 항상 원래 바인딩된 값에 추가 됩니다.  
  
 바인딩 오프셋을 지정 하기 위해 응용 프로그램은 SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성을 SQLINTEGER 버퍼의 주소로 설정 합니다. 응용 프로그램에서 **SQLBulkOperations**, **sqlfetch**, **sqlfetchscroll**또는 **SQLSetPos**와 같은 바인딩을 사용 하는 함수를 호출 하기 전에 데이터 버퍼 주소와 길이/표시기 버퍼 주소가 모두 0이 아니고, 바인딩된 열이 결과 집합에 있는 한이 버퍼에서 오프셋을 바이트 단위로 배치 합니다. 주소와 오프셋의 합은 올바른 주소 여야 합니다. 즉, 오프셋이 추가 된 오프셋 및 주소 중 하나 또는 둘 모두가 유효 하지 않을 수 있습니다 (합계가 유효한 주소인 경우). SQL_ATTR_ROW_BIND_OFFSET_PTR statement 특성은 오프셋 값을 둘 이상의 바인딩 데이터 집합에 적용할 수 있도록 하는 포인터입니다 .이 값은 하나의 오프셋 값을 변경 하 여 변경할 수 있습니다. 응용 프로그램은 커서가 닫힐 때까지 포인터가 유효한 상태로 남아 있는지 확인 해야 합니다.  
  
> [!NOTE]  
>  바인딩 오프셋은 ODBC 2에서 지원 되지 않습니다. *x* 드라이버.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 커서 라이브러리](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)
