---
title: 백업 개요(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- tables [SQL Server], backing up data
- backups [SQL Server]
- database backups [SQL Server]
- backup types [SQL Server]
- data backups [SQL Server]
- backing up tables [SQL Server]
- database restores [SQL Server], backups
- backing up [SQL Server], about backing up
- restoring [SQL Server], backup types
- backups [SQL Server], about
- backups [SQL Server], table-level backups unsupported
ms.assetid: 09a6e0c2-d8fd-453f-9aac-4ff24a97dc1f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 2b3b550ec7eb42597862c5b20e557aabdc909f13
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62922124"
---
# <a name="backup-overview-sql-server"></a>Backup Overview (SQL Server)
  이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 구성 요소에 대해 소개합니다. 데이터를 보호하려면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 백업해야 합니다. 여기서는 백업 유형과 백업 제한 사항에 대해 설명합니다. 또한 이 항목에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 디바이스와 백업 미디어를 소개합니다.  
  
 **항목 내용:**  
  
-   [구성 요소 및 개념](#TermsAndDefinitions)  
  
-   [백업 압축](#BackupCompression)  
  
-   [SQL Server에서 백업 작업에 대 한 제한](#Restrictions)  
  
-   [관련 작업](#RelatedTasks)  
  
##  <a name="TermsAndDefinitions"></a> 구성 요소 및 개념  
 백업[동사]  
 데이터 또는 로그 레코드를 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스 또는 해당 트랜잭션 로그에서 백업 디바이스(예: 디스크)로 복사하여 데이터 백업 또는 로그 백업을 만들 수 있습니다.  
  
 백업[명사]  
 오류가 발생한 이후에 데이터를 복원 및 복구하는 데 사용할 수 있는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 복사본입니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터 백업은 데이터베이스나 데이터베이스에 있는 하나 이상의 파일 또는 파일 그룹 수준에서 만들어집니다. 테이블 수준 백업은 만들 수 없습니다. 데이터 백업뿐만 아니라 전체 복구 모델에서는 트랜잭션 로그 백업도 만들어야 합니다.  
  
 [복구 모델](recovery-models-sql-server.md)  
 데이터베이스에서 트랜잭션 로그 유지 관리를 제어하는 데이터베이스 속성입니다. 사용할 수 있는 복구 모델은 3가지로 단순, 전체 및 대량 로그 복구 모델입니다. 데이터베이스의 복구 모델에 따라 백업 및 복원 요구 사항이 결정됩니다.  
  
 [복원(restore)](restore-and-recovery-overview-sql-server.md)  
 지정된 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업에서 지정된 데이터베이스로 모든 데이터 및 로그 페이지를 복사하고 기록된 변경 사항을 적용하여 데이터를 최신 상태로 전환함으로써 백업에 기록된 모든 트랜잭션을 롤포워드하는 다단계 프로세스입니다.  
  
 **백업 유형**  
  
 [copy-only backup](copy-only-backups-sql-server.md)  
 정기적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 특수 백업입니다.  
  
 데이터 백업(data backup)  
 전체 데이터베이스(데이터베이스 백업), 부분 데이터베이스(부분 백업) 또는 데이터 파일 집합이나 파일 그룹(파일 백업)의 데이터 백업입니다.  
  
 [데이터베이스 백업(database backup)](full-database-backups-sql-server.md)  
 데이터베이스 백업입니다. 전체 데이터베이스 백업은 백업이 완료된 시점의 전체 데이터베이스를 나타냅니다. 차등 데이터베이스 백업은 가장 최근의 전체 데이터베이스 백업 이후에 데이터베이스에 수행된 변경 내용만 포함합니다.  
  
 [차등 백업(differential backup)](full-database-backups-sql-server.md)  
 전체 또는 부분 데이터베이스, 데이터 파일 집합 또는 파일 그룹( *차등 기반*)에 대한 최신 전체 백업을 기반으로 하고, 해당 차등 기준 이후에 변경된 데이터 범위만 포함하는 데이터 백업입니다.  
  
 차등 부분 백업은 차등 기반이라고 하는 이전 부분 백업 이후에 파일 그룹에서 변경된 데이터 익스텐트만 기록합니다.  
  
 전체 백업(full backup)  
 특정 데이터베이스나 파일 그룹 또는 파일 집합에 있는 모든 데이터와 그러한 데이터를 복구할 수 있을 만큼의 로그를 포함하는 데이터 백업입니다.  
  
 [로그 백업(log backup)](transaction-log-backups-sql-server.md)  
 이전 로그 백업에서 백업되지 않은 모든 로그 레코드를 포함하는 트랜잭션 로그 백업입니다. (전체 복구 모델)  
  
 [파일 백업](full-file-backups-sql-server.md)  
 하나 이상의 데이터베이스 파일 또는 파일 그룹에 대한 백업입니다.  
  
 [부분 백업](partial-backups-sql-server.md)  
 주 파일 그룹, 모든 읽기/쓰기 파일 그룹 및 필요에 따라 지정된 읽기 전용 파일을 비롯하여 데이터베이스에 있는 일부 파일 그룹의 데이터만 포함합니다.  
  
 **백업 미디어 용어 및 정의**  
  
 [백업 장치](backup-devices-sql-server.md)  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업이 기록되는 대상이자 백업을 복원하는 원본이 되는 디스크 또는 테이프 장치입니다. SQL Server 백업은 Windows Azure Blob 스토리지 서비스에 기록할 수도 있으며 백업 파일의 대상과 이름을 지정하기 위해 **URL** 형식이 사용됩니다. 자세한 내용은 [Windows Azure Blob Storage 서비스로 SQL Server 백업 및 복원](sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.  
  
 [백업 미디어](media-sets-media-families-and-backup-sets-sql-server.md)  
 하나 이상의 백업이 기록된 하나 이상의 테이프 또는 디스크 파일입니다.  
  
 [백업 세트(backup set)](media-sets-media-families-and-backup-sets-sql-server.md)  
 백업 작업이 성공할 때 미디어 세트에 추가되는 백업 내용입니다.  
  
 [미디어 패밀리(media family)](media-sets-media-families-and-backup-sets-sql-server.md)  
 미디어 세트의 미러되지 않은 단일 디바이스나 일련의 미러된 디바이스에 생성된 백업입니다.  
  
 [미디어 세트(media set)](media-sets-media-families-and-backup-sets-sql-server.md)  
 하나 이상의 백업 작업에서 고정된 유형과 개수의 백업 디바이스를 사용하여 기록한 백업 미디어, 테이프 또는 디스크 파일의 모음입니다.  
  
 [미러된 미디어 세트](mirrored-backup-media-sets-sql-server.md)  
 미디어 세트의 여러 복사본(미러)입니다.  
  
##  <a name="BackupCompression"></a> 백업 압축  
 [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상 버전에서 압축 백업을 지원하며, [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] 이상 버전에서 압축된 백업을 복원할 수 있습니다. 자세한 내용은 [백업 압축&#40;SQL Server&#41;](backup-compression-sql-server.md)을 참조하세요.  
  
##  <a name="Restrictions"></a> SQL Server에서 백업 작업에 대 한 제한  
 백업은 데이터베이스가 온라인 상태이며 사용 중인 경우 발생할 수 있습니다. 그러나 다음과 같은 제한 사항이 있습니다.  
  
### <a name="offline-data-cannot-be-backed-up"></a>오프라인 데이터는 백업할 수 없음  
 오프라인 데이터를 암시적으로 또는 명시적으로 참조하는 백업 작업은 실패합니다. 그러한 경우를 몇 가지 예로 들면 다음과 같습니다.  
  
-   전체 데이터베이스 백업을 요청하지만 데이터베이스의 파일 그룹 한 개가 오프라인입니다. 모든 파일 그룹이 암시적으로 전체 데이터베이스 백업에 포함되므로 이 작업은 실패합니다.  
  
     이 데이터베이스를 백업하려면 파일 백업을 사용하고 온라인 파일 그룹만 지정합니다.  
  
-   부분 백업을 요청하지만 읽기/쓰기 파일 그룹이 오프라인입니다. 부분 백업에는 모든 읽기/쓰기 파일 그룹이 필요하므로 작업은 실패합니다.  
  
-   특정 파일의 파일 백업을 요청하지만 파일 중 하나가 온라인이 아닙니다. 작업은 실패합니다. 온라인 파일을 백업하려면 파일 목록에서 오프라인 파일을 생략하고 작업을 반복합니다.  
  
 일반적으로 로그 백업은 하나 이상의 데이터 파일을 사용할 수 없더라도 성공적으로 수행됩니다. 그러나 일부 파일에 대량 로그 복구 모델에서 수행된 대량 로그 변경 내용이 포함되어 있는 경우 모든 파일이 온라인 상태에 있어야 백업이 성공합니다.  
  
### <a name="concurrency-restrictions-during-backup"></a>백업 중 동시성 제한 사항  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서는 온라인 백업 프로세스를 사용하여 데이터베이스가 사용 중일 때도 데이터베이스 백업을 수행할 수 있습니다. 백업 시 대부분의 작업을 수행할 수 있습니다. 예를 들어 INSERT, UPDATE 또는 DELETE 문은 백업 작업 시에도 사용할 수 있습니다. 그러나 데이터베이스 파일을 만들거나 삭제하는 동안 백업 작업을 시작하려고 하면 만들기 또는 삭제 작업이 완료되거나 백업 시간 제한이 초과될 때까지 백업 작업이 대기합니다.  
  
 데이터베이스 백업 또는 트랜잭션 로그 백업 시에 실행할 수 없는 작업은 다음과 같습니다.  
  
-   ADD FILE이나 REMOVE FILE 옵션과 함께 사용되는 ALTER DATABASE 문 등의 파일 관리 작업  
  
-   데이터베이스 축소 또는 파일 축소 작업. 자동 축소 작업도 포함됩니다.  
  
-   백업 작업이 진행 중일 때는 데이터베이스 파일을 만들거나 삭제하려고 해도 해당 작업이 실패합니다.  
  
 백업 작업이 파일 관리 작업 또는 축소 작업과 겹치면 충돌이 발생합니다. 충돌하는 작업 중 어떤 작업이 먼저 시작되었는지에 관계없이 두 번째 작업은 첫 번째 작업에서 설정한 잠금 제한 시간이 초과될 때까지 대기합니다. 제한 시간은 세션 제한 시간 설정에서 제어합니다. 제한 시간 동안에 잠금이 해제되면 두 번째 작업이 계속됩니다. 잠금 제한 시간이 초과되면 두 번째 작업이 실패합니다.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **백업 장치와 백업 미디어를 사용 하려면**  
  
-   [디스크 파일에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-disk-file-sql-server.md)  
  
-   [테이프 드라이브에 대한 논리적 백업 장치 정의&#40;SQL Server&#41;](define-a-logical-backup-device-for-a-tape-drive-sql-server.md)  
  
-   [디스크 또는 테이프를 백업 대상으로 지정&#40;SQL Server&#41;](specify-a-disk-or-tape-as-a-backup-destination-sql-server.md)  
  
-   [백업 장치 삭제&#40;SQL Server&#41;](delete-a-backup-device-sql-server.md)  
  
-   [백업의 만료 날짜 설정&#40;SQL Server&#41;](set-the-expiration-date-on-a-backup-sql-server.md)  
  
-   [백업 테이프 또는 파일의 내용 보기&#40;SQL Server&#41;](view-the-contents-of-a-backup-tape-or-file-sql-server.md)  
  
-   [백업 세트의 데이터와 로그 파일 보기&#40;SQL Server&#41;](view-the-data-and-log-files-in-a-backup-set-sql-server.md)  
  
-   [논리적 백업 장치의 속성 및 내용 보기&#40;SQL Server&#41;](view-the-properties-and-contents-of-a-logical-backup-device-sql-server.md)  
  
-   [장치에서 백업 복원&#40;SQL Server&#41;](restore-a-backup-from-a-device-sql-server.md)  
  
-   [자습서: Microsoft Azure Blob Storage Service로 SQL Server 백업 및 복원](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
 **백업을 만들려면**  
  
> [!NOTE]  
>  부분 또는 복사 전용 백업의 경우 각각 PARTIAL 또는 COPY_ONLY 옵션과 함께 [!INCLUDE[tsql](../../includes/tsql-md.md)][BACKUP](/sql/t-sql/statements/backup-transact-sql) 문을 사용해야 합니다.  
  
-   [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)  
  
-   [트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-a-transaction-log-sql-server.md)  
  
-   [파일 및 파일 그룹 백업&#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-differential-database-backup-sql-server.md)  
  
-   [데이터베이스가 손상된 경우 트랜잭션 로그 백업&#40;SQL Server&#41;](back-up-the-transaction-log-when-the-database-is-damaged-sql-server.md)  
  
-   [백업 또는 복원 중 백업 체크섬 설정 또는 해제&#40;SQL Server&#41;](enable-or-disable-backup-checksums-during-backup-or-restore-sql-server.md)  
  
-   [오류 발생 후 백업 또는 복원 작업 계속 또는 중지 여부 지정&#40;SQL Server&#41;](specify-if-backup-or-restore-continues-or-stops-after-error.md)  
  
-   [Resource GovernoR을 사용하여 백업 압축을 통해 CPU 사용량 제한&#40;Transact-SQL&#41;](use-resource-governor-to-limit-cpu-usage-by-backup-compression-transact-sql.md)  
  
-   [자습서: Microsoft Azure Blob Storage Service로 SQL Server 백업 및 복원](../tutorial-sql-server-backup-and-restore-to-azure-blob-storage-service.md)  
  
## <a name="see-also"></a>관련 항목  
 [SQL Server 데이터베이스 백업 및 복원](back-up-and-restore-of-sql-server-databases.md)   
 [복원 및 복구 개요&#40;SQL Server&#41;](restore-and-recovery-overview-sql-server.md)   
 [유지 관리 계획](../maintenance-plans/maintenance-plans.md)   
 [트랜잭션 로그&#40;SQL Server&#41;](../logs/the-transaction-log-sql-server.md)   
 [복구 모델&#40;SQL Server&#41;](recovery-models-sql-server.md)  
  
  
