---
title: DiagnosticInformation 요소 (ssbdiagnose) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: a6dfc3946f0087b65699968448bdb1c014750572
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48194891"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 요소(ssbdiagnose)
  **DiagnosticInformation** 요소에는  유틸리티가 발견한 진단 정보를 보고하는 모든 요소가 포함됩니다. **DiagnosticInformation** 은 **ssbdiagnostic** XML 출력 파일의 루트 요소입니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<DiagnosticInformation>   
    ...   
</DiagnosticInformation>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
|attribute|Description|  
|---------------|-----------------|  
|`None`|해당 사항 없음|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**ssbdiagnose** XML 출력 파일당 한 번|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|없음|  
|**자식 요소**|[Banner 요소 &#40;ssbdiagnose&#41;](banner-element-ssbdiagnose.md)<br /><br /> [Issue 요소 &#40;ssbdiagnose&#41;](issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>Remarks  
 XML 네임스페이스에 대한 자세한 내용은 [MSDN Library의](http://go.microsoft.com/fwlink/?LinkId=7341) XML 문서의 네임스페이스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하십시오.  
  
## <a name="see-also"></a>관련 항목  
 [ssbdiagnose 유틸리티&#40;Service Broker&#41;](ssbdiagnose-utility-service-broker.md)  
  
  
