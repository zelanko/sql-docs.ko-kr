---
title: "PerspectiveKpi 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: scripting
ms.reviewer: 
ms.suite: sql
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname: PerspectiveKpi Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: PerspectiveKpi
helpviewer_keywords: PerspectiveKpi data type
ms.assetid: e8d19ec8-70d3-4947-904a-fb81fcac9afd
caps.latest.revision: "32"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 99540f2d29c0ae2d40d07b6ef66b8b7bc036026e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="perspectivekpi-data-type-assl"></a>PerspectiveKpi 데이터 형식(ASSL)
  에 핵심 성과 지표 (KPI)에 대 한 정보를 나타내는 기본 데이터 형식을 정의 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<PerspectiveKpi>  
   <KpiID>...</KpiID>  
   <Annotations>...</Annotations>  
</PerspectiveKpi>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|없음|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[주석](../../../analysis-services/scripting/collections/annotations-element-assl.md), [KpiID](../../../analysis-services/scripting/properties/kpiid-element-assl.md)|  
|파생 요소|[Kpi](../../../analysis-services/scripting/objects/kpi-element-assl.md) ([Kpi](../../../analysis-services/scripting/collections/kpis-element-assl.md) 컬렉션 [관점](../../../analysis-services/scripting/objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>주의  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.PerspectiveKpi>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
