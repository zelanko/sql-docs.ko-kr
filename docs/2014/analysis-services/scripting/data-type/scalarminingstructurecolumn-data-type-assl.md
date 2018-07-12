---
title: ScalarMiningStructureColumn 데이터 형식 (ASSL) | Microsoft Docs
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
- ScalarMiningStructureColumn Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ScalarMiningStructureColumn
helpviewer_keywords:
- ScalarMiningStructureColumn data type
ms.assetid: 8f4afc15-601c-4189-bc45-f5a216aed879
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 90f855bf55292b310e32a167dc005ab2f2f81c14
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37211693"
---
# <a name="scalarminingstructurecolumn-data-type-assl"></a>ScalarMiningStructureColumn 데이터 형식(ASSL)
  나타내는 파생된 데이터 형식을 정의 [MiningStructureColumn](miningstructurecolumn-data-type-assl.md) 와 연결 된 중첩된 테이블과 달리 스칼라 값을 포함 하는 요소는 [TableMiningStructureColumn](tableminingstructurecolumn-data-type-assl.md) 요소 중첩된 테이블이 들어 있는입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ScalarMiningStructureColumn>  
   <!-- The following elements extend MiningStructureColumn -->  
   <IsKey>...</IsKey>  
   <Source>...</Source>  
   <Distribution>...</Distribution>  
   <ModelingFlags>...</ModelingFlags>  
   <Content>...</Content>  
   <ClassifiedColumnID>...</<ClassifiedColumnI  
   <DiscretizationMethod>...</DiscretizationMethod>  
   <DiscretizationBucketCount>...</DiscretizationBucketCount>  
   <KeyColumns>...</KeyColumns>  
   <NameColumn>...</NameColumn>  
   <Translations>...</Translations>  
</ScalarMiningStructureColumn>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[MiningStructureColumn](miningstructurecolumn-data-type-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[ClassifiedColumnID](../properties/id-element-assl.md), [콘텐츠](../properties/content-element-assl.md)를 [DiscretizationBucketCount](../properties/discretizationbucketcount-element-assl.md)를 [DiscretizationMethod](../properties/discretizationmethod-element-assl.md)를 [배포](../properties/distribution-element-assl.md), [IsKey](../properties/iskey-element-assl.md)를 [KeyColumns](../collections/columns-element-assl.md)를 [ModelingFlags](../collections/modelingflags-element-assl.md)를 [NameColumn](../objects/column-element-assl.md)를 [원본](../properties/source-element-binding-assl.md), [ 번역](../collections/translations-element-assl.md)|  
|파생 요소|[열](../objects/column-element-assl.md) ([열](../collections/columns-element-assl.md) 모음인 [MiningStructure](../objects/miningstructure-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ScalarMiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
