---
title: TuningTimeInMin 요소(DTA)
description: dta 유틸리티에서 TuningTimeInMin 요소는 튜닝 세션의 최대 길이(분)를 지정합니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
dev_langs:
- XML
helpviewer_keywords:
- TuningTimeInMin element
ms.assetid: 4973d9ac-20fd-4ac3-bc9f-5d60e39fdb7d
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: d4e7443a3263ac580b5619b6f44b5ad8dea8823f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85731992"
---
# <a name="tuningtimeinmin-element-dta"></a>TuningTimeInMin 요소(DTA)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

튜닝 세션의 최대 길이(분)를 지정합니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DTAInput>  
...code removed...  
    <TuningOptions>  
      <TuningTimeInMin>...</TuningTimeInMin>  
```  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**unsignedInt**, 길이 제한 없음|  
|**기본값**|480분(8시간)|  
|**발생 빈도**|**NumberOfEvents** 요소에 값을 지정하지 않은 경우 지정해야 합니다.|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[TuningOptions 요소&#40;DTA&#41;](../../tools/dta/tuningoptions-element-dta.md)|  
|**자식 요소**|None|  
  
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
  
## <a name="see-also"></a>참고 항목  
 [XML 입력 파일 참조&#40;데이터베이스 엔진 튜닝 관리자&#41;](../../tools/dta/xml-input-file-reference-database-engine-tuning-advisor.md)  
  
  
