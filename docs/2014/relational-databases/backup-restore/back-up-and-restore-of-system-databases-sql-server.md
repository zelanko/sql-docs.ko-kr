---
title: 시스템 데이터베이스 백업 및 복원(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- system databases [SQL Server], backing up and restoring
- restoring system databases [SQL Server]
- backing up [SQL Server], system databases
- database backups [SQL Server], system databases
- servers [SQL Server], backup
ms.assetid: aef0c4fa-ba67-413d-9359-1a67682fdaab
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 83dd88ee1c95f5d88319a60b0c17e4ddc2882ef4
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48129168"
---
# <a name="back-up-and-restore-of-system-databases-sql-server"></a>시스템 데이터베이스 백업 및 복원(SQL Server)
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 서버 인스턴스의 작업에 필수적인*시스템 데이터베이스*라는 시스템 수준 데이터베이스의 집합을 유지 관리합니다. 모든 중요한 업데이트 후에는 여러 시스템 데이터베이스를 백업해야 합니다. 항상 백업해야 하는 시스템 데이터베이스에는 **msdb**, **master**및 **model**이 있습니다. 데이터베이스가 서버 인스턴스에서 복제를 사용할 경우 **배포** 시스템 데이터베이스도 백업해야 하며 이러한 시스템 데이터베이스를 백업하면 하드 디스크 손실과 같은 시스템 오류 이벤트에서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템을 복원 및 복구할 수 있습니다.  
  
 다음 표에서는 모든 시스템 데이터베이스를 요약합니다.  
  
|시스템 데이터베이스|Description|백업 필요 여부|복구 모델|주석|  
|---------------------|-----------------|---------------------------|--------------------|--------------|  
|[master](../databases/master-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 시스템의 모든 시스템 수준 정보를 기록하는 데이터베이스입니다.|사용자 계정 컨트롤|간단|업무상 데이터 보호가 특별히 요구되는 경우 **master** 를 필요한 만큼 자주 백업하십시오. 정기 백업 일정을 사용하고 중요한 업데이트 후에는 추가 백업으로 보완하는 것이 좋습니다.|  
|[model](../databases/model-database.md)|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에서 생성되는 모든 데이터베이스용 템플릿입니다.|사용자 계정 컨트롤|사용자 구성 가능<sup>1</sup>|해당 데이터베이스 옵션을 사용자 지정한 후 즉시 백업하는 경우와 같이 업무상 필요한 경우에만 **model** 을 백업합니다.<br /><br /> **최선의 방법:** 필요에 따라 **model**의 전체 데이터베이스 백업만 만드는 것이 좋습니다. **model** 은 작고 거의 변경되지 않으므로 로그를 백업할 필요가 없습니다.|  
|[msdb](../databases/msdb-database.md)|경고 및 작업을 예약하고 운영자를 기록하기 위해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에이전트가 사용하는 데이터베이스입니다. **msdb** 는 백업 및 복원 기록 테이블과 같은 기록 테이블도 포함합니다.|사용자 계정 컨트롤|단순(기본값)|**msdb** 가 업데이트될 때마다 백업하십시오.|  
|[리소스](../databases/resource-database.md) (RDB)|다음과 함께 제공되는 모든 시스템 개체의 복사본이 포함된 읽기 전용 데이터베이스입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|아니요|—|**리소스** 데이터베이스는 코드만 포함하는 mssqlsystemresource.mdf 파일에 있습니다. 따라서 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 **리소스** 데이터베이스를 백업할 수 없습니다.<br /><br /> 참고: mssqlsystemresource.mdf 파일을 데이터베이스 파일이 아니라 이진 파일(.exe)로 취급하는 방법으로 파일 기반 백업 또는 디스크 기반 백업을 수행할 수 있습니다. 그러나 이러한 백업에 대해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 복원은 사용할 수 없습니다. 수동으로만 mssqlsystemresource.mdf 백업 복사본을 복원할 수 있으며 현재 **Resource** 데이터베이스를 오래된 버전이나 안전하지 않은 버전으로 덮어쓰지 않도록 주의해야 합니다.|  
|[tempdb](../databases/tempdb-database.md)|임시 또는 중간 결과 집합을 유지하기 위한 작업 영역입니다. 이 데이터베이스는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 시작될 때마다 다시 생성됩니다. 서버 인스턴스가 종료될 때 **tempdb** 에 있는 모든 데이터는 영구적으로 삭제됩니다.|아니요|간단|**tempdb** 시스템 데이터베이스는 백업할 수 없습니다.|  
|[배포 구성](../replication/configure-distribution.md)|서버가 복제 배포자로 구성된 경우에만 존재하는 데이터베이스입니다. 이 데이터베이스는 모든 유형의 복제 및 트랜잭션(트랜잭션 복제의 경우)에 대한 메타데이터 및 기록 데이터를 저장합니다.|사용자 계정 컨트롤|간단|**distribution** 데이터베이스의 백업 시기는 [복제된 데이터베이스 백업 및 복원](../replication/administration/back-up-and-restore-replicated-databases.md)을 참조하세요.|  
  
 <sup>1</sup> 모델의 현재 복구 모델에 알아보려면 [데이터베이스의 복구 모델 보기 또는 변경 &#40;SQL Server&#41; ](view-or-change-the-recovery-model-of-a-database-sql-server.md) 하거나 [sys.databases &#40;TRANSACT-SQL&#41; ](/sql/relational-databases/system-catalog-views/sys-databases-transact-sql).  
  
## <a name="limitations-on-restoring-system-databases"></a>시스템 데이터베이스 복원의 제한 사항  
  
-   시스템 데이터베이스는 서버 인스턴스가 현재 실행 중인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 버전에서 생성된 백업에서만 복원될 수 있습니다. 예를 들어에서 실행 되는 서버 인스턴스에서 시스템 데이터베이스를 복원 하려면 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] SP1.  
  
-   데이터베이스를 복원하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행 중이어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스를 시작하려면 **master** 데이터베이스에 액세스할 수 있고 최소한 부분적으로 사용할 수 있어야 합니다. **master** 를 사용할 수 없게 된 경우 다음 방법 중 하나로 데이터베이스를 사용 가능한 상태로 되돌릴 수 있습니다.  
  
    -   현재 데이터베이스 백업에서 **master** 를 복원합니다.  
  
         서버 인스턴스를 시작할 수 있으면 전체 데이터베이스 백업에서 **master** 를 복원할 수 있습니다.  
  
    -   **master** 를 완전히 다시 작성합니다.  
  
         **master** 에 발생한 심각한 손상으로 인해 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]를 시작할 수 없는 경우에는 **master**를 다시 작성해야 합니다. 자세한 내용은 [시스템 데이터베이스 다시 작성](../databases/system-databases.md)을 참조하세요.  
  
        > [!IMPORTANT]  
        >  **master** 를 다시 작성하면 모든 시스템 데이터베이스가 다시 작성됩니다.  
  
-   model 데이터베이스 복구를 위해 시스템 데이터베이스를 다시 작성하거나 model 데이터베이스에 대한 mdf 및 ldf 파일을 바꿔야 하는 경우도 있습니다. 자세한 내용은 [시스템 데이터베이스 다시 작성](../databases/system-databases.md)을 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [전체 데이터베이스 복원&#40;단순 복구 모델&#41;](complete-database-restores-simple-recovery-model.md)  
  
-   [master 데이터베이스 복원&#40;Transact-SQL&#41;](restore-the-master-database-transact-sql.md)  
  
-   [데이터베이스 복구 모델 보기 또는 변경&#40;SQL Server&#41;](view-or-change-the-recovery-model-of-a-database-sql-server.md)  
  
-   [시스템 데이터베이스 이동](../databases/move-system-databases.md)  
  
## <a name="see-also"></a>관련 항목  
 [배포 데이터베이스](../../relational-databases/replication/distribution-database.md)   
 [master 데이터베이스](../databases/master-database.md)   
 [msdb 데이터베이스](../databases/msdb-database.md)   
 [model 데이터베이스](../databases/model-database.md)   
 [Resource 데이터베이스](../databases/resource-database.md)   
 [tempdb 데이터베이스](../databases/tempdb-database.md)  
  
  
