---
title: 백업 및 복원으로 데이터베이스 복사 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- full-text search [SQL Server], back up and restore
- restoring databases [SQL Server], previous SQL Server versions
- database restores [SQL Server], copying databases
- restoring databases [SQL Server], onto another server instance
- restoring [SQL Server], onto another server instance
- backing up databases [SQL Server], copying databases
- database backups [SQL Server], copying databases
ms.assetid: b93e9701-72a0-408e-958c-dc196872c040
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b51404c994bd4a5029bc9e2d592db020747492fb
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48057193"
---
# <a name="copy-databases-with-backup-and-restore"></a>백업 및 복원으로 데이터베이스 복사
  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서는 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상 버전을 사용하여 만든 사용자 데이터베이스 백업을 복원하여 새 데이터베이스를 만들 수 있습니다. 그러나 이전 **버전을 사용하여 만든**master **,** model **및** msdb [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업은 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]를 통해 복원할 수 없습니다. 또한 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 백업을 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]로 복원할 수도 없습니다.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 는 이전 버전과는 다른 기본 경로를 사용합니다. 따라서 이전 버전의 기본 위치에 만든 데이터베이스 백업을 복원하려면 MOVE 옵션을 사용해야 합니다. 새 기본 경로에 대한 자세한 내용은 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)를 참조하십시오. 데이터베이스 파일을 이동하는 방법은 이 항목의 뒷부분에 나오는 "데이터베이스 파일 이동"을 참조하십시오.  
  
## <a name="general-steps-for-using-backup-and-restore-to-copy-a-database"></a>백업과 복원을 사용하여 데이터베이스를 복사하는 일반적인 단계  
 백업과 복원을 사용하여 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]의 다른 인스턴스로 데이터베이스를 복사할 때는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]가 실행되는 모든 플랫폼이 원본 컴퓨터 및 대상 컴퓨터가 될 수 있습니다.  
  
 일반적인 단계는 다음과 같습니다.  
  
1.  [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 이상의 인스턴스에 있을 수 있는 원본 데이터베이스를 백업합니다. 이 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 인스턴스가 실행 중인 컴퓨터가 *원본 컴퓨터*입니다.  
  
2.  데이터베이스 복사 하려는 컴퓨터의 (합니다 *대상 컴퓨터*)의 인스턴스에 연결할 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 에서 데이터베이스를 복원 하려고 하는 합니다. 필요한 경우 대상 서버 인스턴스에 원본 데이터베이스의 백업에 사용된 것과 같은 백업 장치를 만듭니다.  
  
3.  대상 컴퓨터에서 원본 데이터베이스의 백업을 복원합니다. 데이터베이스를 복원하면 자동으로 모든 데이터베이스 파일이 생성됩니다.  
  
 다음 항목에서는 이 프로세스에 영향을 줄 수 있는 추가 고려 사항에 대해 설명합니다.  
  
## <a name="before-you-restore-database-files"></a>데이터베이스 파일을 복원하기 전 고려 사항  
 데이터베이스를 복원하면 복원 중인 데이터베이스에 필요한 데이터베이스 파일이 자동으로 생성됩니다. 기본적으로 복원 프로세스 중에 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 만든 파일은 원본 컴퓨터에 있는 원본 데이터베이스의 백업 파일과 같은 이름과 경로를 사용합니다.  
  
 원하는 경우 데이터베이스를 복원할 때 장치 매핑, 파일 이름 또는 데이터베이스 복원 경로를 지정할 수 있습니다. 이 방법은 다음과 같은 경우 유용합니다.  
  
-   원래 컴퓨터에서 데이터베이스에 사용된 디렉터리 구조나 드라이브 매핑이 다른 컴퓨터에는 존재하지 않는 경우. 예를 들어 백업에 포함된 파일이 기본적으로 E 드라이브에 복원되는데 대상 컴퓨터에는 E 드라이브가 없을 수 있습니다.  
  
-   대상 위치의 공간이 부족한 경우.  
  
-   복원 대상에 있는 데이터베이스 이름을 다시 사용하며, 데이터베이스의 모든 파일 이름이 백업 집합의 데이터베이스 파일 이름과 동일하게 지정되는 경우에는 다음 중 한 가지 현상이 발생합니다.  
  
    -   기존 데이터베이스 파일을 덮어쓸 수 있는 경우 덮어씁니다. 이 경우 다른 데이터베이스 이름이 속하는 파일에는 아무런 영향이 없습니다.  
  
    -   기존 파일을 덮어쓸 수 없는 경우 복원 오류가 발생합니다.  
  
 오류 및 복원 작업 전에 의도 하지 않은 결과 방지 하려면 사용 합니다 [backupfile](/sql/relational-databases/system-tables/backupfile-transact-sql) 복원 하려는 백업에서 데이터베이스 및 로그 파일을 확인 하려면 기록 테이블입니다.  
  
## <a name="moving-the-database-files"></a>데이터베이스 파일 이동  
 위에서 설명한 이유 때문에 데이터베이스 백업 내의 파일을 대상 컴퓨터에 복원할 수 없으면 복원 도중에 이 파일을 새 위치로 이동해야 합니다. 이는 아래와 같이 함수의 반환값을 데이터 프레임으로 바로 변환하는 데 사용할 수 있음을 나타냅니다.  
  
-   이전 버전의 기본 위치에 만든 백업에서 데이터베이스를 복원하려는 경우  
  
-   용량을 고려해야 하기 때문에 백업의 데이터베이스 파일 일부를 다른 드라이브로 복원해야 할 경우. 이는 조직 내에 있는 대부분의 컴퓨터가 디스크 드라이브의 크기 및 번호가 다르고 소프트웨어 구성이 같지 않기 때문에 흔히 있는 일입니다.  
  
-   테스트용으로 같은 컴퓨터에 기존 데이터베이스의 복사본을 만들 경우. 이 경우 원래 데이터베이스에 대한 데이터베이스 파일이 이미 존재하므로 복사 작업 중에 데이터베이스 복사본을 만들 때 파일 이름을 다르게 지정해야 합니다.  
  
 자세한 내용은 이 항목의 뒷부분에 나오는 "파일과 파일 그룹을 새 위치로 복원"을 참조하십시오.  
  
## <a name="changing-the-database-name"></a>데이터베이스 이름 변경  
 데이터베이스를 대상 컴퓨터에 복원할 때 데이터베이스를 먼저 복원한 다음 이름을 수동으로 변경하지 않고도 데이터베이스 이름을 변경할 수 있습니다. 예를 들어 데이터베이스 이름을 **Sales** 에서 **SalesCopy** 로 변경하면 이것이 데이터베이스의 복사본임을 나타낼 수 있습니다.  
  
 데이터베이스를 복원할 때 명시적으로 제공한 데이터베이스 이름은 자동으로 새 데이터베이스의 이름으로 사용됩니다. 데이터베이스 이름이 기존에 존재하지 않기 때문에 백업에 있는 파일을 사용하여 새 이름을 만듭니다.  
  
## <a name="when-upgrading-a-database-by-using-restore"></a>복원을 사용하여 데이터베이스를 업그레이드하는 경우  
 이전 버전에서 백업을 복원할 때는 백업에 있는 각각의 전체 텍스트 카탈로그의 경로(드라이브 및 디렉터리)가 대상 컴퓨터에 존재하는지 미리 알아 두면 도움이 됩니다. 카탈로그 파일을 비롯하여 백업에 있는 모든 파일의 논리적 이름, 물리적 이름, 경로 및 파일 이름을 나열하려면 RESTORE FILELISTONLY FROM *<backup_device>* 문을 사용합니다. 자세한 내용은 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)를 참조하세요.  
  
 대상 컴퓨터에 같은 경로가 존재하지 않을 경우 다음 두 가지 대체 방법이 있습니다.  
  
-   대상 컴퓨터에 원본과 동일한 드라이브/디렉터리 매핑을 만듭니다.  
  
-   RESTORE DATABASE 문 안에 WITH MOVE 절을 사용하여 복원 작업을 하는 중에 카탈로그 파일을 새 위치로 이동합니다. 자세한 내용은 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)를 통해 복원할 수 없습니다.  
  
 다른 전체 텍스트 인덱스 업그레이드 옵션에 대한 자세한 내용은 [전체 텍스트 검색 업그레이드](../search/upgrade-full-text-search.md)를 참조하세요.  
  
## <a name="database-ownership"></a>데이터베이스 소유권  
 데이터베이스를 다른 컴퓨터에서 복원할 때 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로그인 또는 복원 작업을 시작하는 [!INCLUDE[msCoName](../../includes/msconame-md.md)] Windows 사용자가 자동으로 새 데이터베이스 소유자가 됩니다. 데이터베이스를 복원할 때 시스템 관리자나 새 데이터베이스 소유자는 데이터베이스 소유권을 변경할 수 있습니다. 데이터베이스가 무단으로 복원되는 것을 방지하려면 미디어 또는 백업 세트에 암호를 사용하십시오.  
  
## <a name="managing-metadata-when-restoring-to-another-server-instance"></a>다른 서버 인스턴스로 복원 시 메타데이터 관리  
 데이터베이스를 다른 서버 인스턴스로 복원하는 경우 사용자와 응용 프로그램에 일관된 환경을 제공하려면 로그인, 작업 등 데이터베이스의 일부 또는 모든 메타데이터를 다른 서버 인스턴스에서 다시 만들어야 할 수도 있습니다. 자세한 내용은 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리&#40;SQL Server&#41;](manage-metadata-when-making-a-database-available-on-another-server.md)을 참조하세요.  
  
 **백업 세트의 데이터와 로그 파일을 보려면**  
  
-   [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)  
  
 **새 위치로 파일 및 파일 그룹을 복원 하려면**  
  
-   [새 위치로 파일 복원&#40;SQL Server&#41;](../backup-restore/restore-files-to-a-new-location-sql-server.md)  
  
-   [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](../backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **기존 파일에서 파일과 파일 그룹 복원**  
  
-   [기존 파일에서 파일 및 파일 그룹 복원&#40;SQL Server&#41;](../backup-restore/restore-files-and-filegroups-over-existing-files-sql-server.md)  
  
 **새 이름의 데이터베이스를 복원 하려면**  
  
-   [데이터베이스 백업 복원 &#40;SQL Server Management Studio&#41;](../backup-restore/restore-a-database-backup-using-ssms.md)  
  
 **중단된 된 복원 작업을 다시 시작**  
  
-   [중단된 복원 작업 다시 시작&#40;Transact-SQL&#41;](../backup-restore/restart-an-interrupted-restore-operation-transact-sql.md)  
  
 **데이터베이스의 소유자를 변경 하려면**  
  
-   [sp_changedbowner&#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedbowner-transact-sql)  
  
 **SQL Server Management Objects (SMO)를 사용 하 여 데이터베이스 복사**  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReadFileList%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.RelocateFiles%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore.ReplaceDatabase%2A>  
  
-   <xref:Microsoft.SqlServer.Management.Smo.Restore>  
  
## <a name="see-also"></a>관련 항목  
 [데이터베이스를 다른 서버로 복사](copy-databases-to-other-servers.md)   
 [SQL Server 기본 인스턴스 및 명명된 인스턴스의 파일 위치](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)   
 [RESTORE FILELISTONLY&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-filelistonly-transact-sql)   
 [RESTORE&#40;Transact-SQL&#41;](/sql/t-sql/statements/restore-statements-transact-sql)  
  
  
