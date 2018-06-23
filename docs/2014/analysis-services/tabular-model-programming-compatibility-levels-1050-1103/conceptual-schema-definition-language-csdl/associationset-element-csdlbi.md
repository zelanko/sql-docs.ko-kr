---
title: AssociationSet 요소 (CSDLBI) | Microsoft Docs
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
ms.assetid: 93e5ac4d-d7e8-490e-b775-28263a48cfcc
caps.latest.revision: 8
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d28f903b4e501f648329a65824292256bca7520b
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36187477"
---
# <a name="associationset-element-csdlbi"></a>AssociationSet 요소(CSDLBI)
  `AssociationSet` 요소는 연결을 정의하는 복합 유형입니다. CSDLBI 데이터 모델에서 연결은 두 테이블 간의 관계입니다.  
  
 모델의 고유 관계별로 `AssociationSet`를 지정해야 합니다. `AssociationSet`는 `Association` 요소를 사용하여 끝점을 정의합니다. 또한 `AssociationSet` 요소는 데이터 모델에서 관계와 사용법에 대한 메타데이터도 정의합니다.  
  
## <a name="applicable-attributes"></a>적용 가능한 특성  
 다음 표는 `AssociationSet` 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|속성|필수 여부|Description|  
|----------|-----------------|-----------------|  
|State|예|연결이 활성인지 여부를 나타내는 문자열입니다. 값은 State 요소에 따라 정의됩니다.|  
|숨김|아니요|관계가 표시되는지 여부를 나타내는 부울 값입니다. 기본적으로 Hidden은 모든 관계가 모델에 표시됨을 의미하는 `false`입니다.|  
  
## <a name="state-element"></a>State 요소  
 `State` 요소는 연결이 활성이고 계산에 사용해야 하는지, 아니면 비활성이어서 계산에 명시적으로 참조해야 하는지를 설명하는 단순 유형입니다.  
  
 두 엔터티를 연결하는 연결 집합이 여러 개인 경우, 연결 집합 하나만 활성으로 표시할 수 있습니다. 다시 말해, 동일한 두 테이블 사이에 두 가지 관계가 있는 경우 하나의 관계만 활성일 수 있습니다.  
  
 다음 표는 `State` 요소의 값을 보여 줍니다.  
  
|값|Description|  
|-----------|-----------------|  
|활성|연결이 활성입니다.|  
|비활성|연결이 활성입니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예제에서는 CSDLBI 버전 1.1에서 AdventureWorks 테이블 형식 모델의 관계를 보여 줍니다. OrderKey 및 Date 사이에 기존 관계가 있기 때문에 연결은 비활성으로 표시됩니다.  
  
```  
<AssociationSet   
    Name="InternetSales_Date_Date_Date"  
    Association="Sandbox.InternetSales_Date_Date_Date">  
    <End EntitySet="InternetSales" />  
    <End EntitySet="DimDate" />  
<bi:AssociationSet State="Inactive" />  
</AssociationSet>  
  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 예제에서는 Contoso Operations 큐브에서 Sales 및 Currency 테이블 사이에 정의되는 관계를 보여 줍니다.  
  
```  
<AssociationSet   
    Name ="Sales_Currency_Currency_Currency_Name2"  
    Association ="Sandbox.Sales_Currency_Currency_Currency_Name2">  
    <End EntitySet ="Sales" />  
    <End EntitySet ="Currency" />  
<bi:AssociationSet />  
</AssociationSet>  
```  
  
## <a name="see-also"></a>관련 항목  
 [CSDL용 BI 주석에 대한 기술 참조](technical-reference-for-bi-annotations-to-csdl.md)  
  
  