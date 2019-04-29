---
title: 차등 데이터베이스 백업 만들기(SQL Server) | Microsoft 문서
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
helpviewer_keywords:
- full differential backups [SQL Server]
- database backups [SQL Server], full differential backups
- backing up databases [SQL Server], full differential backups
- backups [SQL Server], creating
ms.assetid: 70f49794-b217-4519-9f2a-76ed61fa9f99
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 4be1c196adbe21635c1339da3d5ec7ca519001fc
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62876603"
---
# <a name="create-a-differential-database-backup-sql-server"></a>차등 데이터베이스 백업 만들기(SQL Server)
  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] 또는 [!INCLUDE[tsql](../../includes/tsql-md.md)]을 사용하여 차등 데이터베이스 백업을 만드는 방법에 대해 설명합니다.  
  
 **항목 내용**  
  
-   **시작하기 전 주의 사항:**  
  
     [제한 사항](#Restrictions)  
  
     [필수 구성 요소](#Prerequisites)  
  
     [권장 사항](#Recommendations)  
  
     [보안](#Security)  
  
-   **다음을 사용하여 차등 데이터베이스 백업을 만듭니다.**  
  
     다른 도구는 [SQL Server Management Studio](#SSMSProcedure)  
  
     [Transact-SQL](#TsqlProcedure)  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전에  
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.  
  
###  <a name="Prerequisites"></a> 사전 요구 사항  
  
-   차등 데이터베이스 백업을 만들려면 이전 전체 데이터베이스 백업이 있어야 합니다. 선택한 데이터베이스를 백업한 적이 없으면 차등 백업을 만들기 전에 전체 데이터베이스 백업을 실행합니다. 자세한 내용은 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)에서 차등 데이터베이스 백업을 만듭니다.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   차등 백업의 크기가 커질수록 차등 백업을 복원할 때 데이터베이스 복원 시간이 훨씬 길어질 수 있습니다. 따라서 새 전체 백업을 지정된 간격으로 수행하여 데이터의 새 차등 기반을 설정하는 것이 좋습니다. 예를 들어 전체 데이터베이스의 전체 백업(즉, 전체 데이터베이스 백업)을 매주 수행하고 주중에 일련의 정기적인 차등 데이터베이스 백업을 수행할 수 있습니다.  
  
###  <a name="Security"></a> 보안  
  
####  <a name="Permissions"></a> Permissions  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 디바이스의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 장치를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 있어야 합니다. 그러나 시스템 테이블의 백업 디바이스에 대한 항목을 추가하는 [sp_addumpdevice](/sql/relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql)는 파일 액세스 권한을 확인하지 않습니다. 백업 디바이스의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
#### <a name="to-create-a-differential-database-backup"></a>차등 데이터베이스 백업을 만들려면  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 개체 탐색기에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 해당 데이터베이스에 따라 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  
  
4.  **데이터베이스** 목록 상자에서 데이터베이스 이름을 확인합니다. 필요에 따라 목록에서 다른 데이터베이스를 선택할 수 있습니다.  
  
     모든 복구 모델(전체, 대량 로그, 단순)에 대해 차등 백업을 수행할 수 있습니다.  
  
5.  **백업 유형** 목록 상자에서 **차등**을 선택합니다.  
  
    > [!IMPORTANT]  
    >  때 **차등** 은 확인을 선택 합니다 **복사 전용 백업** 확인란의 선택을 취소 합니다.  
  
6.  **백업 구성 요소**의 경우 **데이터베이스**를 클릭합니다.  
  
7.  **이름** 입력란에 제시된 기본 백업 세트 이름을 사용하거나 다른 이름을 입력합니다.  
  
8.  필요에 따라 **설명** 입력란에 백업 세트에 대한 설명을 입력합니다.  
  
9. 백업 세트가 만료될 시기를 다음과 같이 지정합니다.  
  
    -   백업 세트가 특정 일수가 지난 후에 만료되도록 하려면 **다음 이후** (기본 옵션)를 클릭한 다음 백업 세트를 만든 후 백업 세트가 만료되기까지 경과해야 하는 일수를 입력합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.  
  
         기본값은 **서버 속성** 대화 상자( **데이터베이스 설정** 페이지)의**백업 미디어 기본 보존 기간(일)** 옵션에 설정되어 있습니다. 이 페이지에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 **데이터베이스 설정** 페이지를 선택합니다.  
  
    -   백업 세트가 특정 일자에 만료되게 하려면 **날짜**를 클릭한 다음 백업 세트가 만료될 날짜를 입력합니다.  
  
10. **디스크** 나 **테이프**를 클릭하여 백업 대상 유형을 선택합니다. **추가**를 클릭하면 단일 미디어 세트를 포함하는 디스크나 테이프 드라이브에 대한 경로를 64개까지 선택할 수 있습니다. 선택한 경로는 **백업 대상** 목록 상자에 표시됩니다.  
  
     백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거**를 클릭합니다. 백업 대상의 내용을 보려면 선택한 다음 **내용**을 클릭합니다.  
  
11. 고급 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **옵션** 을 클릭합니다.  
  
12. 다음 중 하나를 클릭하여 **미디어 덮어쓰기** 옵션을 선택합니다.  
  
    -   **기존 미디어 세트에 백업**  
  
         이 옵션에는 **기존 백업 세트에 추가** 또는 **기존 백업 세트 모두 덮어쓰기**를 클릭합니다. 필요에 따라 **미디어 세트 이름 및 백업 세트 만료 확인** 확인란을 선택하거나 **미디어 세트 이름** 입력란에 이름을 입력합니다. 이름을 지정하지 않는 경우 이름이 비어 있는 미디어 세트가 생성됩니다. 미디어 세트 이름을 지정하는 경우 실제 이름과 입력한 이름이 일치하는지 확인하도록 미디어(테이프 또는 디스크)를 확인합니다.  
  
         미디어 이름을 비워 두고 검사하도록 확인란을 선택한 경우 미디어에서 미디어 이름을 비워 두는 것과 같은 결과가 나타납니다.  
  
    -   **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**  
  
         이 옵션에는 **새 미디어 세트 이름** 입력란에 이름을 입력하고 필요에 따라 **새 미디어 세트 설명** 입력란에 미디어 세트에 대한 설명을 입력합니다.  
  
13. **안정성** 섹션에서 필요에 따라 다음을 선택합니다.  
  
    -   **완료 시 백업 확인**  
  
    -   **미디어에 쓰기 전에 체크섬 수행**및 필요에 따라 **체크섬 오류 발생 시 계속**. 체크섬에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
  
14. **일반** 페이지의 **대상** 섹션에서 지정한 대로 테이프 드라이브에 백업하는 경우 **백업 후 테이프 언로드** 옵션이 활성화됩니다. 이 옵션을 클릭하면 **언로드 전에 테이프 되감기** 옵션이 활성화됩니다.  
  
    > [!NOTE]  
    >  **일반** 페이지의 **백업 유형** 섹션에서 지정한 대로 트랜잭션 로그를 백업하지 않으면 **트랜잭션 로그** 섹션의 옵션이 비활성화됩니다.  
  
15. [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상에서는 [백업 압축](backup-compression-sql-server.md)을 지원합니다. 기본적으로 백업은 **백업-압축 기본값** 서버 구성 옵션의 값에 따라 압축됩니다. 그러나 현재 서버 수준 기본값에 관계없이 **백업 압축**을 선택하여 백업을 압축하고, **백업 압축 안 함**을 선택하여 압축을 방지할 수 있습니다.  
  
     **현재 백업 압축 기본값을 보려면**  
  
    -   [backup compression default 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)  
  
    > [!NOTE]  
    >  또는 유지 관리 계획 마법사를 사용하여 차등 데이터베이스 백업을 만들 수 있습니다.  
  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
#### <a name="to-create-a-differential-database-backup"></a>차등 데이터베이스 백업을 만들려면  
  
1.  BACKUP DATABASE 문을 실행하여 차등 데이터베이스 백업을 만듭니다. 이때 다음을 지정합니다.  
  
    -   백업할 데이터베이스의 이름  
  
    -   전체 데이터베이스 백업이 기록되는 백업 디바이스  
  
    -   마지막 전체 데이터베이스 백업이 생성된 후 변경된 데이터베이스 부분만 백업하도록 지정하는 DIFFERENTIAL 절  
  
     필요한 구문은 다음과 같습니다.  
  
     BACKUP DATABASE *database_name* TO <backup_device> WITH DIFFERENTIAL  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
 이 예에서는 `MyAdvWorks` 데이터베이스에 대한 전체 및 차등 데이터베이스 백업을 만듭니다.  
  
```sql  
-- Create a full database backup first.  
BACKUP DATABASE MyAdvWorks   
   TO MyAdvWorks_1   
   WITH INIT;  
GO  
-- Time elapses.  
-- Create a differential database backup, appending the backup  
-- to the backup device containing the full database backup.  
BACKUP DATABASE MyAdvWorks  
   TO MyAdvWorks_1  
   WITH DIFFERENTIAL;  
GO  
```  
  
## <a name="see-also"></a>관련 항목  
 [차등 백업&#40;SQL Server&#41;](differential-backups-sql-server.md)   
 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](create-a-full-database-backup-sql-server.md)   
 [파일 및 파일 그룹 백업&#40;SQL Server&#41;](back-up-files-and-filegroups-sql-server.md)   
 [차등 데이터베이스 백업 복원&#40;SQL Server&#41;](restore-a-differential-database-backup-sql-server.md)   
 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](restore-a-transaction-log-backup-sql-server.md)   
 [유지 관리 계획](../maintenance-plans/maintenance-plans.md)   
 [전체 파일 백업&#40;SQL Server&#41;](full-file-backups-sql-server.md)  
  
  
