---
title: Hierarchy 데이터 형식 (ASSL) | Microsoft Docs
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
- Hierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
helpviewer_keywords:
- Hierarchy data type
ms.assetid: 2e05917e-7e5d-4dd1-817b-4ff5647747ff
caps.latest.revision: 17
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: b20bed156e97c33a1c9f9df02677ef403767e472
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37230013"
---
# <a name="hierarchy-data-type-assl"></a>Hierarchy 데이터 형식(ASSL)
  차원의 계층을 나타내는 기본 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Hierarchy>  
   <Name>...</Name>  
   <ID>...</ID>  
   <Description>...</Description>  
   <DisplayFolder>...</DisplayFolder>  
   <Translations>...</Translations>  
   <AllMemberName>...</AllMemberName>  
   <AllMemberTranslations>...</AllMemberTranslation>  
   <MemberNamesUnique>...</MemberNamesUnique>  
   <AllowDuplicateNames>...</AllowDuplicateNames>  
   <Levels>...</Levels>  
   <Annotations>...</Annotation>  
</Hierarchy>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[AllMemberName](../properties/name-element-assl.md), [AllMemberTranslations](../collections/translations-element-assl.md), [AllowDuplicateNames](../properties/allowduplicatenames-element-assl.md), [Annotations](../collections/annotations-element-assl.md), [Description](../properties/description-element-assl.md), [DisplayFolder](../properties/displayfolder-element-assl.md), [ID](../properties/id-element-assl.md), [Levels](../collections/levels-element-assl.md), [MemberNamesUnique](../properties/membernamesunique-element-assl.md), [Name](../properties/name-element-assl.md), [Translations](../collections/translations-element-assl.md)|  
|파생 요소|[Hierarchy](../objects/hierarchy-element-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 *MemberNamesUnique* 요소는 DevelopmentMode 1 또는 2(각각 SharePoint 또는 테이블 형식 서버 모드용)에서 지원되지 않습니다.  
  
 *MemberKeysUnique* 요소는 DevelopmentMode 1 또는 2(각각 SharePoint 또는 테이블 형식 서버 모드용)에서 지원되지 않습니다.  
  
 *AllowDuplicateNames* 요소는 DevelopmentMode 1 또는 2(각각 SharePoint 또는 테이블 형식 서버 모드용)에서 지원되지 않습니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.Hierarchy>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
