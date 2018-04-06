---
title: NullProcessing 요소 (ASSL) | Microsoft Docs
ms.date: 03/14/2017
ms.prod: analysis-services
ms.prod_service: analysis-services
ms.service: ''
ms.component: ''
ms.reviewer: ''
ms.suite: pro-bi
ms.custom: ''
ms.technology: ''
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- NullProcessing Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: 36
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: bd814424d42062652d85f780d03a8ac5b818c1b0
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/08/2018
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]방법을 null 값이 정의 되어 처리 됩니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<DataItem>  
   ...  
   <NullProcessing>...</NullProcessing>  
   ...  
</DataItem>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String(열거형)|  
|기본값|*자동*|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[DataItem](../../../analysis-services/scripting/data-type/dataitem-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>주의  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*유지*|Null 값을 유지합니다.<br /><br /> 참고:이 값은 고유 카운트 측정값에 대 한 지원 되지 않습니다.|  
|*오류*|Null 키 오류를 발생시킵니다. 값 [NullKeyNotAllowed](../../../analysis-services/scripting/properties/nullkeynotallowed-element-assl.md) 은 인스턴스가 오류에 반응 하는 방식을 결정 합니다.<br /><br /> 참고:이 값은 측정값에 대 한 지원 되지 않습니다.|  
|*UnknownMember*|알 수 없는 멤버를 생성하고 Null 변환 오류를 발생시킵니다. 값 [NullKeyConvertedToUnknown](../../../analysis-services/scripting/properties/nullkeyconvertedtounknown-element-assl.md) 은 인스턴스가 오류에 반응 하는 방식을 결정 합니다.<br /><br /> 참고:이 값은 측정값에 연결 된 열에 대 한 지원 되지 않습니다.|  
|*ZeroOrBlank*|Null 값을 0(숫자 데이터 항목의 경우) 또는 빈 문자열(문자열 데이터 항목의 경우)로 변환합니다.<br /><br /> 참고:이 값을 이전 버전과의 호환성을 제공 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|*자동*|다음과 같이 요소에 적합한 기본 처리를 사용합니다.<br /><br /> OLAP 데이터 항목의 경우*ZeroOrBlank* <br /><br /> 데이터 마이닝 데이터 항목의 경우*UnknownMember* |  
  
 에 대 한 허용된 된 값에 해당 하는 열거형 **NullProcessing** Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.NullProcessing>합니다.  
  
## <a name="see-also"></a>관련 항목:  
 [속성 &#40; ASSL &#41;](../../../analysis-services/scripting/properties/properties-assl.md)  
  
  
