---
title: 실행 계획 비교 | Microsoft Docs
ms.custom: ''
ms.date: 11/21/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- comparing execution plans
- compare execution plans
- plan comparison
- execution plans [SQL Server], comparing
- Query Store, comparing plans
ms.assetid: 9e583a18-5f4a-4054-bfe1-4b2a76630db6
author: pmasl
ms.author: pelopes
manager: amitban
ms.openlocfilehash: cc42584c6b3f07961e83e53b8b5165243060256f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76910246"
---
# <a name="compare-execution-plans"></a>실행 계획 비교
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 항목에서는 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 계획 비교 기능을 사용하여 실제 그래픽 실행 계획 간의 유사점과 차이점을 비교하는 방법을 설명합니다. 이 기능은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] v16부터 사용할 수 있습니다.
  
> [!NOTE]
> [!INCLUDE[tsql](../../includes/tsql-md.md)] 쿼리 또는 일괄 처리가 실행된 후 실제 실행 계획이 실행됩니다. 이 때문에 실제 실행 계획에는 실제 행 수, 리소스 사용량 메트릭 및 런타임 경고(있는 경우)와 같은 런타임 정보가 포함됩니다. 자세한 내용은 [실제 실행 계획 표시](../../relational-databases/performance/display-an-actual-execution-plan.md)를 참조하세요.
  
계획을 비교하는 기능은 데이터베이스 전문가가 문제 해결을 위해 수행해야 하는 것입니다.
-   쿼리 또는 일괄 처리가 갑자기 저하되는 이유를 찾습니다.
-   쿼리 다시 작성의 영향을 파악합니다.
-   스키마 디자인(예: 새 인덱스)에 소개된 특정 성능 향상 변경에서 실행 계획을 효과적으로 변경하는 방법을 확인합니다.  
 
**계획 비교** 메뉴 옵션을 사용하여 위에 명시된 모든 이유로 다양한 동작을 설명하는 유사성과 변경 내용을 쉽게 식별할 수 있도록 두 개의 다른 실행 계획을 나란히 비교할 수 있습니다. 이 옵션은 다음을 비교할 수 있습니다.
- 두 개의 이전에 저장된 실행 계획 파일( *.sqlplan* 확장)
- 하나의 활성 실행 계획 및 하나의 이전에 저장된 쿼리 실행 계획
- [쿼리 저장소](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)에서 선택된 두 개의 쿼리 계획

> [!TIP]
> 계획 비교는 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서도 모든 *.sqlplan* 파일과 함께 작동합니다. 또한 이 옵션은 오프라인 비교를 활성화하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에 연결할 필요가 없습니다. 

두 실행 계획을 비교할 때 **기본적으로 동일하게 실행하는** 계획의 지역은 동일한 색과 패턴으로 강조 표시됩니다. 하나의 계획에서 색이 지정된 영역을 클릭하면 해당 계획의 일치하는 노드에서 다른 계획이 중앙에 위치합니다. 여전히 실행 계획의 일치하지 않는 연산자 및 노드를 비교할 수 있지만 이 경우 비교할 연산자를 수동으로 선택해야 합니다.

> [!IMPORTANT]
> 계획의 모양을 변경할 것으로 간주되는 노드만 유사성을 확인하는 데 사용됩니다. 따라서 계획의 동일한 하위 섹션에 있는 두 노드 중간에 색상이 지정되지 않은 노드가 있을 수 있습니다. 이 경우 색의 부족은 섹션이 같은지 여부를 확인하는 경우 노드가 고려되지 않았음을 의미합니다.
  
## <a name="to-compare-execution-plans"></a>실행 계획을 비교하려면
  
1.  **파일** 메뉴를 사용하고 **파일 열기**를 클릭하여 이전에 저장된 쿼리 실행 계획 파일(.sqlplan)을 열거나 [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] 창으로 계획 파일을 끌어 놓습니다. 또는 쿼리를 실행하고 해당 실행 계획을 표시하도록 선택한 경우 결과 창의 **실행 계획** 탭으로 이동합니다. 

2.  실행 계획의 빈 영역을 마우스 오른쪽 단추로 클릭하고 **실행 계획 비교**를 클릭합니다. 

    ![실행 계획 비교를 마우스 오른쪽 단추로 클릭](../../relational-databases/performance/media/plancomparisonmenuoption.png "실행 계획 비교를 마우스 오른쪽 단추로 클릭")   

3.  비교하려는 두 번째 쿼리 계획 파일을 선택합니다. 두 번째 파일이 계획을 비교할 수 있도록 열립니다.

4.  비교된 계획이 기본적으로 위쪽에 하나, 아래쪽에 하나로 새 창에서 열립니다. 기본 선택 사항이 비교된 계획에서 공통적이지만 계획 간의 차이점을 보여주는 연산자 또는 노드의 첫 번째 발생이 됩니다. 강조 표시된 모든 연산자 및 노드가 비교된 계획 모두에 존재합니다. 위쪽 또는 왼쪽 계획에서 강조 표시된 연산자를 선택하면 아래쪽 또는 오른쪽 계획에서 해당 연산자가 자동으로 선택됩니다. 비교된 계획(아래 그림의 SELECT 노드) 중 하나에서 루트 노드 연산자를 선택하면 다른 비교된 계획에서 해당 루트 노드 연산자가 선택됩니다.

    ![저장된 두 계획 파일의 계획 비교](../../relational-databases/performance/media/plancomparison-plans.png "저장된 두 계획 파일의 계획 비교")  

     > [!TIP]
     > 실행 계획의 빈 영역을 마우스 오른쪽 단추로 클릭하고 **토글 분할자 방향**을 선택하여 실행 계획 비교의 표시를 병렬로 전환할 수 있습니다.

     > [!TIP]
     > 실행 계획에 사용 가능한 모든 확대/축소 및 탐색 옵션은 계획 비교 모드에서 작동합니다. 자세한 내용은 [실제 실행 계획 표시](../../relational-databases/performance/display-an-actual-execution-plan.md)를 참조하세요.

5.  기본 선택 사항의 범위에서 오른쪽에 이중 속성 창도 열립니다. 비교된 연산자에 모두 있지만 차이점이 있는 속성의 경우 확인하기 쉽도록 ‘같지 않음’ 기호(&ne;)가 앞에 옵니다. 

    ![이중 속성 창](../../relational-databases/performance/media/plancomparison-properties.png "이중 속성 창")  

6.  **실행 계획 분석** 비교 탐색 창이 아래에서 열립니다. 세 개의 탭을 사용할 수 있습니다.

    1.  **명령문 옵션** 탭에서 기본 선택 사항은 *비슷한 작업 강조 표시*이며 비교된 계획에서 강조 표시된 동일한 연산자 또는 노드는 동일한 색과 선 패턴을 공유합니다. 선 패턴을 클릭하여 비교된 계획의 비슷한 영역 간을 이동합니다. *유사한 세그먼트와 일치하지 않는 작업 강조 표시*를 선택하여 유사점보다 계획의 차이점을 강조 표시하도록 선택할 수도 있습니다. 
    
       > [!NOTE]
       > 기본적으로 데이터베이스 이름은 다른 이름이 있지만 동일한 스키마를 공유하는 데이터베이스에 대해 캡처된 계획을 비교할 수 있도록 계획을 비교할 때 무시됩니다. 예를 들어 *ProdDB* 및 *TestDB* 데이터베이스의 계획을 비교하는 경우입니다. *연산자를 비교할 때 데이터베이스 이름 무시* 옵션을 사용하여 이 동작을 변경할 수 있습니다.

       ![실행 계획 분석 창](../../relational-databases/performance/media/plancomparison-analysis.png "실행 계획 분석 창") 

    2.  비교할 올바른 명령문 쌍을 허용하여 다중 명령문으로 계획을 비교할 때 **다중 명령문** 탭은 유용합니다.

        ![비교된 계획의 여러 문](../../relational-databases/performance/media/plancomparison-multiple.png "비교된 계획의 여러 문")  

    3.  **시나리오** 탭에서 비교된 계획에서 [카디널리티 추정](../../relational-databases/performance/cardinality-estimation-sql-server.md) 차이점과 관련된 항목을 살펴보도록 몇 가지 가장 관련성이 높은 측면에 대한 자동화된 분석을 찾을 수 있습니다. 왼쪽 창에서 나열된 각 연산자의 경우 오른쪽 창은 *이 시나리오에 대한 자세한 내용은 여기를 클릭하세요* 링크의 시나리오에 대한 세부 정보를 보여주며, 해당 시나리오를 설명하는 가능한 원인이 나열됩니다. 

        ![예상 행 수가 다름](../../relational-databases/performance/media/plancomparison-scenarios.png "예상 행 수가 다름")  

    이 창이 닫힌 경우 비교된 계획의 빈 영역을 마우스 오른쪽 단추로 클릭하고, **실행 계획 비교 옵션**을 선택하여 다시 엽니다.

    ![계획 비교 옵션](../../relational-databases/performance/media/plancomparison-options.png "계획 비교 옵션")  

## <a name="to-compare-execution-plans-in-query-store"></a>쿼리 저장소에서 실행 계획을 비교하려면

1.  쿼리 저장소에서 둘 이상의 실행 계획이 있는 쿼리를 식별합니다. 쿼리 저장소 시나리오에 대한 자세한 내용은 [쿼리 저장소 사용 시나리오](../../relational-databases/performance/query-store-usage-scenarios.md#identify-and-tune-top-resource-consuming-queries)를 참조하세요.

2.  동일한 쿼리에 대해 두 개의 계획을 선택하려면 SHIFT 키와 마우스의 조합을 사용합니다. 

    ![쿼리 저장소에서 두 계획을 선택](../../relational-databases/performance/media/plancomparison-querystore.png "쿼리 저장소에서 두 계획을 선택")   

3.  **별도 창에서 선택 쿼리에 대한 계획 비교** 단추를 사용하여 계획 비교를 시작합니다. 그런 다음, *실행 계획을 비교하려면*의 4~6단계를 적용할 수 있습니다. 

    ![쿼리 저장소에서 실행 계획 비교](../../relational-databases/performance/media/plancomparison-querystoreoption.png "쿼리 저장소에서 실행 계획 비교") 
