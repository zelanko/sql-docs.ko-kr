---
title: MiningModelColumn 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- MiningModelColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- MiningModelColumn
helpviewer_keywords:
- MiningModelColumn data type
ms.assetid: de8bf815-43b4-4983-bdb9-b67e8563be0e
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b35f260ca14ff416ce5d931457ec741c0736d692
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079463"
---
# <a name="miningmodelcolumn-data-type-assl"></a>MiningModelColumn 데이터 형식(ASSL)
  열에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [MiningModel](../objects/miningmodel-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningModelColumn>  
      <Name>...</Name>  
      <ID>...</ID>  
      <Description>...</<Description>  
      <SourceColumnID>...</SourceColumnID>  
            <Usage>...</Usage>  
            <Translations>...</Translations>  
      <Columns>...</Columns>  
      <ModelingFlags>...</ModelingFlags>  
      <Annotations>...</Annotations>  
</MiningModelColumn>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[주석을](../collections/annotations-element-assl.md), [열](../collections/columns-element-assl.md)를 [설명](../properties/description-element-assl.md)를 [ID](../properties/id-element-assl.md)를 [ModelingFlags](../collections/modelingflags-element-assl.md)를 [이름](../properties/name-element-assl.md) 를 [SourceColumnID](../properties/sourcecolumnid-element-assl.md)하십시오 [번역](../collections/translations-element-assl.md), [사용](../properties/usage-element-dimensionattribute-assl.md)|  
|파생 요소|[열](../objects/column-element-assl.md) ([열](../collections/columns-element-assl.md), 컬렉션 [MiningModel](../objects/miningmodel-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.MiningModelColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
