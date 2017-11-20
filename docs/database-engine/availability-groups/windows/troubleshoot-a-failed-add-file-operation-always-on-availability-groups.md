---
title: "실패한 파일 추가 작업 문제 해결(Always On 가용성 그룹) | Microsoft Docs"
ms.custom: 
ms.date: 05/17/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: availability-groups
ms.reviewer: 
ms.suite: sql
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- secondary databases [SQL Server], Availability Groups
- Availability Groups [SQL Server], troubleshooting
ms.assetid: 31ceaebf-864b-4dd0-9112-0d047b0316ad
caps.latest.revision: 11
author: MikeRayMSFT
ms.author: mikeray
manager: jhubbard
ms.workload: Inactive
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: e859a6d1353a86c58ceed0e0ec10f72135baebfc
ms.contentlocale: ko-kr
ms.lasthandoff: 08/02/2017

---
# <a name="troubleshoot-a-failed-add-file-operation-always-on-availability-groups"></a>실패한 파일 추가 작업 문제 해결(Always On 가용성 그룹)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  일부 Always On 가용성 그룹 배포의 경우 주 복제본을 호스트하는 시스템과 보조 복제본을 호스트하는 시스템 간의 파일 경로가 다릅니다. 파일 추가 작업의 파일 경로가 보조 복제본에 존재하지 않는 경우 파일 추가 작업이 기본 데이터베이스에서 성공합니다. 하지만 파일 추가 작업으로 인해 보조 데이터베이스가 일시 중지될 수 있습니다. 이로 인해 보조 복제본이 NOT SYNCHRONIZING 상태가 됩니다.  
  
> [!NOTE]  
>  지정된 보조 데이터베이스의 드라이브 문자를 포함한 파일 경로는 가급적 해당 주 데이터베이스의 경로와 동일한 것이 좋습니다.  
  
## <a name="problem-resolution"></a>문제 해결  
 이 문제를 해결하려면 데이터베이스 소유자가 다음 단계를 완료해야 합니다.  
  
1.  가용성 그룹에서 보조 데이터베이스를 제거합니다. 자세한 내용은 [가용성 그룹에서 보조 데이터베이스 제거&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/remove-a-secondary-database-from-an-availability-group-sql-server.md)를 참조하세요.  
  
2.  기존 보조 데이터베이스에서 보조 복제본을 호스팅하는 서버 인스턴스에 대한 파일 경로를 지정하고 WITH NORECOVERY 및 WITH MOVE를 사용하여 보조 데이터베이스에 추가된 파일을 포함하는 파일 그룹의 전체 백업을 복원합니다. 자세한 내용은 [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)을 참조하세요.  
  
3.  주 데이터베이스에서 파일 추가 작업을 포함하는 트랜잭션 로그를 백업하고 WITH NORECOVERY 및 WITH MOVE를 사용하여 보조 데이터베이스에서 로그 백업을 수동으로 복원합니다.  
  
4.  WITH NO RECOVERY를 사용하여 주 데이터베이스에서 다른 처리 중인 로그 백업을 복원하여 가용성 그룹을 다시 조인할 수 있도록 보조 데이터베이스를 준비합니다.  
  
5.  가용성 그룹에 보조 데이터베이스를 다시 조인합니다. 자세한 내용은 [가용성 그룹에 보조 데이터베이스 조인&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/join-a-secondary-database-to-an-availability-group-sql-server.md)을 참조하세요.  
  
## <a name="see-also"></a>관련 항목:  
 [Always On 가용성 그룹 개요&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [가용성 그룹에 대한 보조 데이터베이스 수동 준비&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/manually-prepare-a-secondary-database-for-an-availability-group-sql-server.md)   
 [분리된 사용자 문제 해결&#40;SQL Server&#41;](../../../sql-server/failover-clusters/troubleshoot-orphaned-users-sql-server.md)   
 [Always On 가용성 그룹 구성 문제 해결&#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/troubleshoot-always-on-availability-groups-configuration-sql-server.md)

