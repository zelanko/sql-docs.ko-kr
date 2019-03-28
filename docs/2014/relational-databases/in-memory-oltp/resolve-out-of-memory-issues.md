---
title: OOM(메모리 부족) 문제 해결 | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: f855e931-7502-44bd-8a8b-b8543645c7f4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 999f58014d661f2eb476cd195e11788b2a565937
ms.sourcegitcommit: c44014af4d3f821e5d7923c69e8b9fb27aeb1afd
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/27/2019
ms.locfileid: "58527895"
---
# <a name="resolve-out-of-memory-issues"></a>OOM(메모리 부족) 문제 해결
  [!INCLUDE[hek_1](../../includes/hek-1-md.md)] 는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]와 다른 방법으로 더 많은 메모리를 사용합니다. 필요 증가에 따라 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 에 대해 설치하고 할당한 메모리의 양이 불충분해질 수 있습니다. 이 경우 메모리가 부족해질 수 있습니다. 이 항목에서는 OOM 상황에서 복구하는 방법을 설명합니다. 여러 OOM 상황을 방지하는 데 도움이 될 수 있는 지침은 [메모리 사용량 모니터링 및 문제 해결](monitor-and-troubleshoot-memory-usage.md) 을 참조하세요.  
  
## <a name="covered-in-this-topic"></a>이 항목의 내용  
  
|항목|개요|  
|-----------|--------------|  
| [OOM으로 인한 데이터베이스 복원 실패 해결](#resolve-database-restore-failures-due-to-oom) |“'*\<resourcePoolName>*' 리소스 풀의 메모리 부족으로 인해 '*\<databaseName>*' 데이터베이스에 대한 복원 작업이 실패했습니다”라는 오류 메시지가 나타나는 경우 수행할 작업입니다.|  
| [메모리 부족 또는 OOM 상황이 작업에 미치는 영향 해결](#resolve-impact-of-low-memory-or-oom-conditions-on-the-workload)|메모리 부족 문제가 성능에 부정적인 영향을 미치고 있음을 발견할 경우 수행할 작업입니다.|  
| [사용 가능한 메모리가 충분한 경우 메모리 부족으로 인한 페이지 할당 오류 해결](#resolve-page-allocation-failures-due-to-insufficient-memory-when-sufficient-memory-is-available) |작업에 사용할 수 있는 메모리가 충분한데 “'*\<resourcePoolName>*' 리소스 풀의 메모리 부족으로 인해 '*\<databaseName>*' 데이터베이스에 대해 페이지를 할당할 수 없습니다...”라는 오류 메시지가 나타나는 경우 수행할 작업입니다.|  
  
## <a name="resolve-database-restore-failures-due-to-oom"></a>OOM으로 인한 데이터베이스 복원 실패 해결  
 데이터베이스를 복원하려고 할 때 "복원 작업이 데이터베이스에 대 한 실패 했습니다. '*\<데이터베이스 이름 >*'리소스 풀의 메모리 부족으로 인해'*\<a m e >*'." 데이터베이스를 복원하기 전에 사용 가능한 메모리를 늘려 메모리 부족 문제를 해결해야 합니다.  
  
 OOM으로 인한 복구 오류를 해결하려면 다음 방법으로 복구 작업에 사용 가능한 메모리를 임시로 늘리십시오.  
  
-   실행 중인 애플리케이션을 일시적으로 닫습니다.   
    Visual Studio, Internet Explorer, OneNote 등과 같이 실행 중인 애플리케이션을 하나 이상 닫으면 해당 애플리케이션에서 사용 중인 메모리를 복원 작업에 사용할 수 있습니다. 성공적으로 복원한 후 해당 응용 프로그램을 다시 시작할 수 있습니다.  
  
-   MAX_MEMORY_PERCENT의 값을 늘립니다.   
    이 코드 조각은 PoolHk 리소스 풀에 대한 MAX_MEMORY_PERCENT를 설치된 메모리의 70%로 변경합니다.  
  
    > [!IMPORTANT]  
    >  서버가 VM에서 실행 중이고 전용 서버가 아니면 MIN_MEMORY_PERCENT 값을 MAX_MEMORY_PERCENT와 동일한 값으로 설정합니다.   
    > 자세한 내용은 [모범 사례: VM 환경에서 메모리 내 OLTP를 사용 하 여](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) 자세한 내용은 합니다.  
  
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
  
     MAX_MEMORY_PERCENT에 대 한 최대값 정보 항목 섹션을 참조 하세요. [메모리 최적화 테이블 및 인덱스에 대 한 사용 가능한 메모리 비율](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#percent-of-memory-available-for-memory-optimized-tables-and-indexes)
  
-   **최대 서버 메모리**를 다시 구성합니다.  
    **최대 서버 메모리** 구성에 대한 자세한 내용은 [메모리 구성 옵션을 사용하여 서버 성능 최적화](https://technet.microsoft.com/library/ms177455\(v=SQL.105\).aspx) 항목을 참조하세요.  
  
## <a name="resolve-impact-of-low-memory-or-oom-conditions-on-the-workload"></a>메모리 부족 또는 OOM 상황이 작업에 미치는 영향 해결  
 물론 OOM(메모리 부족) 상황에 빠지지 않는 것이 최선입니다. 적절한 계획과 모니터링을 통해 OOM 상황을 방지할 수 있습니다. 그렇지만 최상의 계획을 세우더라도 실제 발생하는 상황을 항상 예측할 수 있는 것은 아니며 결국 메모리 부족 또는 OOM 상황에 도달할 수 있습니다. 다음 두 가지 방법으로 OOM에서 복구할 수 있습니다.  
  
1.  [DAC (관리자 전용된 연결) 열기 ](#open-a-dac-dedicated-administrator-connection) 
  
2.  [수정 조치 수행](#take-corrective-action) 
  
### <a name="open-a-dac-dedicated-administrator-connection"></a>DAC(관리자 전용 연결) 열기  
 Microsoft SQL Server는 DAC(관리자 전용 연결)를 제공합니다. DAC를 사용하면 관리자는 서버가 다른 클라이언트 연결에 응답하지 않는 경우에도 실행 중인 SQL Server 데이터베이스 엔진 인스턴스에 액세스하여 서버에서 문제를 해결할 수 있습니다. DAC는 `sqlcmd` 유틸리티와 SQL Server Management Studio(SSMS)를 통해 사용할 수 있습니다.  
  
 `sqlcmd` 및 DAC 사용에 대한 지침은 [관리자 전용 연결 사용](../../database-engine/configure-windows/diagnostic-connection-for-database-administrators.md)을 참조하십시오. SSMS 통한 DAC 사용에 대 한 지침을 참조 [방법: 관리자 전용된 연결을 사용 하 여 SQL Server Management Studio를 사용 하 여](https://msdn.microsoft.com/library/ms178068.aspx)입니다.  
  
### <a name="take-corrective-action"></a>수정 조치 수행  
 OOM 상태를 해결하려면 사용을 축소하여 기존 메모리를 확보하거나 더 많은 메모리를 메모리 내 테이블에 사용할 수 있게 만들어야 합니다.  
  
#### <a name="free-up-existing-memory"></a>기존 메모리 확보  
  
##### <a name="delete-non-essential-memory-optimized-table-rows-and-wait-for-garbage-collection"></a>필수적이지 않은 메모리 액세스에 최적화된 테이블 행을 삭제하고 가비지 수집 대기  
 메모리 액세스에 최적화된 테이블에서 필수적이지 않은 행을 제거할 수 있습니다. 가비지 수집기는 이러한 행에 사용되는 메모리를 사용 가능한 메모리로 되돌립니다. . 메모리 내 OLTP 엔진은 가비지 행을 적극적으로 수집합니다. 그러나 장기 실행 트랜잭션으로 인해 가비지가 수집되지 않을 수 있습니다. 예를 들어 5분간 실행되는 트랜잭션이 있는 경우 트랜잭션이 활성 상태인 동안 수행되는 업데이트/삭제 작업으로 생성된 모든 행 버전에 대해 가비지가 수집되지 않을 수 있습니다.  
  
##### <a name="move-one-or-more-rows-to-a-disk-based-table"></a>디스크 기반 테이블로 하나 이상의 행 이동  
 다음 TechNet 문서에는 메모리 최적화 테이블에서 디스크 기반 테이블로 행을 이동하는 방법이 나와 있습니다.  
  
-   [애플리케이션 수준 분할](https://technet.microsoft.com/library/dn296452\(v=sql.120\).aspx)  
  
-   [메모리 액세스에 최적화된 테이블 분할을 위한 응용 프로그램 패턴](https://technet.microsoft.com/library/dn133171\(v=sql.120\).aspx)  
  
#### <a name="increase-available-memory"></a>사용 가능한 메모리 늘리기  
  
##### <a name="increase-value-of-maxmemorypercent-on-the-resource-pool"></a>리소스 풀에서 MAX_MEMORY_PERCENT의 값 늘리기  
 메모리 내 테이블에 대한 명명된 리소스 풀을 만들지 않은 경우 이 리소스 풀을 만들고 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 데이터베이스를 이 리소스 풀에 바인딩해야 합니다. 리소스 풀을 만들고 [데이터베이스를 리소스 풀에 바인딩하는 방법에 대한 지침은](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md) 메모리 액세스에 최적화된 테이블이 있는 데이터베이스를 리소스 풀에 바인딩 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 항목을 참조하세요.  
  
 [!INCLUDE[hek_2](../../includes/hek-2-md.md)] 데이터베이스가 리소스 풀에 바인딩된 경우 풀에서 액세스할 수 있는 메모리 비율을 늘릴 수 있습니다. 리소스 풀을 위한 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT의 값 변경에 대한 지침은 하위 항목 [기존 풀에서 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 변경](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool) 을 참조하세요.  
  
 MAX_MEMORY_PERCENT의 값을 늘립니다.   
이 코드 조각은 PoolHk 리소스 풀에 대한 MAX_MEMORY_PERCENT를 설치된 메모리의 70%로 변경합니다.  
  
> [!IMPORTANT]  
>  서버가 VM에서 실행 중이고 전용 서버가 아니면 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 값을 동일한 값으로 설정합니다.   
> 자세한 내용은 [모범 사례: VM 환경에서 메모리 내 OLTP를 사용 하 여](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) 자세한 내용은 합니다.  
  
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
  
 MAX_MEMORY_PERCENT의 최대값에 대한 자세한 내용은 항목 섹션 [메모리 최적화 테이블 및 인덱스에 사용 가능한 메모리 비율](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#percent-of-memory-available-for-memory-optimized-tables-and-indexes)을 참조하세요.  
  
##### <a name="install-additional-memory"></a>추가 메모리 설치  
 가능한 경우 궁극적으로 가장 좋은 해결 방법은 추가 실제 메모리를 설치하는 것입니다. 이렇게 할 경우 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에 메모리가 더 필요하지 않을 것이므로 MAX_MEMORY_PERCENT 값도 늘려서 새로 설치된 메모리 중 전부는 아니라도 대부분을 리소스 풀에 사용하도록 설정할 수 있습니다(하위 항목 [기존 풀에서 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 변경](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md#change-min-memory-percent-and-max-memory-percent-on-an-existing-pool) 참조).  
  
> [!IMPORTANT]  
>  서버가 VM에서 실행 중이고 전용 서버가 아니면 MIN_MEMORY_PERCENT 및 MAX_MEMORY_PERCENT 값을 동일한 값으로 설정합니다.   
> 자세한 내용은 [모범 사례: VM 환경에서 메모리 내 OLTP를 사용 하 여](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md) 자세한 내용은 합니다.  
  
## <a name="resolve-page-allocation-failures-due-to-insufficient-memory-when-sufficient-memory-is-available"></a>사용 가능한 메모리가 충분한 경우 메모리 부족으로 인한 페이지 할당 오류 해결  
 오류 메시지를 받게 되 면 "데이터베이스에 대 한 페이지 할당을 허용 하지 않는 '*\<데이터베이스 이름 >*'리소스 풀의 메모리 부족으로 인해'*\<a m e >*'. 참조 '<https://go.microsoft.com/fwlink/?LinkId=330673>' 자세한. " 라는 오류 메시지가 기록된 경우 리소스 관리자를 사용하지 않기 때문일 수 있습니다. 리소스 관리자를 사용하지 않으면 MEMORYBROKER_FOR_RESERVE가 인위적인 메모리 압력을 유발합니다.  
  
 이 오류를 해결하려면 리소스 관리자를 사용하도록 설정해야 합니다.  
  
 개체 탐색기, 리소스 관리자 속성 또는 Transact-SQL로 리소스 관리자를 사용하도록 설정하는 지침과 제한 사항에 대한 자세한 내용은 [리소스 관리자 사용](https://technet.microsoft.com/library/bb895149.aspx) 을 참조하세요.  
  
## <a name="see-also"></a>관련 항목  
 [메모리 내 OLTP의 메모리 관리](../../database-engine/managing-memory-for-in-memory-oltp.md)   
 [메모리 사용량 모니터링 및 문제 해결](monitor-and-troubleshoot-memory-usage.md)   
 [데이터베이스를 리소스 풀에 바인딩하는 방법에 대한 지침은](bind-a-database-with-memory-optimized-tables-to-a-resource-pool.md)   
 [모범 사례: VM 환경에서 메모리 내 OLTP를 사용 하 여](../../database-engine/using-in-memory-oltp-in-a-vm-environment.md)  
  
  
