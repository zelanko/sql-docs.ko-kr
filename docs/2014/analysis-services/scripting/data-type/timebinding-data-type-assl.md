---
title: TimeBinding 데이터 형식 (ASSL) | Microsoft Docs
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
api_name:
- TimeBinding Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- TimeBinding
helpviewer_keywords:
- TimeBinding data type
ms.assetid: f3c06978-c181-4a73-9b57-8fc30358faab
caps.latest.revision: 37
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7102bbea8eb516b93eb2e539a74b2110f22c6694
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37183340"
---
# <a name="timebinding-data-type-assl"></a>TimeBinding 데이터 형식(ASSL)
  기간에 대한 바인딩을 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<TimeBinding>  
   <!-- The following elements extend Binding -->  
      <CalendarStartDate>...</CalendarStartDate>  
      <CalendarEndDate>...</CalendarEndDate>  
      <FirstDayOfWeek>...</FirstDayOfWeek>  
   <CalendarLanguage>...</CalendarLanguage>  
   <FiscalFirstMonth>...</FiscalFirstMonth>  
   <FiscalFirstDayOfMonth>...</FiscalFirstDayOfMonth>  
   <FiscalYearName>...</FiscalYearName>  
   <ReportingFirstMonth>...</ReportingFirstMonth>  
   <ReportingFirstWeekOfMonth>...</ReportingFirstWeekOfMonth>  
   <ReportingWeekToMonthPattern>...</ReportingWeekToMonthPattern>  
   <ManufacturingFirstMonth>...</ManufacturingFirstMonth>  
   <ManufacturingFirstWeekOfMonth>...</ManufacturingFirstWeekOfMonth>  
   <ManufacturingExtraMonthQuarter>...</ManufacturingExtraMonthQuarter>  
</TimeBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[바인딩](binding-data-type-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[CalendarEndDate](../properties/calendarenddate-element-assl.md), [CalendarLanguage](../properties/language-element-assl.md), [CalendarStartDate](../properties/calendarstartdate-element-assl.md)를 [FirstDayOfWeek](../properties/firstdayofweek-element-assl.md)하십시오 [FiscalFirstDayOfMonth](../properties/fiscalfirstdayofmonth-element-assl.md) 를 [FiscalFirstMonth](../properties/fiscalfirstmonth-element-assl.md), [FiscalYearName](../properties/name-element-assl.md)합니다 [ManufacturingExtraMonthQuarter](../properties/manufacturingextramonthquarter-element-assl.md)를 [ManufacturingFirstMonth](../properties/manufacturingfirstmonth-element-assl.md), [ManufacturingFirstWeekOfMonth](../properties/manufacturingfirstweekofmonth-element-assl.md)하십시오 [ReportingFirstMonth](../properties/reportingfirstmonth-element-assl.md)하십시오 [ReportingFirstWeekOfMonth](../properties/reportingfirstweekofmonth-element-assl.md), [ReportingWeekToMonthPattern](../properties/reportingweektomonthpattern-element-assl.md)|  
|파생 요소|참조 [바인딩](binding-data-type-assl.md)|  
  
## <a name="remarks"></a>Remarks  
 에 대 한 자세한 내용은 합니다 `Binding` 형식, Analysis Services Scripting Language (ASSL) 개체 테이블을 비롯 한는 `Binding` 형식과 상속 계층 `Binding` 참조 하십시오 [바인딩 데이터 형식 &#40;ASSL &#41;](binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩 개요를 보려면 [데이터 원본 및 바인딩 &#40;SSAS 다차원&#41;](../../multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md)합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.TimeBinding>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services Scripting Language XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
