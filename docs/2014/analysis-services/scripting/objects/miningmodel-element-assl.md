---
title: MiningModel 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModel Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModel
helpviewer_keywords:
- MiningModel element
ms.assetid: a61d935f-c8f6-457d-ad0c-44f58bb286f5
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7b6661d5718e36913fd9f706bd1912912e0b17fd
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48221363"
---
# <a name="miningmodel-element-assl"></a>MiningModel 요소(ASSL)
  단일 데이터 마이닝 모델을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModels>  
      <MiningModel>  
      <Name>...</Name>  
            <ID>...</ID>  
      <Description>...</<Descrip  
            <Algorithm>...</Algorithm>  
      <CreatedTimestamp>...</CreatedTimestamp>  
      <LastSchemaUpdate>...</LastSchemaUpdate>  
      <LastProcessed>...</LastProcessed>  
      <AlgorithmParameters>...</AlgorithmParameters>  
      <AllowDrillThrough>...</AllowDrillThrough>  
      <Translations>...</Translations>  
      <Columns>...</Columns>  
      <State>...</State>  
      <MiningModelPermissions>...</MiningModelPermissions>  
      <Language>...</Language>  
            <Collation>...</Collation>  
            <Annotations>...</Annotations>  
            <ddl100_100:FoldingParameters>   </FoldingParameters>  
   </MiningModel>  
</MiningModels>  
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
|부모 요소|[MiningModels](../collections/miningmodels-element-assl.md)|  
|자식 요소|[알고리즘](../properties/algorithm-element-assl.md), [AlgorithmParameters](algorithmparameter-element-assl.md)를 [AllowDrillThrough](../properties/allowdrillthrough-element-assl.md)를 [주석](../collections/annotations-element-assl.md)를 [데이터 정렬을](../properties/collation-element-assl.md), [ 열](../collections/columns-element-assl.md), [CreatedTimestamp](../properties/createdtimestamp-element-assl.md)를 [설명](../properties/description-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [언어](../properties/language-element-assl.md), [ LastProcessed](../properties/lastprocessed-element-assl.md), [LastSchemaUpdate](../properties/lastschemaupdate-element-assl.md)를 [MiningModelPermissions](../collections/miningmodelpermissions-element-assl.md)를 [이름](../properties/name-element-assl.md)를 [상태](../properties/state-element-assl.md), [ 번역](../collections/translations-element-assl.md),<br /><br /> [FoldingParameters](../properties/foldingparameters-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 마이닝 모델의 `FoldingParameters` 요소는 서버 내부에서 사용하기 위한 것이며 DDL 문에서 사용할 수 없습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MiningModel>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [개체 &#40;ASSL&#41;](objects-assl.md)  
  
  
