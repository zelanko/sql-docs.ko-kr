---
title: '백업 및 복원: 기능 상호 운용성'
description: 이 문서에서는 데이터베이스 시작, 온라인 복원 및 비활성 인덱스, 데이터베이스 미러링을 포함하는 SQL Server의 백업 및 복원 기능에 대해 설명합니다.
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- file restores [SQL Server], related features
- restoring [SQL Server], files
- restoring files [SQL Server], related features
- backups [SQL Server], files or filegroups
- file backups [SQL Server], related features
ms.assetid: 69f212b8-edcd-4c5d-8a8a-679ced33c128
author: cawrites
ms.author: chadam
ms.openlocfilehash: 106773df7a5e9f88c123b614688ca19722613d7f
ms.sourcegitcommit: 5a1ed81749800c33059dac91b0e18bd8bb3081b1
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/23/2020
ms.locfileid: "96130530"
---
# <a name="backup-and-restore-interoperability-and-coexistence-sql-server"></a>백업 및 복원: 상호 운용성 및 공존성(SQL Server)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]의 몇 가지 기능에 대한 백업 및 복원 고려 사항에 대해 설명합니다. 이러한 기능에는 파일 복원 및 데이터베이스 시작, 온라인 복원 및 비활성 인덱스, 데이터베이스 미러링, 증분 복원 및 전체 텍스트 인덱스가 포함됩니다.  
  
 **항목 내용:**  
  
-   [파일 복원 및 데이터베이스 시작](#FileRestoreAndDbStartup)  
  
-   [온라인 복원 및 비활성화된 인덱스](#OnlineRestoreAndDisabledIndexes)  
  
-   [데이터베이스 미러링, 백업 및 복원](#DbMandBnR)  
  
-   [증분 복원 및 전체 텍스트 인덱스](#PiecemealAndFTIndexes)  
  
-   [파일 백업과 복원 및 압축](#FileBnRandCompression)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="file-restore-and-database-startup"></a><a name="FileRestoreAndDbStartup"></a> 파일 복원 및 데이터베이스 시작  
 이 섹션에서는 여러 개의 파일 그룹이 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스와 관련된 내용을 다룹니다.  
  
> [!NOTE]  
>  데이터베이스를 시작하면 데이터베이스를 닫았을 때 온라인 상태였던 파일을 포함하는 파일 그룹만 복구되고 온라인 상태가 됩니다.  
  
 데이터베이스 시작 중에 문제가 발생하면 복구에 실패하고 데이터베이스가 주의 대상으로 표시됩니다. 문제를 한 파일이나 몇 개의 파일로 격리시킬 수 있는 경우 데이터베이스 관리자는 해당 파일을 오프라인 상태로 만들고 데이터베이스를 다시 시작할 수 있습니다. 파일을 오프라인 상태로 만들려면 다음 [ALTER DATABASE](../../t-sql/statements/alter-database-transact-sql.md) 문을 실행합니다.  
  
 ALTER DATABASE *database_name* MODIFY FILE (NAME **='** _filename_*_'_*, OFFLINE)  
  
 데이터베이스가 성공적으로 시작되면 오프라인 파일을 포함하는 모든 파일 그룹은 오프라인 상태로 남게 됩니다.  
  
##  <a name="online-restore-and-disabled-indexes"></a><a name="OnlineRestoreAndDisabledIndexes"></a> 온라인 복원 및 비활성화된 인덱스  
 이 섹션에서는 여러 개의 파일 그룹이 있는 데이터베이스와 관련된 내용 및 단순 복구 모델의 경우 하나 이상의 읽기 전용 파일 그룹과 관련된 내용을 다룹니다.  
  
 이러한 경우 데이터베이스가 온라인 상태이면 인덱스를 생성, 삭제, 활성화 또는 비활성화하기 위해서는 일부라도 인덱스를 보유하는 모든 파일 그룹이 온라인 상태여야 합니다.  
  
 오프라인 파일 그룹을 복원하는 방법은 [온라인 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/online-restore-sql-server.md)을 참조하세요.  
  
##  <a name="database-mirroring-and-backup-and-restore"></a><a name="DbMandBnR"></a> 데이터베이스 미러링, 백업 및 복원  
 이 섹션에서는 여러 개의 파일 그룹이 있는 전체 모델 데이터베이스와 관련된 내용을 다룹니다.  
  
> [!NOTE]  
>  이후 버전의 Microsoft [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서는 데이터베이스 미러링 기능이 제거됩니다. 새 개발 작업에서는 이 기능을 사용하지 않도록 하고, 현재 이 기능을 사용하는 애플리케이션은 수정하세요. 대신 [!INCLUDE[ssHADR](../../includes/sshadr-md.md)]를 사용하세요.  
  
 데이터베이스 미러링은 데이터베이스의 가용성을 높이기 위한 솔루션입니다. 미러링은 데이터베이스 단위로 구현되며 전체 복구 모델을 사용하는 데이터베이스에서만 작동합니다. 자세한 내용은 [데이터베이스 미러링&#40;SQL Server&#41;](../../database-engine/database-mirroring/database-mirroring-sql-server.md)을 참조하세요.  
  
> [!NOTE]  
>  데이터베이스에서 파일 그룹의 하위 집합 복사본을 배포하려면 복제를 이용하세요. 다른 서버로 복사할 파일 그룹의 개체만 복제해야 합니다. 복제에 대한 자세한 내용은 [SQL Server 복제](../../relational-databases/replication/sql-server-replication.md)를 참조하세요.  
  
### <a name="creating-the-mirror-database"></a>미러 데이터베이스 만들기  
 미러 데이터베이스는 미러 서버에서 주 데이터베이스의 백업을 복구하지 않고 복원함으로써 생성됩니다. 복원 시 동일한 데이터베이스 이름을 유지해야 합니다. 자세한 내용은 [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)을 사용합니다.  
  
 지원되는 경우 증분 복원 시퀀스를 사용하여 미러 데이터베이스를 만들 수 있습니다. 그러나 파일 그룹을 모두 복원하기 전까지는 미러링을 시작할 수 없으며 일반적으로 미러 데이터베이스를 가져오기 위한 복원된 로그 백업은 주 데이터베이스에 의해 지정 시간 내에 닫을 수 있습니다. 자세한 내용은 [증분 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/piecemeal-restores-sql-server.md)을 참조하세요.  
  
### <a name="restrictions-on-backup-and-restore-during-mirroring"></a>미러링 도중 백업 및 복원에 대한 제한 사항  
 데이터베이스 미러링 세션이 활성화되어 있는 동안에는 다음과 같은 제한 사항이 적용됩니다.  
  
-   미러 데이터베이스의 백업 및 복원이 허용되지 않습니다.  
  
-   주 데이터베이스의 백업은 허용되지만 BACKUP LOG WITH NORECOVERY는 허용되지 않습니다.  
  
-   주 데이터베이스 복원이 허용되지 않습니다.  
  
##  <a name="piecemeal-restore-and-full-text-indexes"></a><a name="PiecemealAndFTIndexes"></a> 증분 복원 및 전체 텍스트 인덱스  
 이 섹션에서는 여러 개의 파일 그룹이 있는 데이터베이스와 관련된 내용 및 단순 모델 데이터베이스의 경우 읽기 전용 파일 그룹과 관련된 내용을 다룹니다.  
  
 전체 텍스트 인덱스는 데이터베이스 파일 그룹에 저장되며 증분 복원의 영향을 받을 수 있습니다. 전체 텍스트 인덱스가 관련 테이블 데이터와 동일한 파일 그룹에 있는 경우 증분 복원은 올바르게 동작합니다.  
  
> [!NOTE]  
>  전체 텍스트 인덱스가 포함된 파일 그룹의 파일 그룹 ID를 보려면 [sys.fulltext_indexes](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)의 data_space_id 열을 선택합니다.  
  
### <a name="full-text-indexes-and-tables-in-separate-filegroups"></a>분리된 파일 그룹 내의 전체 텍스트 인덱스 및 테이블  
 전체 텍스트 인덱스가 모든 관련 테이블 데이터와 별개의 파일 그룹에 존재하는 경우 증분 복원의 동작은 어느 파일 그룹이 먼저 복원되어 온라인 상태가 되는지에 따라 달라집니다.  
  
-   전체 텍스트 인덱스가 포함된 파일 그룹이 관련 테이블 데이터가 포함된 파일 그룹보다 먼저 복원되어 온라인 상태가 되는 경우 전체 텍스트 검색은 전체 텍스트 인덱스가 온라인 상태가 된 직후부터 올바르게 동작합니다.  
  
-   테이블 데이터가 포함된 파일 그룹이 전체 텍스트 인덱스가 포함된 파일 그룹보다 먼저 복원되어 온라인 상태가 되는 경우 전체 텍스트 동작이 영향을 받을 수 있습니다. 이는 채우기를 트리거하고 카탈로그를 다시 작성하거나 카탈로그를 인식하는 [!INCLUDE[tsql](../../includes/tsql-md.md)] 문은 인덱스가 온라인 상태가 될 때까지 실패하기 때문입니다. 이러한 문에는 CREATE FULLTEXT INDEX, ALTER FULLTEXT INDEX, DROP FULLTEXT INDEX 및 ALTER FULLTEXT CATALOG가 포함됩니다.  
  
     이 경우 다음과 같은 사항이 중요합니다.  
  
    -   전체 텍스트 인덱스에 변경 내용 추적이 있는 경우 사용자 DML은 인덱스 파일 그룹이 온라인 상태가 될 때까지 실패합니다. 삭제 작업도 인덱스 파일 그룹이 온라인 상태가 될 때까지 실패합니다.  
  
    -   인덱스를 사용할 수 없으므로 변경 내용 추적에 관계 없이 전체 텍스트 쿼리는 실패합니다. 전체 텍스트 인덱스가 포함된 파일 그룹이 오프라인일 때 전체 텍스트 쿼리를 시도하면 오류가 반환됩니다.  
  
    -   상태 함수(예: FULLTEXTCATALOGPROPERTY)는 전체 텍스트 인덱스에 액세스할 필요가 없을 때에만 성공합니다. 예를 들어 온라인 전체 텍스트 메타데이터에 대한 액세스는 성공하지만 **uniquekeycount, itemcount** 는 실패합니다.  
  
     전체 텍스트 인덱스 파일 그룹을 복원하여 온라인 상태로 만든 후에는 인덱스 데이터와 테이블 데이터가 일치합니다.  
  
 기본 테이블 파일 그룹과 전체 텍스트 인덱스 파일 그룹이 모두 온라인 상태가 된 직후부터 일시 중지된 전체 텍스트 채우기가 재개됩니다.  
  
##  <a name="file-backup-and-restore-and-compression"></a><a name="FileBnRandCompression"></a> 파일 백업과 복원 및 압축  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 읽기 전용 파일 그룹과 읽기 전용 데이터베이스에 대한 NTFS 파일 시스템 데이터 압축을 지원합니다.  
  
 압축된 NTFS 파일에 대해 읽기 전용 파일 그룹의 파일 복원이 지원됩니다. 이러한 파일 그룹의 백업 및 복원은 기본적으로 모든 읽기 전용 파일 그룹에서와 동일하게 동작하지만 다음과 같은 예외가 있습니다.  
  
-   읽기/쓰기 파일(읽기/쓰기 데이터베이스의 기본 또는 로그 파일 포함)을 압축된 볼륨으로 복원하는 경우 실패하고 오류 메시지가 표시됩니다.  
  
-   읽기 전용 데이터베이스의 경우 압축된 볼륨으로 복원할 수 있습니다.  
  
> [!NOTE]  
>  읽기/쓰기 데이터베이스의 로그 파일은 압축 파일 시스템에 저장할 수 없습니다.  
  
##  <a name="related-tasks"></a><a name="RelatedTasks"></a> 관련 작업  
  
-   [미러 데이터베이스의 미러링 준비&#40;SQL Server&#41;](../../database-engine/database-mirroring/prepare-a-mirror-database-for-mirroring-sql-server.md)  
  
-   [전체 텍스트 카탈로그와 인덱스 백업 및 복원](../../relational-databases/search/back-up-and-restore-full-text-catalogs-and-indexes.md)  
  
## <a name="see-also"></a>참고 항목  
 [SQL Server 데이터베이스 백업 및 복원](../../relational-databases/backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [복제된 데이터베이스 백업 및 복원](../../relational-databases/replication/administration/back-up-and-restore-replicated-databases.md)   
[활성 보조 복제본: 보조 복제본에 백업\((Always On 가용성 그룹)\)](../../database-engine/availability-groups/windows/active-secondaries-backup-on-secondary-replicas-always-on-availability-groups.md)  
  
  
