---
title: DrillThroughAction 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- DrillThroughAction Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- DrillThroughAction
helpviewer_keywords:
- DrillThroughAction data type
ms.assetid: e212d575-a0d7-4548-92b4-33542ef59034
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: e6a1ccdedbcb1b70e9673afe687a62f95065c3aa
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48219393"
---
# <a name="drillthroughaction-data-type-assl"></a>DrillThroughAction 데이터 형식(ASSL)
  드릴스루 동작을 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DrillThroughAction>  
   <!-- The following elements extend Action -->  
   <Default>...</Default>  
   <Columns>...</Columns>  
</DrillThroughAction>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[동작](action-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[열](../collections/columns-element-assl.md), [기본](../properties/default-element-assl.md)|  
|파생 요소|[동작](../objects/action-element-assl.md) ([동작](../collections/actions-element-assl.md), 컬렉션 [큐브](../objects/cube-element-assl.md), 또는 [관점](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.DrillThroughAction>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
