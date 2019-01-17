---
title: 가용성 그룹의 보조 복제본으로 지원되는 백업 오프로드
description: Always On 가용성 그룹의 보조 복제본으로 백업을 오프로딩하는 경우 지원되는 다양한 백업 유형에 대해 알아봅니다.
ms.custom: seodec18
ms.date: 09/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
helpviewer_keywords:
- backup priority
- backup on secondary replicas
- Availability Groups [SQL Server], availability replicas
- Availability Groups [SQL Server], backup on secondary replicas
- active secondary replicas [SQL Server], backup on
- automated backup preference
- Availability Groups [SQL Server], active secondary replicas
ms.assetid: 82afe51b-71d1-4d5b-b20a-b57afc002405
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 40fa3d6f3464c92a16e27a2a8bdddbf664909504
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53209442"
---
# <a name="offload-supported-backups-to-secondary-replicas-of-an-availability-group"></a>가용성 그룹의 보조 복제본으로 지원되는 백업 오프로드
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  [!INCLUDE[ssHADR](../../../includes/sshadr-md.md)] 활성 보조 기능에는 보조 복제본에서의 백업 작업 수행 지원이 포함됩니다. 백업 작업은 백업 압축과 함께 I/O 및 CPU에 상당한 부담을 줄 수 있습니다. 백업을 동기화되었거나 동기화 중인 보조 복제본으로 오프로드하면 계층 1 작업에 대한 주 복제본을 호스팅하는 서버 인스턴스에서 리소스를 사용할 수 있습니다.  

> [!NOTE]  
>  RESTORE 문은 가용성 그룹의 주 데이터베이스나 보조 데이터베이스에서 허용되지 않습니다.  
  
-   [지원되는 백업 유형](#SupportedBuTypes)  
  
-   [백업 작업이 실행되는 위치 구성](#WhereBuJobsRun)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="SupportedBuTypes"></a> 보조 복제본에서 지원되는 백업 유형  
  
-   **BACKUP DATABASE** 는 보조 복제본에서 실행될 때 데이터베이스, 파일 또는 파일 그룹의 복사 전용 전체 백업만 지원합니다. 복사 전용 백업은 로그 체인에 영향을 미치거나 차등 비트맵을 지우지 않습니다.  
  
-   차등 백업은 보조 복제본에서 지원되지 않습니다.  
  
-   **BACKUP LOG** 는 정기적인 로그 백업만 지원합니다(COPY_ONLY 옵션은 보조 복제본의 로그 백업에 지원되지 않음).  
  
     가용성 모드(동기 커밋 또는 비동기 커밋)에 관계없이 모든 복제본(주 또는 보조)에서 수행되는 로그 백업에 대해 일관된 로그 체인이 보장됩니다.  
  
-   보조 데이터베이스를 백업하려면 보조 복제본이 주 복제본과 통신할 수 있어야 하고 **SYNCHRONIZED** 또는 **SYNCHRONIZING**상태여야 합니다.  

분산 가용성 그룹에서 백업은 활성 주 복제본과 동일한 가용성 그룹 또는 보조 가용성 그룹의 주 복제본에 있는 보조 복제본에서 수행할 수 있습니다. 보조 복제본은 자체 가용성 그룹의 주 복제본과만 통신하기 때문에 보조 가용성 그룹의 보조 복제본에서 백업을 수행 할 수 없습니다. 전역 주 복제본과 직접 통신하는 복제본만 백업 작업을 수행할 수 있습니다.

##  <a name="WhereBuJobsRun"></a> 백업 작업이 실행되는 위치 구성  
 보조 복제본에서 백업을 수행하여 주 프로덕션 서버에서 백업 작업을 오프로드하면 많은 이점이 있습니다. 그러나 보조 복제본에서 백업을 수행하면 백업 작업이 실행되어야 하는 위치를 결정하는 프로세스가 상당히 복잡해집니다. 이 문제를 해결하려면 백업 작업이 실행되는 위치를 다음과 같이 구성합니다.  
  
1.  가용성 그룹을 구성하여 백업을 수행할 가용성 복제본을 지정합니다. 자세한 내용은 *CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;* 또는 *ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;* 에서 [CREATE AVAILABILITY GROUP&amp;#40;Transact-SQL&amp;#41;](../../../t-sql/statements/create-availability-group-transact-sql.md) 또는 [ALTER AVAILABILITY GROUP&amp;#40;Transact-SQL&amp;#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)상태여야 합니다.  
  
2.  백업을 수행할 후보 가용성 복제본을 호스팅하는 모든 서버 인스턴스에서 모든 가용성 데이터베이스에 대한 스크립트 백업 작업을 만듭니다. 자세한 내용은 [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)의 보조 복제본에 백업을 구성한 후" 섹션을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **보조 복제본에 백업을 구성하려면**  
  
-   [가용성 복제본에 백업 구성&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/configure-backup-on-availability-replicas-sql-server.md)  
  
 **현재 복제본이 선호 백업 복제본인지 여부를 확인하려면**  
  
-   [sys.fn_hadr_backup_is_preferred_replica](../../../relational-databases/system-functions/sys-fn-hadr-backup-is-preferred-replica-transact-sql.md)  
  
 **백업 작업을 만들려면**  
  
-   [유지 관리 계획 마법사 사용](../../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
-   [작업 구현](../../../ssms/agent/implement-jobs.md)  
  
## <a name="see-also"></a>참고 항목  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [복사 전용 백업&#40;SQL Server&#41;](../../../relational-databases/backup-restore/copy-only-backups-sql-server.md)   
 [CREATE AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/create-availability-group-transact-sql.md)   
 [ALTER AVAILABILITY GROUP&#40;Transact-SQL&#41;](../../../t-sql/statements/alter-availability-group-transact-sql.md)  
  
  
