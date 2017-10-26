---
title: "요소 (CSDLBI) 측정 | Microsoft Docs"
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
ms.assetid: bfbc9274-053a-421a-bb81-2095bba710be
caps.latest.revision: 12
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: ee1d1fdcdd17b9ade86e9f9acc6b6a41ed9cc930
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="measure-element-csdlbi"></a>Measure 요소(CSDLBI)
  Measure 요소는 CSDL Property 요소를 기반으로 하는 복합 유형입니다. CSDLBI 주석은 비즈니스 인텔리전스 데이터 모델에서 사용할 복합 수식의 정의를 지원하는 특성을 추가합니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표에서는 Measure 요소를 정의하는 특성과 해당 요소 및 Property 요소에 적용 가능한 모든 특성을 설명합니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|Kpi|아니요|KPI로 사용되는 측정값 전용의 필수 요소입니다. 모든 측정값이 KPI인 것은 아니지만 모든 KPI는 측정값 정의를 기반으로 해야 합니다.<br /><br /> [KPI 요소 &#40; CSDLBI &#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)|  
|IsSimpleMeasure|아니요|측정값에 사용된 수식이 단순 집계(SUM, COUNT, MIN, MAX, AVG, DistinctCount) 중 하나인지 여부를 나타내는 True/False 값입니다.<br /><br /> 기본값은 true입니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예제는 CSDLBI 버전 1.1에서 AdventureWorks 테이블 형식 모델 예제의 측정값 두 개를 보여 줍니다. 두 번째 측정값은 KPI 요소가 추가되어 KPI로 변환되었습니다.  
  
```  
  
<Property   
    Name="Order_Lines_Count"   
    Type="Int64">  
<bi:Measure   
    Caption="Order Lines Count"   
    ReferenceName="Order Lines Count"   
    Width="0"   
    IsSimpleMeasure="false" />  
</Property>  
  
<Property   
    Name="Total_Current_Quarter_Sales_Performance"   
    Type="Double">  
<bi:Measure   
    Caption="Total Current Quarter Sales Performance"   
    ReferenceName="Total Current Quarter Sales Performance"   
    Width="0"   
    IsSimpleMeasure="false">  
    <bi:Kpi   
    StatusGraphic="Three Signs Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Goal_" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="Measures___Total_Current_Quarter_Sales_Performance_Status_" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
```  
  
## <a name="example"></a>예제  
 **Multidimensiona;**  
  
 다음 예제는 CSDLBI 버전 1.1에서 KPI로 사용되는 Contoso Operations 큐브의 측정값을 보여 줍니다.  
  
```  
  
<Property   
    Name="Sum_of_SalesAmount"   
    Type="Decimal" Precision="19" Scale="4">  
<Documentation>  
<Summary>KPI Description</Summary>  
</Documentation>  
<bi:Measure   
    Caption="Sum of SalesAmount"   
    ReferenceName="Sum of SalesAmount"   
    FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
<bi:Kpi   
    StatusGraphic="Three Circles Colored">  
    <bi:KpiGoal>  
        <bi:PropertyRef Name="v_Sum_of_SalesAmount_Goal" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
        <bi:PropertyRef Name="v_Sum_of_SalesAmount_Status" />  
    </bi:KpiStatus>  
</bi:Kpi>  
</bi:Measure>  
</Property>  
```  
  
## <a name="see-also"></a>관련 항목:  
 [CSDL BI 주석에 대 한 기술 참조](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/technical-reference-for-bi-annotations-to-csdl.md)  
  
  

