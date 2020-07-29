---
title: Issue 요소
description: SQL Server에서 Issue 요소는 ssbdiagnose 유틸리티에서 발견한 문제를 보고합니다. XML 출력 파일에는 보고되는 문제당 하나의 Issue 요소가 포함됩니다.
ms.prod: sql
ms.prod_service: sql-tools
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- issue element
- XML output file format [ssbdiagnose], issue element
- ssbdiagnose
ms.assetid: 2246a886-686b-44ca-9771-b155cedad8be
author: markingmyname
ms.author: maghan
ms.reviewer: ''
ms.custom: seo-lt-2019
ms.date: 03/01/2017
ms.openlocfilehash: 56f677836fb1bd7fc28baf75de2abcb5fea56b7e
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85726801"
---
# <a name="issue-element-ssbdiagnose"></a>Issue 요소(ssbdiagnose)

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

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
  
|attribute|Description|  
|---------------|-----------------|  
|**type**|Issue 요소가 보고하는 문제의 범주를 식별합니다.<br /><br /> **"진단"** 보고서는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 구성을 분석할 때 발견된 구성 문제를 보고합니다.<br /><br /> **"문제"** 는 **ssbdiagnose** 의 분석을 완료하지 못하게 하는 문제를 보고합니다. 문제를 해결하고 **ssbdiagnose**를 다시 실행하십시오.<br /><br /> **"이벤트"** 는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] -RUNTIME **검사를 실행할 때 발견된** 이벤트를 보고합니다. 단, **-SHOWEVENTS** 가 지정된 경우에만 이벤트가 보고됩니다.|  
|**code**|메시지의 오류 번호를 식별합니다.|  
|**server**|문제가 발견된 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 인스턴스를 식별합니다. 문제가 기본 인스턴스에서 발견된 경우에는 서버 특성에 컴퓨터 이름만 포함되고 문제가 명명된 인스턴스에서 발견된 경우에는 서버 특성이 ComputerName\InstanceName 형식으로 지정됩니다.|  
|**database**|문제가 발견된 데이터베이스의 이름을 식별합니다.|  
|**object**|문제가 발견된 개체의 이름을 식별합니다. 문제가 인스턴스 또는 데이터베이스 수준에서 발견된 경우 개체 특성이 인스턴스 또는 데이터베이스 이름을 반복합니다.|  
  
## <a name="element-characteristics"></a>요소 특징  
  
|특성|Description|  
|--------------------|-----------------|  
|**데이터 형식 및 길이**|**string**, 길이 제한 없음|  
|**값**|오류 메시지 텍스트를 반환합니다.|  
|**발생 빈도**|보고되는 오류 당 한 번|  
  
## <a name="element-relationships"></a>요소 관계  
  
|관계|요소|  
|------------------|--------------|  
|**부모 요소**|[DiagnosticInformation 요소&#40;ssbdiagnose&#41;](../../tools/ssbdiagnose/diagnosticinformation-element-ssbdiagnose.md)|  
|**자식 요소**|None|  
  
## <a name="example"></a>예제  
 이 요소는 [!INCLUDE[ssSB](../../includes/sssb-md.md)] 구성을 분석할 때 오류가 발견되었으며 마스터 키가 없는 데이터베이스에 대해 1102 오류를 보고합니다.  
  
```  
<Issue type="Diagnosis" code="1102" server="TestComputer" database="TargetDB" object="TargetDB">The master key was not found</diagnostic>  
```  
  
## <a name="see-also"></a>참고 항목  
 [ssbdiagnose 유틸리티&#40;Service Broker&#41;](../../tools/ssbdiagnose/ssbdiagnose-utility-service-broker.md)  
  
  
