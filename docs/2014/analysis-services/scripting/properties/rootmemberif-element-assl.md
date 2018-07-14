---
title: RootMemberIf 요소 (ASSL) | Microsoft Docs
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
- RootMemberIf Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- RootMemberIf
helpviewer_keywords:
- RootMemberIf element
ms.assetid: b695e271-c748-4abc-a09f-acb1014f768f
caps.latest.revision: 34
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: a7ac45d2111b8d3631160ce78f131f98d53230e7
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37280299"
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
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*ParentIsBlankSelfOrMissing*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DimensionAttribute](../data-type/dimensionattribute-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 값을 `RootMemberIf` 요소는 부모 특성에만 사용 됩니다 (값 즉,는 [사용](usage-element-dimensionattribute-assl.md) 요소의 `DimensionAttribute` 부모 요소가로 설정 되어 *부모*) 루트 (결정할 부모-자식 계층의 최상위) 멤버입니다.  
  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*ParentIsBlankSelfOrMissing*|에 대해 설명 된 조건 중 하나 이상을 만족 하는 멤버만 *ParentIsBlank*하십시오 *ParentIsSelf*, 또는 *ParentIsMissing* 루트 멤버로 처리 됩니다.|  
|*ParentIsBlank*|Null, 0 또는 표시 되는 키 열에서 빈 문자열을 사용 하 여 구성원만 합니다 [KeyColumns](../collections/columns-element-assl.md) 컬렉션인 `DimensionAttribute` 루트 멤버로 처리 됩니다.|  
|*ParentIsSelf*|자신이 부모인 멤버만 루트 멤버로 처리됩니다.|  
|*ParentIsMissing*|부모를 찾을 수 없는 멤버만 루트 멤버로 처리됩니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `RootMemberIf`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.RootIfValue>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
