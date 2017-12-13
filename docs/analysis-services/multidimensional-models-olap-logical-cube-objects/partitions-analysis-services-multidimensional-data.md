---
title: "파티션 (Analysis Services-다차원 데이터) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to: SQL Server 2016 Preview
helpviewer_keywords:
- storage [Analysis Services], partitions
- incremental updates [Analysis Services]
- data sources [Analysis Services], partitions
- data storage [Analysis Services]
- aggregations [Analysis Services], partitions
- OLAP objects [Analysis Services], partitions
- storing data [Analysis Services], partitions
- partitions [Analysis Services], about partitions
- cubes [Analysis Services], partitions
- partitions [Analysis Services]
- remote partitions [Analysis Services]
- measure groups [Analysis Services], partitions
ms.assetid: cd10ad00-468c-4d49-9f8d-873494d04b4f
caps.latest.revision: "43"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: On Demand
ms.openlocfilehash: dab66f2e60e602f163f3c0986719655b6f89f3a5
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="partitions-analysis-services---multidimensional-data"></a>파티션(Analysis Services - 다차원 데이터)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]파티션은은 측정값 그룹 데이터 부분의 컨테이너입니다. MDX 쿼리는 파티션을 표시하지 않으므로 측정값 그룹에 대해 정의된 파티션 수에 관계없이 모든 MDX 쿼리는 측정값 그룹의 전체 콘텐츠를 반영합니다. 파티션의 데이터 콘텐츠는 파티션의 쿼리 바인딩과 조각화 식에 의해 정의됩니다.  
  
 단순 <xref:Microsoft.AnalysisServices.Partition> 개체는 기본 정보, 조각화 정의, 집계 디자인 등으로 구성되어 있습니다. 기본 정보에는 파티션의 이름, 저장소 모드, 처리 모드 등이 포함됩니다. 조각화 정의는 튜플 또는 집합을 지정하는 MDX 식입니다. 조각화 정의에는 StrToSet MDX 함수와 동일한 제한 사항이 있습니다. 조각화 정의는 CONSTRAINED 매개 변수와 함께 큐브의 차원, 계층, 수준, 멤버 이름, 키, 고유 이름 또는 기타 명명된 개체는 사용할 수 있지만 MDX 함수는 사용할 수 없습니다. 집계 디자인은 여러 파티션에서 공유할 수 있는 집계 정의의 컬렉션입니다. 기본값은 부모 큐브의 집계 디자인에서 가져옵니다.  
  
 파티션을 사용 하 여 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 관리 하 고 큐브에서 데이터 및 측정값 그룹에 대 한 집계를 저장 합니다. 모든 측정값 그룹에는 파티션이 하나 이상 있으며 이 파티션은 측정값 그룹을 정의할 때 생성됩니다. 측정값 그룹에 대해 새 파티션을 만들면 해당 측정값 그룹에 대해 이미 존재하는 파티션 집합에 새 파티션이 추가됩니다. 측정값 그룹에는 모든 파티션에 있는 결합된 데이터가 반영됩니다. 즉, 측정값 그룹에 데이터가 여러 번 반영되지 않도록 측정값 그룹의 한 파티션에 대한 데이터에 측정값 그룹의 다른 모든 파티션에 대한 데이터가 포함되지 않도록 해야 합니다. 측정값 그룹의 원래 파티션은 큐브의 데이터 원본 뷰에 있는 단일 팩트 테이블을 기반으로 합니다. 측정값 그룹의 파티션이 여러 개가 있으면 각 파티션은 큐브의 데이터 원본 뷰 또는 기본 관계형 데이터 원본에 있는 서로 다른 테이블을 참조할 수 있습니다. 각 파티션을 테이블의 서로 다른 행으로 제한하는 경우 측정값 그룹에 있는 둘 이상의 파티션이 같은 테이블을 참조할 수 있습니다.  
  
 파티션은 큐브 중에서도 특히 크기가 큰 큐브를 관리하기 위한 강력하고도 융통성 있는 방법입니다. 예를 들어 판매 정보가 포함된 큐브에는 각 지난 연도의 데이터에 대한 파티션과 현재 연도의 각 분기에 대한 파티션이 포함될 수 있습니다. 큐브에 현재 정보를 추가할 때 현재 분기 파티션만 처리되어야 합니다. 적은 양의 데이터를 처리하면 처리 시간이 감소하여 처리 성능이 향상됩니다. 연말에는 4개의 분기별 파티션이 해당 연도에 대한 단일 파티션으로 병합될 수 있으며 새 연도의 첫 번째 분기에 대한 새 파티션이 생성됩니다. 또한 데이터 웨어하우스 로드 및 큐브 처리 절차의 일부로 새 파티션 생성 프로세스를 자동화할 수 있습니다.  
  
 파티션은 큐브의 업무용 사용자에게 표시되지 않습니다. 그러나 관리자가 파티션을 구성, 추가 또는 삭제할 수 있습니다. 각 파티션은 별개의 파일 집합에 저장됩니다. 각 파티션의 집계 데이터를 파티션이 정의된 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 인스턴스, [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 다른 인스턴스 또는 파티션의 원본 데이터를 제공하는 데 사용되는 데이터 원본에 저장할 수 있습니다. 파티션을 사용하면 큐브의 원본 데이터와 집계 데이터를 여러 하드 드라이브와 서버 컴퓨터에 분산할 수 있습니다. 중대형 큐브의 경우 파티션을 통해 쿼리 성능, 로드 성능 및 큐브 유지 관리의 편의성을 크게 향상시킬 수 있습니다.  
  
 각 파티션의 저장소 모드를 측정값 그룹의 다른 파티션과 독립적으로 구성할 수 있습니다. 파티션은 원본 데이터 위치, 저장소 모드, 자동 관리 캐싱 및 집계 디자인 등의 옵션을 함께 사용하여 저장할 수 있습니다. 실시간 OLAP 및 자동 관리 캐싱에 대한 옵션을 사용하면 파티션을 디자인할 때 대기 시간에 맞춰 쿼리 속도를 균형있게 조정할 수 있습니다. 저장소 옵션은 관련된 차원과 차원값 그룹의 팩트에도 적용할 수 있습니다. 이러한 융통성을 통해 사용자의 개별적인 요구에 맞는 큐브 저장소 전략을 디자인할 수 있습니다. 자세한 내용은 참조 [파티션 저장소 모드 및 처리](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [집계 및 집계 디자인](../../analysis-services/multidimensional-models-olap-logical-cube-objects/aggregations-and-aggregation-designs.md) 및 [자동 관리 캐싱 &#40; 파티션 &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md).  
  
## <a name="partition-structure"></a>파티션 구조  
 파티션 구조는 이 측정값 그룹의 구조와 일치해야 하므로 측정값 그룹을 정의하는 측정값을 관련된 모든 차원과 함께 파티션에 정의해야 합니다. 따라서 파티션 생성 시 측정값 그룹에 대해 정의된 것과 동일한 측정값 및 관련 차원 집합이 자동으로 상속됩니다.  
  
 그러나 측정값 그룹의 각 파티션에는 서로 다른 팩트 테이블이 있을 수 있고 이러한 팩트 테이블은 서로 다른 데이터 원본에서 제공될 수 있습니다. 측정값 그룹의 파티션마다 다른 팩트 테이블이 있으면 측정값 그룹의 구조를 유지하기 위해 테이블이 비슷해야 합니다. 즉, 처리 쿼리에서 모든 파티션의 모든 팩트 테이블에 대해 같은 열과 같은 데이터 형식을 반환해야 합니다.  
  
 각 파티션의 팩트 테이블이 서로 다른 데이터 원본을 기반으로 하면 관련 차원에 대한 원본 테이블과 모든 중간 팩트 테이블이 모든 데이터 원본에도 있어야 하며 모든 데이터베이스에서 구조가 같아야 합니다. 또한 측정값 그룹과 관련된 큐브 차원에 대한 특성을 정의하는 데 사용되는 모든 차원 테이블 열이 모든 데이터 원본에 있어야 합니다. 파티션 원본 테이블의 구조와 측정값 그룹 원본 테이블의 구조가 동일한 경우 파티션 원본 테이블과 관련 차원 테이블 간에 모든 조인을 정의할 필요가 없습니다.  
  
 측정값 그룹에서 측정값을 정의하는 데 사용되지 않는 열은 일부 팩트 테이블에만 있고 다른 팩트 테이블에 없을 수 있습니다. 마찬가지로 관련 차원 테이블에서 특성을 정의하는 데 사용되지 않는 열은 일부 데이터베이스에만 있고 다른 데이터베이스에 없을 수 있습니다. 팩트 테이블이나 관련 차원 테이블에 대해 사용되지 않는 테이블은 일부 데이터베이스에만 있고 다른 데이터베이스에 없을 수 있습니다.  
  
## <a name="data-sources-and-partition-storage"></a>데이터 원본 및 파티션 저장소  
 파티션은 데이터 원본의 테이블 또는 뷰를 기반으로 하거나 데이터 원본 뷰의 테이블 또는 명명된 쿼리를 기반으로 합니다. 파티션 데이터가 저장되는 위치는 데이터 원본 바인딩에 의해 정의됩니다. 일반적으로 측정값 그룹을 행이나 열로 분할할 수 있습니다.  
  
-   수평 분할된 측정값 그룹에서 측정값 그룹의 각 파티션은 별개의 테이블을 기반으로 합니다. 이런 종류의 분할은 데이터가 여러 테이블로 구분되어 있을 때 적합합니다. 예를 들어 일부 관계형 데이터베이스에는 각 달의 데이터에 대한 별개의 테이블이 있습니다.  
  
-   수직 분할된 측정값 그룹에서 측정값 그룹은 단일 테이블을 기반으로 하고 각 파티션은 파티션에 대한 데이터를 필터링하는 원본 시스템 쿼리를 기반으로 합니다. 예를 들어 단일 테이블에 여러 달의 데이터가 포함된 경우 파티션마다 서로 다른 달의 데이터를 반환하는 Transact-SQL WHERE 절을 적용하여 측정값 그룹을 월별로 다시 분할할 수 있습니다.  
  
 각 파티션에는 파티션에 대한 데이터와 집계가 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 로컬 인스턴스 또는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 다른 인스턴스를 사용하는 원격 파티션에 저장되는지 결정하는 저장 설정이 있습니다. 저장소 설정을 구성하여 저장소 모드 및 자동 관리 캐싱을 사용하여 파티션의 대기 시간을 제어할지 여부를 지정할 수도 있습니다. 자세한 내용은 참조 [파티션 저장소 모드 및 처리](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-partition-storage-modes-and-processing.md), [자동 관리 캐싱 &#40; 파티션 &#41; ](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-proactive-caching.md), 및 [원격 파티션을](../../analysis-services/multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)합니다.  
  
## <a name="incremental-updates"></a>증분 업데이트  
 여러 개의 파티션으로 이루어진 측정값 그룹에서 파티션을 만들고 관리할 때는 큐브 데이터가 정확하게 유지되도록 특별히 주의해야 합니다. 단일 파티션 측정값 그룹에는 대체로 이러한 주의가 필요하지 않지만 파티션 증분 업데이트를 수행할 때는 주의가 필요합니다. 파티션에 대해 증분 업데이트를 수행하면 원본 파티션과 동일한 구조로 새로운 임시 파티션이 생성됩니다. 임시 파티션은 처리된 다음 원본 파티션과 병합됩니다. 그러므로 임시 파티션을 채우는 처리 쿼리에서 기존 파티션에 있는 데이터를 복제하지 않도록 해야 합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [측정값 속성 구성](../../analysis-services/multidimensional-models/configure-measure-properties.md)   
 [다차원 모델의 큐브](../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)  
  
  
