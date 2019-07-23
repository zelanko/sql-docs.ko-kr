---
title: 전역 추적 옵션 설정 (SQL Server Profiler) | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: sql-tools
ms.reviewer: ''
ms.technology: profiler
ms.topic: conceptual
helpviewer_keywords:
- global trace options [SQL Server]
ms.assetid: 2854608a-c3c7-4eb8-b567-034bfec4b1a9
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 9605f5e12b1dcc206d50e958d8c1787750e98941
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MTE75
ms.contentlocale: ko-KR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104182"
---
# <a name="set-global-trace-options-sql-server-profiler"></a>전역 추적 옵션 설정(SQL Server Profiler)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  이 항목에서는 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]의 특정 인스턴트로 생성되는 모든 추적에 적용되는 옵션을 설정하는 방법에 대해 설명합니다.  
  
### <a name="to-set-global-trace-options"></a>전역 추적 옵션을 설정하려면  
  
1.  **도구** 메뉴에서 **옵션**을 클릭합니다.  
  
2.  **일반 옵션**대화 상자에서 **글꼴 선택**을 클릭하여 표시 옵션을 수정한 다음 **확인**을 클릭합니다.  
  
3.  필요에 따라 **연결한 후 즉시 추적 시작**을 선택합니다.  
  
4.  필요에 따라 **공급자 버전 변경 시 추적 정의 업데이트**를 선택합니다. 이 옵션은 사용하는 것이 좋으며 기본적으로 선택되어 있습니다. 이 옵션을 선택하면 추적 정의가 추적을 수행 중인 현재 버전의 서버로 자동으로 업데이트됩니다.  
  
5.  필요에 따라 서버가 롤오버 파일을 관리하는 방법을 지정합니다.  
  
    -   **확인하지 않고 모든 롤오버 파일을 순서대로 로드** 를 선택하면 재생 시 롤오버 파일을 자동으로 로드할 수 있습니다.  
  
    -   **롤오버 파일 로드 전에 확인** 을 선택하면 재생 시 롤오버 파일을 제어할 수 있습니다.  
  
    -   **다음 롤오버 파일 로드 안 함** 을 선택하면 한 번에 한 개의 파일만 재생할 수 있습니다.  
  
6.  필요에 따라 재생 옵션을 설정합니다.  
  
    -   **기본 재생 스레드 수** 는 재생 중 사용할 프로세서 스레드 수를 제어합니다. 스레드 수가 높을수록 재생이 더 빨리 완료되지만 재생 시 서버 성능이 저하됩니다. **4**로 설정하는 것이 좋습니다. 다음 표에서는 사용 가능한 옵션을 나열합니다.  
  
        |값|설명|  
        |-----------|-----------------|  
        |**2**|최소값. 두 스레드를 사용하여 재생합니다.|  
        |**4**|기본값.|  
        |**255**|최대값. 최대값을 설정하면 다른 프로세스 성능이 저하됩니다.|  
  
    -   **기본 상태 모니터 대기 간격(초)** 은 재생 스레드가 다른 프로세스를 차단할 수 있는 최대 시간(초)을 설정합니다. 다음 표에서는 값을 설명합니다.  
  
        |값|설명|  
        |-----------|-----------------|  
        |**0**|최소값. **0** 은 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 차단 프로세스를 절대로 중지하지 않음을 의미합니다.|  
        |**3600**|기본값. **3600** 초 또는 한 시간을 초과하지 않는 차단 프로세스를 허용합니다.|  
        |**86400**|최대값. **86400** 초 또는 하루를 초과하지 않는 차단 프로세스를 허용합니다.|  
  
    -   **기본 상태 모니터 폴링 간격(초)** 은 차단 프로세스용 재생 스레드를 폴링하는 빈도를 설정합니다. 다음 표에서는 값을 설명합니다.  
  
        |값|설명|  
        |-----------|-----------------|  
        |**1**|최소값. **1** 은 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 가 차단 프로세스를 초당 하나만 폴링함을 의미합니다.|  
        |**60**|기본값. 차단 프로세스를 _분당 하나만 폴링합니다.|  
        |**86400**|최대값. 차단 프로세스를 **86400** 초당 또는 하루에 하나만 폴링합니다.|  
  
## <a name="see-also"></a>참고 항목  
 [추적 표시 기본값 설정&#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/set-trace-display-defaults-sql-server-profiler.md)   
 [SQL Server 프로파일러](../../tools/sql-server-profiler/sql-server-profiler.md)  
  
  
