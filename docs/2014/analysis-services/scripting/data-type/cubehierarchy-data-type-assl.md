---
title: CubeHierarchy 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- CubeHierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeHierarchy
helpviewer_keywords:
- CubeHierarchy data type
ms.assetid: cd633409-0c14-4dd9-97cc-3d30e25df24f
caps.latest.revision: 44
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 48176b4096b7fa7ba8e1847750410be0f65da552
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172045"
---
# <a name="cubehierarchy-data-type-assl"></a>CubeHierarchy 데이터 형식(ASSL)
  에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [계층](../objects/hierarchy-element-assl.md) 요소에는 [큐브](../objects/cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```  
<CubeHierarchy>   <HierarchyID>...</HierarchyID>   <Name>...</Name>   <OptimizedState>...</OptimizedState>   <Visible>...</Visible>   <Enabled>...</Enabled>   <Annotations>...</Annotations></CubeHierarchy>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[주석](../collections/annotations-element-assl.md), [활성화](../properties/enabled-element-assl.md), [HierarchyID](../properties/id-element-assl.md), [이름](../properties/name-element-assl.md), [OptimizedState](../properties/state-element-assl.md), [표시](../properties/visible-element-assl.md)|  
|파생 요소|[계층 구조](../objects/hierarchy-element-assl.md) ([계층](../collections/hierarchies-element-assl.md) 컬렉션 [CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 이 데이터 형식에는 제한이 없으므로 다음과 같은 모든 배포 모드에서 사용할 수 있습니다. 0-다차원 및 데이터 마이닝, 1-SharePoint 및 2-테이블 형식.  
  
 [!INCLUDE[ssASCurrent](../../../includes/ssascurrent-md.md)], *Enabled* 속성 설정할 수 없습니다 `False` 에 대 한 *CubeHierarchy*합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CubeHierarchy>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Discover 메서드 &#40;XMLA&#41;](../../xmla/xml-elements-methods-discover.md)   
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  