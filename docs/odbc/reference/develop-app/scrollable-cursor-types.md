---
title: 스크롤 가능 커서 유형 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6290d18ec26fcfa6e2960c3a2c1c408938d9e0e4
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62468580"
---
# <a name="scrollable-cursor-types"></a>스크롤 가능 커서 형식
스크롤 가능 커서는 네 가지 유형의 정적, 동적, 키 집합 커서 및 혼합 됩니다. 정적 커서 적거나 없는 변경 내용을 검색 되지만 구현에 비교적 저렴 합니다. 동적 커서는 모든 변경 내용을 검색 하지만 구현 하는 데 비용이 많이 드는 합니다. 키 집합 커서와 혼합 커서 사이 동적 커서에 비해 저렴 하지만 대부분의 변경 내용 감지 사이.  
  
 다음 용어는 각 유형의 스크롤 가능 커서의 특징을 정의 하는 데 사용 됩니다.  
  
-   **업데이트, 삭제 및 삽입을 소유 합니다.** 업데이트, 삭제 및 삽입에 대 한 호출을 사용 하 여 커서를 통해 **SQLBulkOperations** 하거나 **SQLSetPos** 배치를 사용 하 여 또는 update 또는 delete 문입니다.  
  
-   **다른 업데이트, 삭제 및 삽입 합니다.** 업데이트, 삭제 및 동일한 트랜잭션에서 다른 작업을 수행한 포함 하 여 커서에 의해 삽입, 다른 트랜잭션을 통해 내용이 및 다른 응용 프로그램에서 수행 합니다.  
  
-   **멤버 자격입니다.** 결과 집합의 행 집합입니다.  
  
-   **순서입니다.** 행이 커서에 의해 반환 되는 순서입니다.  
  
-   **값입니다.** 결과 집합의 각 행의 값입니다.  
  
 업데이트, 삭제 및 데이터를 삽입 하는 방법에 대 한 정보를 참조 하세요 [업데이트 데이터 개요](../../../odbc/reference/develop-app/updating-data-overview.md)합니다.  
  
 이 섹션에서는 다음 항목을 다룹니다.  
  
-   [ODBC 정적 커서](../../../odbc/reference/develop-app/odbc-static-cursors.md)  
  
-   [ODBC 동적 커서](../../../odbc/reference/develop-app/odbc-dynamic-cursors.md)  
  
-   [키 집합 커서](../../../odbc/reference/develop-app/keyset-driven-cursors.md)  
  
-   [혼합 커서](../../../odbc/reference/develop-app/mixed-cursors.md)
