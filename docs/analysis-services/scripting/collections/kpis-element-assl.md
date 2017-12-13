---
title: "Kpis 요소 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: 
ms.component: 
ms.reviewer: 
ms.suite: pro-bi
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: Kpis Element
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: Kpis
helpviewer_keywords: Kpis element
ms.assetid: da4e32a0-1416-4d32-8b7f-7d74be23c9d4
caps.latest.revision: "35"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: be0fde074002913e807c961dbb9c39d85ec4f78b
ms.sourcegitcommit: f1a6944f95dd015d3774a25c14a919421b09151b
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/08/2017
---
# <a name="kpis-element-assl"></a>Kpis 요소(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]핵심 성과 지표의 컬렉션을 포함 ([Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 요소) 부모 요소와 연결 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Cube><!-- or Perspective -->  
   ...  
   <Kpis>  
      <Kpi>...</Kpi> <!-- parent: Cube -->  
<!-- or -->  
      <Kpi xsi:type="PerspectiveKpi">...</Kpi> <!-- parent: Perspective -->  
   ...  
</Cube>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|데이터 형식 및 길이|없음|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[큐브](../../../analysis-services/scripting/objects/cube-element-assl.md), [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md)|  
|자식 요소|아래 표를 참조 합니다.|  
  
|상위 항목 또는 부모|자식 요소|  
|------------------------|-------------------|  
|[Cube](../../../analysis-services/scripting/objects/cube-element-assl.md)|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md)|  
|[큐브 뷰](../../../analysis-services/scripting/objects/perspective-element-assl.md)|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) 형식의 [PerspectiveKpi](../../../analysis-services/scripting/data-type/perspectivekpi-data-type-assl.md)|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.KpiCollection>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [컬렉션 &#40; ASSL &#41;](../../../analysis-services/scripting/collections/collections-assl.md)  
  
  
