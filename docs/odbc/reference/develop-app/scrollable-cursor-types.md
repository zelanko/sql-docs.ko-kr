---
title: 스크롤 가능 커서 유형 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
ms.assetid: dbd32576-0453-4e90-ae45-1a81cee8259d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 54acbd1010d546649b1ad92a34289fa4d04da162
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="scrollable-cursor-types"></a>스크롤 가능 커서 유형
스크롤 가능 커서는 네 가지 유형의 정적, 동적, 키 집합 커서 및 혼합 됩니다. 정적 커서 없는 변경 내용을 거의 검색 되지만 상대적으로 경제적인 구현 하는 합니다. 동적 커서는 모든 변경 내용을 검색 하지만 구현 하는 데 큰 비용이 듭니다. 키 집합 커서와 혼합 커서는 중간으로 대부분의 변경 내용을 검색 하지만 동적 커서 보다 더 적은 비용으로에 두 유형의 합니다.  
  
 각 유형의 스크롤 가능 커서의 특성을 정의 하는 다음과 같은 용어가 사용 됩니다.  
  
-   **업데이트, 삭제 및 삽입을 소유 합니다.** 업데이트, 삭제 및 삽입에 대 한 호출을 사용 하 여 커서를 통해 **SQLBulkOperations** 또는 **SQLSetPos** 또는 위치 지정 업데이트 또는 삭제 문의 합니다.  
  
-   **다른 업데이트, 삭제 및 삽입 합니다.** 업데이트, 삭제 및 동일한 트랜잭션 내에서 다른 작업을 수행한 포함 하 여 커서에 의해 삽입, 다른 트랜잭션을 통해 내용이 및 다른 응용 프로그램에 의해 수행 합니다.  
  
-   **구성원입니다.** 결과 집합의 행 집합입니다.  
  
-   **순서입니다.** 커서에서 행이 반환 되는 순서입니다.  
  
-   **값입니다.** 결과 집합의 각 행의 값입니다.  
  
 업데이트, 삭제 및 데이터를 삽입 하는 방법에 대 한 정보를 참조 하십시오. [업데이트 데이터 개요](../../../odbc/reference/develop-app/updating-data-overview.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 정적 커서](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 동적 커서](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [키 집합 커서](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [혼합 커서](../../../odbc/reference/develop-app/mixed-cursors.md)
