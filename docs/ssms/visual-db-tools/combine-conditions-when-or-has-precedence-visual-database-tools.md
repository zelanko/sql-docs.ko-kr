---
title: OR에 우선 순위가 있는 조건 조합(Visual Database Tools) | Microsoft 문서
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
- search conditions [SQL Server], combining
- precedence [SQL Server], Criteria pane
- search criteria [SQL Server], combining conditions
- combining search conditions
- OR operator
ms.assetid: b30f5ac9-25e7-4163-80ed-44e4bccb455d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4c8ef6c7e40e86710f405d1c293f55f48ee2197d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="combine-conditions-when-or-has-precedence-visual-database-tools"></a>OR에 우선 순위가 있는 조건 조합(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
조건을 OR로 연결하고 AND로 연결된 조건보다 높은 우선 순위를 부여하려면 각 OR 조건에 대하여 AND 조건을 반복해야 합니다.  
  
예를 들어, 근무 연수가 5년이 넘는 직원 중 직급이 낮거나 퇴직한 직원을 모두 찾는다고 가정합니다. 이 쿼리에는 세 개의 조건이 필요하며 하나의 조건이 두 개의 추가 조건과 AND로 연결되어 있어야 합니다.  
  
-   근무 연수가 5년이 넘는 직원  
  
-   직급이 100이거나 상태가 "R"(퇴직)인 직원  
  
다음 절차는 조건 창에서 이런 형식의 쿼리를 만드는 방법을 설명합니다.  
  
### <a name="to-combine-conditions-when-or-has-precedence"></a>OR에 우선 순위가 있는 경우 조건을 조합하려면  
  
1.  [조건 창](../../ssms/visual-db-tools/criteria-pane-visual-database-tools.md)에서 검색할 데이터 열을 추가합니다. AND로 연결된 둘 이상의 조건을 사용하여 동일한 열을 검색하려면 검색할 각 값에 대하여 한 번씩 데이터 열 이름을 표에 추가해야 합니다.  
  
2.  첫째 조건은 표 형태의 **필터** 열에 입력하고 둘째 및 이후의 조건은 별도의 **또는...** 열에 입력하여 OR로 연결할 조건을 만듭니다. 예를 들어 `job_lvl` 열과 `status` 열을 검색하는 조건을 OR로 연결하려면 `= 100` 의 **필터** 열에는 `job_lvl` 을 입력하고 `= 'R'` 의 **또는...** 열에는 `status`를 입력합니다.  
  
    표 형태로 된 값을 입력하면 SQL 창의 문에 다음과 같은 WHERE 절이 만들어집니다.  
  
    ```  
    WHERE (job_lvl = 100) OR (status = 'R')  
    ```  
  
3.  각 OR 조건에 대해 한 번씩 입력하여 AND 조건을 만듭니다. 해당 OR 조건과 동일한 표 형태 열에 각 엔트리를 둡니다. 예를 들어 `hire_date` 열을 검색하여 두 개의 OR 조건에 적용하는 AND 조건을 추가하려면 조건 열과 `< '1/1/91'` 또는... **열에 둘 다** 을 입력합니다.  
  
    표 형태로 된 값을 입력하면 SQL 창의 문에 다음과 같은 WHERE 절이 만들어집니다.  
  
    ```  
    WHERE (job_lvl = 100) AND   
      (hire_date < '01/01/91' ) OR  
      (status = 'R') AND   
      (hire_date < '01/01/91' )  
    ```  
  
    > [!TIP]  
    > AND 조건을 반복하려면 한 번 추가한 다음 **편집** 메뉴에서 **잘라내기** 와 **붙여넣기** 명령을 사용하여 다른 OR 조건에 대해 반복하면 됩니다.  
  
쿼리 및 뷰 디자이너에서 만든 WHERE 절은 괄호를 사용하여 OR의 우선 순위를 AND의 우선 순위보다 높게 지정한 다음의 WHERE 절과 동등합니다.  
  
```  
WHERE (job_lvl = 100 OR status = 'R') AND  
   (hire_date < '01/01/91')  
```  
  
> [!NOTE]  
> [SQL 창](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md)에서 위에 표시된 형식으로 검색 조건을 입력한 다음 다이어그램 창이나 조건 창에서 쿼리를 변경하면 쿼리 및 뷰 디자이너는 두 OR 조건 모두에 명시적으로 배포된 AND 조건과 형식이 일치하는 SQL 문을 다시 만듭니다.  
  
## <a name="see-also"></a>참고 항목  
[조건 창의 검색 조건 결합 규칙&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
