---
title: 스크롤 가능한 커서 유형 | 마이크로 소프트 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 63f29269ea209875a2e775cf8d523302fcb9a976
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304234"
---
# <a name="scrollable-cursor-types"></a>스크롤 가능 커서 형식
스크롤 가능한 커서의 네 가지 유형은 정적, 동적, 키 집합 기반 및 혼합입니다. 정적 커서는 변경 내용을 거의 또는 전혀 감지하지 않지만 구현하는 데 는 상대적으로 저렴합니다. 동적 커서는 모든 변경 내용을 감지하지만 구현하는 데 비용이 많이 듭니다. 키집합 기반 커서와 혼합 커서 사이에 는 대부분의 변경 내용을 감지하지만 동적 커서보다 적은 비용으로 있습니다.  
  
 다음 용어는 스크롤 가능한 커서의 각 유형의 특성을 정의하는 데 사용됩니다.  
  
-   **업데이트, 삭제 및 삽입을 소유합니다.** **SQLBulkOperations** 또는 **SQLSetPos에** 대한 호출 또는 위치 업데이트 또는 삭제 문을 사용하여 커서를 통해 만든 업데이트, 삭제 및 삽입합니다.  
  
-   **다른 업데이트, 삭제 및 삽입.** 동일한 트랜잭션의 다른 작업, 다른 트랜잭션을 통해 만든 작업 및 다른 응용 프로그램에서 만든 업데이트, 삭제 및 삽입을 포함하여 커서에서 작성하지 않은 업데이트, 삭제 및 삽입합니다.  
  
-   **회원.** 결과 집합의 행 집합입니다.  
  
-   **순서.** 커서에서 행을 반환하는 순서입니다.  
  
-   **값.** 결과 집합의 각 행의 값입니다.  
  
 데이터를 업데이트, 삭제 및 삽입하는 방법에 대한 자세한 내용은 [데이터 개요 업데이트를](../../../odbc/reference/develop-app/updating-data-overview.md)참조하십시오.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 정적 커서](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 동적 커서](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [키 집합 커서](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [혼합 커서](../../../odbc/reference/develop-app/mixed-cursors.md)
