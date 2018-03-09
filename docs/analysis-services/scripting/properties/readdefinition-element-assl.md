---
title: "ReadDefinition 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
apiname: ReadDefinition Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: ReadDefinition
helpviewer_keywords: ReadDefinition element
ms.assetid: 1f250129-13b2-41b9-b083-b5aacddf0060
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: afa07f4452bb7815ae30f2be3e8cccab6319eb9e
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="readdefinition-element-assl"></a>ReadDefinition 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]멤버가 데이터베이스의 정의 또는 데이터베이스에서 개체의 정의 읽을 수 있는지 여부를 결정 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Permission> <!-- or one of the elements listed below in the Element Relationships table -->  
   ...  
   <ReadDefinition>...</ReadDefinition>  
   ...  
</Permission>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*없음*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[CubePermission](../../../analysis-services/scripting/objects/cubepermission-element-assl.md), [DatabasePermission](../../../analysis-services/scripting/objects/databasepermission-element-assl.md), [DimensionPermission](../../../analysis-services/scripting/objects/dimensionpermission-element-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [MiningStructurePermission ](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md), [사용 권한](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|개체 정의에 대한 액세스가 허용되지 않습니다.|  
|*기본*|개체 정의에 대한 기본 액세스가 허용됩니다.<br /><br /> 참고:이 권한은 로컬 큐브, 측정값 그룹을 연결 하 고, 차원을 연결 하는 데 필요한입니다.|  
|*허용*|개체 정의에 대한 모든 액세스 권한이 허용됩니다.<br /><br /> 참고:이 권한은 실행 하는 데 필요한는 [Discover](../../../analysis-services/xmla/xml-elements-methods-discover.md) XML for Analysis (XMLA) 호출 DISCOVER_XML_METADATA 매개 변수를 사용 합니다.|  
  
 부모에 해당 하는 요소 **ReadDefinition** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission>, 및 <xref:Microsoft.AnalysisServices.Permission>.  
  
## <a name="see-also"></a>관련 항목:  
 [Role 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
