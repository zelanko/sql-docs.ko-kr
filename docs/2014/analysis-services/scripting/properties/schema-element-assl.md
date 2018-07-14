---
title: Schema 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- Schema Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- Schema
helpviewer_keywords:
- Schema element
ms.assetid: 4b6375fb-7ad8-4d5f-88b1-abd3da2654db
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 3bcf275eafb8a982fa2ddf9d5ecb82d45e435fa5
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37200043"
---
# <a name="schema-element-assl"></a>Schema 요소(ASSL)
  데이터 원본 뷰의 스키마를 포함합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataSourceView>  
   ...  
   <Schema>...</Schema>  
   ...  
</DataSourceView>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|스키마|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataSourceView](../objects/datasourceview-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Schema`는 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework에서 데이터 집합 XSD(XML 스키마 정의) 언어 형식으로 표시됩니다. 여기에는 DDL(데이터 정의 언어)로 된 데이터 집합에 대한 일부 확장명 및 이러한 용도에만 사용되는 확장명이 포함됩니다. 데이터 집합은 XSD에서 관계형 스키마로의 유연한 매핑을 정의하지만 XSD를 정규 형식으로 반환합니다. 이 정규 형식은 데이터 원본에서만 유효합니다.  
  
 부모에 해당 하는 요소가 `Schema` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.DataSourceView>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
