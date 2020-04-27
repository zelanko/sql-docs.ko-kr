---
title: 조건 창의 검색 조건 결합 규칙 (Visual Database Tools) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- multiple OR clauses
- combining search conditions
- OR operator
- AND, Criteria pane
- multiple AND clauses
ms.assetid: d4859be5-ff5b-48b2-a101-ad40c6dbcc68
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3a1022770526386640f0ad2aa114a2161ba16dc8
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63140371"
---
# <a name="conventions-for-combining-search-conditions-in-the-criteria-pane-visual-database-tools"></a>조건 창의 검색 조건 결합 규칙(Visual Database Tools)
  AND와 OR 연산자를 여러 개 연결하여 다수의 검색 조건을 포함하는 쿼리를 만들 수 있습니다. AND 절과 OR 절을 조합하여 만든 쿼리는 복잡할 수 있으므로 쿼리 실행 시 쿼리를 해석하는 방법 및 [조건 창](visual-database-tools.md)과 [SQL 창](sql-pane-visual-database-tools.md)에서 쿼리를 나타내는 방법을 이해하면 도움이 됩니다.  
  
> [!NOTE]  
>  AND 또는 OR 연산자가 하나만 포함된 검색 조건에 대한 자세한 내용은 [한 열에 여러 검색 조건 지정&#40;Visual Database Tools&#41;](specify-multiple-search-conditions-for-one-column-visual-database-tools.md) 및 [여러 열에 여러 검색 조건 지정&#40;Visual Database Tools&#41;](specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)을 참조하세요.  
  
 아래에서 다음에 대한 정보를 찾을 수 있습니다.  
  
-   AND와 OR를 모두 포함하는 쿼리에서 AND와 OR의 우선 순위  
  
-   AND 절과 OR 절에 있는 조건들이 논리적으로 서로 연관되는 방법  
  
-   쿼리 및 뷰 디자이너가 AND와 OR를 모두 포함하는 쿼리를 조건 창에 나타내는 방법  
  
 아래의 설명을 쉽게 이해하기 위해 `employee` , `hire_date`및 `job_lvl`열을 포함하는 `status`테이블을 가정해 봅니다. 이 예제에서는 사용자가 직원의 근무 연수(입사 날짜), 업무 유형(직급), 상태(예: 퇴직) 등의 정보를 알고 있어야 한다고 가정합니다.  
  
## <a name="precedence-of-and-and-or"></a>AND와 OR의 우선 순위  
 쿼리를 실행하면 AND로 연결된 절을 먼저 계산한 다음 OR로 연결된 절을 계산합니다.  
  
> [!NOTE]  
>  NOT 연산자는 AND와 OR보다 우선 순위가 높습니다.  
  
 예를 들어, 직급이 낮은 직원 중에서 근무 연수가 5년이 넘는 직원 또는 입사 날짜에 관계없이 중간 직급의 직원을 찾기 위해 WHERE 절을 다음과 같이 구성할 수 있습니다.  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   job_lvl = 100 OR  
   job_lvl = 200  
  
```  
  
 OR보다 AND가 우선하는 기본 우선 순위를 무시하려면 SQL 창에서 특정 조건을 괄호로 묶으면 됩니다. 괄호 안의 조건은 항상 가장 먼저 계산됩니다. 예를 들어, 직급이 낮거나 중간인 직원 중에서 근무 연수가 5년이 넘는 직원을 모두 찾으려면 WHERE 절을 다음과 같이 구성하면 됩니다.  
  
```  
WHERE   
   hire_date < '01/01/95' AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
> [!TIP]  
>  AND 절과 OR 절을 결합할 때에는 기본 우선 순위에 의존하지 않고 항상 괄호를 사용하여 명확하게 나타내는 것이 좋습니다.  
  
## <a name="how-and-works-with-multiple-or-clauses"></a>OR 절이 여러 개 있는 경우 AND가 적용되는 방법  
 AND 절과 OR 절을 결합할 때 이 절들이 서로 연관되는 방식을 이해하면 쿼리 및 뷰 디자이너에서 복잡한 쿼리를 구성하고 이해하는 데 도움이 됩니다.  
  
 AND를 사용하여 여러 개의 조건을 연결하는 경우 AND로 연결된 첫째 조건 집합이 둘째 집합의 모든 조건에 적용됩니다. 즉 다른 조건에 AND로 연결된 조건은 둘째 집합에 있는 모든 조건에 분배됩니다. 예를 들어, 아래의 표현식은 AND 조건이 OR 조건 집합에 연결된 것을 보여 줍니다.  
  
```  
A AND (B OR C)  
```  
  
 위의 표현은 둘째 조건 집합에 AND 조건이 분배되는 방법을 보여 주는 아래 표현식과 논리적으로 일치합니다.  
  
```  
(A AND B) OR (A AND C)  
```  
  
 분배 법칙은 쿼리 및 뷰 디자이너를 사용하는 방법에 영향을 줍니다. 예를 들어, 직급이 낮거나 중간인 직원 중에서 근무 연수가 5년이 넘는 직원을 모두 찾는다고 가정해 봅니다. SQL 창에서 다음 WHERE 절을 문에 입력합니다.  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
   (job_lvl = 100 OR job_lvl = 200)  
```  
  
 AND로 연결된 절은 OR로 연결된 두 절에 모두 적용됩니다. OR 절에 있는 각 조건에 대해 AND 조건을 한 번씩 반복하면 이를 더 분명하게 표현할 수 있습니다. 다음 문은 앞의 문보다 더 분명하고 길지만 논리적으로는 동일합니다.  
  
```  
WHERE    (hire_date < '01/01/95' ) AND  
  (job_lvl = 100) OR   
  (hire_date < '01/01/95' ) AND   
  (job_lvl = 200)  
```  
  
 AND 절을 연결된 OR절에 분배하는 원칙은 포함된 개별 조건의 수에 관계없이 적용됩니다. 예를 들어, 근무 연수가 5년이 넘거나 현재 퇴직한 직원 중에서 직급이 높거나 중간인 직원을 찾는다고 가정해 봅니다. 이 경우 WHERE 절은 다음과 같습니다.  
  
```  
WHERE   
   (job_lvl = 200 OR job_lvl = 300) AND  
   (hire_date < '01/01/95' ) OR (status = 'R')  
```  
  
 AND로 연결된 조건이 분배된 후 WHERE 절은 다음과 같습니다.  
  
```  
WHERE   
   (job_lvl = 200 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 200 AND status = 'R') OR  
   (job_lvl = 300 AND hire_date < '01/01/95' ) OR  
   (job_lvl = 300 AND status = 'R')   
```  
  
## <a name="how-multiple-and-and-or-clauses-are-represented-in-the-criteria-pane"></a>다수의 AND 절과 OR 절을 조건 창에 나타내는 방법  
 쿼리 및 뷰 디자이너는 검색 조건을 [조건 창](visual-database-tools.md)에 나타냅니다. 그러나 AND와 OR로 연결된 여러 개의 절을 포함하는 경우 조건 창에 나타내는 방법이 예상과 다를 수도 있습니다. 또한 조건 창이나 [다이어그램 창](diagram-pane-visual-database-tools.md)에서 쿼리를 수정하면 SQL 문이 입력한 것과 다르게 변경됩니다.  
  
 일반적으로 다음 규칙에 따라 조건 창에서 AND 절과 OR 절이 나타납니다.  
  
-   AND로 연결된 모든 조건은 표 형태의 **필터** 열 또는 동일한 **또는...** 열에 나타납니다.  
  
-   OR로 연결된 모든 조건은 별도의 **또는...** 열에 나타납니다.  
  
-   AND 및 OR 절 조합의 논리적 결과가 AND가 여러 개의 OR 절에 분배되는 것이면 조건 창은 AND 절을 필요한 만큼 반복하여 이것을 명시적으로 표현합니다.  
  
 예를 들어, SQL 창에 다음과 같은 검색 조건을 만들 수 있습니다. 이 경우 AND로 연결된 두 절은 OR로 연결된 셋째 절보다 우선 순위가 높습니다.  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  (job_lvl = 100) OR   
  (status = 'R')  
```  
  
 쿼리 및 뷰 디자이너는 아래와 같이 조건 창에 이 WHERE 문을 나타냅니다.  
  
 ![조건 창의 OR 절 우선 순위](../../database-engine/media//vs-criteriapane1.gif "조건 창의 OR 절 우선 순위")  
  
 그러나 연결된 OR 절이 AND 절보다 우선 순위가 높으면 AND 절은 각 OR 절에 대해 반복됩니다. 이렇게 하면 AND 절이 각 OR 절에 분배됩니다. 예를 들어, SQL 창에서 다음과 같은 WHERE 절을 만들 수 있습니다.  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ( (job_lvl = 100) OR   
  (status = 'R') )  
```  
  
 쿼리 및 뷰 디자이너는 아래와 같이 조건 창에 이 WHERE 문을 나타냅니다.  
  
 ![조건 창의 여러 AND 및 OR 절](../../database-engine/media//vs-criteriapane2.gif "조건 창의 여러 AND 및 OR 절")  
  
 연결된 OR 절에 데이터 열이 단 하나 포함되어 있는 경우 쿼리 및 뷰 디자이너는 AND 절을 반복할 필요가 없도록 전체 OR 절을 표 형태의 단일 셀에 넣습니다. 예를 들어, SQL 창에서 다음과 같은 WHERE 절을 만들 수 있습니다.  
  
```  
WHERE (hire_date < '01/01/95' ) AND   
  ((status = 'R') OR (status = 'A'))  
```  
  
 쿼리 및 뷰 디자이너는 아래와 같이 조건 창에 이 WHERE 문을 나타냅니다.  
  
 ![조건 창에 정의된 링크된 OR 절](../../database-engine/media//vs-criteriapane3.gif "조건 창에 정의된 링크된 OR 절")  
  
 쿼리를 변경하면(예: 조건 창에서 값 하나를 변경) 쿼리 및 뷰 디자이너는 SQL 창에 SQL 문을 다시 만듭니다. 다시 만들어진 SQL 문은 원래 문보다는 조건 창에 표시되는 것과 비슷합니다. 예를 들어, 분배된 AND 절이 조건 창에 있는 경우 SQL 창에는 명시적으로 분배된 AND 절로 문이 다시 만들어집니다. 자세한 내용은 이 항목의 앞부분에서 설명한 "OR 절이 여러 개 있는 경우 AND가 적용되는 방법"을 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [검색 조건 지정&#40;Visual Database Tools&#41;](specify-search-criteria-visual-database-tools.md)  
  
  
