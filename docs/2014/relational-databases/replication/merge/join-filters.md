---
title: 조인 필터 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- filters [SQL Server replication], join
- publications [SQL Server replication], join filters
- merge replication join filters [SQL Server replication]
- join filters
ms.assetid: dd78fd8f-56e3-4582-9abd-6bc25c91e075
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 6bfb1bf3cd43bac47dfb06e4f24c74dc4835709b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62629749"
---
# <a name="join-filters"></a>Join Filters
  조인 필터를 사용하여 게시의 관련 테이블이 필터링되는 방식에 따라 테이블을 필터링할 수 있습니다. 일반적으로 부모 테이블은 매개 변수가 있는 필터를 사용하여 필터링됩니다. 그리고 나서 테이블 간 조인을 정의하는 방식과 매우 유사하게 하나 이상의 조인 필터가 정의됩니다. 조인 필터는 매개 변수가 있는 필터를 확장하므로 관련 테이블의 데이터는 조인 필터 절과 일치할 경우에만 복제됩니다.  
  
 일반적으로 조인 필터는 조인 필터가 적용되는 테이블에 대해 정의된 기본 키/외래 키 관계를 따르지만 기본 키/외래 키 관계를 엄격하게 따르지는 않습니다. 조인 필터는 두 테이블의 관련 데이터를 비교하는 논리를 기반으로 할 수 있습니다.  
  
 [!INCLUDE[ssSampleDBCoShort](../../../includes/sssampledbcoshort-md.md)] 샘플 데이터베이스에 기본 키/외래 키 관계를 따르는 다음과 같은 테이블이 있다고 가정합니다.  
  
-   **HumanResources.Employee**  
  
-   **Sales.SalesOrderHeader**  
  
-   **Sales.SalesOrderDetail**  
  
 이러한 테이블을 이동이 잦은 영업 직원을 지원하는 애플리케이션에 사용할 수 있지만 **HumanResources.Employee** 테이블의 각 영업 직원이 고객 주문과 관련된 데이터만 받도록 필터링해야 합니다.  
  
 이를 위해서는 먼저 부모 테이블에 매개 변수가 있는 필터를 정의해야 합니다. 이 예에서는 **HumanResources.Employee** 테이블이 부모 테이블입니다. 이 테이블의 **LoginID**열에는 각 직원에 대한 로그인이 *domain\login*형식으로 포함되어 있습니다. 각 직원이 자신에게 관련된 데이터만 받을 수 있도록 이 테이블을 필터링하려면 다음과 같은 매개 변수가 있는 필터 절을 지정합니다.  
  
```  
LoginID = SUSER_SNAME()  
```  
  
 이 필터는 각 직원의 구독이 **HumanResources.Employee** 테이블에서 해당 직원(이 경우에는 단일 행임)과 관련된 데이터만 포함하도록 합니다. 자세한 내용은 [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md)를 참조하세요.  
  
 다음 단계는 두 테이블 간에 조인을 지정하는 데 사용된 구문과 유사한 구문을 사용하여 이 필터를 각 관련 테이블로 확장하는 것입니다. 첫 번째 조인 필터 절은 다음과 같습니다.  
  
```  
Employee.EmployeeID = SalesOrderHeader.SalesPersonID  
```  
  
 이 절은 구독이 각 영업 직원과 관련된 주문 데이터만 포함하도록 합니다. 두 번째 조인 필터 절은 다음과 같습니다.  
  
```  
SalesOrderHeader.SalesOrderID = SalesOrderDetail.SalesOrderID  
```  
  
 이 절은 구독이 각 영업 직원의 주문 데이터와 관련된 정보 데이터만 포함하도록 합니다. 이 예에서는 각 지점에서 조인하는 단일 테이블을 보여 줍니다. 각 지점에 둘 이상의 테이블을 조인할 수도 있습니다.  
  
 조인 필터는 새 게시 마법사 및 **게시 속성** 대화 상자를 통해 한 번에 하나씩 추가하거나 프로그래밍 방식으로 추가할 수 있습니다. 또한 새 게시 마법사를 통해 조인 필터를 자동으로 생성할 수 있습니다. 테이블에 대한 행 필터를 지정하면 조인 필터가 모든 관련 테이블에 적용됩니다. 자세한 내용은 [병합 아티클 사이에서 조인 필터 정의 및 수정](../publish/define-and-modify-a-join-filter-between-merge-articles.md), [병합 아티클 간의 조인 필터 집합 자동 생성&#40;SQL Server Management Studio&#41;](../publish/automatically-generate-join-filters-between-merge-articles.md) 및 [아티클 정의](../publish/define-an-article.md)를 참조하세요.  
  
## <a name="optimizing-join-filter-performance"></a>조인 필터 성능 최적화  
 다음 지침에 따라 조인 필터 성능을 최적화할 수 있습니다.  
  
-   조인 필터 계층에서 테이블의 수를 제한합니다.  
  
     조인 필터는 테이블을 무제한 포함할 수 있지만 테이블 수가 많은 필터는 병합 처리 중 성능에 상당한 영향을 줄 수 있습니다. 5개 이상의 테이블을 가진 조인 필터를 생성하는 경우 다른 해결책을 고려하는 것이 좋습니다. 크기가 작거나, 변경될 가능성이 없거나, 기본적으로 조회 테이블에 해당하는 테이블은 필터링하지 마십시오. 구독 간에 분할해야 하는 테이블 사이에서만 조인 필터를 사용합니다.  
  
-   필요한 경우 **join unique key** 옵션을 **True** 로 설정합니다.  
  
     병합 프로세스는 부모 테이블에서 조인된 열이 고유한 경우 사용할 수 있는 특별 성능 최적화를 가지고 있습니다. 조인 조건이 고유 열을 기반으로 하는 경우에는 조인 필터에 대해 **join unique key** 옵션을 설정합니다. 이러한 옵션을 설정하는 방법은 이전 섹션에 나열된 방법 항목을 참조하십시오.  
  
-   조인 필터에서 참조된 열은 인덱싱되어야 합니다.  
  
     필터에서 참조된 열이 인덱싱된 경우 복제는 필터를 보다 효과적으로 처리할 수 있습니다.  
  
-   조인 필터와 비슷하게 실행되는 행 필터는 만들지 않습니다.  
  
     다음과 같이 WHERE 절에서 하위 쿼리를 사용하여 조인 필터와 비슷하게 실행되는 행 필터를 만들 수 있습니다.  
  
    ```  
    WHERE Customer.SalesPersonID IN (SELECT EmployeeID FROM Employee WHERE LoginID = SUSER_SNAME())   
    ```  
  
     하지만 이러한 모든 논리를 하위 쿼리가 아닌 조인 필터로 표시하는 것이 좋습니다. 애플리케이션에서 행 필터에 하위 쿼리를 사용해야 할 경우에는 하위 쿼리가 변경하지 않는 조회 데이터만 참조하도록 해야 합니다.  
  
## <a name="see-also"></a>관련 항목  
 [병합 복제의 게시된 데이터 필터링](filter-published-data-for-merge-replication.md)   
 [매개 변수가 있는 행 필터](parameterized-filters-parameterized-row-filters.md)  
  
  
