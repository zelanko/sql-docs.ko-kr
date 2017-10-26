---
title: "PropertyRef 요소 (CSDLBI) | Microsoft Docs"
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
ms.assetid: 8299efb9-e224-4a82-bdfc-a74ec92f8711
caps.latest.revision: 7
author: Minewiskan
ms.author: owend
manager: erikre
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6e2b4e43294d4e5c48500560203e778a21b99724
ms.contentlocale: ko-kr
ms.lasthandoff: 09/01/2017

---
# <a name="propertyref-element-csdlbi"></a>PropertyRef 요소(CSDLBI)
  PropertyRef 요소는 단순 유형으로, 다른 속성에 필요한 값을 공급하는 열 참조를 제공합니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 PropertyRef 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|이름|예|참조 대상인 속성의 이름이 포함된 문자열입니다.|  
  
## <a name="propertyrefs-element"></a>PropertyRefs 요소  
 PropertyRefs는 속성 컬렉션을 정의하는 복합 유형으로, 각 속성은 PropertyRef 요소에 포함되어 있습니다.  
  
 다음 표는 PropertyRefs 유형의 요소와 특성을 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|PropertyRef|예|속성 참조가 포함된 문자열입니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 CSDLBI 버전 1.1의 다음 예제는 AdventureWorks 테이블 형식 모델 예제의 측정값으로 사용할 수식의 원본을 지정하는 PropertyRef 요소를 보여 줍니다.  
  
```  
<bi:Measure Caption="Total Current Quarter Margin Performance" ReferenceName="Total Current Quarter Margin Performance" Width="0" IsSimpleMeasure="false">  
  <bi:Kpi StatusGraphic="Three Symbols UnCircled Colored">  
    <bi:KpiGoal>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Goal_" />  
    </bi:KpiGoal>  
    <bi:KpiStatus>  
      <bi:PropertyRef Name="Measures___Total_Current_Quarter_Margin_Performance_Status_" />  
    </bi:KpiStatus>  
  </bi:Kpi>  
</bi:Measure>  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 예제는 CSDLBI 버전 1.1에서 Contoso Operations 큐브의 KPI를 보여 줍니다. PropertyRef 요소는 KPI의 목표와 그 목표에 해당하는 상태를 정의하는 데 사용되는 수식 또는 값이 포함된 열을 가리킵니다.  
  
```  
<Property Name="Sum_of_SalesAmount" Type="Decimal" Precision="19" Scale="4">  
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
  
  

