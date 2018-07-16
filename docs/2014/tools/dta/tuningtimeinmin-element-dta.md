---
title: TuningTimeInMin 요소 (DTA) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningTimeInMin element
ms.assetid: 4973d9ac-20fd-4ac3-bc9f-5d60e39fdb7d
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 82821b8f8cc728c8b2f15d92af1496714414ea40
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37304640"
---
# <a name="tuningtimeinmin-element-dta"></a>TuningTimeInMin 요소(DTA)
  튜닝 세션의 최대 길이(분)를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <TuningTimeInMin>...</TuningTimeInMin>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|`unsignedInt`길이 제한 없음된.|  
|**기본값**|480분(8시간)|  
|**발생 빈도**|에 대 한 값을 지정 하지 않는 필요는 `NumberOfEvents` 요소입니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소 &#40;DTA&#41;](tuningoptions-element-dta.md)|  
|**자식 요소**|InclusionThresholdSetting|  
  
## <a name="example"></a>예제  
  
## <a name="description"></a>Description  
 다음 코드 예에서는 최대 튜닝 시간을 12시간으로 설정하는 방법을 보여 줍니다.  
  
## <a name="code"></a>코드  
  
```  
<DTAInput>  
  <Server>...</Server>  
  <Workload>...</Workload>  
  <TuningOptions>  
    <TuningTimeInMin>720</TuningTimeInMin>  
...code removed here...  
</DTAInput>  
```  
  
## <a name="see-also"></a>관련 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
