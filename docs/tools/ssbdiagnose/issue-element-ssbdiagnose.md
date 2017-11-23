---
title: "Issue 요소 (ssbdiagnose) | Microsoft Docs"
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
caps.latest.revision: "17"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 560df4e8124448a3b3672e9603ef9506572c71be
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/09/2017
---
# <a name="issue-element-ssbdiagnose"></a>Issue 요소(ssbdiagnose)
  **ssbdiagnose** 유틸리티가 발견한 문제를 보고합니다. **ssbdiagnose** XML 출력 파일에는 보고되는 문제 당 하나의 Issue 요소가 포함됩니다.  
  
## <a name="syntax"></a>구문  
  
```  
  
<Issue  
    type="..."   
    code="..."   
    server="..."   
    database="..."   
    object="...">   
    ...   
</Issue>  
```  
  
## <a name="element-attributes"></a>요소 특성  
  
|Attribute|설명|  
|---------------|-----------------|  
|**유형**|Issue 요소가 보고하는 문제의 범주를 식별합니다.<br /><br /> **"진단"** 보고서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 구성을 분석할 때 발견된 구성 문제를 보고합니다.<br /><br /> **"문제"** 는 **ssbdiagnose** 의 분석을 완료하지 못하게 하는 문제를 보고합니다. 문제를 해결하고 **ssbdiagnose**를 다시 실행하십시오.<br /><br /> **"이벤트"** 는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -RUNTIME **검사를 실행할 때 발견된** 이벤트를 보고합니다. 단, **-SHOWEVENTS** 가 지정된 경우에만 이벤트가 보고됩니다.|  
|**코드**|메시지의 오류 번호를 식별합니다.|  
|**서버**|문제가 발견된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 식별합니다. 문제가 기본 인스턴스에서 발견된 경우에는 서버 특성에 컴퓨터 이름만 포함되고 문제가 명명된 인스턴스에서 발견된 경우에는 서버 특성이 ComputerName\InstanceName 형식으로 지정됩니다.|  
|**데이터베이스**|문제가 발견된 데이터베이스의 이름을 식별합니다.|  
|**개체(object)**|문제가 발견된 개체의 이름을 식별합니다. 문제가 인스턴스 또는 데이터베이스 수준에서 발견된 경우 개체 특성이 인스턴스 또는 데이터베이스 이름을 반복합니다.|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특징|설명|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**값**|오류 메시지 텍스트를 반환합니다.|  
|**발생 빈도**|보고되는 오류 당 한 번|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DiagnosticInformation 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**자식 요소**|없음|  
  
## <a name="example"></a>예제  
 이 요소는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 구성을 분석할 때 오류가 발견되었으며 마스터 키가 없는 데이터베이스에 대해 1102 오류를 보고합니다.  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>참고 항목  
 [ssbdiagnose 유틸리티&#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
