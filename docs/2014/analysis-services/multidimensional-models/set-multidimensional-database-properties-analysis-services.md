---
title: 다차원 데이터베이스 속성 설정 (Analysis Services) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- properties [Analysis Services], databases
ms.assetid: a8be5b3f-3148-448a-976c-7222705155d9
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: aa3e1544f625183df3240359aa22b117144244d3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66072999"
---
# <a name="set-multidimensional-database-properties-analysis-services"></a>다차원 데이터베이스 속성 설정(Analysis Services)
  데이터베이스 디자이너에서는 다양 [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 한 데이터베이스 속성을 구성할 수 있습니다. [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]  
  
 이 디자이너에서는 다음과 같은 유형의 태스크를 수행할 수 있습니다.  
  
-   온라인 모드로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스에 연결되어 있으면 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 데이터베이스의 이름을 변경할 수 있습니다. 프로젝트 모드로 작업하는 경우 다음 프로젝트 배포에 대해 데이터베이스 이름을 변경할 수 있습니다. 자세한 내용은 [다차원 데이터베이스 이름 바꾸기&#40;Analysis Services&#41;](rename-a-multidimensional-database-analysis-services.md) 및 [Analysis Services 프로젝트 속성 구성&#40;SSDT&#41;](configure-analysis-services-project-properties-ssdt.md)을 참조하세요.  
  
-   사용자에게 표시되는 데이터베이스에 대한 설명을 제공할 수 있습니다. 데이터베이스 이름을 볼 수도 있지만 변경할 수는 없습니다. 데이터베이스 이름을 변경하려면 프로젝트의 속성을 편집해야 합니다.  
  
-   데이터베이스 이름과 설명에 대한 번역을 하나 이상의 언어로 제공할 수 있습니다. 자세한 내용은 [큐브 번역](../multidimensional-models-olap-logical-cube-objects/cube-translations.md), [차원 번역](../multidimensional-models-olap-logical-dimension-objects/dimension-translations.md)및 [번역 &#40;Analysis Services&#41;](../translations-analysis-services.md)를 참조 하세요.  
  
-   기본 계정 유형 매핑을 보고 수정할 수 있습니다. 계정 유형 매핑은 하나 이상의 측정값에서 *ByAccount* 집계 함수를 사용할 때 사용됩니다. 각 계정 유형에 대해 별칭을 지정하고 계정 유형과 연결된 기본 집계 함수를 수정할 수 있습니다. 기본 집계 수정에 대한 자세한 내용은 [반가산적 동작 정의](define-semiadditive-behavior.md)를 참조하세요.  
  
## <a name="database-properties"></a>데이터베이스 속성  
 위의 기능 외에도 속성 창에서 다양한 데이터베이스 속성을 구성할 수 있습니다.  
  
|속성|Description|  
|--------------|-----------------|  
|Aggregation Prefix|데이터베이스의 모든 파티션에 대한 집계 이름에 사용할 수 있는 공통 접두사입니다. 자세한 내용은 [AggregationPrefix 요소&#40;ASSL&#41;](https://docs.microsoft.com/bi-reference/assl/properties/aggregationprefix-element-assl)를 참조하세요.|  
|데이터 정렬|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 배포하면 다른 값을 제공하지 않는 한 데이터베이스는 Collation 서버 속성에서 상속합니다.|  
|DataSourceImpersonationInfo|데이터베이스의 모든 데이터 원본 개체에 대한 기본 가장 모드를 지정합니다. 이 모드는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 서비스에서 개체를 처리하고 서버를 동기화하며 OpenQuery 및 SystemOpenSchema 데이터 마이닝 문을 실행할 때 사용합니다.|  
|예상 크기|디스크의 데이터베이스 파일에 대한 예상 크기를 제공합니다. 데이터가 여러 위치에 저장된 경우 이 예상 값은 데이터베이스 폴더 아래에 저장된 데이터 파일로만 제한됩니다.<br /><br /> 
  `EstimatedSize`는 메모리 예측을 위한 기초로 사용할 수도 있습니다. 일반적으로 데이터베이스를 메모리에 로드할 때 발생하는 추가적인 데이터 구조로 인해 메모리 요구 사항이 디스크 상의 데이터 크기보다 큽니다.<br /><br /> 메모리 요구 사항을 보다 세부적으로 예측하기 위해서는 데이터베이스 처리 전 및 후에 작업 관리자를 사용하여 Analysis Services 프로세스 메모리를 조사하고 데이터베이스의 메모리 요구 사항을 이해할 수 있도록 메서드로 활용되는 메모리를 관측할 수도 있습니다.|  
|언어|
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트를 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 인스턴스에 배포하면 다른 값을 제공하지 않는 한 데이터베이스는 Language 서버 속성에서 상속합니다.|  
|MasterDataSource ID|원격 파티션에 사용됩니다. 자세한 내용은 [Remote Partitions](../multidimensional-models-olap-logical-cube-objects/partitions-remote-partitions.md)을 참조하세요.|  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 속성 대화 상자 &#40;SSAS-다차원&#41;](../database-properties-dialog-box-ssas-multidimensional.md)   
 [SSDT&#41;&#40;Analysis Services 프로젝트 속성 구성](configure-analysis-services-project-properties-ssdt.md)  
  
  
