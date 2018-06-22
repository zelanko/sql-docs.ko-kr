---
title: NullProcessing 요소 (ASSL) | Microsoft Docs
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
- NullProcessing Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- NullProcessing
helpviewer_keywords:
- NullProcessing element
ms.assetid: 697be5c6-e9a6-4f74-9ff4-5f31400c2178
caps.latest.revision: 35
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 54b75b2e1a7bddd6f7b5df1aeda0311c1b60ff99
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080058"
---
# <a name="nullprocessing-element-assl"></a>NullProcessing Element (ASSL)
  Null 값이 처리되는 방식을 정의합니다.  
  
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
|부모 요소|[DataItem](../data-type/dataitem-data-type-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 이 요소의 값은 다음 표에 나열된 문자열 중 하나로 제한됩니다.  
  
|값|Description|  
|-----------|-----------------|  
|*유지*|Null 값을 유지합니다. **참고:** 이 값은 고유 카운트 측정값에 대 한 지원 되지 않습니다.|  
|*오류*|Null 키 오류를 발생시킵니다. 값 [NullKeyNotAllowed](nullkeynotallowed-element-assl.md) 은 인스턴스가 오류에 반응 하는 방식을 결정 합니다. **참고:** 측정값에 대 한이 값은 지원 되지 않습니다.|  
|*UnknownMember*|알 수 없는 멤버를 생성하고 Null 변환 오류를 발생시킵니다. 값 [NullKeyConvertedToUnknown](nullkeyconvertedtounknown-element-assl.md) 은 인스턴스가 오류에 반응 하는 방식을 결정 합니다. **참고:** 측정값에 연결 된 열에 대 한이 값은 지원 되지 않습니다.|  
|*ZeroOrBlank*|Null 값을 0(숫자 데이터 항목의 경우) 또는 빈 문자열(문자열 데이터 항목의 경우)로 변환합니다. **참고:** 이 값은 이전 버전과의 호환성을 제공 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.|  
|*자동*|다음과 같이 요소에 적합한 기본 처리를 사용합니다.<br /><br /> -   *ZeroOrBlank* OLAP 데이터 항목입니다.<br />-   *UnknownMember* 데이터 마이닝 데이터 항목에 대 한 합니다.|  
  
 AMO(Analysis Management Objects) 개체 모델에서 `NullProcessing`에 대해 허용된 값에 해당하는 열거형은 <xref:Microsoft.AnalysisServices.NullProcessing>입니다.  
  
## <a name="see-also"></a>관련 항목  
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  