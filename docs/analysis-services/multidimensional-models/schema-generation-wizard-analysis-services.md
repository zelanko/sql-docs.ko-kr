---
title: "스키마 생성 마법사 (Analysis Services) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
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
helpviewer_keywords: relational schema [Analysis Services]
ms.assetid: 68bf7ba3-d0cb-437f-9a3e-9edc0999af19
caps.latest.revision: "16"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 5bd04de3519739a08ba65b5ecf2e27e0b5915254
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="schema-generation-wizard-analysis-services"></a>스키마 생성 마법사(Analysis Services)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)][!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)] 내에서 개체를 OLAP를 정의할 때 관계형 스키마 작업의 두 가지 방법을 지원는 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트 또는 데이터베이스입니다. 일반적으로 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트나 데이터베이스 내의 데이터 원본 뷰에 생성된 논리적 데이터 모델을 기반으로 OLAP 개체를 정의합니다. 이 데이터 원본 뷰는 데이터 원본 뷰에 사용자 지정된 대로 하나 이상의 관계형 데이터 원본의 스키마 요소를 기반으로 정의됩니다.  
  
 또는 OLAP 개체를 먼저 정의한 다음 데이터 원본 뷰 및 데이터 원본과, 해당 OLAP 개체를 지원하는 기본 관계형 데이터베이스 스키마를 생성할 수도 있습니다. 이러한 관계형 데이터베이스를 주제 영역 데이터베이스라고 합니다.  
  
 때로는 이 방법을 하향식 디자인이라고 하며 프로토타입 및 분석 모델링에 자주 사용됩니다. 이 방법을 사용할 경우 스키마 생성 마법사를 사용하여 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 프로젝트나 데이터베이스에서 정의한 OLAP 개체를 기반으로 기본 데이터 원본과 데이터 원본 개체를 만듭니다.  
  
 이 방법은 반복적인 방법입니다. 즉, 차원과 큐브의 디자인을 변경할 때마다 마법사를 다시 실행해야 합니다. 마법사를 실행할 때마다 마법사는 변경 내용을 원본 개체에 통합하여 기본 데이터베이스에 포함된 데이터를 최대한 유지합니다.  
  
 생성된 스키마는 SQL Server 관계형 데이터베이스 엔진 스키마입니다. 마법사는 다른 관계형 데이터베이스 제품에 대한 스키마를 생성하지 않습니다.  
  
 주제 영역 데이터베이스에 채워진 데이터는 SQL Server 관계형 데이터베이스를 채우는 데 사용하는 도구 및 기법을 통해 별도로 추가됩니다. 대부분의 경우 마법사를 다시 실행할 때 데이터가 유지되지만 예외가 있습니다. 예를 들어 데이터가 포함된 차원이나 특성을 삭제하면 일부 데이터가 삭제됩니다. 스키마 변경으로 인해 스키마 생성 마법사가 일부 데이터를 삭제해야 하는 경우에는 데이터를 삭제하기 전에 경고 메시지를 표시하므로 재생성을 취소할 수 있습니다.  
  
 일반적으로, 스키마 생성 마법사가 원래 생성했던 개체에서 변경된 내용은 이후에 스키마 생성 마법사가 해당 개체를 다시 생성할 때 덮어쓰게 됩니다. 단, 스키마 생성 마법사가 생성한 테이블에 열을 추가하는 경우는 예외입니다. 이와 같은 경우에는 스키마 생성 마법사가 테이블에 추가된 열 및 해당 열의 데이터를 그대로 유지합니다.  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 표에는 스키마 생성 마법사의 작업 방법을 설명하는 추가 항목이 나와 있습니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[스키마 생성 마법사 사용&#40;Analysis Services&#41;](../../analysis-services/multidimensional-models/use-the-schema-generation-wizard-analysis-services.md)|주제 영역 데이터베이스와 준비 영역 데이터베이스의 스키마를 생성하는 방법에 대해 설명합니다.|  
|[데이터베이스 스키마 이해](../../analysis-services/multidimensional-models/understanding-the-database-schemas.md)|주제 영역 데이터베이스와 준비 영역 데이터베이스에 대해 생성되는 스키마에 대해 설명합니다.|  
|[증분 생성 이해](../../analysis-services/multidimensional-models/understanding-incremental-generation.md)|스키마 생성 마법사의 증분 생성 기능에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [다차원 모델의 데이터 원본 뷰](../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)   
 [다차원 모델의 데이터 원본](../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)   
 [지원되는 데이터 원본&#40;SSAS - 다차원&#41;](../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)  
  
  
