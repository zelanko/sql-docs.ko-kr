---
title: 처리 요구 사항 및 고려 사항 (데이터 마이닝) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: data-mining
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d4228f5ae90f7fdd2510787b6fca6ad10f7302e4
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="processing-requirements-and-considerations-data-mining"></a>처리 요구 사항 및 고려 사항(데이터 마이닝)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  이 항목에서는 데이터 마이닝 개체를 처리할 때 유의해야 할 몇 가지 기술적 고려 사항에 대해 설명합니다. 처리의 정의와 처리가 데이터 마이닝에 적용되는 방식에 대한 일반적인 설명은 [데이터 마이닝 개체 처리](../../analysis-services/data-mining/processing-data-mining-objects.md)를 참조하세요.  
  
 [관계형 저장소에 대한 쿼리](#bkmk_QueryReqs)  
  
 [마이닝 구조 처리](#bkmk_ProcessStructures)  
  
 [마이닝 모델 처리](#bkmk_ProcessModels)  
  
##  <a name="bkmk_QueryReqs"></a> 처리 중의 관계형 저장소에 대한 쿼리  
 데이터 마이닝에는 원본 데이터 쿼리, 원시 통계 확인, 마이닝 모델 학습을 위한 모델 정의 및 알고리즘 사용의 세 가지 단계가 있습니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버는 원시 데이터를 제공하는 데이터베이스에 대해 쿼리를 실행합니다. 이 데이터베이스는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 의 인스턴스일 수도 있고 이전 버전의 SQL Server 데이터베이스 엔진일 수도 있습니다. 데이터 마이닝 구조를 처리할 때 원본의 데이터는 마이닝 구조로 전송되고 디스크에 압축된 새 형식으로 저장됩니다. 데이터 원본의 모든 열이 처리되는 것은 아니고, 마이닝 구조에 포함되어 있으며 바인딩에 의해 정의된 열만 처리됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 는 이 데이터를 사용하여 모든 데이터 및 분할된 열의 인덱스를 작성하고 연속 열에 대한 별도의 인덱스를 만듭니다. 중첩 테이블당 하나의 쿼리가 실행되어 인덱스를 만들고, 중첩 테이블당 또 하나의 추가 쿼리가 생성되어 각 중첩 테이블과 사례 테이블 쌍 간의 관계를 처리합니다. 여러 개의 쿼리를 만드는 이유는 특수 내부 다차원 데이터 저장소를 처리하기 위해서입니다. [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] DatabaseConnectionPoolMax **서버 속성을 설정하여**가 관계형 저장소에 보내는 쿼리의 수를 제한할 수 있습니다. 자세한 내용은 [OLAP Properties](../../analysis-services/server-properties/olap-properties.md)을 참조하세요.  
  
 모델을 처리할 때 모델은 데이터 원본에서 데이터를 다시 읽지 않고 대신 마이닝 구조에서 데이터의 요약을 가져옵니다. 캐시된 인덱스와 함께 만든 큐브를 사용하여 사례 데이터가 캐시되면 서버는 모델 학습을 위한 독립 스레드를 만듭니다.  
  
 버전에 대 한 자세한 내용은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 병렬 모델 처리를 지 원하는 참조 하십시오 [SQL Server 2012 버전에서 지 원하는 기능](http://go.microsoft.com/fwlink/?linkid=232473) (http://go.microsoft.com/fwlink/?linkid=232473)합니다.  
  
##  <a name="bkmk_ProcessStructures"></a> 마이닝 구조 처리  
 모든 종속 모델과 함께 또는 따로 마이닝 구조를 처리할 수 있습니다. 일부 모델이 처리하는 데 오랜 시간이 소요될 것으로 예상되어 해당 작업을 지연시키려는 경우 마이닝 구조를 모델과 따로 처리하는 것이 유용할 수 있습니다.  
  
 자세한 내용은 [Process a Mining Structure](../../analysis-services/data-mining/process-a-mining-structure.md)를 참조하세요.  
  
 하드 디스크 공간을 절약하려는 경우 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 마이닝 구조 캐시를 로컬로 유지한다는 사실에 유념하십시오. 즉, Analysis Services에서는 모든 학습 데이터를 로컬 하드 디스크에 씁니다. 데이터를 캐시하지 않으려면 마이닝 구조의 <xref:Microsoft.AnalysisServices.MiningStructureCacheMode> 속성을 **ClearAfterProcessing**를 참조하세요. 이렇게 하면 모델이 처리된 후 캐시가 삭제됩니다. 단, 이 경우 마이닝 구조에서 드릴스루도 해제됩니다. 자세한 내용은 [드릴스루 쿼리&#40;데이터 마이닝&#41;](../../analysis-services/data-mining/drillthrough-queries-data-mining.md)를 참조하세요.  
  
 또한 캐시를 지우면 홀드아웃 테스트 집합도 사용할 수 없게 되고 테스트 집합 파티션의 정의도 지워집니다. 홀드아웃 테스트 집합에 대한 자세한 내용은 [데이터 집합 학습 및 테스트](../../analysis-services/data-mining/training-and-testing-data-sets.md)를 참조하세요.  
  
##  <a name="bkmk_ProcessModels"></a> 마이닝 모델 처리  
 마이닝 모델을 관련 마이닝 구조와 따로 처리하거나, 구조를 기반으로 하는 모든 모델을 구조와 함께 처리할 수 있습니다.  
  
 자세한 내용은 [마이닝 모델 처리](../../analysis-services/data-mining/process-a-mining-model.md)를 참조하세요.  
  
 하지만 [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]에서는 구조와 함께 처리할 마이닝 모델을 다중 선택할 수 없습니다. 처리되는 모델을 제어해야 하는 경우 모델을 개별적으로 선택하거나 XMLA 또는 DMX을 사용하여 모델을 직렬로 처리해야 합니다.  
  
## <a name="when-reprocessing-is-required"></a>다시 처리가 필요한 경우  
 정의한 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 모델을 사용하려면 먼저 해당 모델을 처리해야 합니다. 또한 마이닝 모델 구조를 변경하거나, 학습 데이터를 업데이트하거나, 기존 마이닝 모델을 변경하거나, 새 마이닝 모델을 구조에 추가할 때마다 마이닝 모델을 다시 처리해야 합니다.  
  
 이러한 시나리오에서는 마이닝 모델도 처리됩니다.  
  
 **프로젝트 배포**: 프로젝트 설정 및 프로젝트의 현재 상태에 따라 프로젝트를 배포할 때 프로젝트의 마이닝 모델은 대개 전체적으로 처리됩니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서버에 이전에 처리한 버전이 있고 구조에 대한 이후 변경 내용이 없지 않으면 배포 시작 시 처리가 자동으로 시작됩니다. 드롭다운 목록에서 **솔루션 배포** 를 선택하거나 F5 키를 눌러 프로젝트를 배포할 수 있습니다. 다음을 수행할 수 있습니다.  
  
 마이닝 모델이 배포되는 방식을 제어하는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 배포 속성을 설정하는 방법은 [데이터 마이닝 솔루션 배포](../../analysis-services/data-mining/deployment-of-data-mining-solutions.md)를 참조하세요.  
  
 **마이닝 모델 이동**: EXPORT 명령을 사용하여 마이닝 모델을 이동하는 경우 모델에 데이터를 제공할 것으로 예상되는 마이닝 구조의 이름이 포함된 모델의 정의만 내보내집니다.  
  
 EXPORT 및 IMPORT 명령을 사용하는 다음 시나리오에 대한 다시 처리 요구 사항은 다음과 같습니다.  
  
-   마이닝 구조가 대상 인스턴스에 있고 마이닝 구조가 처리되지 않은 상태입니다.  
  
     구조와 모델을 모두 다시 처리해야 합니다.  
  
-   마이닝 구조가 대상 인스턴스에 있고 마이닝 구조가 처리되었습니다. 마이닝 모델만 내보냈습니다.  
  
     처리하지 않고 모델을 사용할 수 있습니다.  
  
-   WITH DEENDENCIES 키워드를 사용하여 마이닝 구조 정의도 내보냈습니다.  
  
     구조와 모델을 모두 다시 처리해야 합니다.  
  
 자세한 내용은 [데이터 마이닝 개체 내보내기 및 가져오기](../../analysis-services/data-mining/export-and-import-data-mining-objects.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [마이닝 구조 & #40; Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [마이닝 구조 & #40; Analysis Services-데이터 마이닝 & #41;](../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)   
 [다차원 모델 처리&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/processing-a-multidimensional-model-analysis-services.md)  
  
  
