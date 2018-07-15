---
title: AND에 우선 순위가 있는 조건 조합(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- AND, Criteria pane
ms.assetid: 450eb2eb-6ea3-405b-8dd2-1ff926c016e7
caps.latest.revision: 11
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: dd05831ace669f1d71bb1a46819b1220a766ce27
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37234383"
---
# <a name="combine-conditions-when-and-has-precedence-visual-database-tools"></a>AND에 우선 순위가 있는 조건 조합(Visual Database Tools)
  AND를 사용하여 조건을 조합하려면 각 조건에 한 번씩, 즉 쿼리에 열을 두 번 추가합니다. 조건을 OR와 조합하려면 첫째 조건은 필터 열에 지정하고 추가 조건은 **또는...** 열에 지정합니다.  
  
 예를 들어, 근무 연수가 5년이 넘으면서 직급이 낮은 직원과 고용 날짜에 상관 없이 중간 직급인 직원을 찾는다고 가정합니다. 이 쿼리에는 세 개의 조건이 필요하며 그 중 두 조건은 AND로 연결되어 있어야 합니다.  
  
-   근무 연수가 5년이 넘으면서 직급이 100인 직원  
  
     -또는-  
  
-   직급이 200인 직원  
  
### <a name="to-combine-conditions-when-and-has-precedence"></a>AND에 우선 순위가 있는 경우 조건을 조합하려면  
  
1.  [조건 창](visual-database-tools.md)에서 검색할 데이터 열을 추가합니다. AND로 연결된 둘 이상의 조건을 사용하여 동일한 열을 검색하려면 검색할 각 값에 대하여 한 번씩 데이터 열 이름을 표에 추가해야 합니다.  
  
2.  **필터** 열에 AND로 연결할 모든 조건을 입력합니다. 예를 들어, `hire_date` 열과 `job_lvl` 열을 검색하는 조건을 AND로 연결하려면 필터 열에 각각 `< '1/1/91'` 값과 `= 100`값을 입력합니다.  
  
     이런 표 형태 엔트리는 [SQL 창](sql-pane-visual-database-tools.md)에서 문에 다음과 같은 WHERE 절을 만듭니다.  
  
    ```  
    WHERE (hire_date < '01/01/91') AND  
      (job_lvl = 100)  
    ```  
  
3.  표 형태의 **또는...** 열에 OR로 연결할 조건을 입력합니다. 예를 들어 `job_lvl` 열에서 다른 값을 검색하는 조건을 추가하려면 **또는...** 열에 다른 값(예: `= 200`)을 추가합니다.  
  
     **또는...** 열에 값을 추가하면 SQL 창에 있는 문의 WHERE 절에 또 다른 조건이 추가됩니다.  
  
    ```  
    WHERE (hire_date < '01/01/91' ) AND  
      (job_lvl = 100) OR   
      (job_lvl = 200)  
    ```  
  
## <a name="see-also"></a>관련 항목  
 [OR에 우선 순위가 있는 조건 조합 &#40;Visual Database Tools&#41;](combine-conditions-when-or-has-precedence-visual-database-tools.md)   
 [조건 창의 검색 조건 결합 규칙 &#40;Visual Database Tools&#41;](conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)   
 [검색 값 입력 규칙 &#40;Visual Database Tools&#41;](rules-for-entering-search-values-visual-database-tools.md)   
 [검색 조건 지정&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
