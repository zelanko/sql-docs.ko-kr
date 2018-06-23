---
title: DisplayKey 요소 (CSDLBI) | Microsoft Docs
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
ms.assetid: 7d881278-1e77-42e1-8cfc-f1bbd9ec2340
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: 907bb04d59225180fad91b63971d578181c6663d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36092268"
---
# <a name="displaykey-element-csdlbi"></a>DisplayKey 요소(CSDLBI)
  DisplayKey 요소는 강력한 식별자를 구성하는 다음 요소 목록을 포함합니다. DisplayKey는 EntityType 요소의 자식으로만 사용됩니다. 이 요소는 열 또는 역할 END를 참조할 수 있습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표에서는 DisplayKey 요소의 특성을 보여 줍니다.  
  
|속성|필수 여부|Description|  
|----------|-----------------|-----------------|  
|IsDisplayKey|아니요|True 또는 False입니다.|  
  
## <a name="remarks"></a>Remarks  
 이 요소는 보고서용입니다. 이 특성을 적용할 요소는 실제 테이블 키일 필요가 없으며 키로 표시할 요소이기만 하면 됩니다. 하지만 DisplayKey에 사용하는 열에는 고유의 값이 포함되어야 합니다.  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예제에서는 CSDLBI 버전 1.1에서 테이블의 DisplayKey로 지정된 AdventureWorks 예제 데이터 모델의 열을 보여 줍니다.  
  
```  
<sample in progress>  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 예제는 CSDLBI 버전 1.1에서 Contoso Operations 큐브 표현의 발췌 구문을 보여 줍니다. 이 모델에서는 Color 열이 Bikes 테이블의 표시 키로 표시되었습니다.  
  
```  
  
<EntityType   
    Name="Bike">  
.. .. ..  
<Property   
    Name="Color"   
    Type="String"   
    MaxLength="Max"   
    Unicode="true"   
    FixedLength="false">  
<bi:Property   
    ContextualNameRule="Context"   
    Alignment="Left" Units="counts"   
    SortDirection="Descending"   
    IsRightToLeft="true"   
    DefaultAggregateFunction="Max" />  
</Property>  
.. .. ..  
<bi:EntityType>  
   <bi:DisplayKey>  
      <bi:MemberRef Name="Color" />  
   </bi:DisplayKey>>  
.. .. ..  
</bi:EntityType>  
</EntityType>  
```  
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 개체 모델 이해](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [CSDLBI 개념](../csdlbi-concepts.md)  
  
  