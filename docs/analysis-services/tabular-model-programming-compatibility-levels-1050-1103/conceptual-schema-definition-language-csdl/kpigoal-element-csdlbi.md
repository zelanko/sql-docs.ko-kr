---
title: KpiGoal 요소 (CSDLBI) | Microsoft Docs
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
ms.assetid: fd8afbe7-b57d-4b47-862d-eb7b2489c327
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: ac5a522246c21e286356d4d1fa043e178cb9e78a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="kpigoal-element-csdlbi"></a>KpiGoal 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  KpiGoal 요소는 KPI(핵심 성과 지표) 목표를 정의하는 데 사용되는 열에 대한 참조를 제공합니다.  
  
 테이블 형식 모델에서 KPI는 측정값을 기반으로 하며 Measure 요소에는 수식(있는 경우)이 포함되는 반면 KPI와 연결된 다른 메타데이터는 [KPI 요소&#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)의 일부로 정의됩니다.  Kpigoal 요소는 KPI 요소의 하위 유형입니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 KpiGoal 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|PropertyRef|예|KPI 목표 값을 포함하는 열에 대한 참조입니다.<br /><br /> Kpigoal 요소에는 PropertyRef 요소가 정확히 하나 포함되어야 합니다.<br /><br /> [PropertyRef 요소&#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)를 참조하세요.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 CSDLBI 버전 1.1의 다음 예제는 Adventureworks 예제 모델의 KPI를 보여 줍니다.  
  
```  
  
<Property Name="InternetCurrentSalesPerformance" Type="Double">  
  <bi:Measure>  
    <bi:Kpi StatusGraphic="Three Stars Colored">  
      <bi:KpiGoal>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Goal" />  
      </bi:KpiGoal>  
      <bi:KpiStatus>  
        <bi:PropertyRef Name="v_InternetCurrSalesPerf_Status" />  
      </bi:KpiStatus>  
    </bi:Kpi>  
  </bi:Measure>  
</Property>  
  
```  
  
## <a name="example"></a>예제  
 **다차원**  
  
 다음 예제는 CSDLBI 버전 1.1에서 Contoso Operations 큐브의 KPI를 보여 줍니다.  
  
```  
<bi:Measure   
       Caption="Sum of SalesAmount"   
       ReferenceName="Sum of SalesAmount"   
       FormatString="\$#,0.00;(\$#,0.00);\$#,0.00">  
    <bi:Kpi   
       StatusGraphic="Three Circles Colored">  
      <bi:KpiGoal>  
         <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Goal" />  
       </bi:KpiGoal>  
       <bi:KpiStatus>  
          <bi:PropertyRef   
          Name="v_Sum_of_SalesAmount_Status" />  
        </bi:KpiStatus>  
       </bi:Kpi>  
</bi:Measure>  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [KPI 요소 & #40; CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
  
