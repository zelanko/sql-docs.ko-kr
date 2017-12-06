---
title: "SQL Server Profiler로 교착 상태 분석 | Microsoft Docs"
ms.custom: 
ms.date: 03/03/2017
ms.prod: sql-non-specified
ms.prod_service: sql-non-specified
ms.service: 
ms.component: sql-server-profiler
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- process nodes [SQL Server Profiler]
- Profiler [SQL Server Profiler], deadlocks
- deadlocks [SQL Server], identifying cause
- resource nodes [SQL Server Profiler]
- graphs [SQL Server Profiler]
- SQL Server Profiler, deadlocks
- events [SQL Server], deadlocks
- edges [SQL Server Profiler]
ms.assetid: 72d6718f-501b-4ea6-b344-c0e653f19561
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 7c0de1737702872b1d692a5489afbd4c64eba499
ms.sourcegitcommit: b2d8a2d95ffbb6f2f98692d7760cc5523151f99d
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/05/2017
---
# <a name="analyze-deadlocks-with-sql-server-profiler"></a>SQL Server Profiler를 사용하여 교착 상태 분석
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]사용 하 여 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 교착 상태의 원인을 확인 합니다. 둘 이상의 스레드 또는 프로세스 간에 SQL Server 내의 일부 리소스에 대한 순환 종속성이 있는 경우 교착 상태가 발생합니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)]를 사용하여 교착 상태 이벤트를 기록하고 재생하고 표시하는 추적을 만들어 분석할 수 있습니다.  
  
 교착 상태 이벤트를 추적하려면 **Deadlock graph** 이벤트 클래스를 추적에 추가합니다. 이 이벤트 클래스는 교착 상태와 관련된 프로세스 및 개체에 대한 XML 데이터로 추적 시 **TextData** 데이터 열을 채웁니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 는 XML 문서를 교착 상태 XML(.xdl) 파일로 추출할 수 있습니다. 이 XML 파일은 나중에 SQL Server Management Studio에서 볼 수 있습니다. [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 를 구성하여 모든 **Deadlock graph** 이벤트가 포함되어 있는 단일 파일로 **Deadlock graph** 이벤트를 추출하거나 개별 파일로 추출할 수도 있습니다. 다음과 같은 방법으로 추출할 수 있습니다.  
  
-   추적 구성 시 **이벤트 추출 설정** 탭을 사용합니다. **이벤트 선택** 탭에서 **Deadlock graph** 이벤트를 선택해야만 이 탭이 표시됩니다.  
  
-   **파일** 메뉴에서 **SQL Server 이벤트 추출** 옵션을 사용합니다.  
  
-   개별 이벤트는 특정 이벤트를 마우스 오른쪽 단추로 클릭하고 **이벤트 데이터 추출**을 선택하여 추출 및 저장할 수도 있습니다.  
  
## <a name="deadlock-graphs"></a>교착 상태 그래프  
 [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] 와 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 는 교착 상태 WAITFOR 그래프를 사용하여 교착 상태를 설명합니다. 교착 상태 WAITFOR 그래프에는 프로세스 노드, 리소스 노드 및 프로세스와 리소스 간의 관계를 나타내는 가장자리가 포함됩니다. WAITFOR 그래프의 구성 요소는 다음 표에 정의되어 있습니다.  
  
 프로세스 노드  
 태스크를 수행하는 스레드입니다. 예를 들어 INSERT, UPDATE 또는 DELETE입니다.  
  
 리소스 노드  
 데이터베이스 개체입니다. 예를 들어 테이블, 인덱스 또는 행입니다.  
  
 가장자리  
 프로세스와 리소스 간의 관계입니다. **request** 가장자리는 프로세스가 리소스를 대기할 때 발생합니다. **owner** 가장자리는 리소스가 프로세스를 대기할 때 발생합니다. 잠금 모드는 가장자리 설명에 포함되어 있습니다. 예를 들어 **Mode: X**입니다.  
  
## <a name="deadlock-process-node"></a>교착 상태 프로세스 모드  
 WAITFOR 그래프에서 프로세스 노드는 프로세스에 대해 설명합니다. 다음 표에서는 프로세스의 구성 요소에 대해 설명합니다.  
  
|구성 요소|정의|  
|---------------|----------------|  
|서버 프로세스 ID|SPID(서버 프로세스 식별자)는 서버가 잠금을 소유하고 있는 프로세스에 할당한 식별자입니다.|  
|서버 일괄 처리 ID|SBID(서버 일괄 처리 식별자)입니다.|  
|실행 컨텍스트 ID|ECID(실행 컨텍스트 식별자)입니다. 특정 SPID와 관련된 주어진 스레드의 실행 컨텍스트 ID입니다.<br /><br /> ECID = {0,1,2,3, *...n*}이며 여기서 0은 항상 주 또는 부모 스레드를 의미하고 {1,2,3, *...n*}은 하위 스레드를 의미합니다.|  
|교착 상태 우선 순위|프로세스의 교착 상태 우선 순위입니다. 가능한 값에 대한 자세한 내용은 [SET DEADLOCK_PRIORITY&#40;Transact-SQL&#41;](../../t-sql/statements/set-deadlock-priority-transact-sql.md)를 참조하세요.|  
|사용된 로그|프로세스가 사용한 로그 공간입니다.|  
|소유자 ID|트랜잭션을 사용 중이고 잠금에 대해 현재 대기 중인 프로세스의 트랜잭션 ID입니다.|  
|트랜잭션 설명자|트랜잭션 상태를 설명하는 트랜잭션 설명자에 대한 포인터입니다.|  
|입력 버퍼|현재 프로세스의 입력 버퍼. 이벤트의 유형과 실행 중인 문을 정의합니다. 가능한 값은 다음과 같습니다.<br /><br /> **언어**<br /><br /> **RPC**<br /><br /> **없음**|  
|문|문 유형. 가능한 값은<br /><br /> **NOP**<br /><br /> **SELECT**<br /><br /> **UPDATE**<br /><br /> **INSERT**<br /><br /> **DELETE**<br /><br /> **Unknown**|  
  
## <a name="deadlock-resource-node"></a>교착 상태 리소스 노드  
 두 프로세스가 각각 다른 프로세스에서 소유하고 있는 리소스를 대기하고 있는 상태가 교착 상태입니다. 교착 상태 그래프에서 리소스는 리소스 노드로 표시됩니다.  
  
  
