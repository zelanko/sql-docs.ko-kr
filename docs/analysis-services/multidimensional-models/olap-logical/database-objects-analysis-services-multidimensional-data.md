---
title: "데이터베이스 개체 (Analysis Services-다차원 데이터) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- objects [Analysis Services], about objects
- SQL Server Analysis Services, objects
- Analysis Services objects, about Analysis Services objects
- SSAS, objects
- Analysis Services objects
- objects [Analysis Services]
ms.assetid: f76d869b-fc1d-4807-9f28-da09c7be382d
caps.latest.revision: 32
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 32024dc0799fcc7324fd30349a65e741773db66b
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="database-objects-analysis-services---multidimensional-data"></a>데이터베이스 개체(Analysis Services - 다차원 데이터)
  A [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 인스턴스에 데이터베이스 개체 및 온라인 분석 처리 (OLAP) 및 데이터 마이닝에 사용할 어셈블리를 포함 합니다.  
  
-   데이터베이스에는 OLAP와 데이터 원본, 데이터 원본 뷰, 큐브, 측정값, 측정값 그룹, 차원, 특성, 계층, 마이닝 구조, 마이닝 모델 및 역할과 같은 데이터 마이닝 개체가 포함됩니다.  
  
-   어셈블리에는 MDX(Multidimensional Expressions) 및 DMX(Data Mining Extensions) 언어와 함께 제공된 기본 함수의 기능을 확장하는 사용자 정의 함수가 포함됩니다.  
  
 <xref:Microsoft.AnalysisServices.Database> 개체는 비즈니스 인텔리전스 프로젝트(예: OLAP 큐브, 차원 및 데이터 마이닝 구조) 및 해당 지원 개체(예: <xref:Microsoft.AnalysisServices.DataSource>, <xref:Microsoft.AnalysisServices.Account> 및 <xref:Microsoft.AnalysisServices.Role>)에 필요한 모든 데이터 개체의 컨테이너입니다.  
  
 <xref:Microsoft.AnalysisServices.Database> 개체는 다음을 포함하는 개체와 특성에 대한 액세스 권한을 제공합니다.  
  
-   액세스할 수 있는 모든 큐브(컬렉션)  
  
-   액세스할 수 있는 모든 차원(컬렉션)  
  
-   액세스할 수 있는 모든 마이닝 구조(컬렉션)  
  
-   모든 데이터 원본과 데이터 원본 뷰(두 개의 컬렉션)  
  
-   모든 역할과 데이터베이스 권한(두 개의 컬렉션)  
  
-   데이터베이스에 대한 데이터 정렬 값  
  
-   데이터베이스의 예상 크기  
  
-   데이터베이스의 언어 값  
  
-   데이터베이스의 표시 설정  
  
## <a name="in-this-section"></a>섹션 내용  
 다음 항목에서는 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 OLAP 및 데이터 마이닝 기능이 공유하는 개체에 대해 설명합니다.  
  
|항목|Description|  
|-----------|-----------------|  
|[다차원 모델의 데이터 원본](../../../analysis-services/multidimensional-models/data-sources-in-multidimensional-models.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 데이터 원본에 대해 설명합니다.|  
|[다차원 모델의 데이터 원본 뷰](../../../analysis-services/multidimensional-models/data-source-views-in-multidimensional-models.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]의 하나 이상의 데이터 원본을 기반으로 하는 논리 데이터 모델에 대해 설명합니다.|  
|[다차원 모델의 큐브](../../../analysis-services/multidimensional-models/cubes-in-multidimensional-models.md)|큐브에 대해 설명하고 측정값, 측정값 그룹, 차원 용도 관계, 계산, 핵심 성과 지표, 동작, 번역, 파티션, 큐브 뷰 등의 큐브 개체를 살펴봅니다.|  
|[차원 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)|차원에 대해 설명하고 특성, 특성 관계, 계층, 수준 및 멤버 등의 차원 개체를 살펴봅니다.|  
|[마이닝 구조 &#40; Analysis Services-데이터 마이닝 &#41;](../../../analysis-services/data-mining/mining-structures-analysis-services-data-mining.md)|마이닝 구조와 마이닝 모델을 포함하는 마이닝 개체에 대해 설명합니다.|  
|[보안 역할 &#40; Analysis Services-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/olap-logical/security-roles-analysis-services-multidimensional-data.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 개체에 대한 액세스를 제어하는 데 사용되는 보안 메커니즘인 역할에 대해 설명합니다.|  
|[다차원 모델 어셈블리 관리](../../../analysis-services/multidimensional-models/multidimensional-model-assemblies-management.md)|[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 MDX 및 DMX 언어를 확장하는 데 사용되는 사용자 정의 함수 모음인 어셈블리에 대해 설명합니다.|  
  
## <a name="see-also"></a>관련 항목:  
 [지원 되는 데이터 원본 &#40; SSAS-다차원 데이터 &#41;](../../../analysis-services/multidimensional-models/supported-data-sources-ssas-multidimensional.md)   
 [다차원 모델 솔루션 &#40; Ssas&#41;](../../../analysis-services/multidimensional-models/multidimensional-model-solutions-ssas.md)   
 [데이터 마이닝 솔루션](../../../analysis-services/data-mining/data-mining-solutions.md)  
  
  

