---
description: 행 그룹 축소(Visual Database Tools)
title: 행 그룹 축소
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- group collapsing [SQL Server]
- collapsing rows
- row collapsing [SQL Server]
ms.assetid: 7338dad0-965d-44ba-8c1a-b993acb7156d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: 47689de4d48f7c0e40315efd1b471bbe09f201f0
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88491734"
---
# <a name="collapse-groups-of-rows-visual-database-tools"></a>행 그룹 축소(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
쿼리 결과의 각 결과 행이 원본 데이터의 전체 행 그룹에 대응하는 쿼리 결과를 만들 수 있습니다. 행을 축소하는 경우 다음 사항에 유의해야 합니다.  
  
-   **중복 행을 제거할 수 있습니다.** 일부 쿼리의 경우 동일한 행이 여러 개 나타나는 결과 집합을 만들 수 있습니다. 예를 들어 각 행에 저자가 있는 도시의 이름과 주 이름이 있는 결과 집합을 만들 수 있습니다. 그러나 한 도시에 저자가 여러 명인 경우 똑같은 행이 여러 개 생깁니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT city, state  
    FROM authors  
    ```  
  
    앞의 쿼리에서 생성한 결과 집합은 그다지 유용하지 않습니다. 한 도시에 네 명의 저자가 있을 경우 결과 집합에는 똑같은 행이 네 개 포함됩니다. 결과 집합에 도시와 주 이외의 다른 열이 없으므로 동일한 행을 구분할 수 있는 방법이 없습니다. 행을 서로 다르게 만들 수 있는 추가 열을 포함시키는 것이 중복 행을 방지하는 한 가지 방법입니다. 예를 들어, 저자 이름을 포함하는 경우 같은 이름을 갖는 두 저자가 한 도시에 살고 있는 경우를 제외하고는 각 행은 서로 다르게 됩니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT city, state, fname, minit, lname  
    FROM authors  
    ```  
  
    앞의 쿼리에서는 발생할 수 있는 문제점을 제거할 수 있지만 실제로 문제를 해결하지는 못합니다. 즉, 결과 집합에 중복 행은 없지만 이것은 더 이상 도시에 관한 결과 집합이 아니기 때문입니다. 따라서 원래 결과 집합에서 중복 행을 제거하고 각 행에 도시가 나타나도록 하려면 서로 다른 행만 반환하여 쿼리를 만들면 됩니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT DISTINCT city, state  
    FROM authors  
    ```  
  
    중복 행을 제거하는 방법에 대한 자세한 내용은 [중복 행 제외&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/exclude-duplicate-rows-visual-database-tools.md)를 참조하세요.  
  
-   **행 그룹에서 계산할 수 있습니다.** 행 그룹의 정보를 요약할 수 있습니다. 예를 들어, 각 행에 저자 소재 도시의 이름과 주 이름 및 해당 도시에 있는 저자 수를 포함하는 결과 집합을 만들 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    ```  
  
    행 그룹 계산에 대한 자세한 내용은 [쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md) 및 [쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)를 참조하세요.  
  
-   **선택 기준을 사용하여 행 그룹을 포함할 수 있습니다.** 예를 들어, 각 행에 저자가 여러 명 있는 도시의 이름과 주 이름 및 해당 도시에 있는 저자 수를 포함하는 결과 집합을 만들 수 있습니다. 결과 SQL은 다음과 같습니다.  
  
    ```  
    SELECT city, state, COUNT(*)  
    FROM authors  
    GROUP BY city, state  
    HAVING COUNT(*) > 1  
    ```  
  
    행 그룹에 선택 조건을 적용하는 방법에 대한 자세한 내용은 [그룹 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-conditions-for-groups-visual-database-tools.md) 및 [동일한 쿼리에서 HAVING 및 WHERE 절 사용&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/use-having-and-where-clauses-in-the-same-query-visual-database-tools.md)을 참조하세요.  
  
## <a name="see-also"></a>참고 항목  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
