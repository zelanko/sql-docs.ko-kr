---
title: "NavigationProperty 요소 (CSDLBI) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
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
ms.assetid: a36b4d3b-6a6c-489b-8a46-2e6b925b568f
caps.latest.revision: 10
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 5b1af93e52bc1a2fbd95059c86f73a0481572399
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty 요소(CSDLBI)
  NavigationProperty 요소는 복합 유형으로, 비즈니스 인텔리전스 데이터 모델에서 탐색을 지원하도록 CSDL Member 유형을 확장합니다.  
  
> [!WARNING]  
>  이 요소는 보고용으로, 수정하거나 조작할 수 없습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 NavigationProperty 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|CollectionCaption|아니요|탐색 속성의 인스턴스 집합을 참조하기 위한 복수형 이름입니다.<br /><br /> 이 특성을 생략하면 기본 Member의 Caption 특성이 사용됩니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예는 테이블 형식 모델에서 Product SubCategory 테이블과 Product 테이블 간의 연결을 설명하는 CSDLBI 버전 1.1의 탐색 속성을 보여 줍니다.  
  
```  
  
<NavigationProperty   
    Name="Product_Sub_Category_ProductSubcategoryKey"      
    Relationship="Sandbox.Product_Product_Sub_Category_Product_Sub_Category_ProductSubcategoryKey"  
     FromRole="Product_ProductSubcategoryKey"   
    ToRole="Product_Sub_Category_ProductSubcategoryKey">  
<bi:NavigationProperty   
     ReferenceName="Product Sub-Category_ProductSubcategoryKey" />  
</NavigationProperty>  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 예는 Contoso Operations 큐브에서 두 테이블 간의 관계를 설명하는 CSDLBI 버전 1.1의 탐색 속성을 보여 줍니다. 이 관계는 Bike Category 테이블과 Product Subcategory 테이블을 연결합니다.  
  
```  
  
<NavigationProperty   
     Name="BikeSubcategory_ProductSubcategoryKey"   
     Relationship="Sandbox.Bike_BikeSubcategory_BikeSubcategory_ProductSubcategoryKey"   
     FromRole="Bike_ProductSubcategoryKey"   
     ToRole="BikeSubcategory_ProductSubcategoryKey">  
   <bi:NavigationProperty />  
</NavigationProperty>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [1050-1103을 수준 테이블 형식 개체 모델 호환성을 이해 합니다.](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/understanding-tabular-object-model-at-levels-1050-through-1103.md)  
  
  

