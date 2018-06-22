---
title: LogFileRollover 요소 (ASSL) | Microsoft Docs
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
- LogFileRollover Element
api_location:
- http://schemas.microsoft.com/analysisservices/2003/engine
topic_type:
- apiref
f1_keywords:
- LogFileRollover
helpviewer_keywords:
- LogFileRollover element
ms.assetid: 5484e167-b891-431a-bbae-946ea6eb4a3c
caps.latest.revision: 34
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 4ecaf972c701175d388ab71fa61d94de1c6f2cad
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36080510"
---
# <a name="logfilerollover-element-assl"></a>LogFileRollover 요소(ASSL)
  지정의 로깅을 [추적](../objects/trace-element-assl.md) 해야에 지정 된 최대 로그 파일 크기를 중지할지 또는 출력을 새 파일로 롤오버할 [LogFileSize](logfilesize-element-assl.md) 에 도달 합니다.  
  
## <a name="syntax"></a>구문  
  
```xml  
  
<Trace>  
   ...  
   <LogFileRollover>...</LogFileRollover>  
   ...  
</Trace>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|데이터 형식 및 길이|Boolean|  
|기본값|False|  
|카디널리티|0-1: 한 번만 나타날 수 있는 선택적 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|-------------|  
|부모 요소|[추적](../objects/trace-element-assl.md)|  
|자식 요소|InclusionThresholdSetting|  
  
## <a name="remarks"></a>Remarks  
 `LogFileRollover` 요소의 값을 True로 설정하면 로그 파일의 크기가 `LogFileSize` 부모 요소의 `Trace` 요소에 지정된 값을 초과할 경우 새 파일이 시작됩니다. 그렇지 않으면 로깅이 중지됩니다.  
  
 부모에 해당 하는 요소 `LogFileRollover` Analysis Management Objects (AMO) 개체 모델은 <xref:Microsoft.AnalysisServices.Trace>합니다.  
  
## <a name="see-also"></a>관련 항목  
 [요소를 추적 &#40;ASSL&#41;](../collections/traces-element-assl.md)   
 [속성 &#40;ASSL&#41;](properties-assl.md)  
  
  