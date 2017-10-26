---
title: "RootMemberIf 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- RootMemberIf Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 9c312a638544071697a59bf1a7ddfb44ce9c5746
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="rootmemberif-element-assl"></a>RootMemberIf 요소(ASSL)
  부모 특성의 멤버 또는 루트 멤버를 식별하는 방법을 결정합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DimensionAttribute>  
   ...  
   <RootMemberIf>...</RootMemberIf>  
   ...  
</DimensionAttribute>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*ParentIsBlankSelfOrMissing*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../../../analysis-services/scripting/data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>주의  
 값은 **RootMemberIf** 요소 부모 특성에만 사용 됩니다 (의 값 즉,는 [사용량](../../../analysis-services/scripting/properties/usage-element-dimensionattribute-assl.md) 의 요소는 **DimensionAttribute** 부모 요소가 로 설정 *부모*) 부모-자식 계층의 루트 (최상위) 멤버를 확인 합니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|에 대 한 설명 하는 원인 중 하나 이상을 만족 하는 멤버만 *ParentIsBlank*, *ParentIsSelf*, 또는 *ParentIsMissing* 루트 멤버로 처리 됩니다.|  
|*ParentIsBlank*|Null, 0 또는 빈 문자열이 나타내는 키 열에 있는 멤버만 [KeyColumns](../../../analysis-services/scripting/collections/keycolumns-element-assl.md) 컬렉션 **DimensionAttribute** 루트 멤버로 처리 됩니다.|  
|*ParentIsSelf*|자신이 부모인 멤버만 루트 멤버로 처리됩니다.|  
|*ParentIsMissing*|부모를 찾을 수 없는 멤버만 루트 멤버로 처리됩니다.|  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **RootMemberIf** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.RootIfValue>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  

