---
title: "MiningStructure 요소 (ASSL) | Microsoft Docs"
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
- MiningStructure Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- MiningStructure
helpviewer_keywords:
- MiningStructure element
ms.assetid: b943cd92-0ed8-4bd8-8fbc-7dab0534aede
caps.latest.revision: 48
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 0f0ce9ca930e54c1cf8ac989330e00f298a06a28
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

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
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-n: 두 번 이상 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructures](../../../analysis-services/scripting/collections/miningstructures-element-assl.md)|  
|자식 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [CacheMode](../../../analysis-services/scripting/properties/cachemode-element-assl.md), [데이터 정렬](../../../analysis-services/scripting/properties/collation-element-assl.md), [열](../../../analysis-services/scripting/collections/columns-element-assl.md), [CreatedTimestamp](../../../analysis-services/scripting/properties/createdtimestamp-element-assl.md), [ 설명](../../../analysis-services/scripting/properties/description-element-assl.md), [ErrorConfiguration](../../../analysis-services/scripting/objects/errorconfiguration-element-assl.md),<br /><br /> [HoldoutActualSize](../../../analysis-services/scripting/properties/holdoutactualsize-element.md),<br /><br /> [HoldoutMaxCases](../../../analysis-services/scripting/properties/holdoutmaxcases-element.md),<br /><br /> [HoldoutMaxPercent](../../../analysis-services/scripting/properties/holdoutmaxpercent-element.md),<br /><br /> [HoldoutSeed](../../../analysis-services/scripting/properties/holdoutseed-element.md),<br /><br /> [ID](../../../analysis-services/scripting/properties/id-element-assl.md), [언어](../../../analysis-services/scripting/properties/language-element-assl.md), [LastProcessed](../../../analysis-services/scripting/properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../../../analysis-services/scripting/properties/lastschemaupdate-element-assl.md), [MiningModels](../../../analysis-services/scripting/collections/miningmodels-element-assl.md), [ MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md), [이름](../../../analysis-services/scripting/properties/name-element-assl.md), [소스](../../../analysis-services/scripting/properties/source-element-binding-assl.md), [상태](../../../analysis-services/scripting/properties/state-element-assl.md), [번역](../../../analysis-services/scripting/collections/translations-element-assl.md)|  
  
## <a name="remarks"></a>주의  
 마이닝 구조는 열과 바인딩을 정의합니다. 마이닝 구조를 정의한 후에는 이 구조를 사용하여 다양한 마이닝 모델을 정의할 수 있습니다. 마이닝 구조와 마이닝 구조에 포함된 각 마이닝 모델은 독립적으로 처리될 수 있습니다.  
  
> [!NOTE]  
>  홀드 아웃 속성을 **HoldoutMaxCases**, **HoldoutMaxPercent**, **HoldoutSeed**, 및 **HoldoutActualSize**에 도입 된 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]. 이러한 속성을 사용하면 구조와 연결된 모든 마이닝 모델의 테스트 집합 역할을 하는 마이닝 구조에 파티션을 정의할 수 있습니다. [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)]에서는 이러한 속성을 지원하지 않습니다. 따라서 [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] 인스턴스에서 이러한 속성을 사용하려고 하면 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]에서 오류를 반환합니다.  
  
## <a name="drillthrough-to-structure-columns"></a>구조 열로 드릴스루  
 [!INCLUDE[ssKatmai](../../../includes/sskatmai-md.md)]에 추가 된 새 권한 요소가 [MiningStructurePermissions 요소 &#40; ASSL &#41; ](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) 컬렉션입니다. 추가 하는 경우 **AllowDrillthrough** 둘 다를 수 있는 권한이 [MiningStructurePermissions](../../../analysis-services/scripting/collections/miningstructurepermissions-element-assl.md) 및 [MiningModelPermission](../../../analysis-services/scripting/objects/miningmodelpermission-element-assl.md) 컬렉션, 드릴스루를 사용할 수에서 권한이 있는 역할의 멤버는 방식으로 구조에 마이닝 모델 **AllowDrillthrough** 모델에 대 한 데이터 마이닝 모델을 쿼리를 업데이트 하 고 모델에 포함 되지 않은 구조 열을 반환할 수 있습니다.  
  
 따라서 중요 한 데이터 나 개인 정보를 보호 하려면 구성 해야 권한을 부여 하 고 중요 한 정보를 마스킹 하도록 데이터 원본 뷰 **AllowDrillthrough** 필요한 경우에 마이닝 구조에 대 한 권한이 있습니다. 자세한 내용은 참조 [AllowDrillThrough 요소 &#40; ASSL &#41; ](../../../analysis-services/scripting/properties/allowdrillthrough-element-assl.md).  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MiningStructure>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [MiningModel 요소 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/miningmodel-element-assl.md)   
 [개체 &#40; ASSL &#41;](../../../analysis-services/scripting/objects/objects-assl.md)   
 [SELECT&#40; DMX &#41;](../../../dmx/select-dmx.md)  
  
  
