---
title: 집계 쿼리에서 열 작업
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- HAVING clause, query summary results
- GROUP BY clause, query summary results
- aggregate queries [SQL Server]
- WHERE clause, query summary results
ms.assetid: 1b82681f-3d4f-4b9a-bb1d-2060e44f2577
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.openlocfilehash: 427f367eac38f2c5899f06c022e614bde80f37fb
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/29/2020
ms.locfileid: "75246239"
---
# <a name="work-with-columns-in-aggregate-queries-visual-database-tools"></a>집계 쿼리에서 열 작업(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
집계 쿼리를 만드는 경우 [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 에서는 특정 가정을 만들어 유효한 쿼리를 만들 수 있도록 합니다. 예를 들어 집계 쿼리를 만들 때 출력할 데이터 열을 표시하면 쿼리 및 뷰 디자이너가 이 열을 자동으로 GROUP BY 절의 일부로 만들기 때문에 요약에서 개별 행의 내용을 실수로 표시할 염려가 없습니다.  
  
## <a name="using-group-by"></a>그룹화 방법 사용  
쿼리 및 뷰 디자이너는 아래 지침을 사용하여 열 작업을 수행합니다.  
  
-   그룹화 방법 옵션을 선택하거나 쿼리에 집계 함수를 추가하면 출력용으로 표시되거나 정렬에 사용된 모든 열이 GROUP BY 절에 자동으로 추가됩니다. 열이 이미 집계 함수의 일부인 경우 GROUP BY 절에 자동으로 추가되지 않습니다.  
  
    특정 열을 GROUP BY 절의 일부로 포함하지 않으려면 조건 창의 그룹화 방법 열에서 다른 옵션을 선택하여 수동으로 변경해야 합니다. 그러나 이렇게 하면 쿼리 및 뷰 디자이너가 실행되지 않는 쿼리가 나타날 수 있는 옵션을 선택하는 것을 막을 수 없습니다.  
  
-   조건 창 또는 SQL 창에서 집계 함수에 쿼리 출력 열을 수동으로 추가하는 경우 쿼리 및 뷰 디자이너는 쿼리에서 다른 출력 열을 자동으로 삭제하지 않으므로 쿼리 결과에서 나머지 열을 제거하거나 GROUP BY 절 또는 집계 함수의 일부로 만들어야 합니다.  
  
조건 창의 필터 열에 검색 조건을 입력하는 경우 쿼리 및 뷰 디자이너는 다음 규칙을 따릅니다.  
  
-   집계 쿼리를 아직 지정하지 않아 표의 **그룹화 방법** 열이 표시되지 않는 경우 검색 조건이 WHERE 절에 놓입니다.  
  
-   집계 쿼리에 있으면서 **그룹화 방법** 열에서 **위치** 옵션을 선택한 경우 검색 조건이 WHERE 절에 놓입니다.  
  
-   **그룹화 방법** 열에 **위치**이외의 다른 값이 있는 경우 검색 조건이 HAVING 절에 놓입니다.  
  
## <a name="using-the-having-and-where-clauses"></a>HAVING 및 WHERE 절 사용  
아래 원칙은 검색 조건으로 집계 쿼리에서 열을 참조할 수 있는 방법에 대해 설명합니다. 일반적으로 검색 조건에 열을 사용하면 요약할 행을 필터링하거나(WHERE 절) 최종 출력에 나타날 그룹화된 결과를 결정할 수 있습니다(HAVING 절).  
  
-   개별 데이터 열은 쿼리에 사용되는 방법에 따라 WHERE 절 또는 HAVING 절에 나타날 수 있습니다.  
  
-   WHERE 절은 요약 및 그룹화할 행의 하위 집합을 선택하는 데 사용되므로 그룹화하기 전에 적용됩니다. 따라서 데이터 열이 GROUP BY 절의 일부가 아니거나 집계 함수에 포함되어 있지 않더라도 WHERE 절에 사용할 수 있습니다. 예를 들어 다음 문은 가격이 $10.00가 넘는 책의 제목을 모두 선택하여 해당 가격의 평균을 계산합니다.  
  
    ```  
    SELECT AVG(price)  
    FROM titles  
    WHERE price > 10  
    ```  
  
-   GROUP BY 절 또는 집계 함수에서도 사용되는 열을 포함하는 검색 조건을 만들면 해당 검색 조건이 WHERE 절 또는 HAVING 절로 나타날 수 있으며, 이에 따라 사용자는 조건 작성 여부 및 시기를 결정할 수 있습니다. 예를 들어 다음 문은 각 출판사가 발행하는 책의 평균 가격을 계산한 다음 평균 가격이 $10.00가 넘는 출판사의 평균 가격을 표시합니다.  
  
    ```  
    SELECT pub_id, AVG(price)  
    FROM titles  
    GROUP BY pub_id  
    HAVING (AVG(price) > 10)  
    ```  
  
-   검색 조건으로 집계 함수를 사용하는 경우 조건에는 요약이 포함되며 따라서 HAVING 절의 일부가 되어야 합니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
  
