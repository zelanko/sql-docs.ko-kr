---
title: "전체 데이터베이스 백업 만들기(SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: backup-restore
ms.reviewer: 
ms.suite: sql
ms.technology: dbe-backup-restore
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- backing up databases [SQL Server], full backups
- backing up databases [SQL Server], SQL Server Management Studio
- backups [SQL Server], creating
- database backups [SQL Server], SQL Server Management Studio
ms.assetid: 586561fc-dfbb-4842-84f8-204a9100a534
caps.latest.revision: "63"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: d6049d82cb551c1614f4ea9f76528e53cd29942c
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 11/17/2017
---
# <a name="create-a-full-database-backup-sql-server"></a>전체 데이터베이스 백업 만들기(SQL Server)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
 > SQL Server 2014의 경우 [전체 데이터베이스 백업 만들기(SQL Server)](https://msdn.microsoft.com/en-US/library/ms187510(SQL.120).aspx)로 이동하세요.

  이 항목에서는 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] , [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]또는 PowerShell을 사용하여 [!INCLUDE[tsql](../../includes/tsql-md.md)]에서 전체 데이터베이스 백업을 만드는 방법을 설명합니다.  
  
>  Azure Blob Storage 서비스로 SQL Server 백업 방법에 대한 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md) 및 [URL로 SQL Server 백업](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요.  
  
##  <a name="BeforeYouBegin"></a> 시작하기 전 주의 사항 
  
###  <a name="Restrictions"></a> 제한 사항  
  
-   명시적 또는 암시적 트랜잭션에서는 BACKUP 문을 사용할 수 없습니다.  
  
-   최신 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 로 만든 백업은 이전 버전의 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]에서 복원할 수 없습니다.  
  
-   백업 개념과 태스크의 개요를 보고 자세히 살펴보려면 계속하기 전에 [백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md) 를 참조하세요.  
  
###  <a name="Recommendations"></a> 권장 사항  
  
-   데이터베이스가 커짐에 따라 전체 데이터베이스 백업은 마치는 데 시간이 오래 걸리고 저장 공간도 더 많이 필요하게 됩니다. 대규모 데이터베이스의 경우 일련의 [differential database backups](../../relational-databases/backup-restore/differential-backups-sql-server.md)로 전체 데이터베이스 백업을 보충해 보세요. 자세한 내용은 [SQL Server Backup to URL](../../relational-databases/backup-restore/sql-server-backup-to-url.md)을 참조하세요.  
  
-   [sp_spaceused](../../relational-databases/system-stored-procedures/sp-spaceused-transact-sql.md) 시스템 저장 프로시저를 사용하여 전체 데이터베이스 백업의 크기를 예측합니다.  
  
-   기본적으로 백업 작업을 성공적으로 수행할 때마다 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 오류 로그와 시스템 이벤트 로그에 항목이 추가됩니다. 자주 백업하는 경우 이러한 성공 메시지는 바로 누적되므로 엄청난 오류 로그가 쌓여 다른 메시지를 찾기 힘들 수 있습니다. 이 경우 스크립트가 이러한 백업 로그 항목에 종속되지 않을 경우 추적 플래그 3226을 사용하여 이러한 항목을 표시하지 않을 수 있습니다. 자세한 내용은 [추적 플래그&#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md)를 참조하세요.  
  
###  <a name="Security"></a> 보안  
 데이터베이스 백업에서 TRUSTWORTHY는 OFF로 설정되어 있습니다. TRUSTWORTHY를 ON으로 설정하는 방법은 [ALTER DATABASE SET 옵션&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)을 참조하세요.  
  
 [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] 부터는 **PASSWORD** 및 **MEDIAPASSWORD** 옵션은 백업을 만드는 데 더 이상 사용되지 않습니다. 암호를 사용하여 만든 백업은 계속 복원할 수 있습니다.  
  
####  <a name="Permissions"></a> 사용 권한  
 BACKUP DATABASE 및 BACKUP LOG 권한은 기본적으로 **sysadmin** 고정 서버 역할과 **db_owner** 및 **db_backupoperator** 고정 데이터베이스 역할의 멤버로 설정됩니다.  
  
 백업 장치의 물리적 파일에서 발생하는 소유권과 사용 권한 문제는 백업 작업에 영향을 미칠 수 있습니다. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 는 장치를 읽고 쓸 수 있어야 하므로 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 서비스가 실행되는 계정에는 쓰기 권한이 **있어야 합니다** . 그러나 시스템 테이블의 백업 장치에 대한 항목을 추가하는 [sp_addumpdevice](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)는 파일 액세스 권한을 확인하지 않습니다. 백업 장치의 물리적 파일에서 발생하는 이러한 문제는 백업 또는 복원을 시도할 때 실제 리소스를 액세스하기 전까지는 발생하지 않습니다.  
  
##  <a name="SSMSProcedure"></a> SQL Server Management Studio 사용  
  
>  [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]를 사용하여 백업 태스크를 지정할 때 **스크립트** 단추를 클릭하고 스크립트 대상을 선택하여 해당되는 [!INCLUDE[tsql](../../includes/tsql-md.md)] [BACKUP](../../t-sql/statements/backup-transact-sql.md) 스크립트를 생성할 수 있습니다.  
  
### <a name="back-up-a-database"></a>데이터베이스 백업  
  
1.  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]의 해당 인스턴스에 연결한 다음 **개체 탐색기**에서 서버 이름을 클릭하여 서버 트리를 확장합니다.  
  
2.  **데이터베이스**를 확장하고 사용자 데이터베이스를 선택하거나 **시스템 데이터베이스** 를 확장한 다음 시스템 데이터베이스를 선택합니다.  
  
3.  데이터베이스를 마우스 오른쪽 단추로 클릭하고 **태스크**를 가리킨 다음 **백업**을 클릭합니다. **데이터베이스 백업** 대화 상자가 나타납니다.  

  #### <a name="general-page"></a>**일반 페이지**
  
4.  **데이터베이스** 드롭다운 목록에서 데이터베이스 이름을 확인합니다. 필요에 따라 목록에서 다른 데이터베이스를 선택할 수 있습니다.  
  
5.  **복구 모델** 입력란은 참조용입니다.  모든 복구 모델(**전체**, **대량 로그**또는 **단순**)에서 데이터베이스 백업을 수행할 수 있습니다.  
  
6.  **백업 유형** 드롭다운 목록에서 **전체**를 선택합니다.  
  
     전체 데이터베이스 백업을 만든 후 차등 데이터베이스 백업을 만들 수 있습니다. 자세한 내용은 [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)을 참조하세요.  
  
7.  경우에 따라 **복사 전용 백업** 확인란을 선택하여 복사 전용 백업을 만들 수 있습니다. *복사 전용 백업*은 기존 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업 시퀀스와 독립적인 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업입니다. 자세한 내용은 [복사 전용 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/copy-only-backups-sql-server.md)를 참조하세요.  **서로 다른** 백업 유형에서는 복사 전용 백업을 사용할 수 없습니다.  

8.  **백업 구성 요소**에서 **데이터베이스** 라디오 단추를 선택합니다.  
  
9. **대상** 섹션에서 **백업할 위치** 드롭다운 목록을 사용하여 백업 대상을 선택합니다. **추가** 를 클릭하여 추가 백업 개체 및/또는 대상을 추가합니다.
  
     백업 대상을 제거하려면 해당 대상을 선택한 다음 **제거**를 클릭합니다. 기존 백업 대상의 내용을 보려면 선택한 다음 **내용**을 클릭합니다.  

  #### <a name="media-options-page"></a>**미디어 옵션 페이지**  
10. 미디어 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **미디어 옵션** 을 클릭합니다.   
    
11. 다음 중 하나를 클릭하여 **미디어 덮어쓰기** 옵션을 선택합니다. 

    > [!IMPORTANT]  
    >  **일반** 페이지에서 **URL**을 백업 대상으로 선택한 경우 **미디어 덮어쓰기** 옵션을 사용할 수 없습니다. 자세한 내용은 [데이터베이스 백업&#40;미디어 옵션 페이지&#41;](../../relational-databases/backup-restore/back-up-database-media-options-page.md)을 참조하세요.  


  -   **기존 미디어 세트에 백업**  
  
      > [!IMPORTANT]  
      >  암호화를 사용할 계획인 경우 이 옵션을 선택하지 마세요. 이 옵션을 선택하면 **백업 옵션** 페이지의 암호화 옵션을 사용할 수 없게 됩니다. 기존 백업 세트에 추가할 때는 암호화가 지원되지 않습니다.  
  
         이 옵션에는 **기존 백업 세트에 추가** 또는 **기존 백업 세트 모두 덮어쓰기**를 클릭합니다. 자세한 내용은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
         필요에 따라 **미디어 세트 이름 및 백업 세트 만료 확인** 을 선택하여 백업 작업에서 미디어 세트와 백업 세트가 만료되는 날짜와 시간을 확인하도록 합니다.  
  
         필요에 따라 **미디어 세트 이름** 입력란에 이름을 입력합니다. 이름을 지정하지 않는 경우 이름이 비어 있는 미디어 세트가 생성됩니다. 미디어 세트 이름을 지정하는 경우 미디어(테이프 또는 디스크)를 선택하여 실제 이름과 여기에서 입력한 이름이 일치하는지 여부를 확인합니다.  
  
-   **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**  
  
    이 옵션에는 **새 미디어 세트 이름** 입력란에 이름을 입력하고 필요에 따라 **새 미디어 세트 설명** 입력란에 미디어 세트에 대한 설명을 입력합니다.  
  
14. **안정성** 섹션에서 필요에 따라 다음을 선택합니다.  
  
    -   **완료 시 백업 확인**  
  
    -   **미디어에 쓰기 전에 체크섬 수행**  체크섬에 대한 자세한 내용은 [백업 및 복원 중 발생 가능한 미디어 오류&#40;SQL Server&#41;](../../relational-databases/backup-restore/possible-media-errors-during-backup-and-restore-sql-server.md)를 참조하세요.  
    
    -   **오류 발생 시 계속**. 

15. **일반** 페이지의 **백업 유형** 섹션에서 지정한 대로 트랜잭션 로그를 백업하지 않으면 **트랜잭션 로그** 섹션이 비활성화됩니다.  
      
16. **일반** 페이지의 **대상** 섹션에서 지정한 대로 테이프 드라이브에 백업하는 경우에는 **테이프 드라이브** 섹션에서 **백업 후 테이프 언로드** 옵션이 활성화됩니다. 이 옵션을 클릭하면 **언로드 전에 테이프 되감기** 옵션이 활성화됩니다.   

  #### <a name="backup-options-page"></a>**백업 옵션 페이지**  

17. 백업 옵션을 보거나 선택하려면 **페이지 선택** 창에서 **백업 옵션** 을 클릭합니다.  
  
18. **이름** 입력란에서 기본 백업 세트 이름을 사용하거나 다른 백업 세트 이름을 입력합니다.  
  
19. **설명** 입력란에 백업 세트에 대한 설명을 필요에 따라 입력할 수 있습니다.  
  
20. 백업 세트가 만료되고 명시적으로 만료 날짜 확인을 생략할 필요 없이 덮어쓸 수 있는 시기를 지정합니다.  
  
    -   백업 세트가 특정 일수가 지난 후에 만료되도록 하려면 **다음 이후** (기본 옵션)를 클릭한 다음 백업 세트를 만든 후 백업 세트가 만료되기까지 경과해야 하는 일수를 입력합니다. 이 값은 0일에서 99999일 사이일 수 있습니다. 값 0일은 백업 세트 기간 제한이 없음을 의미합니다.  
  
         기본값은 데이터베이스 설정 페이지에 있는 **서버 속성** 대화 상자의 **백업 미디어 기본 보존 기간(일)** 옵션에 설정되어 있습니다. 이 페이지에 액세스하려면 개체 탐색기에서 서버 이름을 마우스 오른쪽 단추로 클릭하고 속성을 선택한 다음 **데이터베이스 설정** 페이지를 선택합니다.  
  
    -   백업 세트가 특정 일자에 만료되게 하려면 **날짜**를 클릭한 다음 백업 세트가 만료될 날짜를 입력합니다.  
  
         백업 만료 날짜에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.  
  
21. **압축** 섹션에서 **백업 압축 설정** 드롭다운 목록을 사용하여 원하는 압축 수준을 선택합니다.  [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상에서는 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md)을 지원합니다. 기본적으로 백업은 **백업-압축 기본값** 서버 구성 옵션의 값에 따라 압축됩니다. 그러나 현재 서버 수준 기본값에 관계없이 **백업 압축**을 선택하여 백업을 압축하고, **백업 압축 안 함**을 선택하여 압축을 방지할 수 있습니다.  
  
     백업 설정에 대한 자세한 내용은 [백업 압축 기본값 서버 구성 옵션 보기 또는 구성](../../database-engine/configure-windows/view-or-configure-the-backup-compression-default-server-configuration-option.md)을 참조하세요.  
  
22. **암호화** 섹션에서 **백업 암호화** 확인란을 사용하여 백업에 암호화를 사용할지 여부를 결정합니다. 암호화 알고리즘을 선택하려면 **알고리즘** 드롭다운 목록을 사용합니다.  기존 인증서 또는 비대칭 키를 선택하려면 **인증서 또는 비대칭 키** 드롭다운 목록을 사용합니다. 암호화는 SQL Server 2014 이상에서 지원됩니다. 암호화 옵션에 대한 자세한 내용은 [데이터베이스 백업&#40;백업 옵션 페이지&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)을 참조하세요.  
  
  
[유지 관리 계획 마법사](../maintenance-plans/use-the-maintenance-plan-wizard.md) 를 사용하여 데이터베이스 백업을 만들 수 있습니다. 

### <a name="examples"></a>예  
#### <a name="a--full-back-up-to-disk-to-default-location"></a>**A.  기본 위치로 디스크 전체 백업**
이 예제에서는 `Sales` 데이터베이스가 기본 백업 위치에서 디스크로 백업됩니다.  `Sales` 백업은 수행되지 않았습니다.
1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2.  **데이터베이스**를 확장하고 `Sales`를 마우스 오른쪽 단추로 클릭한 다음 **태스크**를 가리키고 **백업...**을 클릭합니다.

3.  **확인**을 클릭합니다.

#### <a name="b--full-back-up-to-disk-to-non-default-location"></a>**B.  기본이 아닌 위치로 디스크 전체 백업**
이 예제에서는 `Sales` 데이터베이스가 `E:\MSSQL\BAK`에서 디스크로 백업됩니다.  `Sales` 의 이전 백업은 수행되었습니다.
1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2.  **데이터베이스**를 확장하고 `Sales`를 마우스 오른쪽 단추로 클릭한 다음 **태스크**를 가리키고 **백업...**을 클릭합니다.

3.  **대상** 섹션의 **일반** 페이지에 있는 **백업할 위치:** 드롭다운 목록에서 **디스크** 를 선택합니다.

4.  모든 기존 백업 파일이 제거될 때까지 **제거** 를 클릭합니다.

5.  **추가** 를 클릭하면 **백업 대상 선택** 대화 상자가 열립니다.

6.  `E:\MSSQL\BAK\Sales_20160801.bak` 파일 이름 **입력란에** 을 입력합니다.

7.  **확인**을 클릭합니다.

8.  **확인**을 클릭합니다.

#### <a name="c--create-an-encrypted-backup"></a>**C.  암호화된 백업 만들기**
이 예제에서는 `Sales` 데이터베이스가 기본 백업 위치로 암호화를 사용하여 백업됩니다.  [**데이터베이스 마스터 키**](../../relational-databases/security/encryption/create-a-database-master-key.md) 는 이미 만들었습니다.  [**인증서**](../../t-sql/statements/create-certificate-transact-sql.md) 도 `MyCertificate`로 이미 만들었습니다. **데이터베이스 마스터 키** 및 **인증서** 를 만드는 T-SQL 예제는 [암호화된 백업 만들기](../../relational-databases/backup-restore/create-an-encrypted-backup.md)를 참조하세요.  
1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2.  **데이터베이스**를 확장하고 `Sales`를 마우스 오른쪽 단추로 클릭한 다음 **태스크**를 가리키고 **백업...**을 클릭합니다.

3.  **미디어 옵션** 페이지의 **미디어 덮어쓰기** 섹션에서 **새 미디어 세트에 백업하고 기존 백업 세트 모두 지우기**를 선택합니다.

4.  **백업 옵션** 페이지의 **암호화** 섹션에서 **백업 암호화** 확인란을 선택합니다.

5.  **알고리즘** 드롭다운 목록에서 **AES 256**을 선택합니다.

6.  **인증서 또는 비대칭 키** 드롭다운 목록에서 `MyCertificate`를 선택합니다.

7.  **확인**을 클릭합니다.

#### <a name="d--back-up-to-the-azure-blob-storage-service"></a>**D.  Azure Blob Storage 서비스에 백업**
#### <a name="common-steps"></a>**공통 단계**  
아래 세 가지 예제에서는 Microsoft Azure Blob 저장소 서비스로 `Sales` 의 전체 데이터베이스 백업을 수행합니다.  저장소 계정 이름은 `mystorageaccount`입니다.  컨테이너는 `myfirstcontainer`입니다.  간단히 말해 처음 네 단계는 여기에 한 번 나열되며 모든 예제는 **5단계**에서 시작됩니다.
1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.

2.  **데이터베이스**를 확장하고 `Sales`를 마우스 오른쪽 단추로 클릭한 다음 **태스크**를 가리키고 **백업...**을 클릭합니다.

3.  **대상** 섹션의 **일반** 페이지에 있는 **백업할 위치:** 드롭다운 목록에서 **URL** 을 선택합니다.

4.  **추가** 를 클릭하면 **백업 대상 선택** 대화 상자가 열립니다.

    **D1.  URL로 스트라이프 백업 및 SQL Server 자격 증명에 이미 있는 경우**  
읽기, 쓰기 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다.  저장된 액세스 정책에 연결된 공유 액세스 서명을 사용하여 SQL Server 자격 증명인 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`를 만들었습니다.  
*
    5.  `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` Azure 저장소 컨테이너: **텍스트 상자에서** 를 선택합니다.

    6.  **백업 파일:** 텍스트 상자에 `Sales_stripe1of2_20160601.bak`를 입력합니다.

    7.  **확인**을 클릭합니다.

    8.  **4** 단계와 **5**단계를 반복합니다.

    9.  **백업 파일:** 텍스트 상자에 `Sales_stripe2of2_20160601.bak`를 입력합니다.

    10.  **확인**을 클릭합니다.

    11.   **확인**을 클릭합니다.

    **D2.  공유 액세스 서명이 있고 SQL Server 자격 증명이 없는 경우**
  5.    `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` Azure 저장소 컨테이너: **텍스트 상자에** 를 입력합니다.
  
  6.    **공유 액세스 정책:** 텍스트 상자에 공유 액세스 서명을 입력합니다.
  
  7.    **확인**을 클릭합니다.
  
  8.    **확인**을 클릭합니다.

    **D3.  공유 액세스 서명이 없는 경우**
  5.    **새 컨테이너** 단추를 클릭하면 **Microsoft 구독에 연결** 대화 상자가 열립니다.  
  
  6.    **Microsoft 구독에 연결** 대화 상자를 완성하고 **확인** 을 클릭하여 **백업 대상 선택** 대화 상자로 돌아갑니다.  자세한 내용은 [Microsoft Azure 구독에 연결](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) 을 참조하세요.
  
  7.    **백업 대상 선택** 대화 상자에서 **확인** 을 클릭합니다.
  
  8.    **확인**을 클릭합니다.

  
##  <a name="TsqlProcedure"></a> Transact-SQL 사용  
  
### <a name="create-a-full-database-backup"></a>전체 데이터베이스 백업 만들기  
  
1.  BACKUP DATABASE 문을 실행하여 전체 데이터베이스 백업을 만듭니다. 이때 다음을 지정합니다.  
  
    -   백업할 데이터베이스의 이름  
  
    -   전체 데이터베이스 백업이 기록되는 백업 장치  
  
     전체 데이터베이스 백업의 기본 [!INCLUDE[tsql](../../includes/tsql-md.md)] 구문은 다음과 같습니다.  
  
     BACKUP DATABASE *database*  
  
     TO *backup_device* [ **또는 PowerShell을 사용하여**...*n* ]  
  
     [ WITH *with_options* [ **,**...*o* ] ] ;  
  
    |옵션|설명|  
    |------------|-----------------|  
    |*database*|백업할 데이터베이스입니다.|  
    |*backup_device* [ **또는 PowerShell을 사용하여**...*n* ]|백업 작업에 사용할 1-64개의 백업 장치 목록을 지정합니다. 물리적 백업 장치를 지정하거나, 이미 정의된 경우 해당 논리적 백업 장치를 지정할 수 있습니다. 물리적 백업 장치를 지정하려면 다음 DISK 또는 TAPE 옵션을 사용합니다.<br /><br /> { DISK &#124; TAPE } **=***physical_backup_device_name*<br /><br /> 자세한 내용은 [백업 장치&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.|  
    |WITH *with_options* [ **,**...*o* ]|필요에 따라 *o*등과 같은 하나 이상의 추가 옵션을 지정합니다. 몇 가지 WITH의 기본 옵션에 대한 자세한 내용은 2단계를 참조하세요.|  
  
2.  필요에 따라 한 개 이상의 WITH 옵션을 지정합니다. 몇 가지 WITH의 기본 옵션은 이 페이지에 설명되어 있습니다. 모든 WITH 옵션에 대한 자세한 내용은 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)을 참조하세요.  
  
    -   기본 백업 세트 WITH 옵션  
  
         { COMPRESSION | NO_COMPRESSION }  
         [!INCLUDE[ssEnterpriseEd10](../../includes/ssenterpriseed10-md.md)] 이상에서만 사용 가능. 이 백업에서 [백업 압축](../../relational-databases/backup-restore/backup-compression-sql-server.md) 을 수행하고 서버 수준 기본값을 재정의할지 여부를 지정합니다.  
  
         ENCRYPTION (ALGORITHM, SERVER CERTIFICATE |ASYMMETRIC KEY)  
         SQL Server 2014 이상에서만 사용할 암호화 알고리즘과 암호화 보안에 사용할 인증서 또는 비대칭 키를 지정합니다.  
  
         DESCRIPTION **=** { **'***text***'** | **@***text_variable* }  
         백업 세트를 설명하는 자유 형식의 텍스트를 지정합니다. 문자열을 최대 255자까지 지정할 수 있습니다.  
  
         NAME **=** { *backup_set_name* | **@***backup_set_name_var* }  
         백업 세트의 이름을 지정합니다. 이름은 최대 128자까지 지정할 수 있습니다. NAME을 지정하지 않으면 공백이 됩니다.  
  
    -   기본 백업 세트 WITH 옵션  
  
         기본적으로 BACKUP은 기존 백업 세트를 유지하면서 기존 미디어 세트에 백업을 추가합니다. 이것을 명시적으로 지정하려면 NOINIT 옵션을 사용합니다. 기존 백업 세트에 추가하는 방법은 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)을 참조하세요.  
  
         또는 백업 미디어의 형식을 지정하기 위해 FORMAT 옵션을 사용합니다.  
  
         FORMAT [ **,** MEDIANAME**=** { *media_name* | **@***media_name_variable* } ] [ **,** MEDIADESCRIPTION **=** { *text* | **@***text_variable* } ]  
         미디어를 처음 사용하거나 기존의 모든 데이터를 덮어쓰려고 하는 경우 FORMAT 절을 사용합니다. 필요에 따라 새 미디어에 미디어 이름과 설명을 지정합니다.  
  
        > [!IMPORTANT]  
        >  BACKUP 문의 FORMAT 절을 사용하는 경우 백업 미디어에 이전에 저장된 백업이 모두 삭제되므로 각별히 주의해야 합니다.  
  
###  <a name="TsqlExample"></a> 예(Transact-SQL)  
  
#### <a name="a-back-up-to-a-disk-device"></a>**A. 디스크 장치에 백업**  
 다음 예에서는 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 을 사용하여 새 미디어 세트를 만들어 `FORMAT` 데이터베이스 전체를 디스크에 백업합니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
TO DISK = 'Z:\SQLServerBackups\AdventureWorks2012.Bak'  
   WITH FORMAT,  
      MEDIANAME = 'Z_SQLServerBackups',  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="b-back-up-to-a-tape-device"></a>**B. 테이프 장치에 백업**  
 다음 예제에서는 이전 백업에 백업을 추가하여 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스 전체를 테이프에 백업합니다.  
  
```tsql  
USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO TAPE = '\\.\Tape0'  
   WITH NOINIT,  
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
#### <a name="c-back-up-to-a-logical-tape-device"></a>**C. 논리적 테이프 장치에 백업**  
 다음 예에서는 테이프 드라이브에 대한 논리적 백업 장치를 만듭니다. 그런 다음 [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)] 데이터베이스 전체를 이 장치에 백업합니다.  
  
```tsql  
-- Create a logical backup device,   
-- AdventureWorks2012_Bak_Tape, for tape device \\.\tape0.  
USE master;  
GO  
EXEC sp_addumpdevice 'tape', 'AdventureWorks2012_Bak_Tape', '\\.\tape0'; USE AdventureWorks2012;  
GO  
BACKUP DATABASE AdventureWorks2012  
   TO AdventureWorks2012_Bak_Tape  
   WITH FORMAT,  
      MEDIANAME = 'AdventureWorks2012_Bak_Tape',  
      MEDIADESCRIPTION = '\\.\tape0',   
      NAME = 'Full Backup of AdventureWorks2012';  
GO  
```  
  
##  <a name="PowerShellProcedure"></a> PowerShell 사용  
**Backup-SqlDatabase** cmdlet을 사용합니다. 전체 데이터베이스 백업임을 명시적으로 나타내기 위해 **-BackupAction**  매개 변수에 기본값인 **Database**를 지정합니다. 전체 데이터베이스 백업의 경우 이 매개 변수는 선택 사항입니다.  

### <a name="examples"></a>예
#### <a name="a--full-local-backup"></a>**A.  전체 로컬 백업**  
다음 예에서는 서버 인스턴스 `MyDB` 의 기본 백업 위치에 `Computer\Instance`데이터베이스의 전체 데이터베이스 백업을 만듭니다. 선택 사항으로, 이 예제에서는 **-BackupAction Database**를 지정합니다.  
```powershell 
Backup-SqlDatabase -ServerInstance Computer\Instance -Database MyDB -BackupAction Database  
```
 
#### <a name="b--full-backup-to-microsoft-azure"></a>**B.  Microsoft Azure로 전체 백업**  
다음 예제에서는 Microsoft Azure Blob Storage 서비스로 `Sales` 인스턴스의 `MyServer` 데이터베이스 전체 백업을 만듭니다.  읽기, 쓰기 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다.  저장된 액세스 정책에 연결된 공유 액세스 서명을 사용하여 SQL Server 자격 증명인 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`를 만들었습니다.  PowerShell 명령은 **BackupFile** 매개 변수를 사용하여 위치(URL)와 백업 파일 이름을 지정합니다.

```powershell  
import-module sqlps;
$container = 'https://mystorageaccount.blob.core.windows.net/myfirstcontainer';
$FileName = 'Sales.bak';
$database = 'Sales';
$BackupFile = $container + '/' + $FileName ;
  
Backup-SqlDatabase -ServerInstance "MyServer" –Database $database -BackupFile $BackupFile;
```
 
 **SQL Server PowerShell 공급자를 설정하고 사용하려면**  
  
-   [SQL Server PowerShell 공급자](../../relational-databases/scripting/sql-server-powershell-provider.md)  
  
##  <a name="RelatedTasks"></a> 관련 태스크  
  
-   [데이터베이스 백업(SQL Server)](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)  
  
-   [차등 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-differential-database-backup-sql-server.md)  
  
-   [Restore a Database Backup Using SSMS](../../relational-databases/backup-restore/restore-a-database-backup-using-ssms.md)  
  
-   [단순 복구 모델에서 데이터베이스 백업 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-a-database-backup-under-the-simple-recovery-model-transact-sql.md)  
  
-   [전체 복구 모델에서 특정 오류 지점으로 데이터베이스 복원&#40;Transact-SQL&#41;](../../relational-databases/backup-restore/restore-database-to-point-of-failure-full-recovery.md)  
  
-   [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)  
  
-   [유지 관리 계획 마법사 사용](../../relational-databases/maintenance-plans/use-the-maintenance-plan-wizard.md)  
  
## <a name="see-also"></a>참고 항목  
**[SQL Server 백업 및 복원 작업 문제 해결](https://support.microsoft.com/en-us/kb/224071)**          
[백업 개요&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-overview-sql-server.md)   
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/transaction-log-backups-sql-server.md)   
 [미디어 세트, 미디어 패밀리 및 백업 세트&#40;SQL Server&#41;](../../relational-databases/backup-restore/media-sets-media-families-and-backup-sets-sql-server.md)   
 [sp_addumpdevice&#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addumpdevice-transact-sql.md)   
 [BACKUP&#40;Transact-SQL&#41;](../../t-sql/statements/backup-transact-sql.md)   
 [데이터베이스 백업&#40;일반 페이지&#41;](../../relational-databases/backup-restore/back-up-database-general-page.md)   
 [데이터베이스 백업&#40;백업 옵션 페이지&#41;](../../relational-databases/backup-restore/back-up-database-backup-options-page.md)   
 [차등 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/differential-backups-sql-server.md)   
 [전체 데이터베이스 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/full-database-backups-sql-server.md)  
  
  
