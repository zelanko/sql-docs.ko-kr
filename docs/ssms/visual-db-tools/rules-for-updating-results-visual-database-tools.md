---
title: 결과 업데이트 규칙(Visual Database Tools) | Microsoft 문서
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- View Designer, Results pane
- updating query results
- Query Designer [SQL Server], Results pane
- Results pane
ms.assetid: de131ef0-ccbd-446f-9400-b93c7b8fa537
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8815f7e5bf0192222a0dfdf9917a39606642da1c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47716654"
---
# <a name="rules-for-updating-results-visual-database-tools"></a>결과 업데이트 규칙(Visual Database Tools)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
대부분의 경우 [결과 창](../../ssms/visual-db-tools/results-pane-visual-database-tools.md)에 표시된 결과 집합을 업데이트할 수 있지만 업데이트를 할 수 없는 경우도 종종 있습니다.  
  
일반적으로 결과를 업데이트하려면 [쿼리 및 뷰 디자이너](../../ssms/visual-db-tools/query-and-view-designer-tools-visual-database-tools.md) 에 테이블의 행을 고유하게 식별할 수 있는 충분한 정보가 있어야 합니다. 예를 들어 쿼리에 출력 목록의 기본 키가 포함되어 있는 경우입니다. 또한 사용자는 데이터베이스를 업데이트할 수 있는 충분한 권한이 있어야 합니다.  
  
쿼리가 뷰를 기반으로 하는 경우 해당 쿼리를 업데이트할 수 있습니다. 뷰 자체가 아니라 뷰의 원본으로 사용하는 테이블에 적용된다는 점을 제외하면 동일한 지침이 적용됩니다.  
  
> [!NOTE]  
> 쿼리 및 뷰 디자이너에서는 뷰를 기반으로 하여 결과 집합을 업데이트할 수 있는지 여부를 미리 결정할 수 없습니다. 따라서 결과 집합을 업데이트할 수 없는 경우에도 모든 뷰가 표시됩니다.  
  
아래 표는 결과 창에서 쿼리 결과를 업데이트할 수 있거나 업데이트할 수 없는 특정 예제를 요약한 것입니다. 대부분의 경우 현재 사용하고 있는 데이터베이스가 쿼리 결과의 업데이트 여부를 결정합니다.  
  
|쿼리|결과의 업데이트 가능 여부|  
|---------|---------------------------|  
|출력 목록의 기본 키가 있는 테이블 하나를 기반으로 하는 쿼리|예(아래 항목은 예외)|  
|고유 인덱스 및 기본 키가 없는 테이블 하나를 기반으로 하는 쿼리|쿼리와 데이터베이스에 따라 다릅니다. 일부 데이터베이스는 기록을 고유하게 식별할 수 있는 충분한 정보가 있는 경우 업데이트할 수 있습니다.|  
|조인되지 않은 여러 테이블을 기반으로 하는 쿼리|아니요.|  
|데이터베이스에서 읽기 전용으로 표시된 데이터를 기반으로 하는 쿼리|아니요.|  
|제한 조건이 없는 테이블 하나를 포함하는 뷰를 기반으로 하는 쿼리|예(아래 항목은 예외)|  
|일 대 일 관계로 조인된 테이블을 기반으로 하는 쿼리|예(아래 항목은 예외)|  
|일 대 다 관계로 조인된 테이블을 기반으로 하는 쿼리|일반적으로 업데이트 가능|  
|다 대 다 관계가 있는 세 개 이상의 테이블을 기반으로 하는 쿼리|아니요.|  
|업데이트 권한이 없는 테이블을 기반으로 하는 쿼리|삭제할 수 있지만 업데이트할 수 없음|  
|삭제 권한이 없는 테이블을 기반으로 하는 쿼리|업데이트할 수 있지만 삭제할 수 없음|  
|집합 쿼리|아니요.|  
|totals 또는 aggregate 함수를 포함하는 하위 쿼리를 기반으로 하는 쿼리|아니요.|  
|중복 행을 제외하기 위해 DISTINCT 키워드를 포함하는 쿼리|아니요.|  
|FROM 절에 테이블을 반환하는 사용자 정의 함수 및 여러 개의 select 문이 들어 있는 사용자 정의 함수를 포함하는 쿼리|아니요.|  
|FROM 절에 인라인 사용자 정의 함수를 포함하는 쿼리|예|  
  
또한 쿼리 결과의 특정 열을 업데이트할 수 없는 경우도 있습니다. 다음은 결과 창에서 업데이트할 수 없는 특정 열 형식을 요약한 것입니다.  
  
-   식을 기반으로 하는 열  
  
-   스칼라 사용자 정의 함수를 기반으로 하는 열  
  
-   다른 사용자가 삭제한 행 또는 열  
  
-   다른 사용자가 잠근 행 또는 열(잠긴 행은 잠금이 해제되는 즉시 업데이트될 수 있음)  
  
-   타임스탬프 또는 BLOB 열  
  
## <a name="see-also"></a>참고 항목  
[쿼리 및 뷰 디자인 방법 도움말 항목&#40;Visual Database Tools&#41;](../../ssms/visual-db-tools/design-queries-and-views-how-to-topics-visual-database-tools.md)  
  
