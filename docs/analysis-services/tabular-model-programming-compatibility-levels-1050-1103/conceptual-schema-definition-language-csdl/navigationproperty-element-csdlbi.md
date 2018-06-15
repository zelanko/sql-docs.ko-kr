---
title: NavigationProperty 요소 (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 9db2facd93380fa3d0e011104bb95950e43340fb
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
ms.locfileid: "34038746"
---
# <a name="navigationproperty-element-csdlbi"></a>NavigationProperty 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
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
  
  
