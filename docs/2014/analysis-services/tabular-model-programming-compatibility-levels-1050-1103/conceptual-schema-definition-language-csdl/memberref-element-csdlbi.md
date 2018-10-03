---
title: MemberRef 요소 (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
ms.assetid: 399aaa34-896c-48e7-aacb-18564f31b568
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bb0912afd99c7a4859ca4750a3ba1b66fdecd5f5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48205721"
---
# <a name="memberref-element-csdlbi"></a>MemberRef 요소(CSDLBI)
  MemberRef 요소는 참조 대상인 속성의 이름을 식별합니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 MemberRef 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|Description|  
|----------|-----------------|-----------------|  
|이름|사용자 계정 컨트롤|MemberRef 요소에 포함된 속성의 이름입니다.|  
  
## <a name="memberrefs-element"></a>MemberRefs 요소  
 MemberRefs는 각 멤버가 MemberRef 요소에 포함된 멤버 컬렉션을 정의하는 복합 유형입니다.  
  
 다음 표는 MemberRefs 유형의 요소와 특성을 보여 줍니다.  
  
|이름|필수 여부|Description|  
|----------|-----------------|-----------------|  
|MemberRef|사용자 계정 컨트롤|멤버 참조가 포함된 문자열입니다.|  
  
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
  
## <a name="see-also"></a>관련 항목  
 [CSDL용 BI 주석에 대한 기술 참조](technical-reference-for-bi-annotations-to-csdl.md)  
  
  
