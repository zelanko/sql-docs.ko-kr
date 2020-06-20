---
title: 카디널리티 추정(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 11/24/2015
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: aa56127f649d71bfcc8825322f8bf729175d41df
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85066041"
---
# <a name="cardinality-estimation-sql-server"></a>카디널리티 추정(SQL Server)
  카디널리티 평가기라고 하는 카디널리티 추정 논리가 쿼리 계획의 품질을 개선하여 쿼리 성능을 향상시키도록 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 에서 다시 디자인되었습니다. 새로운 카디널리티 평가기는 최신 OLTP 및 데이터 웨어하우징 작업에서 제대로 작동하는 가정 및 알고리즘을 통합합니다. 이 평가기는 최신 작업에 대한 자세한 카디널리티 추정 연구와 SQL Server 카디널리티 평가기를 향상시키기 위해 과거 15년 동안 학습한 지식을 기반으로 합니다. 고객의 의견은 대부분의 쿼리가 변경을 통해 이점을 얻거나 변경되지 않은 채로 유지되는 반면 소수의 쿼리는 이전 카디널리티 평가기와 비교했을 때 회귀를 보여줄 수도 있음을 나타냅니다.  
  
> [!NOTE]  
>  카디널리티 예상치는 쿼리 결과에 있는 행 수의 예측치입니다. 쿼리 최적화 프로그램은 이러한 예상치를 사용하여 쿼리 실행 계획을 선택합니다. 쿼리 계획의 품질은 쿼리 성능 향상에 직접적인 영향을 줍니다.  
  
## <a name="performance-testing-and-tuning-recommendations"></a>성능 테스트 및 튜닝 권장 구성  
 새로운 카디널리티 평가기는 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]에서 만든 모든 새로운 데이터베이스에 대해 설정됩니다. 그러나 [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 로 업그레이드하면 기존 데이터베이스에 대해 새 카디널리티 평가기가 사용되지 않습니다.  
  
 최고의 쿼리 성능을 위해서는 프로덕션 시스템에서 새 카디널리티 평가기를 설정하기 전에 이러한 권장 구성을 사용하여 새 카디널리티 평가기로 작업을 테스트하십시오  
  
1.  새 카디널리티 평가기를 사용하도록 모든 기존 데이터베이스를 업그레이드합니다. 이렇게 하려면 [ALTER Database 호환성 수준 &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) 를 사용 하 여 데이터베이스 호환성 수준을 120로 설정 합니다.  
  
2.  새 카디널리티 평가기로 테스트 작업을 실행한 다음 현재 성능 문제를 해결하는 방식과 동일한 방식으로 새로운 성능 문제를 해결합니다.  
  
3.  사용자의 작업이 새 카디널리티 평가기로 실행 중이고(데이터베이스 호환성 수준 120(SQL Server 2014)) 특정 쿼리가 회귀한 경우 추적 플래그 9481로 쿼리를 실행하여 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 에서와 그 이전에 사용한 카디널리티 평가기 버전을 사용할 수 있습니다. 추적 플래그로 쿼리를 실행하려면 기술 자료 문서 [특정 쿼리 수준에서 여러 다른 추적 플래그를 통해 제어할 수 있는 계획에 영향을 주는 SQL Server 쿼리 최적화 프로그램 동작 설정](https://support.microsoft.com/kb/2801413)을 참조하십시오.  
  
4.  새 카디널리티 평가기를 사용 하기 위해 한 번에 모든 데이터베이스를 변경할 수 없는 경우 [ALTER DATABASE Compatibility level &#40;transact-sql&#41;](/sql/t-sql/statements/alter-database-transact-sql-compatibility-level) 를 사용 하 여 데이터베이스 호환성 수준을 110로 설정 하 여 모든 데이터베이스에 대해 이전 카디널리티 평가기를 사용할 수 있습니다.  
  
5.  사용자의 작업이 데이터베이스 호환성 수준 110으로 실행 중이고 새 카디널리티 평가기로 특정 쿼리를 테스트 또는 실행하려는 경우 추적 플래그 2312로 쿼리를 실행하여 카디널리티 평가기의 SQL Server 2014 버전을 사용할 수 있습니다.  추적 플래그로 쿼리를 실행하려면 기술 자료 문서 [특정 쿼리 수준에서 여러 다른 추적 플래그를 통해 제어할 수 있는 계획에 영향을 주는 SQL Server 쿼리 최적화 프로그램 동작 설정](https://support.microsoft.com/kb/2801413)을 참조하십시오.  
  
## <a name="new-xevents"></a>새로운 XEvent  
 새 쿼리 계획을 지원하는 두 개의 새로운 query_optimizer_estimate_cardinality XEvent가 있습니다.  
  
-   *query_optimizer_estimate_cardinality* 는 쿼리 최적화 프로그램이 관계형 식의 카디널리티를 예측할 때 발생합니다.  
  
-   *query_optimizer_force_both_cardinality_estimation*_behaviors는 두 추적 플래그 2312 및 9481이 모두 설정되어 이전 카디널리티 추정 동작과 새 카디널리티 추정 동작 모두를 동시에 적용하려고 시도할 때 발생합니다.  
  
## <a name="examples"></a>예제  
 다음 예에서는 새 카디널리티 예상치의 변경 내용 중 일부를 보여 줍니다. 카디널리티를 예측하기 위한 코드는 다시 작성되었습니다. 논리는 복잡하며, 모든 변경 내용의 전체 목록을 제공할 수는 없습니다.  
  
> [!NOTE]  
>  이 예는 개념 정보로 제공됩니다. 데이터베이스와 쿼리를 디자인하는 방식을 변경하기 위해 별도의 동작을 취할 필요가 없습니다.  
  
### <a name="example-a-new-cardinality-estimates-use-an-average-cardinality-for-recently-added-ascending-data"></a>예 A. 새 카디널리티 예상치는 최근에 추가된 오름차순 데이터에 대한 평균 카디널리티를 사용합니다.  
 이 예에서는 새 카디널리티 평가기가 가장 최근 통계 업데이트 시 테이블의 최대값을 초과하는 오름차순 데이터에 대한 카디널리티 예상치를 향상시키는 방법을 보여 줍니다.  
  
```  
SELECT item, category, amount FROM dbo.Sales AS s WHERE Date = '2013-12-19';  
```  
  
 이 예에서는 매일 Sales 테이블에 새 행이 추가되고, 쿼리가 12/19/2013에 발생한 판매량을 요청하며, 통계가 12/18/2013에 마지막으로 업데이트되었습니다. 이전 카디널리티 평가기는 날짜가 최대 날짜를 초과하고 통계가 12/19/2013 값을 포함하도록 업데이트되지 않았기 때문에 12/19/2013 값이 존재하지 않는다고 가정합니다. 오름차순 키 문제라고 하는 이러한 상황은 하루 동안 데이터를 로드한 다음 통계가 업데이트되기 전에 데이터에 대한 쿼리를 실행하는 경우 발생합니다.  
  
 이 동작은 변경되었습니다. 이제, 마지막 통계 업데이트 이후에 추가된 가장 최근 오름차순 데이터에 대해 통계가 업데이트되지 않은 경우에도 새 카디널리티 평가기는 값이 존재한다고 가정하며 열의 각 값에 대한 평균 카디널리티를 카디널리티 예상치로 사용합니다.  
  
### <a name="example-b-new-cardinality-estimates-assume-filtered-predicates-on-the-same-table-have-some-correlation"></a>예 B. 새 카디널리티 예상치는 동일한 테이블에 있는 필터링된 조건자에 상관 관계가 있다고 가정합니다.  
 이 예에서는 Cars 테이블에 행이 1000개 있고 Make가 'Honda'에 해당하는 행이 200개 있고 Model이 'Civic'에 해당하는 행이 50개 있고, Civic은 모두 Honda라고 가정합니다. 따라서 Make 열 값의 20%가 'Honda', Model 열 값의 5%가 'Civic', Honda Civics의 실제 수가 50입니다. 이전 카디널리티 예상치는 Make 열과 Model 열의 값이 서로 독립적이라고 가정합니다. 이전 쿼리 최적화 프로그램은 10 개의 Honda Civics (.20 \* 1000 rows = 10 개 행)을 추정 합니다.  
  
```  
SELECT year, purchase_price FROM dbo.Cars WHERE Make = 'Honda' AND Model = 'Civic';  
```  
  
 이 동작은 변경되었습니다. 이제 새 카디널리티 예상치는 Make열과 Model 열에 상관 관계가 *있다고* 가정합니다. 쿼리 최적화 프로그램은 추정 수식에 지수 성분을 추가하여 높은 카디널리티를 예측합니다. 이제 쿼리 최적화 프로그램에서 22.36 행 (.05 * SQRT (. 20) \* 1000 rows = 22.36 rows)이 조건자와 일치 하는 것으로 추정 합니다. 이 시나리오와 특정 데이터 분산에서는 22.36개의 행이 쿼리가 실제로 반환할 50개의 행과 가깝습니다.  
  
 새 카디널리티 평가기 논리는 조건자 선택도를 정렬하고 지수를 늘립니다. 예를 들어, 조건자 선택도가 .05, .20 및 0.25 인 경우 카디널리티 예상치는 (. 05 * SQRT (. 20) \* sqrt (SQRT (. 25)))입니다.  
  
### <a name="example-c-new-cardinality-estimates-assume-filtered-predicates-on-different-tables-are-independent"></a>예 C. 새 카디널리티 예상치는 서로 다른 테이블의 필터링된 조건자가 독립적이라고 가정합니다.  
 이 예에서 이전 카디널리티 평가기는 조건자 필터 s.type 및 r.date에 서로 상관 관계가 있다고 가정합니다. 그러나 최신 작업에 대한 테스트 결과는 서로 다른 테이블의 열에 있는 조건자 필터에 일반적으로 서로 상관 관계가 없음을 보여 주었습니다.  
  
```  
SELECT s.ticket, s.customer, r.store FROM dbo.Sales AS s CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND s.type = 'toy' AND r.date = '2013-12-19';  
```  
  
 이 동작은 변경되었습니다. 이제 새 카디널리티 평가기 논리는 s.type과 r.date에 상관 관계가 없다고 가정합니다. 실제로 장난감이 특정한 날에만 반환되지 않고 매일 반환된다고 가정합니다. 이 경우 새 카디널리티 예상치는 이전 카디널리티 예상치보다 적은 숫자입니다.  
  
## <a name="see-also"></a>참고 항목  
 [성능 모니터링 및 튜닝](monitor-and-tune-for-performance.md)  
  
  
