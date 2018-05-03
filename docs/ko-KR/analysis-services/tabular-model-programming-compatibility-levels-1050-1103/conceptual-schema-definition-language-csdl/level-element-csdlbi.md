---
title: 수준 요소 (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: fdf75c47-77dc-4bdb-9931-8eca198fdb88
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: f11ee59d6001df01670feb1f08906e41f57b5c5a
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="level-element-csdlbi"></a>Level 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  Level 요소는 계층 구조에서 단일 수준을 정의하는 복합 유형입니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 Level 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|원본|예|속성 참조를 위한 컨테이너입니다.|  
|PropertyRef|예|인스턴스 속성에 대한 참조입니다. 캡션, 이름 및 참조 이름 등 그 밖의 수준 특성은 참조된 인스턴스 속성에서 가져올 수 있습니다. 그 경우 Level 요소에서 지정할 필요가 없습니다.|  
  
## <a name="remarks"></a>주의  
 테이블 형식 모델의 계층에 대한 자세한 내용은 [Hierarchy 요소&#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 CSDLBI 버전 1.1의 다음 예는 AdventureWorks 테이블 형식 모델 예제의 계층에 있는 여러 수준의 정의를 보여 줍니다.  
  
```  
  
<bi:Hierarchy Name="Category">  
   <bi:Level Name="CategoryName">  
     <bi:Source>  
       <bi:PropertyRef Name="CategoryName" />  
     </bi:Source>  
   </bi:Level>  
   <bi:Level Name="ProductName">  
     <bi:Source>  
       <bi:PropertyRef Name="ProductName" />  
     </bi:Source>  
   </bi:Level>  
</bi:Hierarchy>  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 CSDLBI 버전 1.1의 다음 예는 Contoso Operations 큐브의 여러 수준이 있는 계층을 보여 줍니다.  
  
```  
<bi:Hierarchy   
   Name="Product_Hierarchy"   
   Caption="Product Hierarchy"   
   ReferenceName="Product Hierarchy">  
     <bi:Documentation>  
        <bi:Summary>DESCRIPTION_ProductModelCateg_Hierarchies</bi:Summary>  
     </bi:Documentation>  
  
     <bi:Level Name="ProductLine">  
        <bi:Source>  
        <bi:PropertyRef Name="ProductLine" />  
        </bi:Source>  
     </bi:Level>  
  
     <bi:Level Name="ModelName">  
        <bi:Source>  
        <bi:PropertyRef Name="ModelName" />  
        </bi:Source>  
     </bi:Level>  
</bi:Hierarchy>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [1050-1103을 수준 테이블 형식 개체 모델 호환성을 이해 합니다.](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [DAX의 부모-자식 계층에 대 한 함수 이해](http://msdn.microsoft.com/en-us/b11f0cff-cee4-4ae7-a5b3-ebe288fc42d3)   
 [구성에서 & #40; 모든 & #41; 특성 계층의 수준](../../../analysis-services/multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  
