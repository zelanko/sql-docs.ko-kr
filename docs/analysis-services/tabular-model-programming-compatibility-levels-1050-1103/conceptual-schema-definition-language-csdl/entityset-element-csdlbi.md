---
title: "EntitySet 요소 (CSDLBI) | Microsoft Docs"
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
applies_to:
- SQL Server 2016 Preview
ms.assetid: d4703c9e-5594-472e-a85b-0f5bd0d73d6f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: e48f4d90853e954618d770feda70c4a72d0f607a
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="entityset-element-csdlbi"></a>EntitySet 요소(CSDLBI)
  EntitySet 요소는 CSDLBI 데이터 모델에서 특정 유형의 엔터티 컬렉션을 정의합니다.  
  
 EntitySet는 데이터 모델에 포함된 각 엔터티 유형을 지정해야 합니다. 이러한 모델 엔터티에 대한 정보는 해당 형식, 즉 Entity 요소의 자식 엔터티를 나열하여 지정됩니다. 자세한 내용은 [EntityType 요소&#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/entitytype-element-csdlbi.md)를 참조하세요.  
  
 데이터 정렬 및 언어와 같은 속성은 개별 개체가 아니라 EntityContainer의 수준에서 정의됩니다. 그러나 모델 내의 열 및 텍스트 특성에는 다른 언어의 캡션이나 번역이 있을 수 있습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 아래 표는 EntitySet를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|특성 이름|필수 여부|설명|  
|--------------------|-----------------|-----------------|  
|Caption|아니요|엔터티 집합에 대한 알기 쉬운 설명입니다.|  
|CollectionCaption|아니요|엔터티의 복수 이름이 포함된 문자열입니다.|  
|ReferenceName|아니요|병합되지 않고 정규화된 엔터티 이름이 포함됩니다. 다차원 모델에서 이 특성은 CubeDimension 이름에 해당합니다.|  
|숨김|아니요|엔터티를 숨길지 여부를 나타냅니다. 기본적으로 엔터티는 숨김 상태가 아닙니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예제는 CSDLBI 버전 1.1에서 AdventureWorks 테이블 형식 모델의 Date 및 Geography 테이블 정의를 보여 줍니다.  
  
```  
  
<EntitySet   
   Name="Date"   
   EntityType="Sandbox. Date">  
<bi:EntitySet />  
</EntitySet>  
  
<EntitySet   
   Name="Geography"   
   EntityType="Sandbox.Geography">  
<bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 CSDLBI 버전 1.1의 다음 예제는 Contoso Retail Operations 큐브의 여러 EntitySet 요소를 보여 줍니다.  
  
```  
  
<EntitySet Name="Outage" EntityType="Sandbox.Outage">  
       <bi:EntitySet />  
</EntitySet>  
  
<EntitySet Name="Store" EntityType="Sandbox.Store">  
     <bi:EntitySet />  
</EntitySet>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CSDL BI 주석에 대 한 기술 참조](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
