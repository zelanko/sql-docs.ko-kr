---
title: DiagnosticInformation 요소
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- XML output file format [ssbdiagnose], diagnosticinformation element
- diagnosticinformation element
- ssbdiagnose
ms.assetid: 0cfda544-542c-4cf4-86d2-8031c91b10f6
author: markingmyname
ms.author: maghan
ms.manager: jroth
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.openlocfilehash: 06d67e0a20067390c14837221725fd4b27c8c337
ms.sourcegitcommit: b78f7ab9281f570b87f96991ebd9a095812cc546
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 01/31/2020
ms.locfileid: "75257790"
---
# <a name="diagnosticinformation-element-ssbdiagnose"></a>DiagnosticInformation 요소(ssbdiagnose)

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

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
|**없음**|해당 없음|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|없음|  
|**기본값**|없음|  
|**발생 빈도**|**ssbdiagnose** XML 출력 파일당 한 번|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|없음|  
|**자식 요소**|[Banner 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/banner-element-ssbdiagnose.md)<br /><br /> [Issue 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/issue-element-ssbdiagnose.md)|  
  
## <a name="remarks"></a>설명  
 XML 네임스페이스에 대한 자세한 내용은 [MSDN Library의](https://go.microsoft.com/fwlink/?LinkId=7341) XML 문서의 네임스페이스 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 를 참조하십시오.  
  
## <a name="see-also"></a>참고 항목  
 [ssbdiagnose 유틸리티&#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
