---
title: "서버 구성 옵션(SQL Server) | Microsoft Docs"
ms.custom:
- SQL2016_New_Updated
ms.date: 04/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
keywords:
- "서버 구성(SQL Server)"
helpviewer_keywords:
- surface area configuration [SQL Server], sp_configure
- configuration options [SQL Server], when take effect
- server management [SQL Server], configuration options
- SQL Server Management Studio [SQL Server], servers
- servers [SQL Server], configuring
- configuration options [SQL Server], setting
- options [SQL Server], configuration
- RECONFIGURE statement
- performance [SQL Server], servers
- configuration options [SQL Server]
- RECONFIGURE WITH OVERRIDE statement
- SQL Server, configuring
- sp_configure
- stored procedures [SQL Server], configuration options
- server configuration [SQL Server]
- administering SQL Server, configuration options
ms.assetid: 9f38eba6-39b1-4f1d-ba24-ee4f7e2bc969
caps.latest.revision: 128
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e5fd7bae9ba05669af1b21a931b39aba3132e25e
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="server-configuration-options-sql-server"></a>서버 구성 옵션(SQL Server)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx_md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 sp_configure 시스템 저장 프로시저를 사용하면 구성 옵션을 통해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 리소스를 관리하고 최적화할 수 있습니다. 자주 사용하는 서버 구성 옵션은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 통해 사용할 수 있으며 모든 구성 옵션에 액세스하려면 sp_configure를 사용해야 합니다. 이러한 옵션을 변경하기 전에 시스템에 주는 영향을 신중히 고려해야 합니다. 자세한 내용은 [서버 속성 보기 또는 변경&#40;SQL Server&#41;](../../database-engine/configure-windows/view-or-change-server-properties-sql-server.md)을 참조하세요.  
  
>**중요!!** 고급 옵션은 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
## <a name="categories-of-configuration-options"></a>구성 옵션 범주  
 구성 옵션은 다음 경우에 적용됩니다.  
  
-   옵션 설정 및 **RECONFIGURE** (또는 경우에 따라 **RECONFIGURE WITH OVERRIDE**) 문 실행 후 즉시 특정 옵션을 다시 구성하면 계획 캐시에서 계획을 무효화하여 새 계획이 컴파일됩니다. 자세한 내용은 [DBCC FREEPROCCACHE &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)을 참조하세요.
  
     -또는-  
  
-   위의 동작을 수행하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작한 후
  
[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 하는 옵션은 초기에 value 열에만 변경된 값이 표시되며 다시 시작한 뒤에는 value 열과 value_in_use 열 모두에 새 값이 표시됩니다.  
  
일부 옵션은 서버를 다시 시작해야 새 구성 값이 적용됩니다. 새 값을 설정하고 sp_configure를 실행해도 서버를 다시 시작하지 않으면 구성 옵션 **value** 열에만 새 값이 나타나고 **value_in_use** 열에는 나타나지 않습니다. 서버를 다시 시작하면 **value_in_use** 열에도 새 값이 나타납니다.  
  
자체 구성 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시스템의 필요에 따라 조정하는 옵션입니다. 대부분의 경우 이 값을 수동으로 설정할 필요가 없습니다. 자체 구성 옵션의 예로는 **min server memory** , **max server memory** 및 user connections가 있습니다.  
  
## <a name="configuration-options-table"></a>구성 옵션 표  
 다음 표에서는 사용할 수 있는 모든 구성 옵션, 가능한 설정 범위 및 기본값을 보여 줍니다. 구성 옵션은 다음과 같은 문자 코드로 표시됩니다.  
  
-   A= 고급 옵션이며 숙련된 데이터베이스 관리자나 인증된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자를 위한 옵션입니다. show advanced options를 1로 설정해야 이용할 수 있습니다.  
  
-   RR = [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 다시 시작해야 하는 옵션입니다.  
  
-   RP = PolyBase 엔진을 다시 시작해야 하도록 지정하는 옵션입니다.  
  
-   SC = 자체 구성 옵션입니다.  
  
    |구성 옵션|최소값|최대값|기본값|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[access check cache bucket count](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[access check cache quota](../../database-engine/configure-windows/access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[ad hoc distributed queries](../../database-engine/configure-windows/ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity I/O mask](../../database-engine/configure-windows/affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 I/O mask](../../database-engine/configure-windows/affinity64-input-output-mask-server-configuration-option.md) (A, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]64비트 버전에만 해당)|-2147483648|2147483647|0|  
    |[affinity mask](../../database-engine/configure-windows/affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](../../database-engine/configure-windows/affinity64-mask-server-configuration-option.md) (A, RR), 64비트 버전에만 해당 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[Agent XPs](../../database-engine/configure-windows/agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 시작하면 1로 변경됩니다. 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 자동으로 시작되도록 설정하는 경우 기본값은 0입니다.|  
    |[allow updates](../../database-engine/configure-windows/allow-updates-server-configuration-option.md) (구식. 사용하지 마십시오. 사용할 경우 다시 구성하는 동안 오류 발생)|0|1|0|  
    |[자동 soft-NUMA 사용 안 함](http://msdn.microsoft.com/library/ms345357.aspx)|0|1|0|  
    |[백업 체크섬 기본값](../../database-engine/configure-windows/backup-checksum-default.md)|0|1|0|  
    |[backup compression default](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0| 
    |[blocked process threshold](../../database-engine/configure-windows/blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 audit mode](../../database-engine/configure-windows/c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](../../database-engine/configure-windows/clr-enabled-server-configuration-option.md)|0|1|0|  
    |[clr strict security](../../database-engine/configure-windows/clr-strict-security.md) (A) <br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[sssqlv14-md](../../includes/sssqlv14-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)). |0|1|0|  
    |[common criteria compliance enabled](../../database-engine/configure-windows/common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[contained database authentication](../../database-engine/configure-windows/contained-database-authentication-server-configuration-option.md)|0|1|0|  
    |[cost threshold for parallelism](../../database-engine/configure-windows/configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[cursor threshold](../../database-engine/configure-windows/configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[Database Mail XPs](../../database-engine/configure-windows/database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[default full-text language](../../database-engine/configure-windows/configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1033|  
    |[default language](../../database-engine/configure-windows/configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[default trace enabled](../../database-engine/configure-windows/default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[disallow results from triggers](../../database-engine/configure-windows/disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](../../database-engine/configure-windows/ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[external scripts enabled](../../database-engine/configure-windows/external-scripts-enabled-server-configuration-option.md) (RR)<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|0|1|0|  
    |[filestream_access_level](../../database-engine/configure-windows/filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[fill factor](../../database-engine/configure-windows/configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth(max), [ft crawl bandwidth](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A) 참조|0|32767|100|  
    |ft crawl bandwidth(min), [ft crawl bandwidth](../../database-engine/configure-windows/ft-crawl-bandwidth-server-configuration-option.md)(A) 참조|0|32767|0|  
    |ft notify bandwidth(max), [ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A) 참조|0|32767|100|  
    |ft notify bandwidth(min), [ft notify bandwidth](../../database-engine/configure-windows/ft-notify-bandwidth-server-configuration-option.md)(A) 참조|0|32767|0|  
    |[index create memory](../../database-engine/configure-windows/configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[in-doubt xact resolution](../../database-engine/configure-windows/in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[lightweight pooling](../../database-engine/configure-windows/lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[locks](../../database-engine/configure-windows/configure-the-locks-server-configuration-option.md) (A, RR, SC)|5000|2147483647|0|  
    |[max degree of parallelism](../../database-engine/configure-windows/configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[max full-text crawl range](../../database-engine/configure-windows/max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[max server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](../../database-engine/configure-windows/configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[max worker threads](../../database-engine/configure-windows/configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> 32비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 권장 최대값은 1024이고 64비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 권장 최대값은 2048입니다. 32비트 운영 체제에서 제공되었던 마지막 버전은[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 입니다.|0<br /><br /> 0을 선택하면 32비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 (256+(*\<프로세서 수>* -4) * 8) 수식을 사용하고, 64비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 경우 32비트의 2배를 사용하여 프로세서 수에 따라 최대 작업자 스레드 수가 자동으로 구성됩니다. 32비트 운영 체제에서 제공되었던 마지막 버전은[!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] 입니다.|  
    |[media retention](../../database-engine/configure-windows/configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[min memory per query](../../database-engine/configure-windows/configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](../../database-engine/configure-windows/server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[중첩 트리거](../../database-engine/configure-windows/configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[network packet size](../../database-engine/configure-windows/configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole Automation Procedures](../../database-engine/configure-windows/ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](../../database-engine/configure-windows/open-objects-server-configuration-option.md) (A, RR, 구식)|0|2147483647|0|  
    |[optimize for ad hoc workloads](../../database-engine/configure-windows/optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](../../database-engine/configure-windows/ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[PolyBase Hadoop 및 Azure Blob Storage](../../database-engine/configure-windows/polybase-connectivity-configuration-transact-sql.md) (RP)<br /><br /> **적용 대상**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] ~ [현재 버전](http://go.microsoft.com/fwlink/p/?LinkId=299658)).|0|7|0|   
    |[precompute rank](../../database-engine/configure-windows/precompute-rank-server-configuration-option.md) (A)|0|1|0|  
    |[priority boost](../../database-engine/configure-windows/configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[query governor cost limit](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[query wait](../../database-engine/configure-windows/configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[recovery interval](../../database-engine/configure-windows/configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |[remote access](../../database-engine/configure-windows/configure-the-remote-access-server-configuration-option.md) (RR)|0|1|1|  
    |[remote admin connections](../../database-engine/configure-windows/remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[원격 데이터 보관](../../database-engine/configure-windows/configure-the-remote-data-archive-server-configuration-option.md)|0|1|0|  
    |[remote login timeout](../../database-engine/configure-windows/configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[remote proc trans](../../database-engine/configure-windows/configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](../../database-engine/configure-windows/configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|0|  
    |[Replication XPs 옵션](../../database-engine/configure-windows/replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[scan for startup procs](../../database-engine/configure-windows/configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](../../database-engine/configure-windows/server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[set working set size](../../database-engine/configure-windows/set-working-set-size-server-configuration-option.md) (A, RR, 구식)|0|1|0|  
    |[show advanced options](../../database-engine/configure-windows/show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO and DMO XPs](../../database-engine/configure-windows/smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[transform noise words](../../database-engine/configure-windows/transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[two digit year cutoff](../../database-engine/configure-windows/configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[user connections](../../database-engine/configure-windows/configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[user options](../../database-engine/configure-windows/configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](../../database-engine/configure-windows/xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>참고 항목  
 [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md)   
 [RECONFIGURE&#40;Transact-SQL&#41;](../../t-sql/language-elements/reconfigure-transact-sql.md)  
 [DBCC FREEPROCCACHE&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-freeproccache-transact-sql.md)
  
  

