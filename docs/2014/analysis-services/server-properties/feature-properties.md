---
title: 기능 속성 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQMSupportEnabled property
- ComUdfEnabled property
- LinkToOtherInstanceEnabled property
- ManagedCodeEnabled property
- ConnStringEncryptionEnabled property
- LinkFromOtherInstanceEnabled property
- LinkInsideInstanceEnabled property
- UseCachedPageAllocators property
ms.assetid: a34d046a-6562-4d98-b827-37cebc6d77b4
caps.latest.revision: 20
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 7c91c6d037bbb01c47f22159d846b40f8e1bbcca
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36093846"
---
# <a name="feature-properties"></a>기능 속성
  기능 속성은 서버 인스턴스 간 연결을 제어하는 속성을 비롯한 제품 기능(대부분 고급 기능)에 해당합니다.  
  
 [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] 에서는 다음 표에 나열된 서버 속성을 지원합니다. 추가 서버 속성 및 해당 속성 설정 방법은 [Configure Server Properties in Analysis Services](server-properties-in-analysis-services.md)을 참조하세요.  
  
 **적용 대상:** 다차원 서버 모드에만 적용됩니다.  
  
## <a name="properties"></a>속성  
  
|속성|Default|Description|  
|--------------|-------------|-----------------|  
|`ManagedCodeEnabled`|1|CLR 저장소 프로시저가 설정되어 있는지 여부를 나타내는 부울 속성입니다.|  
|`LinkInsideInstanceEnabled`|1|연결된 개체를 동일 서버 인스턴스 내에 만들 수 있는지 여부를 나타내는 부울 속성입니다.|  
|`LinkToOtherInstanceEnabled`|0|원격 서버의 개체를 연결할 수 있는지 여부를 나타내는 부울 속성입니다.|  
|`LinkFromOtherInstanceEnabled`|0|개체를 다른 서버 인스턴스로부터 연결할 수 있는지 여부를 나타내는 부울 속성입니다.|  
|`ConnStringEncryptionEnabled`|1|연결 문자열이 서버 구성 파일에 암호화되어 있는지 여부를 나타내는 부울 속성입니다.|  
|`UseCachedPageAllocators`|0|캐시된 페이지 할당자가 설정되어 있는지 여부를 나타내는 부울 속성입니다.|  
|`ComUdfEnabled`|0|COM 개체로 정의된 사용자 정의 함수가 설정되어 있는지 여부를 나타내는 부울 속성입니다.|  
|`SQMSupportEnabled`|1|오류 및 기능 사용 보고서를 [!INCLUDE[msCoName](../../includes/msconame-md.md)] 로 자동으로 보낼지 여부를 나타내는 부울 속성입니다.|  
|`ResourceMonitoringEnabled`|1|내부 리소스 모니터링 카운터를 사용할 수 있는지 여부를 나타내는 부울 속성입니다. 이 속성은 기본적으로 설정되어 있습니다. 이 속성을 사용하도록 설정되어 있으면 카운터에서 CPU, 메모리 및 I/O 작업에 대한 사용 데이터를 수집할 수 있습니다.<br /><br /> 내부 리소스 모니터링 카운터는 리소스 사용률에 대해 보고하는 DMV(동적 관리 뷰)에서 사용됩니다. 이 속성을 사용하지 않도록 설정하는 경우 DMV 쿼리는 계속 실행되지만 결과 집합은 유효하지 않은 상태가 됩니다. 이 속성에 따라 달라지는 DMV는 다음과 같습니다.<br />**DISCOVER_OBJECT_ACTIVITY**<br />**DISCOVER_COMMAND_OBJECTS**<br />**DISCOVER_SESSIONS** (SESSION_READS, SESSION_WRITES, SESSION_CPU_TIME_MS의 경우)<br /><br /> <br /><br /> NUMA 아키텍처를 사용하는 다중 코어 시스템에서 이 속성을 사용하지 않도록 설정하면 특히 다중 사용자 작업량이 많은 경우 쿼리 성능이 향상될 수 있습니다. 이 속성을 변경한 결과로 쿼리 성능이 향상되는지 여부를 확인하려면 비교 테스트를 실행해야 합니다. 캐시를 지우고 일반적인 실수를 피하는 등 비교 테스트 실행에 대한 최상의 방법을 보려면 [SQL Server 2008 R2 Analysis Services 작업 가이드](http://go.microsoft.com/fwlink/?LinkID=225539)를 참조하십시오.|  
  
## <a name="see-also"></a>관련 항목  
 [Analysis Services에서 서버 속성 구성](server-properties-in-analysis-services.md)   
 [Analysis Services 인스턴스의 서버 모드 확인](../instances/determine-the-server-mode-of-an-analysis-services-instance.md)   
 [동적 관리 뷰를 사용 하 여 &#40;Dmv&#41; Services 분석을 모니터링 하려면](../instances/use-dynamic-management-views-dmvs-to-monitor-analysis-services.md)  
  
  