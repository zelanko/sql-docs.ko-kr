---
title: 행 포함 또는 제외(Visual Database Tools) | Microsoft 문서
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
- included rows
- search conditions [SQL Server], HAVING clause
- search criteria [SQL Server], including rows
- row excluded in search [SQL Server]
- search criteria [SQL Server], HAVING clause
- search conditions [SQL Server], WHERE clause
- row included in search [SQL Server]
- excluding rows
ms.assetid: ba4e1202-31a2-444d-8365-c68a530ef223
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: dfb60ac381570489fe5fdb5d8ac0b6ec75e15cd0
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65096802"
---
# <a name="include-or-exclude-rows-visual-database-tools"></a>행 포함 또는 제외(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
선택 쿼리가 반환할 행 수를 제한하려면 검색 조건 또는 필터링 기준을 만듭니다. SQL에서 검색 조건은 문의 WHERE 절에 나타나거나 집계 쿼리를 만들 경우 HAVING 절에 나타납니다.  
  
> [!NOTE]  
> 검색 조건을 사용하여 업데이트, 결과 삽입, 값 삽입, 삭제 또는 테이블 만들기 쿼리의 영향을 받는 행을 표시할 수도 있습니다.  
  
쿼리를 실행할 때 [!INCLUDE[ssDE](../../includes/ssde_md.md)] 은 검색 조건을 검사하여 검색할 테이블의 각 행에 검색 조건을 적용합니다. 행이 검색 조건에 맞으면 쿼리에 포함됩니다. 예를 들어, 특정 지역에 있는 직원들을 모두 찾는 검색 조건은 다음과 같습니다.  
  
```  
region = 'UK'  
```  
  
여러 검색 조건을 사용하여 결과에 행을 포함시키는 기준을 만들 수 있습니다. 예를 들어, 다음 검색 조건은 두 개의 검색 조건으로 구성됩니다. 쿼리는 행이 두 조건을 모두 충족하는 경우에만 해당 행을 결과 집합에 포함시킵니다.  
  
```  
region = 'UK' AND product_line = 'Housewares'  
```  
  
이러한 조건을 AND 또는 OR를 사용하여 결합할 수 있습니다. 위의 예에서는 AND를 사용하였으며 반대로 아래 조건에서는 OR를 사용합니다. 결과 집합에는 검색 조건 중 한 개 또는 두 개를 모두 충족하는 행이 포함됩니다.  
  
```  
region = 'UK' OR product_line = 'Housewares'  
```  
  
검색 조건을 단일 열에 결합할 수도 있습니다. 예를 들어, 다음 조건은 region 열에 두 개의 조건을 결합합니다.  
  
```  
region = 'UK' OR region = 'US'  
```  
  
검색 조건 결합에 대한 자세한 내용은 다음 항목을 참조하십시오.  
  
-   [조건 창의 검색 조건 결합 규칙&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/conventions-combine-search-conditions-in-criteria-pane-visual-db-tools.md)  
  
-   [한 열에 여러 검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-one-column-visual-database-tools.md)  
  
-   [여러 열에 여러 검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-multiple-search-conditions-for-multiple-columns-visual-database-tools.md)  
  
-   [AND에 우선 순위가 있는 조건 조합&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/combine-conditions-when-and-has-precedence-visual-database-tools.md)  
  
-   [OR에 우선 순위가 있는 조건 조합&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/combine-conditions-when-or-has-precedence-visual-database-tools.md)  
  
## <a name="examples"></a>예  
다음은 여러 가지 연산자와 행 조건을 사용한 쿼리의 몇 가지 예입니다.  
  
-   **리터럴** 단일 텍스트, 숫자, 날짜 또는 논리 값입니다. 아래 예에서는 리터럴을 사용하여 영국에 있는 직원에 대한 행을 모두 찾습니다.  
  
    ```  
    WHERE region = 'UK'  
    ```  
  
-   **열 참조** 한 열의 값을 다른 열의 값과 비교합니다. 아래 예에서는 `products` 테이블을 검색하여 운반 비용보다 생산 비용이 싼 행을 모두 찾습니다.  
  
    ```  
    WHERE prod_cost < ship_cost  
    ```  
  
-   **함수** 검색할 값을 계산하기 위해 데이터베이스 백 엔드가 사용할 수 있는 함수에 대한 참조입니다. 함수는 데이터베이스 서버에서 정의한 함수 또는 스칼라 값을 반환하는 사용자 정의 함수일 수 있습니다. 아래 예에서는 오늘 받은 주문을 검색하며 GETDATE( ) 함수는 현재 날짜를 반환합니다.  
  
    ```  
    WHERE order_date = GETDATE()  
    ```  
  
-   **NULL** 아래 예에서는 `authors` 테이블을 검색하여 파일에 이름이 있는 모든 작성자를 찾습니다.  
  
    ```  
    WHERE au_fname IS NOT NULL  
    ```  
  
-   **계산** 리터럴, 열 참조 또는 다른 식을 포함할 수 있는 계산 결과입니다. 아래 예에서는 `products` 테이블을 검색하여 소매 가격이 생산 비용의 2배 이상인 행을 모두 찾습니다.  
  
    ```  
    WHERE sales_price > (prod_cost * 2)  
    ```  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
[매개 변수를 사용하여 쿼리&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/query-with-parameters-visual-database-tools.md)  
  
