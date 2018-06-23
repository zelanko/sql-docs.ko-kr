---
title: ReportAction 데이터 형식 (ASSL) | Microsoft Docs
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
- ReportAction Data Type
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- ReportAction
helpviewer_keywords:
- ReportAction data type
ms.assetid: b22f0d52-ed3a-4239-840e-0eaf172d7276
caps.latest.revision: 40
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7c2c5140f3d2723f0456b007bc9228c5f87bbaa6
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36089641"
---
# <a name="reportaction-data-type-assl"></a>ReportAction 데이터 형식(ASSL)
  생성 하는 동작을 나타내는 파생된 데이터 형식을 정의 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] 보고서입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ReportAction>  
   <!-- The following elements extend Action -->  
   <ReportServer>...</ReportServer>  
   <Path>...</Path>  
   <ReportParameters>...</ReportParameters>  
   <ReportFormatParameters>...</ReportFormatParameters>  
</ReportAction>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|기본 데이터 형식|[동작](action-data-type-assl.md)|  
|파생 데이터 형식|InclusionThresholdSetting|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|InclusionThresholdSetting|  
|자식 요소|[경로](../properties/path-element-assl.md), [ReportFormatParameters](../collections/reportformatparameters-element-assl.md), [ReportParameters](../collections/reportparameters-element-assl.md), [ReportServer](../objects/server-element-assl.md)|  
|파생 요소|[동작](../objects/action-element-assl.md) ([동작](../collections/actions-element-assl.md) 컬렉션 [큐브](../objects/cube-element-assl.md) 또는 [관점](../objects/perspective-element-assl.md))|  
  
## <a name="remarks"></a>Remarks  
 보고서 서버는 URL 기반 보고서 요청에 응답합니다. 보고서 형식은 *Report*유형으로 정의됩니다. 동작이 생성되면 리소스 및 매개 변수가 서버로 전송됩니다. 이때 서버는 이러한 동작을 행 집합 형식으로 표시합니다.  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ReportAction>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services 스크립팅 언어 XML 데이터 형식 &#40;ASSL&#41;](analysis-services-scripting-language-xml-data-types-assl.md)  
  
  