---
title: "Property 요소 (CSDLBI) | Microsoft Docs"
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
applies_to: SQL Server 2016 Preview
ms.assetid: f0770c5e-6420-4d0c-a5bf-b94eaf6877ca
caps.latest.revision: "7"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 1b71657fa8ff566b36e93b8c2bacfe3fb05630d7
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="property-element-csdlbi"></a>Property 요소(CSDLBI)
  CSDLBI의 Property 요소는 비즈니스 인텔리전스 데이터 모델을 지원하여 CSDL Property 요소에 대한 추가 기능을 제공하는 복합 유형입니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 CSDLBI Property 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|내용|아니요|요청의 LCID를 포함하는 문자열입니다.|  
|DefaultAggregationFunction|예|다른 기능을 지정하지 않고 특성으로 계산할 때 사용해야 하는 집계 기능을 지정하는 문자열입니다.<br /><br /> 이 특성을 지정하지 않으면 모델에 대한 기본 집계가 사용됩니다(일반적으로 SUM).|  
|GroupingBehavior|아니요|쿼리 결과를 그룹화하는 방법을 지정하는 값입니다. 이 특성의 내용은 TGroupingBehavior 단순 유형에 따라 정의됩니다(아래 표 참조).|  
|OrderBy|아니요|해당 속성 값의 정렬 순서를 정의하는 모델 내 다른 속성에 대한 참조입니다.<br /><br /> 두 속성의 값이 일대일로 매핑되어야 합니다. 그러지 않으면 정렬 동작이 정의되지 않습니다.<br /><br /> 이 요소를 생략하면 값을 기준으로 속성이 정렬됩니다.|  
|안정성|아니요|새로 고침 작업 사이에 속성 값의 안정성을 지정하는 특성입니다.<br /><br /> 이 특성은 사용자가 설정하지 않으며 불안정한 값에 대해서만 디자인 타임 환경에서 내보냅니다. 이 특성은 행 번호가 포함된 열과, NOW() 또는 RAND()와 같이 확정되지 않은 결과를 생성하는 특정 수식이 포함된 열에 항상 적용됩니다.<br /><br /> Stabilitysimple 유형을 설명하는 아래 표에 이 특성의 값이 나열되어 있습니다.|  
  
## <a name="groupingbehavior"></a>GroupingBehavior  
 다음 표에서는 GroupingBehavior 단순 유형의 값을 나열합니다.  
  
|값|Description|  
|-----------|-----------------|  
|GroupOnValue|xthe 특성의 값을 기준으로 그룹화합니다.|  
|GroupOnEntityKey|엔터티 키를 기준으로 그룹화합니다.|  
  
 다음 예에서는 이 두 값의 사용을 설명합니다. 이름으로 지정한 특정 사용자에 대해 급여 공제를 반환하도록 쿼리를 설계했다고 가정합시다. 이름은 같고 데이터베이스 식별자는 다른 두 사용자가 데이터베이스에 있을 때, 쿼리 결과는 열에 적용된 특성 값에 따라 달라집니다.  
  
-   **GroupOnValue**: 쿼리 결과 두 사용자의 급여 공제가 합계를 포함 합니다.  
  
-   **GroupOnEntityKey**: 쿼리 결과 개별적으로 나열 되지만 각 사용자에 대 한 급여 공제가 합계를 포함 합니다.  
  
## <a name="stability"></a>안정성  
 다음 표에서 값을 나열는 **안정성** 단순 유형입니다.  
  
|값|Description|  
|-----------|-----------------|  
|안정적|속성은 새로 고침 작업 사이에 상수로 유지됩니다.|  
|RowNumber|속성에는 행 번호가 포함됩니다.|  
|일시적|속성은 새로 고침 작업 사이에 상수로 유지되지 않을 수 있습니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 XML은 CSDLBI 버전 1.1에서 AdventureWorks 테이블 형식 모델 예제에 있는 일부 속성의 표현을 보여 줍니다.  
  
```  
  
<EntityType   
   Name="DimEmployee">  
   <Key>  
      <PropertyRef   
      Name="RowNumber" />  
   </Key>  
  
   <Property   
      Name="RowNumber"   
      Type="Int64"   
      Nullable="false">  
   <bi:Property   
      Hidden="true"   
      Contents="RowNumber"   
      Stability="RowNumber" />  
   </Property>  
  
   <Property   
      Name="EmployeeKey"   
      Type="Int64">  
   <bi:Property />  
   </Property>  
….  
</bi:EntityType>  
</EntityType>  
  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 CSDLBI 버전 1.1의 다음 예제는 Contoso Operations 큐브를 나타내는 데이터 모델에 있는 열의 일부 속성을 보여 줍니다. 대부분의 열에는 BI 주석이 필요하지 않거나 적용되지 않으며, 프레젠테이션 계층에서 특수 처리가 필요한 열에만 적용됩니다.  
  
```  
  
<EntityType   
   Name="Bike">  
  
   <Key>  
      <PropertyRef Name="RowNumber" />  
   </Key>  
  
   <Property   
      Name="RowNumber"   
      Type="Int64"   
      Nullable="false">  
   <bi:Property   
      Hidden="true"   
      Contents="RowNumber"   
      Stability="RowNumber"   
   />  
   </Property>  
  
   <Property   
      Name="ProductAlternateKey"   
      Type="String"   
      MaxLength="Max"   
      Unicode="true"   
      FixedLength="false">  
   <bi:Property />  
   </Property>  
  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CSDL용 BI 주석에 대한 기술 참조](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  
