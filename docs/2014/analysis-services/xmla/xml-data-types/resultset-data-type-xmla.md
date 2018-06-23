---
title: Resultset 데이터 형식 (XMLA) | Microsoft Docs
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
- Resultset Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- http://schemas.microsoft.com/analysisservices/2003/engine#Resultset
- urn:schemas-microsoft-com:xml-analysis#Resultset
- Resultset
helpviewer_keywords:
- Resultset data type
ms.assetid: 45e7d7d6-1f89-4dc8-b39d-9270ea2db541
caps.latest.revision: 30
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: d8a571012c82c9e4d26d9f586cf67344f19258a6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36079850"
---
# <a name="resultset-data-type-xmla"></a>Resultset 데이터 형식(XMLA)
  반환 된 데이터를 나타내는 추상 기본 데이터 형식을 정의 [Discover](../xml-elements-methods-discover.md) 또는 [Execute](../xml-elements-methods-execute.md) 메서드를 호출 합니다.  
  
 **네임스페이스** urn:schemas-microsoft-com:xml-analysis:resultset  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Resultset>  
   <Exception>...</Exception>  
   <Messages>...</Messages>  
</Resultset>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|InclusionThresholdSetting|  
|파생 데이터 형식|[MDDataSet](mddataset-data-type-xmla.md), [olapxmla_EmptyResult](emptyresult-data-type-xmla.md), [행 집합](rowset-data-type-xmla.md)|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[예외](../xml-elements-properties/exception-element-xmla.md), [메시지](../xml-elements-properties/messages-element-xmla.md)|  
|파생 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `Resultset` 데이터 형식은 반환되는 정보의 유형에 따라 스키마와 데이터를 모두 포함할 수 있는 자체 설명적인 XML 결과 집합입니다.  
  
## <a name="see-also"></a>관련 항목  
 [XML 데이터 형식 &#40;XMLA&#41;](xml-data-types-xmla.md)  
  
  