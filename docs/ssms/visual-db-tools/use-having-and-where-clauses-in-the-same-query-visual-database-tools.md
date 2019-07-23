---
title: 동일한 쿼리에서 HAVING 및 WHERE 절 사용 | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], excluding rows
- search criteria [SQL Server], WHERE clause
- search conditions [SQL Server], HAVING clause
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- HAVING clause, search criteria
- search conditions [SQL Server], WHERE clause
- WHERE clause, search criteria
- excluding rows
ms.assetid: 1e07cf56-b4b7-4c49-8ddd-c276812a7148
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 84abe2405901012565e98950320c8d5aa92fa903
ms.sourcegitcommit: e7d921828e9eeac78e7ab96eb90996990c2405e9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/16/2019
ms.locfileid: "68263036"
---
# <a name="use-having-and-where-clauses-in-the-same-query-visual-database-tools"></a>동일한 쿼리에서 HAVING 및 WHERE 절 사용(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
경우에 따라서는 HAVING 절을 사용하여 그룹 전체에 조건을 적용하기 전에 WHERE 절을 사용하여 그룹에서 개별 행을 제외해야 할 수도 있습니다.  
  
HAVING 절은 WHERE 절과 비슷하지만 그룹 전체 즉, 그룹을 나타내는 결과 집합의 행에만 적용된다는 점에서 차이가 있습니다. 반면, WHERE 절은 개별 행에 적용됩니다. 쿼리에는 WHERE 절과 HAVING 절이 모두 포함될 수 있습니다. 이 경우 다음을 수행합니다.  
  
-   다이어그램 창에서 테이블이나 테이블 반환 개체의 개별 행에 WHERE 절이 먼저 적용됩니다. WHERE 절의 조건에 맞는 행만 그룹화됩니다.  
  
-   그런 다음 결과 집합의 행에 HAVING 절이 적용됩니다. HAVING 조건에 맞는 그룹만 쿼리 출력에 표시됩니다. 집계 함수나 GROUP BY 절에도 나타나는 열에만 HAVING 절을 적용할 수 있습니다.  
  
예를 들어 `titles` 및 `publishers` 테이블을 조인하여 여러 출판사의 평균 도서 가격을 표시하는 쿼리를 만드는 경우를 생각해 볼 수 있습니다. 캘리포니아 주에 있는 출판사 등과 같이 특정 출판사 세트에 대해서만 평균 가격을 표시하려는 경우 그 중에서도 평균 가격이 $10.00 이상인 경우로만 결과를 제한하려고 합니다.  
  
평균 가격을 계산하기 전에 캘리포니아에 있지 않은 출판사는 모두 제외하도록 WHERE 절을 사용하여 첫 번째 조건을 설정할 수 있습니다. 두 번째 조건은 데이터를 그룹화하고 요약한 결과를 기반으로 해야 하므로 이 조건에는 HAVING 절이 필요합니다. 결과 SQL 문은 다음과 같습니다.  
  
```  
SELECT titles.pub_id, AVG(titles.price)  
FROM titles INNER JOIN publishers  
   ON titles.pub_id = publishers.pub_id  
WHERE publishers.state = 'CA'  
GROUP BY titles.pub_id  
HAVING AVG(price) > 10  
```  
  
HAVING 절과 WHERE 절을 모두 조건 창에서 만들 수 있습니다. 기본적으로 열에 대한 검색 조건을 지정하면 이 조건이 HAVING 절의 일부가 됩니다. 그러나 이 조건이 WHERE 절에 사용되도록 변경할 수도 있습니다.  
  
동일한 열을 대상으로 WHERE 절과 HAVING 절을 만들 수 있습니다. 이렇게 하려면 조건 창에 열을 두 번 추가한 다음 한 인스턴스는 HAVING 절의 일부로 지정하고 다른 인스턴스는 WHERE 절의 일부로 지정해야 합니다.  
  
### <a name="to-specify-a-where-condition-in-an-aggregate-query"></a>집계 쿼리에서 WHERE 조건을 지정하려면  
  
1.  쿼리의 그룹을 지정합니다. 자세한 내용은 [쿼리 결과 행 그룹화(Visual Database Tools)](../../ssms/visual-db-tools/group-rows-in-query-results-visual-database-tools.md)를 참조하세요.  
  
2.  WHERE 조건의 기반으로 삼을 열이 아직 조건 창에 없으면 이 열을 추가합니다.  
  
3.  데이터 열이 GROUP BY 절의 일부가 아니거나 집계 함수에 포함되지 않은 경우 **출력** 열을 지웁니다.  
  
4.  **필터** 열에서 WHERE 조건을 지정합니다. 쿼리 및 뷰 디자이너에서 SQL 문의 HAVING 절에 조건을 추가합니다.  
  
    > [!NOTE]  
    > 이 절차의 예제로 나와 있는 쿼리에서는 `titles` 테이블과 `publishers`테이블을 조인합니다.  
  
    HAVING 절은 쿼리의 다음 지점에서 SQL 문에 포함되어 있습니다.  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    GROUP BY titles.pub_id  
    HAVING publishers.state = 'CA'  
    ```  
  
5.  **그룹화 방법** 열의 그룹 및 요약 옵션 목록에서 **Where** 를 선택합니다. 쿼리 및 뷰 디자이너에서 SQL 문의 HAVING 절에 있던 조건이 제거되고 WHERE 절에 조건이 추가됩니다.  
  
    다음과 같이 WHERE 절이 대신 포함되도록 SQL 문이 변경됩니다.  
  
    ```  
    SELECT titles.pub_id, AVG(titles.price)  
    FROM titles INNER JOIN publishers   
       ON titles.pub_id = publishers.pub_id  
    WHERE publishers.state = 'CA'  
    GROUP BY titles.pub_id  
    ```  
  
## <a name="see-also"></a>참고 항목  
[쿼리 결과 정렬 및 그룹화(Visual Database Tools)](../../ssms/visual-db-tools/sort-and-group-query-results-visual-database-tools.md)  
[쿼리 결과 요약(Visual Database Tools)](../../ssms/visual-db-tools/summarize-query-results-visual-database-tools.md)  
  
