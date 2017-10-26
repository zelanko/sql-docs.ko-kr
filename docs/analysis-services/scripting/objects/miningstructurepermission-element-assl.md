---
title: "MiningStructurePermission 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- MiningStructurePermission Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningStructurePermission
helpviewer_keywords:
- MiningStructurePermission element
ms.assetid: 4ba2bfd2-9003-4eed-8049-a74d452894ea
caps.latest.revision: 43
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 22713569509019e9d0aac30f82c898c73a034fda
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="miningstructurepermission-element-assl"></a>MiningStructurePermission 요소(ASSL)
  사용 권한을 해당 멤버의 정의 [역할](../../../analysis-services/scripting/objects/role-element-assl.md) 요소 가지는 개별 [MiningStructure](../../../analysis-services/scripting/objects/miningstructure-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructurePermissions>  
   <MiningStructurePermission xsi:type="Permission">  
      <AllowDrillthrough>...</AllowDrillthrough>  
  
      <!-- This element also inherits all the child elements listed in Permission -->  
   </MiningStructurePermission>  
</MiningStructurePermissions>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|[사용 권한](../../../analysis-services/scripting/data-type/permission-data-type-assl.md)|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MiningStructurePermission>합니다.  
  
 [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)], 권한을 **AllowDrillthrough** 마이닝 구조에 적용 되도록 확장 되었습니다. 이 권한을 역할에 할당하면 해당 역할의 멤버인 모든 사용자가 다음 구문을 사용하여 마이닝 구조를 직접 쿼리할 수 있습니다.  
  
```  
SELECT <structure column list> FROM <structure>.CASES  
```  
  
 또한 마이닝 구조와 마이닝 모델 모두에 **AllowDrillthrough** 가 설정된 경우 사용자는 다음 구문을 사용하여 마이닝 모델에 포함되지 않은 구조 열을 쿼리할 수 있습니다.  
  
```  
SELECT StructureColumn('<structure column name>' FROM <model>.CASES  
```  
  
 예를 들어 고객 키, 고객 소득 및 고객 구매 내역 열만 사용하는 모델을 만들 수 있습니다. 드릴스루를 사용할 경우 사용자는 고객 연락 정보와 같이 마이닝 모델에 포함되지 않은 다른 구조 열을 반환할 수 있습니다.  
  
 따라서 중요한 데이터나 개인 정보를 보호하려면 개인 정보를 마스킹하도록 데이터 원본 뷰를 생성하고 필요한 경우에만 구조에 대한 **AllowDrillthrough** 권한을 부여해야 합니다.  
  
 자세한 내용은 [드릴스루 쿼리&#40;데이터 마이닝&#41;](../../../analysis-services/data-mining/drillthrough-queries-data-mining.md)를 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 <xref:Microsoft.AnalysisServices.MiningModel.AllowDrillThrough%2A>   
 <xref:Microsoft.AnalysisServices.AdomdClient.MiningModel.AllowDrillThrough%2A>   
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)  
  
  

