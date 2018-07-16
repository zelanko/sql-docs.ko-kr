---
title: Type 요소 (MiningStructureColumn) (ASSL) | Microsoft Docs
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
- Type Element (MiningStructureColumn)
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TYPE
helpviewer_keywords:
- Type element
ms.assetid: ce999716-9487-4348-bc42-270a2026a452
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 30ce9327fb28e9f452e643ded604f2a8dd72a084
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304243"
---
# <a name="type-element-miningstructurecolumn-assl"></a>Type 요소(MiningStructureColumn)(ASSL)
  형식을 포함 합니다 [MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<MiningStructureColumn>  
   ...  
   <Type>...</Type>  
   ...  
</MiningStructureColumn>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|InclusionThresholdSetting|  
|카디널리티|1-1: 한 번만 나타나는 필수 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[MiningStructureColumn](../data-type/miningstructurecolumn-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*Long*|부호 있는 64비트 정수입니다. 이 데이터 형식은 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] .NET Framework의 `Int64` 데이터 형식 및 OLE DB의 DBTYPE_I8 데이터 형식에 매핑됩니다.|  
|*Boolean*|부울 값입니다. 이 데이터 형식은 .NET Framework의 `Boolean` 데이터 형식 및 OLE DB의 DBTYPE_BOOL 데이터 형식에 매핑됩니다.|  
|*텍스트*|유니코드 문자의 Null로 끝나는 스트림입니다. 이 데이터 형식은 .NET Framework의 `String` 데이터 형식 및 OLE DB의 DBTYPE_WSTR 데이터 형식에 매핑됩니다.|  
|*Double*|-1.79E+308부터 1.79E+308 사이의 배정밀도 부동 소수점 숫자입니다. 이 데이터 형식은 .NET Framework의 `Double` 데이터 형식 및 OLE DB의 DBTYPE_R8 데이터 형식에 매핑됩니다.|  
|*날짜*|배정밀도 부동 소수점 숫자로 저장되는 날짜 데이터입니다. 정수 부분은 1899년 12월 30일 이후의 날짜 수이고, 소수 부분은 하루를 분수로 표시한 수입니다. 이 데이터 형식은 .NET Framework의 `DateTime` 데이터 형식 및 OLE DB의 DBTYPE_DATE 데이터 형식에 매핑됩니다.|  
|*테이블*|중첩 테이블입니다. 이 데이터 형식은 OLE DB의 DBTYPE_HCHAPTER 데이터 형식에 매핑됩니다. **참고:** .NET Framework의 테이블 열을 해당 기본 데이터 형식이 없지만 대신 지는 `DataReader` 클래스입니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `Type`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.MiningStructureColumnTypes>입니다.  
  
 부모에 해당 하는 요소가 `Type` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.MiningStructureColumn>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
