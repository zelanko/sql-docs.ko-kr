---
title: EntityType 요소 (CSDLBI) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
ms.assetid: 372e2c13-ec38-4bb1-981c-50758d59a1da
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: d154816ae6aa2d540961721a6a0a84e454085242
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="entitytype-element-csdlbi"></a>EntityType 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  **EntityType** 요소는 데이터 모델에서 고객 또는 주문과 같은 높은 수준의 엔터티 구조를 나타내는 복합 유형입니다. **bi: EntityType** 요소 확장의 정의 [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) 에 사용 되는 [엔터티 데이터 프레임 워크](http://msdn.microsoft.com/library/bb399567.aspx)합니다.  
  
 데이터 모델에 포함된 엔터티별로 EntityType 요소를 지정해야 합니다. EntityType의 하위 요소는 테이블의 열 및 측정값을 설명합니다. 테이블 간의 관계는 **EntityContainer**에 포함됩니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 **EntityType** 요소를 정의하는 특성과 해당 요소를 보여 줍니다. 또한 [EntityType](http://msdn.microsoft.com/library/bb399206.aspx) 요소의 특성도 살펴봅니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|내용|아니요|가능한 데이터 형식이 열에 포함된 문자열입니다. 값은 데이터 모델에 있는 DimensionAttributeTypeEnumType의 값에서 파생됩니다.<br /><br /> DimensionAttributeTypeEnumType의 값이 'ExtendedType'이면 Contents의 값은 DimensionAttribute의 ExtendedType 요소에서 파생됩니다. 클라이언트는 이러한 값에 응답할 필요가 없습니다.|  
|DefaultDetails|아니요|테이블의 열 집합을 나타내는 속성 참조의 목록입니다.<br /><br /> 참조 [DefaultDetails 요소 & #40; CSDLBI & #41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/defaultdetails-element-csdlbi.md).|  
|DefaultImage|아니요|엔터티 이미지가 포함된 열에 대한 참조입니다.<br /><br /> 다차원 모델에서 이 요소는 차원 특성의 이진 특성에 해당합니다. 이 특성이 있으면 요소는 MemberRef 요소를 정확히 한 개 포함해야 합니다.<br /><br /> 참조 [MemberRef 요소 & #40; CSDLBI & #41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DefaultMeasure|아니요|엔터티를 통해 계산할 때 엔터티에서 기본값으로 사용해야 하는 측정값에 대한 참조입니다. 지정하지 않으면 기본값은 SUM입니다.<br /><br /> 참조 [MemberRef 요소 & #40; CSDLBI & #41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/memberref-element-csdlbi.md).|  
|DisplayKey|아니요|엔터티 인스턴스의 강력한 고유 식별자를 구성하는 열 또는 역할 End에 대한 참조 목록입니다.<br /><br /> 참조 [DisplayKey 요소 & #40; CSDLBI & #41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/displaykey-element-csdlbi.md).|  
|계층|아니요|모델에 있는 계층 목록입니다.<br /><br /> 참조 [Hierarchy 요소 & #40; CSDLBI & #41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/hierarchy-element-csdlbi.md).|  
|ReferenceName|예|DAX(Data Analysis Expressions) 쿼리에서 이 엔터티를 참조하는 데 사용할 수 있는 식별자입니다.<br /><br /> 이 특성이 없으면 엔터티의 정규화된 필드 이름이 사용됩니다.|  
|SortMembers|아니요|정렬할 속성 목록입니다. SortDirection 특성은 순서가 오름차순인지 아니면 내림차순인지를 나타냅니다.|  
  
## <a name="contents-element"></a>Contents 요소  
 **Contents** 요소는 엔터티에서 데이터의 형식을 설명하는 단순 유형입니다.  
  
 엔터티(열)의 내용은 다음 값 중 하나일 수 있습니다.  
  
|값|Description|  
|-----------|-----------------|  
|일반|다른 방식으로 정의되지 않습니다.|  
|Time|이 특성은 연도, 반기, 분기, 월 또는 일과 같은 기간을 나타냅니다.|  
|Geography|이 특성은 도시 또는 우편 번호와 같은 지리적 정보를 나타냅니다.|  
|조직|이 특성은 직원이나 자회사와 같은 조직 정보를 나타냅니다.|  
|제품 구성 정보|이 특성은 제품의 부품 목록 같은 재고 또는 제조 정보를 나타냅니다.|  
|계정|이 특성은 재무 보고를 위한 계정 차트를 나타냅니다.|  
|Customers|이 특성은 고객 또는 연락처 정보를 나타냅니다.|  
|제품|이 특성은 제품 정보를 나타냅니다.|  
|시나리오|이 특성은 계획 또는 전략 분석 정보를 나타냅니다.|  
|정량|이 특성은 정량 정보를 나타냅니다.|  
|유틸리티|이 특성은 기타 정보를 나타냅니다.|  
|Currency|통화 데이터와 메타데이터가 포함됩니다.|  
|요율|이 특성은 환율 정보를 나타냅니다.|  
|채널|이 특성은 채널 정보를 나타냅니다.|  
|Promotion|이 특성은 마케팅 홍보 행사 정보를 나타냅니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예제는 AdventureWorks 테이블 형식 모델에 사용되는 Geography 테이블의 일부 CSDLBI 버전 1.1 표현을 보여 줍니다. RowNumber 열은 테이블 형식 모델에서 행 식별자로 자동 생성된 숨겨진 열이며, 따라서 Contents 특성이 **RowNumber**입니다.  
  
```  
  
<EntityType   
     Name="DimGeography">  
     <Key>  
        <PropertyRef Name="RowNumber" />  
     </Key>  
     <Property   
        Name="RowNumber"   
        Type="Int64" Nullable="false">  
     <bi:Property   
        Hidden="true"   
        Contents="RowNumber"   
        Stability="RowNumber" />  
     </Property>  
....  
  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 예제는 Contoso Operations 큐브의 시간 차원 중 일부분을 나타내는 CSDLBI 버전 1.1의 EntityType 요소를 보여 줍니다.  
  
```  
<EntityType   
       Name="CalendarQuarter">  
    <Key>  
       <PropertyRef Name="RowNumber" />  
    </Key>  
  
    <Property Name="RowNumber"   
       Type="Int64"   
       Nullable="false">  
    <bi:Property   
       Hidden="true"   
       Contents="RowNumber"   
       Stability="RowNumber"   
    />  
    </Property>  
  
    <Property Name="CalendarQuarter2"   
       Type="String"   
       MaxLength="Max"   
       Unicode="true"   
       FixedLength="false"   
       Nullable="false">  
    <bi:Property   
       Caption="CalendarQuarter"   
       ReferenceName="CalendarQuarter"   
    />  
    </Property>  
   <bi:EntityType />  
</EntityType>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CSDL BI 주석에 대 한 기술 참조](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
