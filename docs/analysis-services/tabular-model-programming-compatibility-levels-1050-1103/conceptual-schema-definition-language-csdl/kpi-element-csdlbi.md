---
title: KPI 요소 (CSDLBI) | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bc368aed1186c20e76ce643a33673030713547ba
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/10/2018
---
# <a name="kpi-element-csdlbi"></a>KPI 요소(CSDLBI)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  KPI 요소는 KPI(핵심 성과 지표)로 사용할 수 있는 계산을 정의합니다. 비즈니스 인텔리전스 데이터 모델에서 KPI는 측정값을 기반으로 하며, KPI 정의처럼 측정값과 관련된 모든 메타데이터뿐 아니라 KPI 값을 표시하는 데 필요한 기본 그래픽 등의 정보를 포함합니다.  
  
 Kpi 요소는 측정값 정의에 포함되는 수식을 지정하는 것이 아니라 KPI로 사용되는 측정값과 관련된 추가 메타데이터를 지정합니다. 측정값을 KPI로 지정한 후에는 이를 다른 컨텍스트에서 측정값으로 사용할 수 없습니다.  
  
## <a name="elements-and-attributes"></a>요소 및 특성  
 다음 표는 KPI 요소를 정의하는 특성과 해당 요소를 보여 줍니다.  
  
|이름|필수 여부|설명|  
|----------|-----------------|-----------------|  
|설명서|아니요|KPI에 대한 설명입니다.|  
|KpiGoal|예|목표로 사용할 수 있는 값이 포함된 열에 대한 참조입니다.<br /><br /> [PropertyRef 요소&#40;CSDLBI&#41;](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/conceptual-schema-definition-language-csdl/propertyref-element-csdlbi.md)a를 참조하세요.|  
|KpiStatus|예|KPI의 현재 상태를 나타내는 값이 포함된 열에 대한 참조입니다.|  
|StatusGraphic|예|KPI에 정의된 대상에 대한 음수, 보통 또는 양수 진행률을 나타내는 이미지에 대한 참조입니다.|  
  
## <a name="remarks"></a>주의  
 모델을 디자인할 때 측정값을 만든 다음 이 측정값을 KPI로 사용하도록 할당하여 KPI를 만들 수 있습니다. 그런 다음 추세를 나타내는 데 사용할 그래픽과 같은 KPI 관련 정보를 추가합니다.  
  
## <a name="example"></a>예제  
 **테이블 형식**  
  
 다음 예제는 CSDLBI 버전 1.0에서 AdventureWorks 테이블 형식 모델 예제의 판매를 측정하는 KPI를 보여 줍니다.  
  
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
  
 다음 예제는 CSDLBI 버전 1.1에서 Contoso Operations 큐브의 KPI를 보여 줍니다.  
  
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
  
  
