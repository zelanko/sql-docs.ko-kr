---
title: 서버 구성 옵션(SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 02/29/2016
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
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
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 645aee1374f7dbf3c290500bb35ca47115983670
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62809571"
---
# <a name="server-configuration-options-sql-server"></a>서버 구성 옵션(SQL Server)
  
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 또는 sp_configure 시스템 저장 프로시저를 사용하면 구성 옵션을 통해 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 리소스를 관리하고 최적화할 수 있습니다. 자주 사용하는 서버 구성 옵션은 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 통해 사용할 수 있으며 모든 구성 옵션에 액세스하려면 sp_configure를 사용해야 합니다. 이러한 옵션을 변경하기 전에 시스템에 주는 영향을 신중히 고려해야 합니다. 자세한 내용은 [서버 속성 보기 또는 변경&#40;SQL Server&#41;](view-or-change-server-properties-sql-server.md)을 참조하세요.  
  
> [!IMPORTANT]  
>  고급 옵션은 숙련된 데이터베이스 관리자나 공인된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자만 변경해야 합니다.  
  
## <a name="categories-of-configuration-options"></a>구성 옵션 범주  
 구성 옵션은 다음 경우에 적용됩니다.  
  
-   옵션 설정 및 RECONFIGURE(또는 경우에 따라 RECONFIGURE WITH OVERRIDE) 문 실행 후 즉시  
  
     또는  
  
-   위의 동작을 수행하고 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 다시 시작한 후  
  
 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 를 다시 시작해야 하는 옵션은 초기에 value 열에만 변경된 값이 표시되며 다시 시작한 뒤에는 value 열과 value_in_use 열 모두에 새 값이 표시됩니다.  
  
 일부 옵션은 서버를 다시 시작해야 새 구성 값이 적용됩니다. 새 값을 설정하고 sp_configure를 실행해도 서버를 다시 시작하지 않으면 구성 옵션 value 열에만 새 값이 나타나고 value_in_use 열에는 나타나지 않습니다. 서버를 다시 시작하면 value_in_use 열에도 새 값이 나타납니다.  
  
 자체 구성 옵션은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 시스템의 필요에 따라 조정하는 옵션입니다. 대부분의 경우 이 값을 수동으로 설정할 필요가 없습니다. 자체 구성 옵션의 예로는 min server memory, max server memory 및 user connections가 있습니다.  
  
## <a name="configuration-options-table"></a>구성 옵션 표  
 다음 표에서는 사용할 수 있는 모든 구성 옵션, 가능한 설정 범위 및 기본값을 보여 줍니다. 구성 옵션은 다음과 같은 문자 코드로 표시됩니다.  
  
-   A= 고급 옵션이며 숙련된 데이터베이스 관리자나 인증된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 기술 지원 담당자를 위한 옵션입니다. show advanced options를 1로 설정해야 이용할 수 있습니다.  
  
-   RR = [!INCLUDE[ssDE](../../includes/ssde-md.md)]을 다시 시작해야 하는 옵션입니다.  
  
-   SC = 자체 구성 옵션입니다.  
  
    |구성 옵션|최솟값|최댓값|기본값|  
    |--------------------------|-------------------|-------------------|-------------|  
    |[액세스 검사 캐시 버킷 수](access-check-cache-server-configuration-options.md) (A)|0|16384|0|  
    |[액세스 검사 캐시 할당량](access-check-cache-server-configuration-options.md) (A)|0|2147483647|0|  
    |[임시 분산 쿼리](ad-hoc-distributed-queries-server-configuration-option.md) (A)|0|1|0|  
    |[affinity i/o mask](affinity-input-output-mask-server-configuration-option.md) (A, RR)|-2147483648|2147483647|0|  
    |[affinity64 i/o mask](affinity64-input-output-mask-server-configuration-option.md) (A, 64 비트 버전 에서만 사용 가능 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)])|-2147483648|2147483647|0|  
    |[선호도 마스크](affinity-mask-server-configuration-option.md) (A)|-2147483648|2147483647|0|  
    |[affinity64 mask](affinity64-mask-server-configuration-option.md) (A, RR), 64 비트 버전 에서만 사용 가능[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|-2147483648|2147483647|0|  
    |[에이전트 XPs](agent-xps-server-configuration-option.md) (A)|0|1|0<br /><br /> 
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트를 시작하면 1로 변경됩니다. 설치 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 자동으로 시작되도록 설정하는 경우 기본값은 0입니다.|  
    |[업데이트 허용](allow-updates-server-configuration-option.md) (사용 되지 않음 사용하지 마십시오. 사용할 경우 다시 구성하는 동안 오류 발생)|0|1|0|  
    |[백업 체크섬 기본값](../backup-checksum-default.md)|0|1|0|  
    |[백업 압축 기본값](view-or-configure-the-backup-compression-default-server-configuration-option.md)|0|1|0|  
    |[차단 된 프로세스 임계값](blocked-process-threshold-server-configuration-option.md) (A)|0|86400|0|  
    |[c2 감사 모드](c2-audit-mode-server-configuration-option.md) (A, RR)|0|1|0|  
    |[clr enabled](clr-enabled-server-configuration-option.md)|0|1|0|  
    |[common criteria 호환성 사용](common-criteria-compliance-enabled-server-configuration-option.md) (A, RR)|0|1|0|  
    |[contained database authentication](contained-database-authentication-server-configuration-option.md)|0||0|  
    |[병렬 처리에 대 한 비용 임계값](configure-the-cost-threshold-for-parallelism-server-configuration-option.md) (A)|0|32767|5|  
    |[cross db ownership chaining](cross-db-ownership-chaining-server-configuration-option.md)|0|1|0|  
    |[커서 임계값](configure-the-cursor-threshold-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[데이터베이스 메일 XPs](database-mail-xps-server-configuration-option.md) (A)|0|1|0|  
    |[기본 전체 텍스트 언어](configure-the-default-full-text-language-server-configuration-option.md) (A)|0|2147483647|1033|  
    |[기본 언어](configure-the-default-language-server-configuration-option.md)|0|9999|0|  
    |[기본 추적 사용](default-trace-enabled-server-configuration-option.md) (A)|0|1|1|  
    |[트리거에서 결과 반환 허용 안 함](disallow-results-from-triggers-server-configuration-option.md) (A)|0|1|0|  
    |[EKM provider enabled](ekm-provider-enabled-server-configuration-option.md)|0|1|0|  
    |[filestream_access_level](filestream-access-level-server-configuration-option.md)|0|2|0|  
    |[채우기 비율](configure-the-fill-factor-server-configuration-option.md) (A, RR)|0|100|0|  
    |ft crawl bandwidth(max), [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A) 참조|0|32767|100|  
    |ft crawl bandwidth(min), [ft crawl bandwidth](ft-crawl-bandwidth-server-configuration-option.md)(A) 참조|0|32767|0|  
    |ft notify bandwidth(max), [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A) 참조|0|32767|100|  
    |ft notify bandwidth(min), [ft notify bandwidth](ft-notify-bandwidth-server-configuration-option.md)(A) 참조|0|32767|0|  
    |[인덱스 생성 메모리](configure-the-index-create-memory-server-configuration-option.md) (A, SC)|704|2147483647|0|  
    |[미결 트랜잭션 확인](in-doubt-xact-resolution-server-configuration-option.md) (A)|0|2|0|  
    |[경량 풀링](lightweight-pooling-server-configuration-option.md) (A, RR)|0|1|0|  
    |[잠금](configure-the-locks-server-configuration-option.md) (A, RR, SC)|5,000|2147483647|0|  
    |[최대 병렬 처리 수준](configure-the-max-degree-of-parallelism-server-configuration-option.md) (A)|0|32767|0|  
    |[최대 전체 텍스트 탐색 범위](max-full-text-crawl-range-server-configuration-option.md) (A)|0|256|4|  
    |[최대 서버 메모리](server-memory-server-configuration-options.md) (A, SC)|16|2147483647|2147483647|  
    |[max text repl size](configure-the-max-text-repl-size-server-configuration-option.md)|0|2147483647|65536|  
    |[최대 작업자 스레드](configure-the-max-worker-threads-server-configuration-option.md) (A)|128|32767<br /><br /> 32비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 최대 1024, 64비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에는 최대 2048을 설정하는 것이 좋습니다.|0<br /><br /> 0을 사용 하면 32 64 비트 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 의 경우 (256 + (*\<프로세서>* -4) * 8) 수식을 사용 하 여 프로세서 수에 따라 최대 작업자 스레드 수가 자동으로 구성 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]됩니다.|  
    |[미디어 보존](configure-the-media-retention-server-configuration-option.md) (A, RR)|0|365|0|  
    |[쿼리당 최소 메모리](configure-the-min-memory-per-query-server-configuration-option.md) (A)|512|2147483647|1024|  
    |[min server memory](server-memory-server-configuration-options.md) (A, SC)|0|2147483647|0|  
    |[중첩 트리거](configure-the-nested-triggers-server-configuration-option.md)|0|1|1|  
    |[네트워크 패킷 크기](configure-the-network-packet-size-server-configuration-option.md) (A)|512|32767|4096|  
    |[Ole 자동화 프로시저](ole-automation-procedures-server-configuration-option.md) (A)|0|1|0|  
    |[open objects](open-objects-server-configuration-option.md) (A, RR, 사용 되지 않음)|0|2147483647|0|  
    |[임시 작업을 위해 최적화](optimize-for-ad-hoc-workloads-server-configuration-option.md) (A)|0|1|0|  
    |[PH_timeout](ph-timeout-server-configuration-option.md) (A)|1|3600|60|  
    |[순위](precompute-rank-server-configuration-option.md) 미리 계산 (A)|0|1|0|  
    |[우선 순위 높임](configure-the-priority-boost-server-configuration-option.md) (A, RR)|0|1|0|  
    |[쿼리 관리자 비용 제한](configure-the-query-governor-cost-limit-server-configuration-option.md) (A)|0|2147483647|0|  
    |[쿼리 대기](configure-the-query-wait-server-configuration-option.md) (A)|-1|2147483647|-1|  
    |[복구 간격](configure-the-recovery-interval-server-configuration-option.md) (A, SC)|0|32767|0|  
    |RR ( [원격 액세스](configure-the-remote-access-server-configuration-option.md) )|0|1|1|  
    |[remote admin connections](remote-admin-connections-server-configuration-option.md)|0|1|0|  
    |[원격 로그인 제한 시간](configure-the-remote-login-timeout-server-configuration-option.md)|0|2147483647|10|  
    |[원격 프로시저 트랜잭션](configure-the-remote-proc-trans-server-configuration-option.md)|0|1|0|  
    |[remote query timeout](configure-the-remote-query-timeout-server-configuration-option.md)|0|2147483647|600|  
    |[Replication XPs 옵션](replication-xps-server-configuration-option.md) (A)|0|1|0|  
    |[시작 프로시저 검색](configure-the-scan-for-startup-procs-server-configuration-option.md) (A, RR)|0|1|0|  
    |[server trigger recursion](server-trigger-recursion-server-configuration-option.md)|0|1|1|  
    |[작업 집합 크기 설정](set-working-set-size-server-configuration-option.md) (A, RR, 사용 되지 않음)|0|1|0|  
    |[show advanced options](show-advanced-options-server-configuration-option.md)|0|1|0|  
    |[SMO 및 DMO XPs](smo-and-dmo-xps-server-configuration-option.md) (A)|0|1|1|  
    |[의미 없는 단어 변환](transform-noise-words-server-configuration-option.md) (A)|0|1|0|  
    |[두 자리 연도 구분](configure-the-two-digit-year-cutoff-server-configuration-option.md) (A)|1753|9999|2049|  
    |[사용자 연결](configure-the-user-connections-server-configuration-option.md) (A, RR, SC)|0|32767|0|  
    |[user options](configure-the-user-options-server-configuration-option.md)|0|32767|0|  
    |[xp_cmdshell](xp-cmdshell-server-configuration-option.md) (A)|0|1|0|  
  
## <a name="see-also"></a>참고 항목  
 [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)   
 [RECONFIGURE&#40;Transact-SQL&#41;](/sql/t-sql/language-elements/reconfigure-transact-sql)  
  
  
