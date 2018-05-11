---
title: OOM(메모리 부족) 문제 해결 | Microsoft 문서
ms.custom: ''
ms.date: 12/21/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: in-memory-oltp
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
caps.latest.revision: 18
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 9074089595162fd36d3a2aecadaf1306df968240
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="resolve-out-of-memory-issues"></a>OOM(메모리 부족) 문제 해결
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다른 방법으로 더 많은 메모리를 사용합니다. 필요 증가에 따라 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 에 대해 설치하고 할당한 메모리의 양이 불충분해질 수 있습니다. 이 경우 메모리가 부족해질 수 있습니다. 이 항목에서는 OOM 상황에서 복구하는 방법을 설명합니다. 여러 OOM 상황을 방지하는 데 도움이 될 수 있는 지침은 [메모리 사용량 모니터링 및 문제 해결](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md) 을 참조하세요.  
  
## <a name="covered-in-this-topic"></a>이 항목의 내용  
  
|항목|개요|  
|-----------|--------------|  
|[OOM으로 인한 데이터베이스 복원 실패 해결](#bkmk_resolveRecoveryFailures)|“'*\<resourcePoolName>*' 리소스 풀의 메모리 부족으로 인해 '*\<databaseName>*' 데이터베이스에 대한 복원 작업이 실패했습니다.”라는 오류 메시지가 나타나는 경우 수행할 작업입니다.|  
|[메모리 부족 또는 OOM 상황이 작업에 미치는 영향 해결](#bkmk_recoverFromOOM)|메모리 부족 문제가 성능에 부정적인 영향을 미치고 있음을 발견할 경우 수행할 작업입니다.|  
|[사용 가능한 메모리가 충분한 경우 메모리 부족으로 인한 페이지 할당 오류 해결](#bkmk_PageAllocFailure)|작업에 사용할 수 있는 메모리가 충분한데 “'*\<resourcePoolName>*' 리소스 풀의 메모리 부족으로 인해 '*\<databaseName>*' 데이터베이스에 대해 페이지를 할당할 수 없습니다. …” 오류 메시지가 나타나는 경우 수행할 작업입니다.|
|[최선의 구현 방법: VM 환경에서 메모리 내 OLTP 사용](#bkmk_VMs)|가상화된 환경에서 메모리 내 OLTP를 사용할 때의 참고 사항입니다.|
  
##  <a name="bkmk_resolveRecoveryFailures"></a> OOM으로 인한 데이터베이스 복원 실패 해결  
 데이터베이스 복원을 시도하면 "'*\<resourcePoolName>*' 리소스 풀의 메모리 부족으로 인해 *\<databaseName>*' 데이터베이스에 대한 복원 작업이 실패했습니다."라는 오류 메시지가 나타날 수 있습니다. 이 오류는 서버에 데이터베이스를 복원하는 데 충분히 사용 가능한 메모리가 없는 것을 나타냅니다. 
   
데이터베이스를 복원할 서버에는 데이터베이스 백업 시 메모리 최적화 테이블에 대해 충분한 사용 가능한 메모리가 있어야 합니다. 그렇지 않으면 데이터베이스가 온라인 상태가 되지 않으며 주의 대상으로 표시됩니다.  
  
서버에 충분한 실제 메모리가 있지만 이 오류가 계속 나타나면 다른 프로세스에서 너무 많은 메모리를 사용하거나, 구성 문제로 복원에 사용할 수 있는 메모리가 충분하지 않을 수 있습니다. 이 문제 유형의 경우 다음 조치를 수행하여 복원 작업에 필요한 메모리를 더 많이 확보하세요. 
  
-   실행 중인 응용 프로그램을 일시적으로 닫습니다.   
    실행 중인 응용 프로그램을 하나 이상 닫거나 현재 필요 없는 서비스를 중지하여 해당 응용 프로그램에서 사용 중인 메모리를 복원 작업에 사용할 수 있습니다. 성공적으로 복원한 후 해당 응용 프로그램을 다시 시작할 수 있습니다.  
  
-   MAX_MEMORY_PERCENT의 값을 늘립니다.   
    데이터베이스가 [리소스 풀에 바인딩된](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)경우 복원에 사용할 수 있는 메모리는 MAX_MEMORY_PERCENT에서 관리됩니다(모범 사례). 값이 너무 작으면 복원이 실패합니다. 이 코드 조각은 PoolHk 리소스 풀에 대한 MAX_MEMORY_PERCENT를 설치된 메모리의 70%로 변경합니다.  
  
    > [!IMPORTANT]  
    > 서버가 VM에서 실행 중이고 전용 서버가 아니면 MIN_MEMORY_PERCENT 값을 MAX_MEMORY_PERCENT와 동일한 값으로 설정합니다.   
    > 자세한 내용은 [최선의 구현 방법: VM 환경에서 메모리 내 OLTP 사용](#bkmk_VMs) 항목을 참조하세요.  
  
    ```sql  
    -- disable resource governor  
    ALTER RESOURCE GOVERNOR DISABLE  
  
    -- change the value of MAX_MEMORY_PERCENT  
    ALTER RESOURCE POOL PoolHk  
    WITH  
         ( MAX_MEMORY_PERCENT = 70 )  
    GO  
  
    -- reconfigure the Resource Governor  
    --    RECONFIGURE enables resource governor  
    ALTER RESOURCE GOVERNOR RECONFIGURE  
    GO  
  
    ```  
  
     MAX_MEMORY_PERCENT의 최대값에 대한 자세한 내용은 항목 섹션 [메모리 최적화 테이블 및 인덱스에 사용 가능한 메모리 비율](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)을 참조하세요.  
  
-   **최대 서버 메모리**를 늘립니다.  
    **최대 서버 메모리** 구성에 대한 자세한 내용은 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 항목을 참조하세요.  
  
##  <a name="bkmk_recoverFromOOM"></a> 메모리 부족 또는 OOM 상황이 작업에 미치는 영향 해결  
 물론 OOM(메모리 부족) 상황에 빠지지 않는 것이 최선입니다. 적절한 계획과 모니터링을 통해 OOM 상황을 방지할 수 있습니다. 그렇지만 최상의 계획을 세우더라도 실제 발생하는 상황을 항상 예측할 수 있는 것은 아니며 결국 메모리 부족 또는 OOM 상황에 도달할 수 있습니다. 다음 두 가지 방법으로 OOM에서 복구할 수 있습니다.  
  
1.  [DAC(관리자 전용 연결) 열기](#bkmk_openDAC)  
  
2.  [수정 조치 수행](#bkmk_takeCorrectiveAction)  
  
###  <a name="bkmk_openDAC"></a> DAC(관리자 전용 연결) 열기  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 DAC(관리자 전용 연결)를 제공합니다. DAC를 사용하면 관리자는 서버가 다른 클라이언트 연결에 응답하지 않는 경우에도 실행 중인 SQL Server 데이터베이스 엔진 인스턴스에 액세스하여 서버에서 문제를 해결할 수 있습니다. DAC는 `sqlcmd` 유틸리티 및 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 통해 사용할 수 있습니다.  
  
 SSMS 또는 `sqlcmd`를 통한 DAC 사용에 대한 지침은 [데이터베이스 관리자를 위한 진단 연결](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)을 참조하세요.  
  
###  <a name="bkmk_takeCorrectiveAction"></a> 수정 조치 수행  
 OOM 상태를 해결하려면 사용을 축소하여 기존 메모리를 확보하거나 더 많은 메모리를 메모리 내 테이블에 사용할 수 있게 만들어야 합니다.  
  
#### <a name="free-up-existing-memory"></a>기존 메모리 확보  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>필수적이지 않은 메모리 액세스에 최적화된 테이블 행을 삭제하고 가비지 수집 대기  
 메모리 액세스에 최적화된 테이블에서 필수적이지 않은 행을 제거할 수 있습니다. 가비지 수집기는 이러한 행에 사용되는 메모리를 사용 가능한 메모리로 되돌립니다. 메모리 내 OLTP 엔진은 가비지 행을 적극적으로 수집합니다. 그러나 장기 실행 트랜잭션으로 인해 가비지가 수집되지 않을 수 있습니다. 예를 들어, 5분간 실행되는 트랜잭션이 있는 경우 트랜잭션이 활성 상태인 동안 수행되는 업데이트/삭제 작업으로 생성된 모든 행 버전에 대해 가비지 수집이 수행되지 않을 수 있습니다.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>디스크 기반 테이블로 하나 이상의 행 이동  
 다음 TechNet 문서에는 메모리 최적화 테이블에서 디스크 기반 테이블로 행을 이동하는 방법이 나와 있습니다.  
  
-   [응용 프로그램 수준 분할](../../relational-databases/in-memory-oltp/application-level-partitioning.md)  
  
-   [메모리 액세스에 최적화된 테이블 분할을 위한 응용 프로그램 패턴](../../relational-databases/in-memory-oltp/application-pattern-for-partitioning-memory-optimized-tables.md)  
  
#### <a name="increase-available-memory"></a>사용 가능한 메모리 늘리기  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>리소스 풀에서 MAX_MEMORY_PERCENT의 값 늘리기  
 메모리 내 테이블에 대한 명명된 리소스 풀을 만들지 않은 경우 이 리소스 풀을 만들고 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 데이터베이스를 이 리소스 풀에 바인딩해야 합니다. 리소스 풀을 만들고 [데이터베이스를 리소스 풀에 바인딩하는 방법에 대한 지침은](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) 메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 항목을 참조하세요.  
  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 데이터베이스가 리소스 풀에 바인딩된 경우 풀에서 액세스할 수 있는 메모리 비율을 늘릴 수 있습니다. 리소스 풀을 위한 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT의 값 변경에 대한 지침은 하위 항목 [기존 풀에서 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 변경](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation) 을 참조하세요.  
  
 MAX_MEMORY_PERCENT의 값을 늘립니다.   
이 코드 조각은 PoolHk 리소스 풀에 대한 MAX_MEMORY_PERCENT를 설치된 메모리의 70%로 변경합니다.  
  
> [!IMPORTANT]  
>  서버가 VM에서 실행 중이고 전용 서버가 아니면 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 값을 동일한 값으로 설정합니다.   
> 자세한 내용은 [최선의 구현 방법: VM 환경에서 메모리 내 OLTP 사용](#bkmk_VMs) 항목을 참조하세요.  
  
```sql  
-- disable resource governor  
ALTER RESOURCE GOVERNOR DISABLE  
  
-- change the value of MAX_MEMORY_PERCENT  
ALTER RESOURCE POOL PoolHk  
WITH  
     ( MAX_MEMORY_PERCENT = 70 )  
GO  
  
-- reconfigure the Resource Governor to enabled it
ALTER RESOURCE GOVERNOR RECONFIGURE  
GO  
```  
  
 MAX_MEMORY_PERCENT의 최대값에 대한 자세한 내용은 항목 섹션 [메모리 최적화 테이블 및 인덱스에 사용 가능한 메모리 비율](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_PercentAvailable)을 참조하세요.  
  
##### <a name="install-additional-memory"></a>추가 메모리 설치  
 가능한 경우 궁극적으로 가장 좋은 해결 방법은 추가 실제 메모리를 설치하는 것입니다. 이렇게 할 경우 [에 더 이상 메모리 부족이 발생하지 않을 것이므로 MAX_MEMORY_PERCENT 값도 늘려서 새로 설치된 메모리 중 전부는 아니라도 대부분을 리소스 풀에 사용하도록 설정할 수 있습니다(하위 항목](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#bkmk_ChangeAllocation)기존 풀에서 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 변경 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 참조).  
  
> [!IMPORTANT]  
>  서버가 VM에서 실행 중이고 전용 서버가 아니면 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 값을 동일한 값으로 설정합니다.   
> 자세한 내용은 [최선의 구현 방법: VM 환경에서 메모리 내 OLTP 사용](#bkmk_VMs) 항목을 참조하세요.  
  
##  <a name="bkmk_PageAllocFailure"></a> 사용 가능한 메모리가 충분한 경우 메모리 부족으로 인한 페이지 할당 오류 해결  
 페이지를 할당하는 데 사용할 수 있는 물리적 메모리가 충분할 때 오류 로그에 오류 메시지 `Disallowing page allocations for database '*\<databaseName>*' due to insufficient memory in the resource pool '*\<resourcePoolName>*'. See 'http://go.microsoft.com/fwlink/?LinkId=330673' for more information.`가 나타나는 경우 이는 리소스 관리자를 사용하지 않기 때문일 수 있습니다. 리소스 관리자를 사용하지 않으면 MEMORYBROKER_FOR_RESERVE가 인위적인 메모리 압력을 유발합니다.  
  
 이 오류를 해결하려면 리소스 관리자를 사용하도록 설정해야 합니다.  
  
 개체 탐색기, 리소스 관리자 속성 또는 Transact-SQL로 리소스 관리자를 사용하도록 설정하는 지침과 제한 사항에 대한 자세한 내용은 [리소스 관리자 사용](../../relational-databases/resource-governor/enable-resource-governor.md) 을 참조하세요.  
 
## <a name="bkmk_VMs"></a> 최선의 구현 방법: VM 환경에서 메모리 내 OLTP 사용
서버 가상화 기술을 사용하면 IT 자본 및 운영 비용을 줄이고 향상된 응용 프로그램 프로비전, 유지 관리, 가용성 및 백업/복구 프로세스를 통해 IT 효율성을 높일 수 있습니다. 최근의 기술적 진보에 따라 가상화를 사용하면 복잡한 데이터베이스 작업도 보다 쉽고 간단하게 통합할 수 있습니다. 이 항목에서는 가상화된 환경에서 SQL Server In-Memory OLTP를 사용하기 위한 모범 사례에 대해 설명합니다.

### <a name="memory-pre-allocation"></a>메모리 사전 할당
가상화된 환경의 메모리에 대해 필수적으로 고려해야 할 사항은 더 나은 성능과 향상된 지원 방식입니다. 요구 사항(최대 및 최소 부하)에 따라 가상 컴퓨터에 메모리를 신속하게 할당하면서도 메모리가 낭비되지 않도록 방지하는 두 마리 토끼를 모두 잡아야 합니다. Hyper-V 동적 메모리 기능을 사용하면 호스트에서 실행되는 가상 컴퓨터 간에 메모리를 할당하고 관리하는 작업을 신속하게 수행할 수 있습니다.

메모리 최적화 테이블이 포함된 데이터베이스를 가상화할 때는 SQL Server 가상화 및 관리를 위한 일부 모범 사례에 대한 수정이 필요합니다. 메모리 최적화 테이블이 없는 경우의 모범 사례 중 두 가지는 다음과 같습니다.
-  min server memory를 사용하는 경우에는 다른 프로세스용으로 메모리가 충분히 남아 있도록 필요한 양의 메모리만 할당하여 페이징이 수행되지 않도록 하는 것이 좋습니다.
-  메모리 미리 할당 값은 너무 높게 설정하지 마십시오. 그렇지 않으면 다른 프로세스에 메모리가 필요할 때 충분한 메모리를 사용하지 못하게 되어 메모리 페이징이 발생할 수 있습니다.

메모리 최적화 테이블이 포함된 데이터베이스에서 위와 같은 방식을 따를 경우, 데이터베이스 복구에 사용할 수 있는 메모리가 충분하더라도 데이터베이스를 복원 및 복구하려고 하면 데이터베이스가 "복구 보류 중" 상태가 될 수 있습니다. 그 이유는 In-Memory OLTP는 시작 시 동적 메모리 할당이 데이터베이스에 메모리를 할당하는 것보다 더 많은 데이터를 메모리로 가져오기 때문입니다.

### <a name="resolution"></a>해결 방법
이 문제를 완화하기 위해서는 필요할 때 추가 메모리를 제공하기 위한 동적 메모리에 따라 달라지는 최소 값이 아니라 데이터베이스를 복구 또는 다시 시작하기 위한 충분한 메모리를 데이터베이스에 미리 할당하십시오.
  
## <a name="see-also"></a>참고 항목  
 [메모리 내 OLTP의 메모리 관리](http://msdn.microsoft.com/library/d82f21fa-6be1-4723-a72e-f2526fafd1b6)   
 [메모리 사용량 모니터링 및 문제 해결](../../relational-databases/in-memory-oltp/monitor-and-troubleshoot-memory-usage.md)   
 [메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩](../../relational-databases/in-memory-oltp/bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [메모리 관리 아키텍처 가이드](../../relational-databases/memory-management-architecture-guide.md)  
 [서버 메모리 서버 구성 옵션](../../database-engine/configure-windows/server-memory-server-configuration-options.md) 
  
