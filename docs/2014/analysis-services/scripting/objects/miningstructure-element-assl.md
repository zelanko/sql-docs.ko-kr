---
title: MiningStructure 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningStructure Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3d03e52ccb38dc35fada602b6a293d018150efd5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48052093"
---
# <a name="miningstructure-element-assl"></a>MiningStructure 요소(ASSL)
  마이닝 모델 집합에 대한 구조를 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructures>  
   <MiningStructure>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <Source>...</Source>  
      <CreatedTimestamp>...</<CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <Translations>...</Translations>  
      <Language>...</Language>  
            <Collation>...</Collation>  
      <ErrorConfiguration>...</ErrorConfiguration>  
      <CacheMode>...</CacheMode>  
            <Columns>...</Columns>  
      <State>...</State>  
      <HoldoutActualSize>...</HoldoutActualSize>  
      <HoldoutMaxCases>...</HoldoutMaxCases>  
      <HoldoutMaxPercent>...</HoldoutMaxPercent>  
      <HoldoutSeed>...</HoldoutSeed>        
            <MiningStructurePermissions>...</<MiningStructurePermissions>  
            <MiningModels>...</MiningModels>  
            <Annotations>...</Annotations>  
   </MiningStructure>  
</MiningStructures>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructures](../collections/miningstructures-element-assl.md)|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [CacheMode](../properties/cachemode-element-assl.md)를 [데이터 정렬을](../properties/collation-element-assl.md)를 [열](../collections/columns-element-assl.md)를 [CreatedTimestamp](../properties/createdtimestamp-element-assl.md), [설명 ](../properties/description-element-assl.md)하십시오 [ErrorConfiguration](errorconfiguration-element-assl.md),<br /><br /> [HoldoutActualSize](../properties/holdoutactualsize-element.md),<br /><br /> [HoldoutMaxCases](../properties/holdoutmaxcases-element.md),<br /><br /> [HoldoutMaxPercent](../properties/holdoutmaxpercent-element.md),<br /><br /> [HoldoutSeed](../properties/holdoutseed-element.md),<br /><br /> [ID](../properties/id-element-assl.md), [언어](../properties/language-element-assl.md)합니다 [LastProcessed](../properties/lastprocessed-element-assl.md)를 [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)를 [MiningModels](../collections/miningmodels-element-assl.md), [ MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md), [이름](../properties/name-element-assl.md)합니다 [소스](../properties/source-element-binding-assl.md)를 [상태](../properties/state-element-assl.md), [번역](../collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 마이닝 구조는 열과 바인딩을 정의합니다. 마이닝 구조를 정의한 후에는 이 구조를 사용하여 다양한 마이닝 모델을 정의할 수 있습니다. 마이닝 구조와 마이닝 구조에 포함된 각 마이닝 모델은 독립적으로 처리될 수 있습니다.  
  
> [!NOTE]  
>  홀드아웃 속성 `HoldoutMaxCases`, `HoldoutMaxPercent`, `HoldoutSeed` 및 `HoldoutActualSize`는 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에서 도입되었습니다. 이러한 속성을 사용하면 구조와 연결된 모든 마이닝 모델의 테스트 집합 역할을 하는 마이닝 구조에 파티션을 정의할 수 있습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서는 이러한 속성을 지원하지 않습니다. 따라서 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 인스턴스에서 이러한 속성을 사용하려고 하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
## <a name="drillthrough-to-structure-columns"></a>구조 열로 드릴스루  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에 추가 된 새 권한 요소를 [MiningStructurePermissions 요소 &#40;ASSL&#41; ](../collections/miningstructurepermissions-element-assl.md) 컬렉션입니다. 추가 하는 경우 `AllowDrillthrough` 권한이 둘 다에 [MiningStructurePermissions](../collections/miningstructurepermissions-element-assl.md) 하 고 [MiningModelPermission](miningmodelpermission-element-assl.md) 방식으로 구조에 마이닝 모델에서 컬렉션에 드릴스루를 활성화 권한이 있는 역할의 멤버가 `AllowDrillthrough` 모델에 대 한 권한을 데이터 마이닝 모델을 쿼리하고 모델에 포함 되지 않은 구조 열을 반환할 수 있습니다.  
  
 따라서 중요한 데이터나 개인 정보를 보호하려면 중요한 정보를 마스킹하도록 데이터 원본 뷰를 생성하고 필요한 경우에만 마이닝 구조에 대한 `AllowDrillthrough` 권한을 부여해야 합니다. 자세한 내용은 [AllowDrillThrough 요소 &#40;ASSL&#41;](../properties/allowdrillthrough-element-assl.md)합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [MiningModel 요소 &#40;ASSL&#41;](miningmodel-element-assl.md)   
 [개체 &#40;ASSL&#41;](objects-assl.md)   
 [선택 &AMP;#40;DMX&AMP;#41;](/sql/dmx/select-dmx)  
  
  
