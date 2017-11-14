---
title: "MemberRef 요소 (CSDLBI) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: tabular-models
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
caps.latest.revision: 5
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 3ca4fcb2b59e2a99153ccd55fce93be47a58d961
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="memberref-element-csdlbi"></a>MemberRef 요소(CSDLBI)
  MemberRef 요소는 참조 대상인 속성의 이름을 식별합니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 MemberRef 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|이름|예|MemberRef 요소에 포함된 속성의 이름입니다.|  
  
## <a name="memberrefs-element"></a>MemberRefs 요소  
 MemberRefs는 각 멤버가 MemberRef 요소에 포함된 멤버 컬렉션을 정의하는 복합 유형입니다.  
  
 다음 표는 MemberRefs 유형의 요소와 특성을 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|MemberRef|예|멤버 참조가 포함된 문자열입니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 CSDLBI 버전 1.1의 다음 예제는 Products 테이블을 정의하는 AdventureWorks 예제 데이터 모델의 일부를 나타냅니다. 여기서 MemberRef 요소는 모델의 기본 필드 집합에 포함된 각 열에 사용됩니다.  
  
```  
  
<bi:EntityType>  
   <bi:DefaultDetails>  
     <bi:MemberRef Name="Color" />  
     <bi:MemberRef Name="DealerPrice" />  
     <bi:MemberRef Name="Status" />  
   </bi:DefaultDetails>  
  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 예제는 CSDLBI 버전 1.1에서 Bikes 테이블을 정의하는 Contoso Operations 큐브의 일부를 나타냅니다. 이 예제에서는 MemberRef 요소를 사용하여 보고서에서 기본 필드 집합이 될 열의 이름을 지정하고, 또 다른 MemberRef 요소를 사용하여 정렬 순서가 될 열을 참조합니다.  
  
```  
  
<bi:DefaultDetails>  
   <bi:MemberRef Name="Color" />  
</bi:DefaultDetails>  
  
<bi:SortMembers>  
   <bi:MemberRef Name="Color" />  
</bi:SortMembers>  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CSDL BI 주석에 대 한 기술 참조](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  

