---
title: KpiStatus 요소 (CSDLBI) | Microsoft Docs
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
ms.assetid: 6fee5b82-caa8-46a1-ad68-bbce3e11e01e
caps.latest.revision: 13
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 8895d3fce311650e60de08304abe211ba5306c96
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="kpistatus-element-csdlbi"></a>KpiStatus 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  KpiStatus 요소는 KPI(핵심 성과 지표)의 상태 지표 값이 포함된 열에 대한 참조를 정의합니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 KpiStatus 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|PropertyRef|예|KPI에서 상태 지표로 사용되는 값이 포함된 열에 대한 참조입니다.<br /><br /> 이 요소는 TPropertyRefcomplex 유형에 의해 정의된 열 참조를 정확히 한 개만 포함해야 합니다.|  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예제는 CSDLBI 버전 1.1에서 AdventureWorks 테이블 형식 모델 예제의 KPI를 보여 줍니다. KpiStatus 요소는 값이 포함된 열(PropertyRef로 표시됨)을 참조합니다.  
  
```  
  
<Property Name="InternetCurrSalesPerf" Type="Double">  
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
  
 다음 예제는 CSDLBI 버전 1.1에서 Contoso Operations 큐브의 KPI를 보여 줍니다. KpiStatus 요소는 KPI 상태의 값을 계산하는 측정값을 참조합니다.  
  
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
  
## <a name="see-also"></a>관련 항목:  
 [KPI 요소 & #40; CSDLBI & #41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/kpi-element-csdlbi.md)  
  
  
