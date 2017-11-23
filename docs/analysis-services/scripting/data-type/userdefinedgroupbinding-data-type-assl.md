---
title: "UserDefinedGroupBinding 데이터 형식 (ASSL) | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
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
apiname: UserDefinedGroupBinding Data Type
apilocation: http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to: SQL Server 2016 Preview
f1_keywords: UserDefinedGroupBinding
helpviewer_keywords: UserDefinedGroupBinding data type
ms.assetid: 70149929-0ff7-4a67-84bf-e94908ae7611
caps.latest.revision: "37"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: 048d2693d4b3876559b8492581ae905ac69a00db
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="userdefinedgroupbinding-data-type-assl"></a>UserDefinedGroupBinding 데이터 형식(ASSL)
  특성에 대한 사용자 정의 그룹화를 나타내는 파생 데이터 형식을 정의합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<UserDefinedGroupBinding>  
   <!-- The following elements extend Binding -->  
      <AttributeID>...</AttributeID>  
      <Groups>...</Groups>  
</UserDefinedGroupBinding>  
```  
  
## <a name="data-type-characteristics"></a>데이터 형식 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|기본 데이터 형식|[바인딩](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
|파생 데이터 형식|없음|  
  
## <a name="data-type-relationships"></a>데이터 형식 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|없음|  
|자식 요소|[AttributeID](../../../analysis-services/scripting/properties/attributeid-element-assl.md), [그룹](../../../analysis-services/scripting/collections/groups-element-assl.md)|  
|파생 요소|참조 [바인딩](../../../analysis-services/scripting/data-type/binding-data-type-assl.md)|  
  
## <a name="remarks"></a>주의  
 **UserDefinedGroupBinding** 으로 자동으로 처리 되는 [AttributeBinding](../../../analysis-services/scripting/data-type/attributebinding-data-type-assl.md), 해당 [형식](../../../analysis-services/scripting/properties/type-element-binding-assl.md) 로 설정 된 *모든*합니다.  
  
 에 대 한 자세한 내용은 **바인딩** 유형의 Analysis Services Scripting Language (ASSL) 개체 테이블을 포함 하 여는 **바인딩** 유형과의 상속 계층 구조 **바인딩**  형식 참조 [바인딩 데이터 형식 &#40; ASSL &#41; ](../../../analysis-services/scripting/data-type/binding-data-type-assl.md).  
  
 ASSL의 데이터 바인딩에 대 한 개요를 참조 하십시오. [데이터 원본 및 바인딩 &#40; SSAS 다차원 &#41; ](../../../analysis-services/multidimensional-models/data-sources-and-bindings-ssas-multidimensional.md).  
  
 Analysis Management Objects (AMO) 개체 모델의 해당 요소는 <xref:Microsoft.AnalysisServices.UserDefinedGroupBinding>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [스크립팅 언어 XML 데이터 형식 &#40; analysis Services ASSL &#41;](../../../analysis-services/scripting/data-type/analysis-services-scripting-language-xml-data-types-assl.md)  
  
  
