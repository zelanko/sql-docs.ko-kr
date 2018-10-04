---
title: LogFileName 요소 (ASSL) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
- docset-sql-devref
ms.topic: reference
api_name:
- LogFileName Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileName
helpviewer_keywords:
- LogFileName element
ms.assetid: 80c7530d-ef73-44c3-88b5-c11c0f290946
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 14f2ae0f1d90459bbe7d1fc1b80e43847c15c1b3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48174323"
---
# <a name="logfilename-element-assl"></a>LogFileName 요소(ASSL)
  에 대 한 로그 파일의 파일 이름을 포함 합니다 [추적](../objects/trace-element-assl.md) 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Trace>  
   ...  
   <LogFileName>...</LogFileName>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|String|  
|기본값|없음|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[추적](../objects/trace-element-assl.md)|  
|자식 요소|없음|  
  
## <a name="remarks"></a>Remarks  
 인스턴스의 Log 폴더에 로그 파일이 저장 됩니다 [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]합니다.  
  
 부모에 해당 하는 요소가 `LogFileName` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Trace>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 추적 합니다. &#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  
