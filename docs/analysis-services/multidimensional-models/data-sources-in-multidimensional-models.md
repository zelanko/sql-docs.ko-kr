---
title: "다차원 모델의 데이터 원본 | Microsoft Docs"
ms.custom: 
ms.date: 03/04/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- analysis-services/multidimensional-tabular
- analysis-services/data-mining
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- metadata [Analysis Services]
- Analysis Services objects, data sources
- storing data [Analysis Services], data sources
- data sources [Analysis Services], about data sources
- security [Analysis Services], data sources
- data sources [Analysis Services]
- storage [Analysis Services], data sources
ms.assetid: a16469d9-9d53-4e35-9982-fc06327a9d33
caps.latest.revision: "45"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 8c8da4c13bdddd0994ec67548ce2666d7b06fea8
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="data-sources-in-multidimensional-models"></a>다차원 모델의 데이터 원본
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]가져오거나를 다차원 모델에 로드 하는 모든 데이터는 외부 데이터 원본에서 생성 됩니다. 일반적으로 원본 데이터는 보고용으로 디자인된 데이터 웨어하우스의 데이터이지만 [!INCLUDE[ssIS](../../includes/ssis-md.md)] 패키지와 같은 매개자를 통해 직접 또는 간접으로 액세스되는 관계형 데이터베이스의 데이터일 수도 있습니다.  
  
 **의** 데이터 원본 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 개체는 외부 데이터 원본에 대한 직접 연결을 지정합니다. 물리적 위치 외에 데이터 원본 개체는 연결 문자열, 데이터 공급자, 자격 증명 및 연결 동작을 제어하는 기타 속성도 지정합니다.  
  
 데이터 원본 개체에서 제공되는 정보는 다음과 같은 작업 중에 사용됩니다.  
  
-   데이터 원본 뷰를 모델에 생성하기 위해 사용되는 스키마 정보 및 기타 메타데이터를 가져옵니다.  
  
-   처리 중 데이터를 쿼리하거나 모델에 로드합니다.  
  
-   ROLAP 저장소 모드를 사용하는 다차원 또는 데이터 마이닝 모델에 대해 쿼리를 실행합니다.  
  
-   원격 파티션을 읽거나 씁니다.  
  
-   연결된 개체에 연결하고 대상과 원본 간에 동기화합니다.  
  
-   관계형 데이터베이스에 저장된 팩트 테이블 데이터를 업데이트하는 쓰기 저장(write back) 작업을 수행합니다.  
  
 다차원 모델을 아래쪽에서 위쪽으로 작성할 때 데이터 원본 개체를 만들어 시작한 다음 이 개체를 사용하여 다음 개체인 **데이터 원본 뷰**를 생성합니다. 데이터 원본 뷰는 모델의 데이터 추상화 계층입니다. 일반적으로 원본 데이터베이스의 스키마를 기본으로 사용하여 데이터 원본 개체 이후에 생성됩니다. 그러나 큐브 및 차원으로 시작하여 디자인을 가장 잘 지원하는 스키마를 생성하는 것을 비롯하여 모델을 생성하는 다른 방법을 선택할 수 있습니다.  
  
 모델 생성 방법에 관계없이 각 모델에는 원본 데이터에 대한 연결을 지정하는 적어도 하나 이상의 데이터 원본 개체가 필요합니다. 여러 데이터 원본 개체를 하나의 모델로 생성하여 다른 원본에서 데이터를 사용하거나 특정 개체에 대한 연결 속성을 변경할 수 있습니다.  
  
 데이터 원본 개체는 모델의 다른 개체에 관계없이 관리할 수 있습니다. 데이터 원본을 만든 후 해당 속성을 나중에 변경할 수 있으며 그 후 데이터가 제대로 검색되는지 확인하기 위해 모델을 전처리할 수 있습니다.  
  
## <a name="related-topics-and-tasks"></a>관련 항목 및 태스크  
  
|항목|Description|  
|-----------|-----------------|  
|[지원되는 데이터 원본&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)|다차원 모델에서 사용할 수 있는 데이터 원본 유형에 대해 설명합니다.|  
|[데이터 원본 만들기&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/create-a-data-source-ssas-multidimensional.md)|다차원 모델에 데이터 원본 개체를 추가하는 방법에 설명합니다.|  
|[솔루션 탐색기에서 데이터 원본 삭제&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/delete-a-data-source-in-solution-explorer-ssas-multidimensional.md)|이 절차를 사용하여 다차원 모델에서 데이터 원본 개체를 삭제할 수 있습니다.|  
|[데이터 원본 속성 설정&#40;SSAS 다차원&#41;](../../analysis-services/multidimensional-models/set-data-source-properties-ssas-multidimensional.md)|각 속성과 각 속성을 설정하는 방법에 대해 설명합니다.|  
|[가장 옵션 설정&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/set-impersonation-options-ssas-multidimensional.md)|가장 정보 대화 상자에서 옵션을 구성하는 방법을 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [데이터베이스 개체&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/olap-logical/database-objects-analysis-services-multidimensional-data.md)   
 [논리적 아키텍처&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models/olap-logical/understanding-microsoft-olap-logical-architecture.md)   
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [데이터 원본 및 바인딩 &#40; SSAS 다차원 &#41;](../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)  
  
  
