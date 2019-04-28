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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5199fb82cbc6b2a9da644554db12dc525cc0be40
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62998897"
---
# <a name="retrieving-results-advanced"></a>결과 검색(고급)
응용 프로그램 오프셋이 바인딩된 데이터 버퍼 주소 및 해당 길이/표시기에 추가 되었는지를 지정할 수 있습니다 때 버퍼 주소 **SQLBulkOperations**하십시오 **SQLFetch**,  **SQLFetchScroll**, 또는 **SQLSetPos** 라고 합니다. 이러한 추가의 결과 이러한 작업에 사용 되는 주소를 확인 합니다.  
  
 호출 하지 않고 바인딩을 변경 하려면 응용 프로그램을 허용 하는 바인딩 오프셋 **SQLBindCol** 이전에 바인딩된 열에 대 한 합니다. 에 대 한 호출 **SQLBindCol** 데이터 바인딩할 버퍼 주소 및 길이/표시기 포인터를 변경 합니다. 기존 바인딩된 데이터 버퍼 주소 및 길이/표시기 버퍼 주소 오프셋을 간단히 추가 다른 한편으로 오프셋을 사용 하 여 다시 바인딩. 오프셋을 사용 하는 경우 바인딩에 응용 프로그램 버퍼를 레이아웃 하는 방법의 "템플릿" 하 고 응용 프로그램 메모리의 다른 영역에 오프셋을 변경 하 여에 "템플릿"이를 이동할 수 있습니다. 새 오프셋을 언제 든 지 지정할 수 있으며은 항상 원래 바인딩된 값에 추가 합니다.  
  
 바인딩 오프셋을 지정 하려면 응용 프로그램을 SQLINTEGER 버퍼의 주소에 SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성을 설정 합니다. 응용 프로그램 같은 바인딩을 사용 하는 함수를 호출 하기 전에 **SQLBulkOperations**, **SQLFetch**하십시오 **SQLFetchScroll**, 또는 **SQLSetPos**, 및 바인딩된 열은 결과 집합으로 데이터 버퍼 주소 아니고 길이/표시기 버퍼 주소는 0으로 오프셋이이 버퍼의 바이트에 배치 합니다. 주소와 오프셋의 합계에는 유효한 주소 여야 합니다. (즉, 중 하나 또는 모두 오프셋 및 오프셋 추가 되는 주소 수 있는 유효한 합계는 유효한 주소입니다.) SQL_ATTR_ROW_BIND_OFFSET_PTR 문 특성 포인터가 오프셋된 값을 오프셋된 값을 변경 하 여 변경할 수 있는 모든 데이터 바인딩 둘 이상의 집합에 적용할 수 있도록 합니다. 응용 프로그램은 커서를 닫을 때까지 포인터를 잘못 유지 되는지 확인 해야 합니다.  
  
> [!NOTE]  
>  바인딩 오프셋 ODBC 2에서 지원 되지 않습니다. *x* 드라이버입니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [블록 커서](../../../odbc/reference/develop-app/block-cursors.md)  
  
-   [스크롤 가능 커서](../../../odbc/reference/develop-app/scrollable-cursors.md)  
  
-   [ODBC 커서 라이브러리](../../../odbc/reference/develop-app/the-odbc-cursor-library.md)  
  
-   [여러 결과](../../../odbc/reference/develop-app/multiple-results.md)
