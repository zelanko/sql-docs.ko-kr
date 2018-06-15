---
title: 지원되는 쿼리 형식(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.component: ssms-visual-db
ms.reviewer: ''
ms.suite: sql
ms.technology: ssms
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Delete query
- queries [SQL Server], types
- Update query
- Query Designer [SQL Server], query types
- Criteria pane
- Insert Values query
- Select query
- Make Table query
- Insert Results query
- Diagram pane [Visual Database Tools]
- View Designer, query types
ms.assetid: 72b9116c-c128-4078-a78d-257a2955a3f6
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f451e77bec1a7609066280bcd5ef6bab2695e733
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "33050270"
---
# <a name="supported-query-types-visual-database-tools"></a>지원되는 쿼리 형식(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md)의 다이어그램 창과 조건 창(그래픽 창)에서 다음과 같은 쿼리 형식을 만들 수 있습니다.  
  
-   **선택 쿼리** 하나 이상의 테이블 또는 뷰에서 데이터를 검색합니다. 이 쿼리 형식은 SQL SELECT 문을 만듭니다.  
  
-   **결과 삽입** 기존 행을 한 테이블에서 다른 테이블에 복사하거나 동일한 테이블에 새 행으로 복사하여 새 행을 만듭니다. 이 쿼리 형식은 SQL INSERT INTO...SELECT 문을 만듭니다.  
  
-   **값 삽입** 새 행을 만들고 지정된 열에 값을 삽입합니다. 이 쿼리 형식은 SQL INSERT INTO...VALUES 문을 만듭니다.  
  
-   **업데이트 쿼리** 테이블에서 하나 이상의 기존 행에 있는 개별 열의 값을 변경합니다. 이 쿼리 형식은 SQL UPDATE...SET 문을 만듭니다.  
  
-   **삭제 쿼리** 테이블에서 하나 이상의 행을 제거합니다. 이 쿼리 형식은 SQL DELETE 문을 만듭니다.  
  
    > [!NOTE]  
    > 삭제 쿼리는 테이블의 전체 행을 제거합니다. 따라서 개별 데이터 열의 값을 삭제하려면 업데이트 쿼리를 사용하십시오.  
  
-   **테이블 만들기 쿼리** 새 테이블을 만들고 이 테이블에 쿼리 결과를 복사하여 행을 만듭니다. 이 쿼리 형식은 SQL SELECT...INTO 문을 만듭니다.  
  
그래픽 창을 사용하여 만들 수 있는 쿼리 외에 Union 쿼리를 포함하여 어떤 SQL 문이든지 SQL 창에 입력할 수 있습니다.  
  
그래픽 창에 나타낼 수 없는 SQL 문을 사용하여 쿼리를 만드는 경우 쿼리 및 뷰 디자이너는 해당 창을 흐리게 표시하여 현재 만들고 있는 쿼리를 반영하지 않음을 표시합니다. 그러나 흐리게 표시된 창은 여전히 활성 상태이며 대부분 이 창에서도 쿼리를 변경할 수 있습니다. 그래픽 창에 나타낼 수 있는 쿼리에 변경 내용이 반영되면 해당 그래픽 창은 더 이상 흐리게 표시되지 않습니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목(Visual Database Tools)](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[쿼리 형식(Visual Database Tools)](../../ssms/visual-db-tools/types-of-queries-visual-database-tools.md)  
  
