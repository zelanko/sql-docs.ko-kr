---
title: PartitionBinding 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- PartitionBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- PartitionBinding
helpviewer_keywords:
- PartitionBinding data type
ms.assetid: 859d4b47-31c7-4678-9388-254fec484299
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bc5053c872b804740f121a9b8712eb3569a95444
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48227935"
---
# <a name="partitionbinding-data-type-assl"></a>PartitionBinding 데이터 형식(ASSL)
  에 대 한 바인딩을 나타내는 파생된 데이터 형식을 정의 [파티션](../objects/partition-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PartitionBinding>  
   <DatabaseID>...</DatabaseID>  
   <CubeID>...</CubeID>  
   <PartitionID>...</PartitionID>  
   <Source>...</Source>  
</PartitionBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[바인딩](binding-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[CubeID](../../xmla/xml-elements-properties/id-element-xmla.md)하십시오 [DatabaseID](../../xmla/xml-elements-properties/databaseid-element-xmla.md)를 [PartitionID](../../xmla/xml-elements-properties/partitionid-element-xmla.md), [원본](../properties/source-element-binding-assl.md)|  
|파생 요소|참조 [바인딩](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 추가 정보에 대 한는 `Binding` 형식, Analysis Services Scripting Language (ASSL) 개체 테이블을 비롯 한는 `Binding` 형식과 상속 계층 `Binding` 참조 하십시오 [바인딩 데이터 형식 &#40;ASSL&#41;](binding-data-type-assl.md)합니다.  
  
 ASSL의 데이터 바인딩 개요를 보려면 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
