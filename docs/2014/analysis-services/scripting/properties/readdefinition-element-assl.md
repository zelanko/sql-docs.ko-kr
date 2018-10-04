---
title: ReadDefinition 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- ReadDefinition Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReadDefinition
helpviewer_keywords:
- ReadDefinition element
ms.assetid: 1f250129-13b2-41b9-b083-b5aacddf0060
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 176f1fa1f1a9f4fca3e773d65a5fda01c2f6752d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48218113"
---
# <a name="readdefinition-element-assl"></a>ReadDefinition 요소(ASSL)
  멤버가 데이터베이스의 정의 또는 데이터베이스의 개체 정의를 읽을 수 있는지 여부를 결정합니다.  
  
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
|부모 요소|[CubePermission](../objects/cubepermission-element-assl.md), [DatabasePermission](../objects/databasepermission-element-assl.md)를 [DimensionPermission](../objects/dimensionpermission-element-assl.md)하십시오 [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission ](../objects/miningstructurepermission-element-assl.md), [권한](../data-type/permission-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*없음*|개체 정의에 대한 액세스가 허용되지 않습니다.|  
|*기본*|개체 정의에 대한 기본 액세스가 허용됩니다. **참고:** 만드는 로컬 큐브, 측정값 그룹을 연결 하 고, 차원을 연결에이 권한이 필요 합니다.|  
|*허용*|개체 정의에 대한 모든 액세스 권한이 허용됩니다. **참고:** 실행에이 권한이 필요를 [Discover](../../xmla/xml-elements-methods-discover.md) XML for Analysis (XMLA) 호출 DISCOVER_XML_METADATA 매개 변수를 사용 합니다.|  
  
 AMO(Analysis Management Object) 개체 모델에서 `ReadDefinition`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.CubePermission>, <xref:Microsoft.AnalysisServices.DatabasePermission>, <xref:Microsoft.AnalysisServices.DimensionPermission>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, <xref:Microsoft.AnalysisServices.MiningStructurePermission> 및 <xref:Microsoft.AnalysisServices.Permission>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [역할 요소 &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
