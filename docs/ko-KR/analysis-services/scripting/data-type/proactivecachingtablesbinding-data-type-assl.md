---
title: ProactiveCachingTablesBinding 데이터 형식 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- ProactiveCachingTablesBinding Data Type
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- ProactiveCachingTablesBinding data type
ms.assetid: f6b3f6fc-757c-4b1e-bb3a-d26482888d14
caps.latest.revision: 16
author: Minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 9148902cdeb0bd19511d88ca75887669a010abba
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="proactivecachingtablesbinding-data-type-assl"></a>ProactiveCachingTablesBinding 데이터 형식(ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]
  캐시를 다시 작성해야 하는 지정된 테이블 및 뷰의 데이터 원본 변경 내용에 대한 정보를 [ProactiveCaching](../../../analysis-services/scripting/objects/proactivecaching-element-assl.md) 요소에 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<ProactiveCachingTablesBinding>  
   <!-- The following elements extend ProactiveCachingObjectNotificationBinding -->  
   <TableNotification>...</TableNotification>  
</ProactiveCachingTablesBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[ProactiveCachingObjectNotificationBinding](../../../analysis-services/scripting/data-type/proactivecachingobjectnotificationbinding-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[TableNotification](../../../analysis-services/scripting/objects/tablenotification-element-assl.md)|  
|파생 요소|없음|  
  
## <a name="remarks"></a>주의  
 에 대 한 자세한 내용은 **ProactiveCachingBinding** 테이블의 상속 계층을 포함 하 여 **ProactiveCachingBinding** 형식 참조 [ProactiveCachingBinding 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/proactivecachingbinding-data-type-assl.md)합니다.  
  
 에 대 한 자세한 내용은 **바인딩** 유형의 Analysis Services Scripting Language (ASSL) 개체 테이블을 포함 하 여는 **바인딩** 유형과의 상속 계층 구조 **바인딩**  형식 참조 [바인딩 데이터 형식 &#40;ASSL&#41;](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)합니다.  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하십시오. [데이터 원본 및 바인딩 & #40; SSAS 다차원 & #41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.ProactiveCachingTablesBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 & #40; analysis Services ASSL & #41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
