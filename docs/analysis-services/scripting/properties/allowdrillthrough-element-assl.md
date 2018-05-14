---
title: AllowDrillThrough 요소 (ASSL) | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: assl
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 25bad363975494fc8bd6c8cb343a165d8bb85f85
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="allowdrillthrough-element-assl"></a>AllowDrillThrough 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  부모 요소에서 드릴스루가 허용되는지 여부를 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModel> <!-- or MiningModelPermission -->  
<!-- or MiningStructurePermission -->   ...  
   <AllowDrillThrough>...</AllowDrillThrough>  
   ...  
</MiningModel>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|**False**|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModel 요소](../../../analysis-services/scripting/objects/miningmodel-element-assl.md), [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../../../analysis-services/scripting/objects/miningstructurepermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 부모에 해당 하는 요소 **AllowDrillThrough** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningModelPermission>, 및 <xref:Microsoft.AnalysisServices.MiningStructurePermission>합니다.  
  
## <a name="drillthrough-on-mining-structures"></a>마이닝 구조에서의 드릴스루  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]를 정의할 수 있습니다 **AllowDrillthrough** 마이닝 구조와 마이닝 모델에 대 한 권한. 이 권한을 역할에 할당하면 해당 역할의 모든 멤버가 데이터 마이닝 모델을 쿼리하고 모델에 포함되지 않은 구조 열을 반환할 수 있습니다. 예를 들어 고객 키, 고객 소득 및 고객 구매 내역 열만 사용하는 모델을 만들 수 있습니다. 모델에서 드릴스루를 설정하면 사용자가 고객 전자 메일 또는 이름과 같은 마이닝 구조의 다른 열로 정보를 반환할 수 있습니다.  
  
 따라서 중요한 데이터를 보호하려면 마이닝 구조에 열을 추가할 때 주의해야 합니다. 또한 구조에 대한 **AllowDrillthrough** 권한은 꼭 필요한 경우에만 부여하십시오.  
  
 구조 열로 드릴스루하려면 다음 형식 중 하나로 쿼리를 사용하십시오.  
  
 `SELECT * FROM <structure>.CASES`  
  
 또는  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>관련 항목:  
 [Role 요소 & #40; ASSL & #41;](../../../analysis-services/scripting/objects/role-element-assl.md)   
 [속성 & #40; ASSL & #41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
