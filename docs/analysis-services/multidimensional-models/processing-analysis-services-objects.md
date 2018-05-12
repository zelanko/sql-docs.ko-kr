---
title: Analysis Services 개체 처리 | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: multidimensional-models
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d1cd8be08afc7ea0e8e7bf811db4e26208a2feae
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="processing-analysis-services-objects"></a>Analysis Services 개체 처리
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  처리를 수행하면 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체 유형인 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스, 큐브, 차원, 측정값 그룹, 파티션, 데이터 마이닝 구조 및 모델이 영향을 받습니다. 각 개체에 대해 개체 처리 수준을 지정하거나 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 자동으로 최적 처리 수준을 선택하도록 기본값 처리 옵션을 지정할 수 있습니다. 각 개체의 다른 처리 수준에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
 부정적인 영향을 최소화하기 위해 처리 작업의 결과를 파악해야 합니다. 예를 들어 차원을 전체 처리하면 해당 차원에 종속되는 모든 파티션이 처리되지 않은 상태로 자동 설정됩니다. 이렇게 되면 종속 파티션이 처리될 때까지 쿼리에 영향을 받는 큐브를 사용할 수 없습니다.  
  
 이 항목은 다음과 같은 섹션으로 구성됩니다.  
  
 [데이터베이스 처리](#bkmk_procdb)  
  
 [차원 처리](#bkmk_procdim)  
  
 [큐브 처리](#bkmk_proccube)  
  
 [측정값 그룹 처리](#bkmk_procmeasure)  
  
 [파티션 처리](#bkmk_procpartition)  
  
 [데이터 마이닝 구조 및 데이터 마이닝 모델 처리](#bkmk_procdm)  
  
##  <a name="bkmk_procdb"></a> 데이터베이스 처리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 데이터베이스에는 개체가 포함되어 있지만 데이터는 포함되어 있지 않습니다. 데이터베이스를 처리할 때 차원, 파티션, 마이닝 구조 및 마이닝 모델처럼 모델에 데이터를 저장하는 해당 개체를 재귀적으로 처리하도록 서버에 지시합니다.  
  
 데이터베이스를 처리하면 데이터베이스에 있는 파티션, 차원 및 마이닝 모델의 전체 또는 일부가 처리됩니다. 실제 처리 유형은 각 개체의 상태 및 선택하는 처리 옵션에 따라 달라집니다. 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_proccube"></a> 큐브 처리  
 큐브를 측정값 그룹 및 파티션에 대한 래퍼 개체로 생각할 수 있습니다. 큐브는 파티션에 저장된 하나 이상의 측정값 및 차원으로 구성됩니다. 차원은 큐브의 데이터 레이아웃을 정의합니다. 큐브를 처리할 때는 SQL 쿼리가 실행되어 팩트 테이블에서 값을 검색하고 큐브의 각 멤버를 적절한 측정값으로 채웁니다. 큐브의 노드에 대한 모든 특정 경로에는 값 또는 계산 가능한 값이 있습니다.  
  
 큐브를 처리하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 큐브에서 처리되지 않은 차원 및 큐브의 측정값 그룹에 있는 파티션의 전체 또는 일부를 처리합니다. 세부 사항은 처리 시작 시의 개체 상태와 선택하는 처리 옵션에 따라 달라집니다. 처리 옵션에 대한 자세한 내용은 [처리 옵션 및 설정&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-options-and-settings-analysis-services.md)을 참조하세요.  
  
 큐브를 처리하면 컴퓨터에서 읽을 수 있는 파일이 생성되며 이 파일에 관련 팩트 데이터가 저장됩니다. 생성된 집계가 있으면 집계 데이터 파일에 저장됩니다. 그러면 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 의 개체 탐색기나 [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]  
  
##  <a name="bkmk_procdim"></a> 차원 처리  
 차원을 처리하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 차원 테이블에 대해 쿼리를 생성 및 실행하여 처리에 필요한 정보를 반환합니다.  
  
|Country|Sales Region|State|  
|-------------|------------------|-----------|  
|United States|West|California|  
|United States|West|Oregon|  
|United States|West|Washington|  
  
 처리 자체에서는 테이블 형식의 데이터를 사용 가능한 계층으로 변환합니다. 이러한 계층은 완전히 표시된 멤버 이름이며 내부적으로 고유 숫자 경로로 표시됩니다. 다음 예에서는 계층을 텍스트로 표시합니다.  
  
||  
|-|  
|[United States]|  
|[United States].[West]|  
|[United States].[West].[California]|  
|[United States].[West].[Oregon]|  
|[United States].[West].[Washington]|  
  
 차원 처리 시 큐브 수준에서 정의된 계산 멤버를 만들거나 업데이트하지 않습니다. 계산 멤버는 큐브 정의가 업데이트될 때 영향을 받습니다. 또한 차원 처리 시 집계를 만들거나 업데이트하지 않지만 집계가 삭제될 수 있습니다. 집계는 파티션을 처리하는 동안에만 생성 또는 업데이트됩니다.  
  
 차원을 처리할 때는 해당 차원이 여러 큐브에서 사용될 수 있다는 점을 기억해야 합니다. 차원을 처리하면 해당 큐브는 처리되지 않은 것으로 표시되고 쿼리에 사용할 수 없게 됩니다. 차원과 관련 큐브 둘 다 동시에 처리하려면 일괄 처리 설정을 사용합니다. 자세한 내용은 [일괄 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)을 참조하세요.  
  
##  <a name="bkmk_procmeasure"></a> 측정값 그룹 처리  
 측정값 그룹을 처리하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 가 측정값 그룹의 전체 또는 일부 파티션 및 측정값 그룹에 참여하지만 처리되지 않은 모든 차원을 처리합니다. 처리 작업의 세부 사항은 선택하는 처리 옵션에 따라 달라집니다. 큐브의 다른 측정값 그룹에 영향을 미치지 않고 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 하나 이상의 측정값 그룹을 처리할 수 있습니다.  
  
> [!NOTE]  
>  프로그래밍 방식으로 또는 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]를 사용하여 개별 측정값 그룹을 처리할 수 있습니다. [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)]에서 개별 측정값 그룹을 처리할 수 없지만 파티션을 사용하여 처리할 수 있습니다.  
  
##  <a name="bkmk_procpartition"></a> 파티션 처리  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 를 효과적으로 관리하려면 데이터를 분할해야 합니다. 파티션을 처리할 때 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 데이터 구조 제한 사항과 함께 하드 디스크 사용 및 공간 제약 조건을 고려해야 하므로 파티션 처리는 고유한 프로세스입니다. 빠른 쿼리 응답 시간과 높은 처리량을 유지하려면 정기적으로 파티션을 생성, 처리 및 병합해야 합니다. 파티션을 병합하는 동안 중복 데이터가 통합될 가능성을 인식하고 관리하는 것이 중요합니다. 자세한 내용은 [Analysis Services의 파티션 병합&#40;SSAS - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/merge-partitions-in-analysis-services-ssas-multidimensional.md)을 참조하세요.  
  
 파티션을 처리하면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 선택하는 처리 옵션에 따라 파티션과 해당 파티션에서 처리되지 않은 모든 차원을 처리합니다. 파티션을 사용하면 처리 시 여러 가지 이점이 있습니다. 큐브의 다른 파티션에 영향을 미치지 않고 파티션을 처리할 수 있습니다. 파티션은 셀 쓰기 저장(writeback)이 필요한 데이터를 저장할 때 유용합니다. 쓰기 저장은 사용자가 새 데이터를 파티션에 다시 기록하여 예상한 변경 내용의 결과를 보는 가정(what-if) 분석을 수행할 수 있게 해 주는 기능입니다. 쓰기 저장 파티션은 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 셀 쓰기 저장 기능을 사용하는 경우에 필요합니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 처리 능력을 보다 효율적으로 사용하여 전체 처리 시간을 상당히 줄일 수 있으므로 파티션을 병렬로 처리하는 것이 유용합니다. 파티션을 순서대로 처리할 수도 있습니다.  
  
##  <a name="bkmk_procdm"></a> 데이터 마이닝 구조 및 데이터 마이닝 모델 처리  
 마이닝 구조는 데이터 마이닝 모델을 생성할 데이터 도메인을 정의합니다. 하나의 마이닝 구조는 둘 이상의 마이닝 모델을 포함할 수 있습니다. 마이닝 구조를 연결된 해당 마이닝 모델과 별도로 처리할 수 있습니다. 마이닝 구조를 별도로 처리하면 이 구조는 데이터 원본의 학습 데이터로 채워집니다.  
  
 데이터 마이닝 모델을 처리할 때 학습 데이터는 마이닝 모델 알고리즘을 통과하고 마이닝 모델 알고리즘을 사용하여 모델 성향을 습득하고 내용을 빌드합니다. 데이터 마이닝 모델 개체에 대한 자세한 내용은 [마이닝 구조&#40;Analysis Services - 데이터 마이닝&#41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)를 참조하세요.  
  
 마이닝 구조 및 모델을 처리하는 방법은 [처리 요구 사항 및 고려 사항&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [도구 및 처리 접근 방법&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/tools-and-approaches-for-processing-analysis-services.md)   
 [일괄 처리 & #40; Analysis Services & #41;](../../analysis-services/multidimensional-models/batch-processing-analysis-services.md)   
 [다차원 모델 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
