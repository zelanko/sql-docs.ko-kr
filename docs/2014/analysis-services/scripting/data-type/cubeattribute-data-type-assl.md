---
title: CubeAttribute 데이터 형식 (ASSL) | Microsoft Docs
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
- CubeAttribute Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- CubeAttribute
helpviewer_keywords:
- CubeAttribute data type
ms.assetid: 114ffb44-460b-4971-b31b-dd844e960b81
caps.latest.revision: 44
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b1df72c234fe7835d739e2b1835b01041aa9cbe6
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37319353"
---
# <a name="cubeattribute-data-type-assl"></a>CubeAttribute 데이터 형식(ASSL)
  연결 된 특성을 나타내는 기본 데이터 형식을 정의 [큐브](../objects/cube-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<CubeAttribute>  
   <AttributeID>...</AttributeID>  
   <AggregationUsage>...</AggregationUsage>  
   <AttributeHierarchyOptimizedState>...</AttributeHierarchyOptimizedState>  
   <AttributeHierarchyEnabled>...</AttributeHierarchyEnabled>  
   <AttributeHierarchyVisible>...</AttributeHierarchyVisible>  
   <Annotations>...</Annotations>  
</CubeAttribute>  
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
|자식 요소|[AggregationUsage](../properties/aggregationusage-element-assl.md), [주석](../collections/annotations-element-assl.md), [AttributeHierarchyEnabled](../properties/enabled-element-assl.md)하십시오 [AttributeHierarchyOptimizedState](../properties/state-element-assl.md), [ AttributeHierarchyVisible](../properties/visible-element-assl.md), [AttributeID](../properties/id-element-assl.md)|  
|파생 요소|[특성](../objects/attribute-element-assl.md) ([특성](../collections/attributes-element-assl.md) 모음인 [CubeDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 DeploymentMode 구성 속성 값이 1 또는 2(PowerPivot 및 테이블 형식 모델 데이터베이스를 실행하는 데 사용되는 SharePoint 또는 테이블 형식 모드)로 설정된 상태에서 서비스를 실행하는 경우 *AttributeHierarchyOptimizedState* 요소가 지원되지 않습니다.  
  
 *AtttributeHierarchyEnabled*속성이 FALSE로 설정되고 인스턴스가 DeploymentMode 1 또는 2(SharePoint 또는 테이블 형식 서버 모드)에서 실행되는 경우 특성을 계층 구조 수준으로 추가할 수 없습니다.  
  
 특성을 [CubeDimension](dimension-data-type-assl.md) 에서 명시적으로 포함 되지 않은 요소를 [특성](../collections/attributes-element-assl.md) 될 컬렉션에 할당 된 기본값을 사용 하 여 컬렉션에 포함 합니다. 특성 컬렉션에 추가 되는 특성으로 반환 될 수 있습니다 합니다 [Discover](../../xmla/xml-elements-methods-discover.md) 메서드.  
  
 [AggregationUsage](../properties/aggregationusage-element-assl.md) 요소 제어 하는 방법 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] 자동으로 특성에 대 한 집계를 디자인 합니다. `AggregationUsage` 요소는 큐브에 대해 수동으로 생성되는 집계를 제한하지 않습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.CubeAttribute>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
