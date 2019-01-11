---
title: (Analysis Services)는 로컬 파티션 만들기 및 관리 | Microsoft Docs
ms.custom: ''
ms.date: 05/24/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
helpviewer_keywords:
- local partitions [Analysis Services]
- partitions [Analysis Services], local
- partitions [Analysis Services], creating
ms.assetid: eaa95278-9ce9-47d5-a6b6-1046e7076599
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 5665db92828c5a6ea6a6d94587414dc6b411a01b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48091303"
---
# <a name="create-and-manage-a-local-partition-analysis-services"></a>로컬 파티션 만들기 및 관리(Analysis Services)
  처리 성능 향상을 위해 측정값 그룹에 대한 추가 파티션을 만들 수 있습니다. 여러 개의 파티션이 있으면 로컬 서버뿐만 아니라 원격 서버의 해당하는 개수의 실제 데이터 파일에 팩트 데이터를 할당할 수 있습니다. Analysis Services에서는 파티션을 독립적으로 병렬 처리할 수 있어 서버에서 작업을 처리할 때 더 세부적으로 제어할 수 있습니다.  
  
 모델을 디자인할 때 또는 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)] 나 XMLA를 사용하여 솔루션을 배포한 후 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 파티션을 만들 수 있습니다. 한 가지 방법만 선택하는 것이 좋습니다. 도구를 번갈아 사용하면 이후에 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 솔루션을 다시 배포할 때 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 배포된 데이터베이스에 대한 변경 내용이 덮어쓰기될 수도 있습니다.  
  
## <a name="before-you-start"></a>시작하기 전 주의 사항  
 가지고 있는 버전이 비즈니스 인텔리전스 버전인지 엔터프라이즈 버전인지 확인합니다. 스탠더드 버전에서는 여러 파티션을 지원하지 않습니다. 버전을 확인하려면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 에서 서버 노드를 마우스 오른쪽 단추로 클릭하고 **보고서** | **일반**을 선택합니다. 기능 가용성에 대 한 자세한 내용은 참조 하세요. [SQL Server 2014 버전에서 지 원하는 기능](../../getting-started/features-supported-by-the-editions-of-sql-server-2014.md)합니다.  
  
 나중에 파티션을 병합하려는 경우 처음부터 해당 파티션이 같은 집계 디자인을 공유해야 합니다. 파티션은 집계 디자인과 스토리지 모드가 동일한 경우에만 병합할 수 있습니다.  
  
> [!TIP]  
>  DSV(데이터 원본 뷰)를 탐색하여 분할할 데이터의 범위와 깊이를 파악합니다. 예를 들어 날짜별로 분할하는 경우 날짜 열을 기준으로 정렬하여 각 파티션의 상한과 하한을 확인할 수 있습니다.  
  
## <a name="choose-an-approach"></a>방법 선택  
 파티션을 만들 때 가장 중요한 고려 사항은 중복 행이 없도록 데이터를 분할하는 것입니다. 데이터를 한 파티션에만 저장하여 행이 두 번 계산되지 않도록 해야 합니다. 따라서 각 파티션 간에 명확한 경계를 정의할 수 있도록 날짜별로 분할하는 것이 일반적입니다.  
  
 팩트 데이터를 여러 파티션에 배포하는 기술을 사용할 수 있습니다. 다음 방법을 사용하여 데이터를 분할할 수 있습니다.  
  
|방법|권장 사항|  
|---------------|---------------------|  
|SQL 쿼리를 사용하여 팩트 데이터 분할|파티션은 SQL 쿼리를 기반으로 할 수 있습니다. 처리하는 동안 SQL 쿼리가 데이터를 검색합니다. 쿼리의 WHERE 절은 각 파티션의 데이터를 분할하는 필터를 제공합니다. Analysis Services에서 자동으로 쿼리가 생성되지만 데이터가 제대로 분할되도록 사용자가 WHERE 절을 채워야 합니다.<br /><br /> 이 방법의 주요 이점은 단일 원본 테이블에서 데이터를 분할할 수 있는 편의성입니다. 모든 원본 데이터를 큰 팩트 테이블에서 가져오는 경우 DSV(데이터 원본 뷰)에 추가 데이터 구조를 만들 필요 없이 불연속 파티션으로 데이터를 필터링하는 쿼리를 작성할 수 있습니다.<br /><br /> 쿼리를 사용하면 파티션과 DSV 간에 바인딩이 끊긴다는 점이 한 가지 단점입니다. 나중에 팩트 테이블에 열을 추가하는 등 Analysis Services 프로젝트에서 DSV를 업데이트하는 경우 새 열을 포함하도록 각 파티션에 대한 쿼리를 수동으로 편집해야 합니다. 다음에 설명하는 두 번째 방법을 사용할 때는 이러한 단점이 없습니다.|  
|DSV의 테이블을 사용하여 팩트 데이터 분할|DSV의 뷰, 테이블 및 명명된 쿼리에 파티션을 바인딩할 수 있습니다. 파티션의 기반으로 이 세 개는 모두 동일한 기능을 합니다. 전체 테이블, 명명된 쿼리 또는 뷰는 모든 데이터를 단일 파티션에 제공합니다.<br /><br /> 테이블, 뷰 또는 명명된 쿼리를 사용하면 DSV에 모든 데이터 선택 논리가 배치되어 시간이 지남에 따라 관리하기가 더 쉬워질 수 있습니다. 이 방법의 중요 이점은 테이블 바인딩이 유지된다는 점입니다. 나중에 원본 테이블을 업데이트하는 경우 해당 테이블을 사용하는 파티션을 수정할 필요가 없습니다. 두 번째로, 모든 테이블, 명명된 쿼리 및 뷰가 공통 작업 공간에 있어 파티션 쿼리를 개별적으로 열고 편집해야 할 때보다 편리하게 업데이트할 수 있습니다.|  
  
## <a name="option-1-filter-a-fact-table-for-multiple-partitions"></a>옵션 1: 여러 파티션의 팩트 테이블 필터링  
 여러 개의 파티션을 만들려면 기본 파티션의 **원본** 속성을 수정하는 작업으로 시작합니다. 기본적으로 측정값 그룹은 DSV의 단일 테이블에 바인딩된 단일 파티션을 사용하여 만들어집니다. 파티션을 추가하기 전에 먼저 팩트 데이터의 일부만 포함하도록 원래 파티션을 수정해야 합니다. 그러면 나머지 데이터를 저장하기 위한 추가 파티션을 계속해서 만들 수 있습니다.  
  
 해당 데이터가 파티션 간에 중복되지 않도록 필터를 생성합니다. 파티션의 필터는 파티션에서 사용할 팩트 테이블의 데이터를 지정합니다. 큐브의 모든 파티션에 대한 필터가 팩트 테이블에서 상호 배타적인 데이터 세트를 추출하는 것이 중요합니다. 같은 팩트 데이터가 여러 파티션에 나타나는 경우 두 번 계산될 수 있습니다.  
  
1.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 솔루션 탐색기에서 큐브를 두 번 클릭하여 큐브 디자이너에서 큐브를 연 다음 **파티션** 탭을 클릭합니다.  
  
2.  파티션을 추가할 측정값 그룹을 확장합니다. 기본적으로 각 측정값 그룹에는 DSV의 팩트 테이블에 바인딩된 하나의 파티션이 있습니다.  
  
3.  원본 열에서 찾아보기(. .) 단추를 클릭하여 파티션 원본 대화 상자를 엽니다.  
  
     ![파티션 창의 원본 열](../media/ssas-partitionsource.png "파티션 창의 원본 열")  
  
4.  바인딩 유형에서 **쿼리 바인딩**을 선택합니다. 데이터를 선택하는 SQL 쿼리가 자동으로 나타납니다.  
  
5.  아래쪽의 WHERE 절에서 이 파티션에 대한 데이터를 분할하는 필터를 추가합니다.  
  
     WHERE 절 구문의 예로는 `WHERE OrderDateKey >= '20060101'` 또는 `WHERE OrderDateKey BETWEEN '20051001' AND '20051201'`이 포함됩니다. 다른 예제를 보려면 [WHERE&#40;Transact-SQL&#41;](/sql/t-sql/queries/where-transact-sql)를 참조하세요.  
  
     다음 필터는 각 집합 내에서 함께 사용할 수 없습니다.  
  
    |||  
    |-|-|  
    |설정 1:|"SaleYear" = 2012<br /><br /> "SaleYear" = 2013|  
    |설정 2|"Continent" = 'NorthAmerica'<br /><br /> "Continent" = 'Europe'<br /><br /> "Continent" = 'SouthAmerica'|  
    |설정 3:|"Country" = 'USA'<br /><br /> "Country" = 'Mexico'<br /><br /> ("Country" <> 'USA' AND "Country" <> 'Mexico')|  
  
6.  **검사** 를 클릭하여 구문 오류를 검사한 다음 **확인**을 클릭합니다.  
  
7.  다음 데이터 조각을 선택할 때마다 WHERE 절을 수정하여 이전 단계를 반복해서 나머지 파티션을 만듭니다.  
  
8.  솔루션을 배포하거나 파티션을 처리하여 데이터를 로드합니다. 모든 파티션을 처리해야 합니다.  
  
9. 큐브를 검색하여 올바른 데이터가 반환되었는지 확인합니다.  
  
 여러 측정값 그룹을 사용하는 측정값 그룹이 있으면 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서 추가 파티션을 만들 수 있습니다. 측정값 그룹에서 파티션 폴더를 마우스 오른쪽 단추로 클릭하고 **새 파티션** 을 선택하여 마법사를 시작합니다.  
  
> [!NOTE]  
>  파티션에서 데이터를 필터링하지 않고 같은 쿼리를 사용하여 DSV에 이름 쿼리를 만든 다음 명명된 쿼리를 기준으로 파티션을 사용합니다.  
  
## <a name="option-2-use-tables-views-or-named-queries"></a>옵션 2: 테이블, 뷰 또는 명명된 쿼리 사용  
 이미 DSV가 팩트를 개별 테이블(예: 연도 또는 분기별)로 구성하는 경우 각 파티션에 자체 데이터 원본 테이블이 있는 개별 테이블을 기반으로 파티션을 만들 수 있습니다. 이것은 기본적으로 측정값 그룹이 분할되는 방식이지만 여러 파티션의 경우에는 원래 파티션을 여러 파티션으로 나누고 각각의 새 파티션을 데이터를 제공하는 데이터 원본 테이블에 매핑하십시오.  
  
 세 개체 모두 DSV에 정의되고 파티션 원본 대화 상자의 테이블 바인딩 옵션을 사용하여 파티션에 바인딩된다는 점에서 뷰와 명명된 쿼리는 테이블과 기능적으로 동일합니다. 뷰 또는 명명된 쿼리를 만들어 각 파티션에 필요한 데이터 세그먼트를 생성할 수 있습니다. 자세한 내용은 [데이터 원본 뷰에서 명명된 쿼리 정의&#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
> [!IMPORTANT]  
>  DSV의 파티션에 대해 함께 사용할 수 없는 명명된 쿼리를 만드는 경우 파티션에 대해 결합된 데이터가 큐브에 포함할 측정값 그룹의 모든 데이터를 포함하도록 합니다. 이때 기본 파티션이 측정값 그룹에 대한 전체 테이블을 기반으로 하지 않도록 합니다. 그렇게 하지 않으면 쿼리 기반 파티션이 전체 테이블을 기반으로 하는 쿼리와 중복됩니다.  
  
1.  파티션 원본으로 사용할 명명된 쿼리를 하나 이상 만듭니다. 자세한 내용은 [데이터 원본 뷰에서 명명된 쿼리 정의&#40;Analysis Services&#41;](define-named-queries-in-a-data-source-view-analysis-services.md)를 참조하세요.  
  
     명명된 쿼리는 측정값 그룹과 연결된 팩트 테이블을 기반으로 해야 합니다. 예를 들어 FactInternetSales 측정값 그룹을 분할하는 경우 DSV의 명명된 쿼리는 FROM 문에 FactInternetSales 테이블을 지정해야 합니다.  
  
2.  [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]의 솔루션 탐색기에서 큐브를 두 번 클릭하여 큐브 디자이너에서 큐브를 연 다음 **파티션** 탭을 클릭합니다.  
  
3.  파티션을 추가할 측정값 그룹을 확장합니다.  
  
4.  **새 파티션** 을 클릭하여 파티션 마법사를 시작합니다. 측정값 그룹에 바인딩된 팩트 테이블을 사용하여 명명된 쿼리를 만든 경우 이전 단계에서 만든 명명된 쿼리가 각각 표시되어야 합니다.  
  
5.  원본 정보 지정에서 이전 단계에서 만든 명명된 쿼리 중 하나를 선택합니다. 표시되지 않는 명명된 쿼리가 있으면 DSV로 돌아가서 FROM 문을 확인합니다.  
  
6.  **다음** 을 클릭하여 각 후속 페이지에 대한 기본값을 적용합니다.  
  
7.  마법사를 완료하는 마지막 페이지에서 파티션을 설명하는 이름을 제공합니다.  
  
8.  **마침**을 클릭합니다.  
  
9. 다음 데이터 조각을 선택할 때마다 다른 명명된 쿼리를 선택하여 이전 단계를 반복해서 나머지 파티션을 만듭니다.  
  
10. 솔루션을 배포하거나 파티션을 처리하여 데이터를 로드합니다. 모든 파티션을 처리해야 합니다.  
  
11. 큐브를 검색하여 올바른 데이터가 반환되었는지 확인합니다.  
  
## <a name="next-step"></a>다음 단계  
 파티션에 대해 상호 배타적인 쿼리를 작성할 때는 큐브에 포함시킬 데이터가 결합된 파티션 데이터에 모두 포함되게 해야 합니다.  
  
 마지막 단계로, 일반적으로 테이블 자체(아직 있는 경우)를 기반으로 하는 기본 파티션을 제거합니다. 제거하지 않으면 쿼리 기반 파티션이 전체 테이블을 기반으로 하는 쿼리와 겹치게 됩니다.  
  
## <a name="see-also"></a>관련 항목  
 [파티션 &#40;Analysis Services-다차원 데이터&#41;](../multidimensional-models-olap-logical-cube-objects/partitions-analysis-services-multidimensional-data.md)   
 [원격 파티션](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)   
 [Analysis Services의 파티션 병합 &#40;&AMP;#40;SSAS-다차원&#41;](merge-partitions-in-analysis-services-ssas-multidimensional.md)  
  
  
