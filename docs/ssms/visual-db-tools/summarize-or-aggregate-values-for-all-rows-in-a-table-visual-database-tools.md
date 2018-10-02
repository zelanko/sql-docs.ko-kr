---
title: 테이블에 있는 모든 행의 값 요약 또는 집계 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing query results
- aggregate functions [SQL Server], summarizing query results
ms.assetid: f5af876e-f937-4110-ba09-07999c35a699
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1e8d82ed31033d32c714889a2835df95a70bf589
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47808551"
---
# <a name="summarize-or-aggregate-values-for-all-rows-in-a-table-visual-database-tools"></a>테이블에 있는 모든 행의 값 요약 또는 집계(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
## <a name="aggregate-function"></a>집계 함수
집계 함수를 사용하면 테이블의 모든 값을 요약할 수 있습니다. 예를 들어, `titles` 테이블의 책 전체에 대한 가격 합계를 표시하는 다음과 같은 쿼리를 만들 수 있습니다.  
  
```  
SELECT SUM(price)  
FROM titles  
```  
  
집계 함수를 여러 열에 사용하여 동일한 쿼리에서 여러 집계를 만듭니다. 예를 들어, `price` 열의 합계와 `discount` 열의 평균을 계산하는 쿼리를 만들 수 있습니다.  
  
동일한 쿼리에서 합계, 개수, 평균 등과 같이 서로 다른 방식으로 동일한 열을 집계할 수 있습니다. 예를 들어, 다음 쿼리는 `price` 테이블의 `titles` 열에 대한 평균과 합계를 계산합니다.  
  
```  
SELECT AVG(price), SUM(price)  
FROM titles  
```  
  
검색 조건을 추가하면 해당 조건에 맞는 행의 하위 집합을 집계할 수 있습니다.  

**참고!** 테이블의 전체 행 수나 특정 조건에 맞는 행의 수를 계산할 수도 있습니다. 자세한 내용은 [테이블의 행 계산&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/count-rows-in-a-table-visual-database-tools.md)을 참조하세요.  
  
  
테이블의 모든 행에 대한 단일 집계 값을 만들면 집계 값 자체만 표시됩니다. 예를 들어, `price` 테이블의 `titles` 열에 대한 값을 합산하는 경우 개별 제목, 출판사 이름 등은 표시되지 않습니다.  
 
 **!** 부분합을 계산하는 경우 즉, 그룹을 만드는 경우 각 그룹에 대한 열 값을 표시할 수 있습니다. 자세한 내용은 [쿼리 결과 행 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)를 참조하세요.  

## <a name="aggregate-values-for-all-rows"></a>모든 행에 대한 값 집계  
  
1.  집계하려는 테이블이 다이어그램 창에 표시되어 있어야 합니다.  
  
2.  다이어그램 창의 배경을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **그룹화 방법** 을 선택합니다. [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 에서 **그룹화 방법** 열이 조건 창의 표에 추가됩니다.  
  
3.  집계하려는 열을 조건 창에 추가합니다. 열을 출력하도록 선택되어 있어야 합니다.  
  
    쿼리 및 뷰 디자이너에서 요약 대상 열에 대한 열 별칭이 자동으로 할당됩니다. 이 별칭을 좀 더 의미 있는 별칭으로 바꿀 수 있습니다. 자세한 내용은 [열 별칭 만들기&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/create-column-aliases-visual-database-tools.md)를 참조하세요.  
  
4.  표 형태의 **그룹화 방법** 열에서 **Sum**, **Avg**, **Min**, **Max**, **Count** 등 적절한 집계 함수를 선택합니다. 결과 집합에서 고유 행만 집계하려면 집계 함수를 선택할 때 DISTINCT 옵션을 사용합니다(예: **Min Distinct**). **Group By**, **Expression**또는 **Where**는 선택하지 말아야 합니다. 모든 행을 집계할 때는 이러한 옵션이 적용되지 않습니다.  
  
    쿼리 및 뷰 디자이너에서 [SQL 창](../../ssms/visual-db-tools/sql-pane-visual-database-tools.md) 에 있는 문의 열 이름이 사용자가 지정한 집계 함수로 바뀝니다. 예를 들어, SQL 문은 다음과 같은 형식입니다.  
  
    ```  
    SELECT SUM(price)  
    FROM titles  
    ```  
  
5.  쿼리에서 두 개 이상의 집계를 만들려면 3단계와 4단계를 반복합니다.  
  
    쿼리 결과 목록이나 정렬 기준 목록에 다른 열을 추가하면 쿼리 및 뷰 디자이너에서 표 형태의 **그룹화 방법** 열에 **Group By** 라는 용어가 자동으로 입력됩니다. 적절한 집계 함수를 선택합니다.  
  
6.  필요한 경우 검색 조건을 추가하여 요약하려는 행의 하위 집합을 지정합니다.  
  
쿼리를 실행하면 지정된 집계가 결과 창에 표시됩니다.  
  
> [!NOTE]  
> 그룹화 방법 모드를 명시적으로 종료하지 않는 한 쿼리 및 뷰 디자이너의 SQL 창에서 집계 함수가 SQL 문의 일부로 계속 유지됩니다. 따라서, 다이어그램 창에 표시되는 테이블이나 테이블 반환 개체를 변경하거나 쿼리 형식을 변경하여 쿼리를 수정하면 결과 쿼리에 잘못된 집계 함수가 포함될 수 있습니다.  
  
## <a name="see-also"></a>참고 항목  
[쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[쿼리 결과 요약&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
