---
title: PerspectiveHierarchy 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PerspectiveHierarchy Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PerspectiveHierarchy
helpviewer_keywords:
- PerspectiveHierarchy data type
ms.assetid: 30366bd0-ee1c-4940-8c1f-ca5e0dd5fe4b
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 4256390b88a7751116daf9a49b494293e6dceab3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48149283"
---
# <a name="perspectivehierarchy-data-type-assl"></a>PerspectiveHierarchy 데이터 형식(ASSL)
  계층에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [PerspectiveDimension](dimension-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PerspectiveHierarchy>  
   <HierarchyID>...</HierarchyID>  
      <Annotations>...</Annotations>  
</PerspectiveHierarchy>  
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
|자식 요소|[Annotations](../collections/annotations-element-assl.md), [HierarchyID](../properties/id-element-assl.md)|  
|파생 요소|[계층 구조](../objects/hierarchy-element-assl.md) ([계층](../collections/hierarchies-element-assl.md) 모음인 [PerspectiveDimension](dimension-data-type-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.PerspectiveHierarchy>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
