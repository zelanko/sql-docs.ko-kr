---
title: 쿼리에서 테이블 제거(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- deleting tables
- removing tables
- dropping tables
- queries [SQL Server], tables
ms.assetid: 8fea0b4f-99b7-4050-8d6f-a97ffb839619
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: bda582c7b9171e89a43b6870b3b6c2df139b7b11
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52763615"
---
# <a name="remove-tables-from-queries-visual-database-tools"></a>쿼리에서 테이블 제거(Visual Database Tools)
  쿼리에서 테이블이나 모든 테이블 반환 개체를 제거할 수 있습니다.  
  
> [!NOTE]  
>  테이블이나 테이블 반환 개체를 제거해도 데이터베이스에서 실제로 삭제되는 항목은 없으며 현재 쿼리에서 해당 항목이 제거될 뿐입니다. 데이터베이스에서 테이블을 제거 하는 방법에 대 한 자세한 내용은 참조 하세요 [테이블 삭제 &#40;데이터베이스 엔진&#41;](../../relational-databases/tables/delete-tables-database-engine.md)합니다.  
  
### <a name="to-remove-a-table-or-table-structured-object"></a>테이블이나 테이블 구조 개체를 제거하려면  
  
-   **다이어그램 창**에서 테이블, 뷰, 사용자 정의 함수, 동의어 또는 쿼리를 선택한 다음 Delete 키를 누르거나, 개체를 마우스 오른쪽 단추로 클릭한 다음 대화 상자가 나타나면 **제거** 를 선택합니다. 여러 개체를 한번에 선택하거나 제거할 수 있습니다.  
  
     -또는-  
  
-    **SQL 창**에서 개체에 대한 모든 참조를 제거합니다.  
  
 테이블이나 테이블 반환 개체를 제거할 때 쿼리 및 뷰 디자이너에서는 해당 테이블이나 테이블 반환 개체가 관련된 조인을 자동으로 제거하고 **SQL 창** 과 **조건 창**에서 개체의 열에 대한 참조를 제거합니다. 그러나 해당 개체가 관련된 복합 식이 쿼리에 포함되어 있으면 개체가 자동으로 제거되지 않습니다. 이 경우 개체를 제거하려면 해당 개체에 대한 모든 참조를 제거해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [쿼리에 테이블 추가 &#40;Visual Database Tools&#41;](visual-database-tools.md)   
 [테이블 별칭 만들기 &#40;Visual Database Tools&#41;](create-table-aliases-visual-database-tools.md)   
 [검색 조건 지정 &#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)   
 [쿼리 결과 요약 &#40;Visual Database Tools&#41;](summarize-query-results-visual-database-tools.md)   
 [쿼리 관련 기본 작업 수행&#40;Visual Database Tools&#41;](perform-basic-operations-with-queries-visual-database-tools.md)  
  
  
