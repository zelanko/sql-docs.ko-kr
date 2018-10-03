---
title: AllowDrillThrough 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- AllowDrillThrough Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- AllowDrillThrough
helpviewer_keywords:
- AllowDrillThrough element
ms.assetid: 53c9e4a3-a376-447d-a13f-80d845cc9789
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 79abc9833c111c472776d0713a0ca50888cae27d
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48090853"
---
# <a name="allowdrillthrough-element-assl"></a>AllowDrillThrough 요소(ASSL)
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|`False`|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningModel 요소](../objects/miningmodel-element-assl.md)하십시오 [MiningModelPermission](../objects/miningmodelpermission-element-assl.md), [MiningStructurePermission](../objects/miningstructurepermission-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 AMO(Analysis Management Objects) 개체 모델에서 `AllowDrillThrough`의 부모에 해당하는 요소는 <xref:Microsoft.AnalysisServices.MiningModel>, <xref:Microsoft.AnalysisServices.MiningModelPermission> 및 <xref:Microsoft.AnalysisServices.MiningStructurePermission>입니다.  
  
## <a name="drillthrough-on-mining-structures"></a>마이닝 구조에서의 드릴스루  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]에서는 마이닝 모델뿐만 아니라 마이닝 구조에 대한 `AllowDrillthrough` 권한을 정의할 수 있습니다. 이 권한을 역할에 할당하면 해당 역할의 모든 멤버가 데이터 마이닝 모델을 쿼리하고 모델에 포함되지 않은 구조 열을 반환할 수 있습니다. 예를 들어 고객 키, 고객 소득 및 고객 구매 내역 열만 사용하는 모델을 만들 수 있습니다. 모델에서 드릴스루를 설정하면 사용자가 고객 전자 메일 또는 이름과 같은 마이닝 구조의 다른 열로 정보를 반환할 수 있습니다.  
  
 따라서 중요한 데이터를 보호하려면 마이닝 구조에 열을 추가할 때 주의해야 합니다. 또한 구조에 대한 `AllowDrillthrough` 권한은 꼭 필요한 경우에만 부여하십시오.  
  
 구조 열로 드릴스루하려면 다음 형식 중 하나로 쿼리를 사용하십시오.  
  
 `SELECT * FROM <structure>.CASES`  
  
 로 구분하거나 여러  
  
 `SELECT StructureColumn('<structure-column-name>') FROM <model>.CASES`  
  
## <a name="see-also"></a>관련 항목  
 [역할 요소 &#40;ASSL&#41;](../objects/role-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
