---
title: 쿼리 결과 행 그룹화(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- summarizing table subsets
- grouping rows
- grouping query results
ms.assetid: b07082d5-4d55-4903-9af9-4c470554c6d3
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 4cd80e7d999314c549df4ebb5e51aa2a0ca2d3f8
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63154823"
---
# <a name="group-rows-in-query-results-visual-database-tools"></a>쿼리 결과 행 그룹화(Visual Database Tools)
  부분합을 계산하거나 테이블의 하위 집합에 대한 다른 요약 정보를 표시하려면 집계 쿼리를 사용하여 그룹을 만듭니다. 각 그룹은 테이블에서 값이 동일한 모든 행의 데이터를 요약하는 데 사용됩니다.  
  
 예를 들어, `titles` 테이블에서 출판사별로 구분된 도서 평균 가격 결과를 확인해야 할 수도 있습니다. 이 경우 출판사별로 쿼리를 그룹화할 수 있습니다(예: `pub_id`). 다음과 같은 쿼리 결과가 만들어집니다.  
  
 ![쿼리 결과: 게시자별로 그룹화된 평균 가격](../../database-engine/media//dv3w9e1.gif "쿼리 결과: 게시자별로 그룹화된 평균 가격")  
  
 데이터를 그룹화하면 다음과 같이 요약 데이터나 그룹화된 데이터만 표시할 수도 있습니다.  
  
-   GROUP BY 절에 나타나는 그룹화된 열의 값. 위 예제에서 `pub_id` 는 그룹화된 열입니다.  
  
-   SUM( ) 및 AVG( ) 같은 집계 함수를 통해 얻은 값. 위 예제에서 두 번째 열은 AVG( ) 함수를 `price` 열에 적용하여 얻은 결과입니다.  
  
 개별 행의 값은 표시할 수 없습니다. 예를 들어, 출판사만을 기준으로 그룹화한 경우 쿼리의 개별 책 제목은 표시할 수 없습니다. 따라서 쿼리 결과에 열을 추가하면 [쿼리 및 뷰 디자이너](visual-database-tools.md) 의 [SQL 창](sql-pane-visual-database-tools.md)에서 이러한 열이 문의 GROUP BY 절에 자동으로 추가됩니다. 열에 대한 집계 함수를 지정하면 해당 열을 대신 집계할 수 있습니다.  
  
 두 개 이상의 열을 기준으로 그룹화하는 경우 쿼리의 각 그룹에는 전체 그룹 열의 집계 값이 표시됩니다.  
  
 예를 들어, `titles` 테이블에 대한 아래 쿼리에서는 출판사(`pub_id`)와 도서 종류(`type`)를 기준으로 결과를 그룹화합니다. 쿼리 결과는 출판사 순으로 정렬되고 각 출판사에서 발생하는 서로 다른 도서 종류 각각에 대한 요약 정보가 결과에 표시됩니다.  
  
```  
SELECT pub_id, type, SUM(price) Total_price  
FROM titles  
GROUP BY pub_id, type  
```  
  
 출력 결과는 다음과 같습니다.  
  
 ![쿼리 결과: 게시자 및 유형별로 그룹화된 가격](../../database-engine/media//dv3w9e2.gif "쿼리 결과: 게시자 및 유형별로 그룹화된 가격")  
  
### <a name="to-group-rows"></a>행을 그룹화하려면  
  
1.  요약하려는 테이블을 다이어그램 창에 추가하여 쿼리를 시작합니다.  
  
2.  다이어그램 창의 배경을 마우스 오른쪽 단추로 클릭한 다음 바로 가기 메뉴에서 **그룹화 방법 추가** 를 선택합니다. 쿼리 및 뷰 디자이너에서 **그룹화 방법** 열이 조건 창의 표에 추가됩니다.  
  
3.  그룹화하려는 하나 이상의 열을 조건 창에 추가합니다. 쿼리 결과에 열을 표시하려면 해당 결과에 대해 **출력** 열을 선택해야 합니다.  
  
     쿼리 및 뷰 디자이너의 SQL 창에서 GROUP BY 절이 문에 추가됩니다. 예를 들어, SQL 문은 다음과 같은 형식입니다.  
  
    ```  
    SELECT pub_id  
    FROM titles  
    GROUP BY pub_id  
    ```  
  
4.  집계하려는 하나 이상의 열을 조건 창에 추가합니다. 열을 출력하도록 선택되어 있어야 합니다.  
  
5.  집계하려는 열에 대한 **그룹화 방법** 표 셀에서 적절한 집계 함수를 선택합니다.  
  
     쿼리 및 뷰 디자이너에서 요약 대상 열에 대한 열 별칭이 자동으로 할당됩니다. 자동으로 생성된 이 별칭을 좀 더 의미 있는 별칭으로 바꿀 수 있습니다. 자세한 내용은 [열 별칭 만들기&#40;Visual Database Tools&#41;](create-column-aliases-visual-database-tools.md)를 참조하세요.  
  
     ![쿼리 결과 집합에 열 별칭 추가](../../database-engine/media//dv3w9e3.gif "쿼리 결과 집합에 열 별칭 추가")  
  
     해당 문이 **SQL** 창에 다음과 같은 형식으로 표시됩니다.  
  
    ```  
    SELECT   pub_id, SUM(price) AS Totalprice  
    FROM     titles  
    GROUP BY pub_id  
    ```  
  
## <a name="see-also"></a>참고 항목  
 [쿼리 결과 정렬 및 그룹화&#40;Visual Database Tools&#41;](sort-and-group-query-results-visual-database-tools.md)  
  
  
