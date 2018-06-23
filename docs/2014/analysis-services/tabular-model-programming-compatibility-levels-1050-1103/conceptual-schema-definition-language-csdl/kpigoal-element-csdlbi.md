---
title: KpiGoal 요소 (CSDLBI) | Microsoft Docs
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
ms.assetid: fd8afbe7-b57d-4b47-862d-eb7b2489c327
caps.latest.revision: 11
author: mgblythe
ms.author: mblythe
manager: mblythe
ms.openlocfilehash: d75a2178d91b93879e4d08d11ba0fa536f7f2ddd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36172742"
---
# <a name="kpigoal-element-csdlbi"></a>KpiGoal 요소(CSDLBI)
  KpiGoal 요소는 KPI(핵심 성과 지표) 목표를 정의하는 데 사용되는 열에 대한 참조를 제공합니다.  
  
 테이블 형식 모델에서 KPI는 측정값을 기반으로 하며 Measure 요소에는 수식(있는 경우)이 포함되는 반면 KPI와 연결된 다른 메타데이터는 [KPI 요소&#40;CSDLBI&#41;](kpi-element-csdlbi.md)의 일부로 정의됩니다.  Kpigoal 요소는 KPI 요소의 하위 유형입니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 KpiGoal 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|속성|필수 여부|Description|  
|----------|-----------------|-----------------|  
|PropertyRef|예|KPI 목표 값을 포함하는 열에 대한 참조입니다.<br /><br /> Kpigoal 요소에는 PropertyRef 요소가 정확히 하나 포함되어야 합니다.<br /><br /> [PropertyRef 요소&#40;CSDLBI&#41;](propertyref-element-csdlbi.md)를 참조하세요.|  
  
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
  
## <a name="see-also"></a>관련 항목  
 [KPI 요소 &#40;CSDLBI&#41;](kpi-element-csdlbi.md)  
  
  