---
title: 하위 쿼리 만들기
ms.custom: seo-lt-2019
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- search criteria [SQL Server], subqueries
- nested queries
- subqueries [SQL Server], SQL pane
ms.assetid: 34f6b9b4-ca3a-4a4f-9594-36e513f1c547
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.openlocfilehash: ecee42edc9a27cb746615b7343c5014893e23c17
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/06/2020
ms.locfileid: "85999991"
---
# <a name="create-subqueries-visual-database-tools"></a>하위 쿼리 만들기(Visual Database Tools)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
한 쿼리의 결과를 다른 쿼리의 입력 항목으로 사용할 수 있습니다. 하위 쿼리의 결과를 IN( ) 함수, EXISTS 연산자 또는 FROM 절을 사용하는 문으로 사용할 수 있습니다.  
  
SQL 창에 직접 입력하거나 쿼리를 복사하여 다른 쿼리에 붙여넣는 방법으로 하위 쿼리를 만들 수 있습니다.  
  
### <a name="to-define-a-subquery-in-the-sql-pane"></a>SQL 창에서 하위 쿼리를 정의하려면  
  
1.  기본 쿼리를 만듭니다.  
  
2.  SQL 창에서 SQL 문을 선택한 다음 **복사** 명령을 사용하여 쿼리를 클립보드로 이동합니다.  
  
3.  새 쿼리를 시작한 다음 **붙여넣기** 명령을 사용하여 첫 번째 쿼리를 새 쿼리의 WHERE 절이나 FROM 절로 이동합니다.  
  
    예를 들어, `products` 와 `suppliers`라는 두 개의 테이블이 있으며 스웨덴 공급자에 대한 모든 제품을 표시하는 쿼리를 만들려 한다고 가정합니다. `suppliers` 테이블에 첫 번째 쿼리를 만들어 모든 스웨덴 공급자를 찾습니다.  
  
    ```  
    SELECT supplier_id  
    FROM supplier  
    WHERE (country = 'Sweden')  
    ```  
  
    복사 명령을 사용하여 이 쿼리를 클립보드로 이동합니다. `products` 테이블을 사용하여 필요한 제품 정보를 나열하는 두 번째 쿼리를 만듭니다.  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    ```  
  
    SQL 창에서 두 번째 쿼리에 WHERE 절을 추가한 다음 클립보드에 있는 첫 번째 쿼리를 붙여넣습니다. 첫 번째 쿼리를 괄호로 묶은 결과는 다음과 같습니다.  
  
    ```  
    SELECT product_id, supplier_id, product_name  
    FROM products  
    WHERE supplier_id IN  
       (SELECT supplier_id  
      FROM supplier  
      WHERE (country = 'Sweden'))  
    ```  
  
## <a name="see-also"></a>참고 항목  
[지원되는 쿼리 형식&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/supported-query-types-visual-database-tools.md)  
[검색 조건 지정&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/specify-search-criteria-visual-database-tools.md)  
  
