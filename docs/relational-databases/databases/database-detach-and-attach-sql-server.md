---
title: "데이터베이스 분리 및 연결(SQL Server) | Microsoft 문서"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- upgrading databases
- databases [SQL Server], detaching
- detach database [SQL Server]
- databases [SQL Server], attaching
- removing databases
- transaction logs [SQL Server], detaching
- databases [SQL Server], removing
- restoring [SQL Server], attached databases
- transaction logs [SQL Server], attaching
- differential backups, after detaching
- moving databases
- attach database [SQL Server]
- detaching databases [SQL Server]
- differential base [SQL Server]
- attaching databases [SQL Server]
- databases [SQL Server], moving
ms.assetid: d0de0639-bc54-464e-98b1-6af22a27eb86
caps.latest.revision: 98
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: f95cd17c64efff4731b77ba42df3b5dc656f2cf9
ms.lasthandoff: 04/11/2017

---
# <a name="database-detach-and-attach-sql-server"></a>데이터베이스 분리 및 연결(SQL Server)
  데이터베이스의 데이터 및 트랜잭션 로그 파일은 분리할 수 있으며 동일한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스나 다른 인스턴스에 다시 연결할 수 있습니다. 데이터베이스 분리 및 연결은 데이터베이스를 같은 컴퓨터의 다른 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스로 변경하거나 데이터베이스를 이동하는 경우 유용합니다.  
  
  
##  <a name="Security"></a> 보안  
 파일 액세스 권한은 데이터베이스 분리, 연결 등의 여러 데이터베이스 작업 중에 설정됩니다.  
  
> [!IMPORTANT]  
>  알 수 없거나 신뢰할 수 없는 출처의 데이터베이스는 연결 또는 복원하지 않는 것이 좋습니다. 이러한 데이터베이스에 포함된 악성 코드가 의도하지 않은 [!INCLUDE[tsql](../../includes/tsql-md.md)] 코드를 실행하거나 스키마 또는 물리적 데이터베이스 구조를 수정하여 오류가 발생할 수 있습니다. 알 수 없거나 신뢰할 수 없는 소스의 데이터베이스를 사용하기 전에 비프로덕션 서버의 데이터베이스에서 [DBCC CHECKDB](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md) 를 실행하여 데이터베이스에서 코드(예: 저장 프로시저 또는 다른 사용자 정의 코드)를 시험해 보세요.  
  
##  <a name="DetachDb"></a> 데이터베이스 분리  
 데이터베이스를 분리하면 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스에서 해당 데이터베이스가 제거되지만 데이터베이스의 데이터 파일 및 트랜잭션 로그 파일은 그대로 유지됩니다. 이 파일은 데이터베이스가 분리된 해당 서버뿐 아니라 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스가 실행되는 모든 컴퓨터에 데이터베이스를 연결하는 데 사용할 수 있습니다.  
  
 다음 중 하나라도 해당하는 경우 데이터베이스를 분리할 수 없습니다.  
  
-   데이터베이스를 복제하여 게시한 경우. 데이터베이스가 복제된 경우 해당 데이터베이스의 게시를 해제해야 합니다. 따라서 데이터베이스를 분리하려면 먼저 [sp_replicationdboption](../../relational-databases/system-stored-procedures/sp-replicationdboption-transact-sql.md)을 실행하여 게시를 해제해야 합니다.  
  
    > [!NOTE]  
    >  **sp_replicationdboption**을 사용할 수 없는 경우 [sp_removedbreplication](../../relational-databases/system-stored-procedures/sp-removedbreplication-transact-sql.md)을 실행하여 복제를 제거할 수 있습니다.  
  
-   데이터베이스에 데이터베이스 스냅숏이 있는 경우  
  
     데이터베이스를 분리하려면 먼저 해당 데이터베이스의 모든 스냅숏을 삭제해야 합니다. 자세한 내용은 [데이터베이스 스냅숏 삭제&#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)인스턴스나 다른 인스턴스에 다시 연결할 수 있습니다.  
  
    > [!NOTE]  
    >  데이터베이스 스냅숏은 분리하거나 연결할 수 없습니다.  
  
-   데이터베이스가 데이터베이스 미러링 세션에서 미러되고 있는 경우.  
  
     데이터베이스는 세션이 종료된 후에야 분리될 수 있습니다. 자세한 내용은 [데이터베이스 미러링 제거&#40;SQL Server&#41;](../../database-engine/database-mirroring/removing-database-mirroring-sql-server.md)를 참조하세요.  
  
-   주의 대상 데이터베이스인 경우 주의 대상 데이터베이스는 분리할 수 없습니다. 분리하려면 먼저 데이터베이스를 응급 모드로 설정해야 합니다. 데이터베이스를 응급 모드로 설정하는 방법은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
-   데이터베이스가 시스템 데이터베이스인 경우  
  
### <a name="backup-and-restore-and-detach"></a>백업, 복원 및 분리  
 읽기 전용 데이터베이스를 분리하면 차등 백업의 차등 기반에 대한 정보가 손실됩니다. 자세한 내용은 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.  
  
### <a name="responding-to-detach-errors"></a>분리 오류에 대한 대처 방법  
 데이터베이스를 분리하는 동안 발생한 오류로 인해 데이터를 완전히 닫지 못하고 트랜잭션 로그를 다시 작성하지 못할 수 있습니다. 오류 메시지가 표시되면 다음의 수정 동작을 수행하세요.  
  
1.  주 파일뿐 아니라 데이터베이스와 관련된 모든 파일을 다시 연결합니다.  
  
2.  오류 메시지를 발생시킨 문제를 해결합니다.  
  
3.  데이터베이스를 다시 분리합니다.  
  
##  <a name="AttachDb"></a> 데이터베이스 연결  
 복사 또는 분리한 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 데이터베이스를 연결할 수 있습니다. [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 서버 인스턴스에 전체 텍스트 카탈로그 파일이 포함된 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 데이터베이스를 연결할 경우 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]에서와 같이 다른 데이터베이스 파일과 함께 이전 위치에서 카탈로그 파일이 연결됩니다. 자세한 내용은 [전체 텍스트 검색 업그레이드](../../relational-databases/search/upgrade-full-text-search.md)를 참조하세요.  
  
 데이터베이스를 연결할 경우 모든 데이터 파일(MDF 및 NDF 파일)이 사용 가능해야 합니다. 데이터베이스가 처음 생성되었을 때 또는 마지막으로 연결되었을 때와 경로가 다른 데이터 파일이 있으면 해당 파일의 현재 경로를 지정해야 합니다.  
  
> [!NOTE]  
>  연결되는 주 데이터 파일이 읽기 전용일 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 해당 데이터베이스를 읽기 전용으로 가정합니다.  
  
 암호화된 데이터베이스가 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스에 처음 연결된 경우 데이터베이스 소유자는 OPEN MASTER KEY DECRYPTION BY PASSWORD = **'***password***'**문을 실행하여 데이터베이스의 마스터 키를 열어야 합니다. 그런 다음 ALTER MASTER KEY ADD ENCRYPTION BY SERVICE MASTER KEY 문을 실행하여 데이터베이스 마스터 키의 자동 암호 해독을 설정하는 것이 좋습니다. 자세한 내용은 [CREATE MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/create-master-key-transact-sql.md) 및 [ALTER MASTER KEY&#40;Transact-SQL&#41;](../../t-sql/statements/alter-master-key-transact-sql.md)를 참조하세요.  
  
 로그 파일 연결 요구 사항은 데이터베이스가 읽기/쓰기인지 아니면 읽기 전용인지에 따라 다음과 같이 달라집니다.  
  
-   읽기 전용 데이터베이스에서는 보통 새 위치에 로그 파일을 연결할 수 있습니다. 그러나 경우에 따라 데이터베이스를 다시 연결하려면 기존 로그 파일이 필요합니다. 따라서 데이터베이스가 분리된 로그 파일 없이도 성공적으로 연결될 때까지 모든 분리된 로그 파일을 항상 보존하는 것이 중요합니다.  
  
     읽기/쓰기 데이터베이스에 로그 파일이 하나고 이 로그 파일에 새 위치를 지정하지 않은 경우 연결 작업에서 해당 파일의 이전 위치를 검색합니다. 로그 파일을 발견하면 데이터베이스가 완전히 종료되었는지 여부에 관계없이 이전 로그 파일을 사용합니다. 하지만 이전 로그 파일을 찾지 못하고 데이터베이스가 완전히 종료되었으며 활성 로그 체인이 없는 경우 연결 작업에서 해당 데이터베이스의 로그 파일을 새로 작성합니다.  
  
-   연결되는 주 데이터 파일이 읽기 전용일 경우 [!INCLUDE[ssDE](../../includes/ssde-md.md)] 은 해당 데이터베이스를 읽기 전용으로 가정합니다. 읽기 전용 데이터베이스에서 로그 파일 또는 파일은 데이터베이스의 주 파일에 지정된 위치에 있어야 합니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 가 주 파일에 저장된 로그 위치를 업데이트할 수 없으므로 새 로그 파일을 작성할 수 없기 때문입니다.  
  
  
###  <a name="Metadata"></a> 데이터베이스 연결 시 메타데이터 변경  
 읽기 전용 데이터베이스를 분리한 다음 다시 연결하는 경우 현재 차등 기반에 대한 백업 정보는 손실됩니다. *차등 기반* 은 데이터베이스나 데이터베이스에 있는 파일 또는 파일 그룹의 하위 집합에 있는 모든 데이터에 대한 최신 전체 백업입니다. 기반 백업 정보가 없는 경우 **master** 데이터베이스는 읽기 전용 데이터베이스와 동기화되지 않으므로 이후에 수행되는 차등 백업에서 예기치 않은 결과가 발생할 수 있습니다. 그러므로 읽기 전용 데이터베이스를 차등 백업하는 경우에는 데이터베이스를 다시 연결한 다음 전체 백업을 수행하여 새로운 차등 기반을 만들어야 합니다. 차등 백업에 대한 자세한 내용은 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)을 참조하세요.  
  
 연결 시 데이터베이스가 시작됩니다. 일반적으로 데이터베이스를 연결하면 데이터베이스를 분리 또는 복사한 시점과 동일한 상태가 됩니다. 그러나 연결 및 분리 작업을 수행하면 해당 데이터베이스의 데이터베이스 간 소유권 체인을 사용할 수 없게 됩니다. 체인을 사용하도록 설정하는 방법은 [cross db ownership chaining 서버 구성 옵션](../../database-engine/configure-windows/cross-db-ownership-chaining-server-configuration-option.md)을 참조하세요. 또한 데이터베이스를 연결할 때마다 TRUSTWORTHY는 OFF로 설정됩니다. TRUSTWORTHY를 ON으로 설정하는 방법은 [ALTER DATABASE&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql.md)를 참조하세요.  
  
### <a name="backup-and-restore-and-attach"></a>백업, 복원 및 연결  
 완전히 또는 부분적으로 오프라인 상태인 데이터베이스와 마찬가지로 파일을 복원 중인 데이터베이스에는 연결될 수 없습니다. 이때 복원 시퀀스를 중지하면 데이터베이스를 연결할 수 있습니다. 그런 다음 복원 시퀀스를 다시 시작할 수 있습니다.  
  
###  <a name="OtherServerInstance"></a> 다른 서버 인스턴스에 데이터베이스 연결  
  
> [!IMPORTANT]  
>  최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 만든 데이터베이스를 이전 버전에서 연결할 수 없습니다.  
  
 데이터베이스를 다른 서버 인스턴스에 연결하는 경우 사용자와 응용 프로그램에 일관된 환경을 제공하려면 로그인, 작업 등 데이터베이스의 일부 또는 모든 메타데이터를 다른 서버 인스턴스에서 다시 만들어야 할 수도 있습니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)를 참조하세요.  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
 **데이터베이스를 분리하려면**  
  
-   [sp_detach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-detach-db-transact-sql.md)  
  
-   [데이터베이스 분리](../../relational-databases/databases/detach-a-database.md)  
  
 **데이터베이스를 연결하려면**  
  
-   [CREATE DATABASE&#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)  
  
-   [데이터베이스 연결](../../relational-databases/databases/attach-a-database.md)  
  
-   [sp_attach_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-db-transact-sql.md)  
  
-   [sp_attach_single_file_db&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-attach-single-file-db-transact-sql.md)  
  
 **분리 및 연결 작업을 사용하여 데이터베이스를 업그레이드하려면**  
  
-   [분리 및 연결을 사용하여 데이터베이스 업그레이드&#40;Transact-SQL&#41;](../../relational-databases/databases/upgrade-a-database-using-detach-and-attach-transact-sql.md)  
  
 **분리 및 연결 작업을 사용하여 데이터베이스를 이동하려면**  
  
-   [분리 및 연결을 사용하여 데이터베이스 이동&#40;Transact-SQL&#41;](../../relational-databases/databases/move-a-database-using-detach-and-attach-transact-sql.md)  
  
 **데이터베이스 스냅숏을 삭제하려면**  
  
-   [데이터베이스 스냅숏 삭제&#40;Transact-SQL&#41;](../../relational-databases/databases/drop-a-database-snapshot-transact-sql.md)  
  
## <a name="see-also"></a>참고 항목  
 [데이터베이스 파일 및 파일 그룹](../../relational-databases/databases/database-files-and-filegroups.md)  
  
  
