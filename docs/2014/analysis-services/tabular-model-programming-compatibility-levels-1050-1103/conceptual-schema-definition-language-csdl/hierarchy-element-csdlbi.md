---
title: Hierarchy 요소 (CSDLBI) | Microsoft Docs
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
ms.assetid: 9debb638-1b28-401b-9499-8f63943863e9
caps.latest.revision: 12
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: f2846424fdf7104c95cb4a56ac836b57583bf0cc
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36090248"
---
# <a name="hierarchy-element-csdlbi"></a>Hierarchy 요소(CSDLBI)
  Hierarchy 요소는 서로 연결하여 계층을 구성할 수 있는 테이블의 필드에 대한 논리적 컨테이너입니다. Hierarchy 요소는 CSDL Member 요소에서 파생되는 요소로, 비즈니스 인텔리전스 데이터 모델에서 만든 계층을 지원하도록 범위가 확장되었습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 Hierarchy 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|속성|필수 여부|Description|  
|----------|-----------------|-----------------|  
|설명서|아니요|계층에 대한 설명입니다.|  
|Level|예|계층에 사용되는 열을 정의하는 하나 이상의 Level 요소입니다.<br /><br /> [Level 요소&#40;CSDLBI&#41;](level-element-csdlbi.md)를 참조하세요.|  
  
## <a name="remarks"></a>Remarks  
 테이블 형식 모델에서는 동일한 테이블의 열 간에 부모-자식 관계를 지정하여 계층을 만듭니다. 자세한 내용은 [계층 구조&#40;SSAS 테이블 형식&#41;](../../tabular-models/hierarchies-ssas-tabular.md)를 참조하세요.  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예는 CSDLBI 버전 1.0에서 Products 테이블에 추가된 AdventureWorks 예제 모델의 계층을 보여 줍니다.  
  
```  
  
<bi:Hierarchy Name="Categoryy">  
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
  
 다음 예는 CSDLBI 버전 1.1에서 Contoso Retail Operations 큐브의 계층을 보여 줍니다.  
  
```  
  
<bi:Hierarchy Name="Product_Hierarchy" Caption="Product Hierarchy" ReferenceName="Product Hierarchy">  
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
  
## <a name="see-also"></a>관련 항목  
 [테이블 형식 개체 모델 이해](../representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)   
 [DAX의 부모-자식 계층에 대 한 함수 이해](https://msdn.microsoft.com/library/gg492192(v=sql.120).aspx)   
 [구성에서 &#40;모든&#41; 특성 계층의 수준](../../multidimensional-models/database-dimensions-configure-the-all-level-for-attribute-hierarchies.md)  
  
  