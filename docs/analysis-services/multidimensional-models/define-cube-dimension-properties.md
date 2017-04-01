---
title: "큐브 차원 속성 정의 | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "차원 [Analysis Services], 특성"
  - "속성 [Analysis Services], 차원"
ms.assetid: 9314e749-0918-4862-abaf-a21692188122
caps.latest.revision: 17
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 17
---
# 큐브 차원 속성 정의
  큐브 차원은 큐브 내의 데이터베이스 차원 인스턴스입니다. 데이터베이스 차원은 다중 큐브에서 사용할 수 있으며 다중 큐브 차원은 단일 데이터베이스 차원을 기반으로 할 수 있습니다. 다음 표에서는 큐브 차원의 속성을 설명합니다.  
  
|속성|Description|  
|--------------|-----------------|  
|**AllMemberAggregationUsage**| [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]의 집계 디자이너로 집계를 디자인하는 방식을 제어합니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **전체**: 큐브의 모든 집계가 All 멤버를 포함해야 합니다.<br /><br /> **없음**: 큐브의 어떤 집계도 All 멤버를 포함할 수 없습니다. 이 값은 기본값입니다.<br /><br /> **제한 없음**: 집계 디자이너에 제한 사항이 지정되지 않습니다.<br /><br /> **기본값**: 제한 없음과 같습니다.|  
|**Description**|수준에 대한 설명이 포함된 이름을 제공합니다.|  
|**DimensionID**|데이터베이스 차원의 고유 ID를 포함합니다.|  
|**HierarchyUniqueNameStyle**|큐브 차원에 포함된 계층에 고유한 이름을 생성하는 방식을 결정합니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **IncludeDimensionName**:<br />                    차원 이름이 계층 이름의 일부로 포함됩니다. 이 값은 기본값입니다.<br /><br /> **ExcludeDimensionName**:<br />                    차원 이름이 계층 이름의 일부로 포함되지 않습니다.|  
|**ID**|큐브 차원의 고유 ID를 포함합니다.|  
|**MemberUniqueNameStyle**|큐브 차원에 포함된 계층의 멤버에 고유한 이름을 생성하는 방식을 결정합니다. 이 속성 값은 다음 중 하나일 수 있습니다.<br /><br /> **Native**:<br />                      [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서 자동으로 멤버의 고유한 이름을 결정합니다. 이 값은 기본값입니다.<br /><br /> **NamePath**: [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]에서 각 수준의 이름과 멤버의 캡션으로 구성된 복합 이름을 생성합니다.|  
|**이름**|큐브 차원의 이름을 포함합니다. 기본적으로 큐브 차원의 이름은 동일한 이름의 다른 큐브 차원이 이미 정의되어 있지 않는 한 데이터베이스 차원의 이름과 같습니다.|  
|**Visible**|큐브 차원 표시 여부를 결정합니다. 기본값은 **True**입니다.|  
  
## 관련 항목:  
 [차원&#40;Analysis Services - 다차원 데이터&#41;](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/dimensions-analysis-services-multidimensional-data.md)  
  
  