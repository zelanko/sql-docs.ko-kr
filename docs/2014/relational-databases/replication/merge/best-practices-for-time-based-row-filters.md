---
title: 시간 기반 행 필터에 대한 모범 사례 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- replication
ms.topic: conceptual
helpviewer_keywords:
- best practices
ms.assetid: 773c5c62-fd44-44ab-9c6b-4257dbf8ffdb
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 70fb66a1b61dbbdec0fd8443ac150b32c3770818
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48145533"
---
# <a name="best-practices-for-time-based-row-filters"></a>시간 기반 행 필터에 대한 최상의 구현 방법
  애플리케이션 사용자가 테이블의 시간 기반 데이터 하위 집합을 필요로 하는 경우가 종종 있습니다. 예를 들어 영업 사원이 지난 주의 주문 데이터를 필요로 하거나, 행사 계획자가 다음 주의 행사 데이터를 필요로 할 수 있습니다. 대부분의 경우 응용 프로그램에서는 `GETDATE()` 함수가 들어 있는 쿼리를 사용하여 이 작업을 수행합니다. 예를 들어 다음과 같은 행 필터 문을 사용한다고 가정합니다.  
  
```  
WHERE SalesPersonID = CONVERT(INT,HOST_NAME()) AND OrderDate >= (GETDATE()-6)  
```  
  
 이 유형의 필터를 사용하면 일반적으로 병합 에이전트가 실행될 때 항상 두 가지 작업이 실행됩니다. 즉, 이 필터를 만족하는 행은 구독자에 복제되고 이 필터를 더 이상 만족하지 않는 행은 구독자에서 정리됩니다. (사용 하 여 필터링 하는 방법에 대 한 자세한 내용은 `HOST_NAME()`를 참조 하세요 [Parameterized Row Filters](parameterized-filters-parameterized-row-filters.md).) 그러나 병합 복제에서는 데이터에 대한 행 필터 정의 방식에 관계없이 마지막 동기화 이후에 변경된 데이터만 복제되고 정리됩니다.  
  
 행을 처리하는 병합 복제의 경우 행에 있는 데이터는 행 필터를 만족하고 마지막 동기화 이후에 변경된 데이터여야 합니다. **SalesOrderHeader** 테이블의 경우 행이 삽입될 때 **OrderDate** 가 입력됩니다. 행 삽입은 데이터 변경에 해당하므로 해당 행은 구독자에 예상대로 복제됩니다. 그러나 구독자에 필터를 더 이상 만족하지 않는 행(예: 7일 이상 경과된 주문)이 있는 경우 해당 행은 다른 이유로 업데이트되지 않았으면 구독자에서 제거되지 않습니다.  
  
 행사 계획자의 경우 이 유형의 필터링을 사용하여 원하는 항목을 찾을 수 있습니다. 예를 들어 **Events** 테이블에 대해 다음과 같은 필터를 사용한다고 가정합니다.  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND EventDate <= (GETDATE()+6)  
```  
  
 행사가 포함되는 테이블의 경우 행사 날짜 전에 행사를 삽입할 수 있습니다. 다음 주 행사를 한 달 전에 삽입하고 해당 행을 업데이트하지 않았으면 해당 행은 행 필터를 만족하더라도 구독자에 복제되지 않습니다.  
  
 또한 병합 복제에서 필터가 평가되는 시기는 다음과 같이 게시가 구성된 방식에 따라 달라집니다.  
  
-   게시에서 사전 계산 파티션(기본값)을 사용하면 행을 삽입하거나 업데이트할 때 필터가 평가됩니다.  
  
-   게시에서 사전 계산 파티션을 사용하지 않으면 병합 에이전트가 실행할 때 필터가 평가됩니다.  
  
 사전 계산 파티션에 대한 자세한 내용은 [사전 계산 파티션으로 매개 변수가 있는 필터 성능 최적화](parameterized-filters-optimize-for-precomputed-partitions.md)를 참조하세요. 필터가 평가되는 시기는 필터를 만족하는 데이터에 영향을 줍니다. 예를 들어 게시에서 사전 계산 파티션을 사용하는 경우 데이터를 2일마다 동기화하면 영업 사원의 데이터 하위 집합에는 예상보다 최대 2일이 더 오래된 행이 포함될 수 있습니다.  
  
## <a name="recommendations-for-using-time-based-row-filters"></a>시간 기반 행 필터 사용에 대한 권장 사항  
 시간을 기반으로 필터링하기 위한 강력하고 간단한 방법은 다음과 같습니다.  
  
-   데이터 형식의 테이블에 열 추가 `bit`합니다. 이 열은 행이 복제되는지 여부를 나타내는 데 사용합니다.  
  
-   시간 기반 열 이외의 새 열을 참조하는 행 필터를 사용합니다.  
  
-   병합 에이전트의 예약된 실행 시간 전에 열을 업데이트하는 SQL Server 에이전트 작업(또는 다른 메커니즘을 통해 예약된 작업)을 만듭니다.  
  
 이 방법을 사용 하 여 해결할 `GETDATE()` 또는 다른 시간 기반 메서드 및 파티션에 대해 필터가 평가 되는 경우를 지정 하지 않아도의 문제를 방지 합니다. 예를 들어 다음과 같은 **Events** 테이블이 있다고 가정합니다.  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**복제**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|1|  
|2|Dinner|112|2006-10-10|0|  
|3|Party|112|2006-10-11|0|  
|4|Wedding|112|2006-10-12|0|  
  
 이 테이블에 다음과 같은 행 필터를 사용할 수 있습니다.  
  
```  
WHERE EventCoordID = CONVERT(INT,HOST_NAME()) AND Replicate = 1  
```  
  
 각 병합 에이전트가 실행되기 전에 SQL Server 에이전트 작업은 다음과 유사한 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행할 수 있습니다.  
  
```  
UPDATE Events SET Replicate = 0 WHERE Replicate = 1  
GO  
UPDATE Events SET Replicate = 1 WHERE EventDate <= GETDATE()+6  
GO  
```  
  
 첫째 줄은 **Replicate** 열을 **0**으로 다시 설정하고 둘째 줄은 다음 7일 안에 개최되는 행사에 대해 이 열을 **1** 로 설정합니다. 2006년 10월 7일에 이 [!INCLUDE[tsql](../../../includes/tsql-md.md)] 문을 실행하면 해당 테이블은 다음과 같이 업데이트됩니다.  
  
|**EventID**|**EventName**|**EventCoordID**|**EventDate**|**복제**|  
|-----------------|-------------------|----------------------|-------------------|-------------------|  
|1|Reception|112|2006-10-04|0|  
|2|Dinner|112|2006-10-10|1|  
|3|Party|112|2006-10-11|1|  
|4|Wedding|112|2006-10-12|1|  
  
 이제 다음 주의 행사가 복제할 행사로 플래그가 지정됩니다. 다음에 행사 코디네이터 112가 사용하는 구독에 대해 병합 에이전트가 실행되면 행 2, 3 및 4는 구독자에 다운로드되고 행 1은 구독자에서 제거됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [GETDATE&#40;Transact-SQL&#41;](/sql/t-sql/functions/getdate-transact-sql)   
 [작업 구현](../../../ssms/agent/implement-jobs.md)   
 [매개 변수가 있는 행 필터](parameterized-filters-parameterized-row-filters.md)  
  
  
