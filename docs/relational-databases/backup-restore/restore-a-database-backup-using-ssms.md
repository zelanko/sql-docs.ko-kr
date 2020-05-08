---
title: SSMS를 사용하여 데이터베이스 백업 복원 | Microsoft 문서
description: 이 문서에서는 SQL Server Management Studio를 사용하여 전체 SQL Server 데이터베이스 백업을 복원하는 방법을 설명합니다.
ms.custom: ''
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
f1_keywords:
- sql13.swb.locatebackupfileazure.f1
- sql13.swb.specifybackup.f1
helpviewer_keywords:
- full backups [SQL Server]
- database restores [SQL Server], full backups
- backing up databases [SQL Server], full backups
- database backups [SQL Server], full backups
- restoring databases [SQL Server], full backups
ms.assetid: 24b3311d-5ce0-4581-9a05-5c7c726c7b21
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 2a76b91e9f5fd1cab9512cd42f05ce949ccf4d68
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/27/2020
ms.locfileid: "82180857"
---
# <a name="restore-a-database-backup-using-ssms"></a>Restore a Database Backup Using SSMS
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 SQL Server Management Studio를 사용하여 전체 데이터베이스 백업을 복원하는 방법을 설명합니다.    
       
### <a name="important"></a>중요!    
전체 복구 모델 또는 대량 로그 복구 모델에서 데이터베이스를 복원하려면 먼저 활성 트랜잭션 로그( [비상 로그](tail-log-backups-sql-server.md)라고도 함)를 백업해야 할 수 있습니다. 자세한 내용은 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)데이터베이스를 새 위치로 복원하고 선택적으로 데이터베이스 이름을 바꾸는 방법을 설명합니다.  

다른 인스턴스에서 데이터베이스를 복원할 때 [다른 서버 인스턴스에서 데이터베이스를 사용할 수 있도록 할 때 메타데이터 관리(SQL Server)](../../relational-databases/databases/manage-metadata-when-making-a-database-available-on-another-server.md)의 정보를 참조하세요.   
    
암호화된 데이터베이스를 복원하려면 데이터베이스를 암호화하는 데 사용된 인증서 또는 비대칭 키에 대한 액세스 권한이 있어야 합니다. 인증서 또는 비대칭 키가 없으면 해당 데이터베이스를 복원할 수 없습니다. 백업을 저장해야 하는 동안에는 데이터베이스 암호화 키를 암호화하는 데 사용된 인증서를 유지해야 합니다. 자세한 내용은 [SQL Server Certificates and Asymmetric Keys](../../relational-databases/security/sql-server-certificates-and-asymmetric-keys.md)을 참조하세요.    
    
이전 버전 데이터베이스를 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 복원하면 해당 데이터베이스가 자동으로 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]로 업그레이드됩니다. 데이터베이스가 [!INCLUDE[ssde_md](../../includes/ssde_md.md)]의 이전 버전으로 사용되지 않도록 합니다. 그러나 이는 메타데이터 업그레이드와 관련되어 있으며 [데이터베이스 호환성 수준](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md)에 영향을 주지 않습니다. 사용자 데이터베이스의 호환성 수준이 업그레이드 이전에 100 이상이면 업그레이드 후에도 동일하게 유지됩니다. 업그레이드 이전에 호환성 수준이 90이면 업그레이드된 데이터베이스에서는 호환성 수준이 [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]에서 지원되는 가장 낮은 호환성 수준인 100으로 설정됩니다. 자세한 내용은 [ALTER DATABASE 호환성 수준&#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md)을 참조하세요.  
  
일반적으로 데이터베이스는 즉시 사용할 수 있습니다. 그러나 [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] 데이터베이스에 전체 텍스트 인덱스가 있는 경우 업그레이드 프로세스는 **전체 텍스트 업그레이드 옵션** 서버 속성의 설정에 따라 인덱스를 가져오거나, 다시 설정하거나, 다시 작성합니다. 업그레이드 옵션을 **가져오기** 또는 **다시 작성**으로 설정하면 업그레이드하는 동안 전체 텍스트 인덱스를 사용할 수 없습니다. 인덱싱되는 데이터양에 따라 가져오기 작업은 몇 시간씩 걸릴 수 있으며 다시 작성 작업은 10배 정도 더 걸립니다.     
    
업그레이드 옵션을 **가져오기**로 설정하면 전체 텍스트 카탈로그를 사용할 수 없는 경우 관련된 전체 텍스트 인덱스가 다시 작성됩니다. **전체 텍스트 업그레이드 옵션** 속성 설정을 보거나 변경하는 방법은 [서버 인스턴스의 전체 텍스트 검색 관리 및 모니터링](../../relational-databases/search/manage-and-monitor-full-text-search-for-a-server-instance.md)을 참조하세요.    

Microsoft Azure Blob Storage 서비스에서 SQL Server 복원 방법에 대한 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.

## <a name="examples"></a>예
    
### <a name="a-restore-a-full-database-backup"></a>A. 전체 데이터베이스 백업 복원   
    
1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
    
2.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원...** 을 선택합니다.    
    
3.  **일반** 페이지에서 **원본** 섹션을 사용하여 복원할 백업 집합의 원본과 위치를 지정합니다. 다음 옵션 중 하나를 선택합니다.    
    
    -   **Database**    
    
         복원할 데이터베이스를 드롭다운 목록에서 선택합니다. 목록에는 **msdb** 백업 기록에 따라 백업된 데이터베이스만 포함되어 있습니다.    
    
        > [!NOTE]
        > 백업을 다른 서버에서 가져온 경우 대상 서버에 지정한 데이터베이스에 대한 백업 기록 정보가 없습니다. 이 경우 **디바이스** 를 선택하여 복원할 파일이나 디바이스를 수동으로 지정합니다. 
    
    -   **디바이스**    
    
         찾아보기( **...** ) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다. 
         
        -   **백업 디바이스 선택** 대화 상자  
        
            **백업 미디어 유형**  
         **백업 미디어 유형** 드롭다운 목록에서 미디어 유형을 선택합니다.  참고: **테이프** 옵션은 컴퓨터에 테이프 드라이브가 탑재된 경우에만 나타나고 **백업 디바이스** 옵션은 적어도 하나의 백업 디바이스가 있는 경우에만 나타납니다.

            **추가**  
            **백업 미디어** 드롭다운 목록에서 선택한 미디어 유형에 따라 **추가** 를 클릭하면 다음 대화 상자 중 하나가 열립니다. **백업 미디어** 목록 상자의 목록이 꽉 차면 **추가** 단추를 사용할 수 없습니다.

            |미디어 유형|대화 상자|Description|    
            |----------------|----------------|-----------------|    
            |**최근에 사용한 파일**|**백업 파일 찾기**|이 대화 상자에서는 트리에서 로컬 파일을 선택하거나 정규화된 UNC(Universal Naming Convention) 이름을 사용하여 원격 파일을 지정할 수 있습니다. 자세한 내용은 [백업 디바이스&#40;SQL Server&#41;](../../relational-databases/backup-restore/backup-devices-sql-server.md)를 참조하세요.|    
            |**디바이스**|**백업 디바이스 선택**|이 대화 상자에서는 서버 인스턴스에 정의된 논리적 백업 디바이스의 목록에서 디바이스를 선택할 수 있습니다.|    
            |**테이프**|**백업 테이프 선택**|이 대화 상자에서는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스를 실행하는 컴퓨터에 물리적으로 연결된 테이프 드라이브의 목록에서 백업 테이프를 선택할 수 있습니다.|    
            |**URL**|**백업 파일 위치 선택**|이 대화 상자에서 기존 SQL Server 자격 증명/Azure Storage 컨테이너를 선택하거나, 공유 액세스 서명을 사용하여 새 Azure Storage 컨테이너를 추가하거나, 기존 스토리지 컨테이너에 대한 공유 액세스 서명 및 SQL Server 자격 증명을 생성할 수 있습니다.  [Microsoft Azure 구독에 연결](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md)을 참조하세요.|  
         
             **제거**    
             선택한 파일, 테이프 또는 논리적 백업 디바이스를 하나 이상 제거합니다.    
                 
             **내용**    
            선택한 파일, 테이프 또는 논리적 백업 디바이스의 미디어 내용을 표시합니다.  미디어 유형이 **URL**이면 이 단추가 작동하지 않을 수도 있습니다.  

             **백업 미디어**   
             선택한 미디어를 나열합니다.
    
             원하는 디바이스를 **백업 미디어** 목록 상자에 추가한 후 **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.    
    
         **원본: 디바이스: 데이터베이스** 목록 상자에서 복원할 데이터베이스의 이름을 선택합니다.    
    
         > [!NOTE]
         > 이 목록은 **디바이스** 를 선택한 경우에만 사용할 수 있습니다. 선택한 디바이스에 백업이 있는 데이터베이스만 사용할 수 있습니다.    
     
4.  **대상** 섹션의 **데이터베이스** 상자에는 복원할 데이터베이스의 이름이 자동으로 채워집니다. 데이터베이스의 이름을 변경하려면 **데이터베이스** 상자에 새 이름을 입력합니다.    
    
5.  **복원 위치** 상자에서 기본값인 **마지막으로 수행된 백업으로** 를 그대로 적용하거나 **시간대** 를 클릭하여 **백업 시간대** 대화 상자에 액세스한 후 복구 동작을 중지할 지정 시간을 직접 선택합니다. 특정 지정 시간을 지정하는 방법은 [Backup Timeline](../../relational-databases/backup-restore/backup-timeline.md)를 참조하십시오.    
    
6.  **복원에 사용할 백업 세트** 표에서 복원할 백업을 선택합니다. 이 표는 지정한 위치에서 사용 가능한 백업을 표시합니다. 기본적으로 복구 계획이 제안됩니다. 제안된 복구 계획을 재정의하려면 표에서 선택 항목을 변경합니다. 이전 백업의 선택이 취소되면 이전 백업 복원에 기반하는 백업도 자동으로 선택이 취소됩니다. **복원에 사용할 백업 세트** 표의 열에 대한 자세한 내용은 [데이터베이스 복원&#40;일반 페이지&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)을 참조하세요.    
    
7.  필요에 따라 **페이지 선택** 창에서 **파일** 을 클릭하여 **파일** 대화 상자에 액세스합니다. 여기서 **데이터베이스 파일을 다음으로 복원** 표의 각 파일에 대해 새 복원 대상을 지정하여 데이터베이스를 새 위치에 복원할 수 있습니다. 이 표에 대한 자세한 내용은 [데이터베이스 복원&#40;파일 페이지&#41;](../../relational-databases/backup-restore/restore-database-files-page.md)을 참조하세요.    
    
8. 고급 옵션을 보거나 선택하려면 상황에 따라 **옵션** 페이지의 **복원 옵션** 패널에서 다음 옵션 중 하나를 선택할 수 있습니다.    

   1. **WITH** 옵션(필요 없음):    
    
     - **기존 데이터베이스 덮어쓰기(WITH REPLACE)**    
    
     - **복제 설정 유지(WITH KEEP_REPLICATION)**    
    
     - **복원된 데이터베이스에 대한 액세스 제한(WITH RESTRICTED_USER)**    
    
   2. **복구 상태** 상자에 대한 옵션을 선택합니다. 이 상자에서 복원 작업 후 데이터베이스의 상태를 확인합니다.    
    
     - **RESTORE WITH RECOVERY** 는 커밋되지 않은 트랜잭션을 롤백하여 데이터베이스를 사용 준비가 된 상태로 유지하는 기본 동작입니다. 추가 트랜잭션 로그를 복원할 수 없습니다. 필요한 모든 백업을 지금 복원하는 경우 이 옵션을 선택합니다.    
    
     - **RESTORE WITH NORECOVERY** 는 데이터베이스를 비작동 상태로 유지하고 커밋되지 않은 트랜잭션을 롤백하지 않습니다. 추가 트랜잭션 로그를 복원할 수 데이터베이스는 복구할 때까지 사용할 수 없습니다.    
    
     - **RESTORE WITH STANDBY** 는 읽기 전용 모드로 데이터베이스를 유지합니다. 이 옵션은 커밋되지 않은 트랜잭션의 실행을 취소하지만, 복구 결과를 되돌릴 수 있도록 실행 취소 동작을 대기 파일에 저장합니다.    
    
   3. **복원 전에 비상 로그 백업을 수행합니다.** 모든 복원 시나리오에서 비상 로그 백업이 필요한 것은 아닙니다.  자세한 내용은 **비상 로그 백업(SQL Server)** 에서 [비상 로그 백업이 필요한 시나리오](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)를 참조하세요.
  
   4. 데이터베이스에 대한 활성 연결이 있으면 복원 작업이 실패할 수 있습니다. **기존 연결 닫기** 옵션을 선택하여 [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] 와 데이터베이스 간의 모든 활성 연결을 닫습니다. 이 확인란을 선택하면 복원 작업을 수행하기 전에 데이터베이스가 단일 사용자 모드로 설정되고 복원 작업이 완료될 때 데이터베이스가 다중 사용자 모드로 설정됩니다.    
  
   5. 각 복원 작업 사이에 확인 메시지를 표시하려면 **각 백업 복원 전에 확인** 을 선택합니다. 데이터베이스가 크고 복원 작업의 상태를 모니터링하려는 경우가 아니면 이 옵션은 일반적으로 필요하지 않습니다.    
    
이러한 복원 옵션에 대한 자세한 내용은 [데이터베이스 복원&#40;옵션 페이지&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)라고도 함)를 백업해야 할 수 있습니다.    
    
9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="b-restore-an-earlier-disk-backup-over-an-existing-database"></a>B. 기존 데이터베이스에 이전 디스크 백업 복원
다음 예제에서는 `Sales` 의 이전 디스크 백업을 복원하고 기존 `Sales` 데이터베이스를 덮어씁니다.

1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
2.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원...** 을 선택합니다.  
3.  **일반** 페이지의 **원본** 섹션에서 **디바이스** 를 선택합니다.
4.  찾아보기( **...** ) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다. **추가** 를 클릭하고 백업으로 이동합니다. 디스크 백업 파일을 선택한 후 **확인** 을 클릭합니다.
5.  **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.
6.  **페이지 선택** 창에서 **옵션** 을 클릭합니다.
7.  **복원 옵션** 섹션에서 **기존 데이터베이스 덮어쓰기(WITH REPLACE)** 를 선택합니다.

    > [!NOTE]
    > 이 옵션을 선택하지 않으면 다음과 같은 오류 메시지가 발생할 수 있습니다. "System.Data.SqlClient.SqlError: 백업 세트에 기존 '`Sales`' 데이터베이스가 아닌 데이터베이스의 백업이 있습니다. (Microsoft.SqlServer.SmoExtended)"

8.  **비상 로그 백업** 섹션에서 **복원 전 비상 로그 백업 수행**의 선택을 취소합니다.

    > [!NOTE]
    > 모든 복원 시나리오에서 비상 로그 백업이 필요한 것은 아닙니다. 복구 시점이 이전 로그 백업에 포함될 경우에는 비상 로그 백업이 필요하지 않습니다. 데이터베이스를 이동 또는 대체(덮어쓰기)하며 가장 최근 백업 이후의 시점으로 이를 복원할 필요가 없을 경우에도 비상 로그 백업이 필요하지 않습니다. 자세한 내용은 [비상 로그 백업(SQL Server)](../../relational-databases/backup-restore/tail-log-backups-sql-server.md)를 참조하세요.

    이 옵션은 단순 복구 모델의 데이터베이스에 사용할 수 없습니다.

9.  **서버 연결** 섹션에서 **대상 데이터베이스에 대한 기존 연결 닫기**를 선택합니다.

    > [!NOTE]
    > 이 옵션을 선택하지 않으면 다음과 같은 오류 메시지가 발생할 수 있습니다. "System.Data.SqlClient.SqlError: 데이터베이스가 사용 중이어서 배타적으로 액세스할 수 없습니다. (Microsoft.SqlServer.SmoExtended)"
    
10. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="c--restore-an-earlier-disk-backup-with-a-new-database-name-where-the-original-database-still-exists"></a>C.  원래 데이터베이스가 있는 위치에서 이전 디스크 백업을 새 데이터베이스 이름으로 복원
다음 예제에서는 `Sales` 의 이전 디스크 백업을 복원하고 `SalesTest`라는 새 데이터베이스를 만듭니다.  원본 데이터베이스인 `Sales`가 서버에 여전히 있습니다.

1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
2.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원...** 을 선택합니다.  
3.  **일반** 페이지의 **원본** 섹션에서 **디바이스** 를 선택합니다.
4.  찾아보기( **...** ) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다. **추가** 를 클릭하고 백업으로 이동합니다. 디스크 백업 파일을 선택한 후 **확인** 을 클릭합니다.
5.  **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.
6.  **대상** 섹션의 **데이터베이스** 상자에는 복원할 데이터베이스의 이름이 자동으로 채워집니다. 데이터베이스의 이름을 변경하려면 **데이터베이스** 상자에 새 이름을 입력합니다.
7.  **페이지 선택** 창에서 **옵션** 을 클릭합니다.
8.  **비상 로그 백업** 섹션에서 "**복원 전 비상 로그 백업 수행**"의 선택을 취소합니다.

    > [!IMPORTANT]
    > 이 옵션의 선택을 취소하면 기존 데이터베이스인 `Sales`가 복원 중 상태로 바뀝니다.

9. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

    > [!NOTE]
    > 다음과 같은 오류 메시지가 나타나는 경우:      
    > "System.Data.SqlClient.SqlError: 데이터베이스 "`Sales`"의 비상 로그 백업이 수행되지 않았습니다. 로그에 포함된 작업이 손실되지 않도록 하려면 `BACKUP LOG WITH NORECOVERY`를 사용하여 로그를 백업합니다. 로그 내용을 덮어쓰려면 `RESTORE` 문의 `WITH REPLACE` 또는 `WITH STOPAT` 절을 사용합니다. (Microsoft.SqlServer.SmoExtended)"라는 오류 메시지가 표시되면      
    > 위의 6단계에서 사용한 새 데이터베이스 이름을 입력하지 않은 것입니다. 복원은 보통 실수로 복원 중 다른 데이터베이스로 현재 데이터베이스를 덮어쓰는 일을 방지합니다. `RESTORE` 문에서 지정된 데이터베이스가 현재 서버에 이미 존재하고 지정된 데이터베이스 패밀리 GUID가 백업 세트에 기록된 데이터베이스 패밀리 GUID와 다르면 해당 데이터베이스는 복원되지 않습니다. 이것은 중요한 보호 수단입니다.

### <a name="d--restore-earlier-disk-backups-to-a-point-in-time"></a>D.  이전 디스크 백업을 특정 시점으로 복원
다음 예에서는 `1:23:17 PM` , `May 30, 2016` 상태로 데이터베이스를 복원하고 여러 로그 백업이 연관된 복원 작업을 보여 줍니다. 데이터베이스가 현재 서버에 없습니다.

1.  **개체 탐색기**에서 [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] 의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.  
2.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원...** 을 선택합니다.  
3.  **일반** 페이지의 **원본** 섹션에서 **디바이스** 를 선택합니다.
4.  찾아보기( **...** ) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다. **추가** 를 클릭하고 전체 백업 및 관련된 모든 트랜잭션 로그 백업으로 이동합니다.  디스크 백업 파일을 선택한 후 **확인** 을 클릭합니다.
5.  **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.
6.  **대상** 섹션에서 **시간대** 를 클릭하여 **백업 시간대** 대화 상자에 액세스하고 복구 동작을 중지할 특정 시점을 수동으로 선택합니다.
7.  **특정 날짜 및 시간**을 선택합니다.  
8.  드롭다운 상자에서 **시간대 간격** 을 **시간** 으로 변경합니다(옵션).  
9.  슬라이더를 원하는 시간으로 이동합니다.
10. **확인** 을 클릭하여 일반 페이지로 돌아갑니다.
11. [!INCLUDE[clickOK](../../includes/clickok-md.md)] 

### <a name="e--restore-a-backup-from-the-microsoft-azure-storage-service"></a>E.  Microsoft Azure Storage 서비스에서 백업 복원

#### <a name="common-steps"></a>공통 단계
아래의 두 예제에서는 Microsoft Azure Storage 서비스에 있는 백업에서 `Sales` 복원을 수행합니다.  스토리지 계정 이름은 `mystorageaccount`입니다.  컨테이너는 `myfirstcontainer`입니다.  간단히 말해 처음 6단계는 여기에 한 번 나열되며 모든 예제는 **7단계**에서 시작됩니다.
1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.
2.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원...** 을 선택합니다.
3.  **일반** 페이지의 **원본** 섹션에서 **디바이스** 를 선택합니다.
4.  찾아보기(...) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다.    
5.  **백업 미디어 유형:** 드롭다운 목록에서 **URL** 을 선택합니다.
6.  **추가** 를 클릭하면 **백업 파일 위치 선택** 대화 상자가 열립니다.

#### <a name="e1---restore-a-striped-backup-over-an-existing-database-and-a-shared-access-signature-exists"></a>E1.   기존 데이터베이스에 스트라이프 백업을 복원하고 공유 액세스 서명이 있습니다.
읽기, 쓰기, 삭제 및 나열 권한이 있는 저장된 액세스 정책을 만들었습니다.  저장된 액세스 정책과 연결된 공유 액세스 서명을 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`컨테이너에 대해 만들었습니다.  SQL Server 자격 증명이 이미 있는 경우 단계는 대부분 동일합니다.  `Sales` 데이터베이스가 현재 서버에 있습니다.  백업 파일은 `Sales_stripe1of2_20160601.bak` 및 `Sales_stripe2of2_20160601.bak`입니다.  

1.  SQL Server 자격 증명이 이미 있으면 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` Azure Storage 컨테이너: **드롭다운 목록에서** 를 선택하고, 없으면 컨테이너 이름 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`를 수동으로 입력합니다. 
1. **공유 액세스 서명:** 서식 있는 텍스트 상자에 공유 액세스 서명을 입력합니다.
1. **확인** 을 클릭하면 **Microsoft Azure에서 백업 파일 찾기** 대화 상자가 열립니다.
1. **컨테이너** 를 확장하고 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`로 이동합니다.
1. Ctrl 키를 누른 채 `Sales_stripe1of2_20160601.bak` 및 `Sales_stripe2of2_20160601.bak`파일을 선택합니다.
1. **확인**을 클릭합니다.
1. **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.
1. **페이지 선택** 창에서 **옵션** 을 클릭합니다.
1. **복원 옵션** 섹션에서 **기존 데이터베이스 덮어쓰기(WITH REPLACE)** 를 선택합니다.
1. **비상 로그 백업** 섹션에서 **복원 전 비상 로그 백업 수행**의 선택을 취소합니다.
1. **서버 연결** 섹션에서 **대상 데이터베이스에 대한 기존 연결 닫기**를 선택합니다.
1. **확인**을 클릭합니다.

#### <a name="e2---a-shared-access-signature-does-not-exist"></a>E2.   공유 액세스 서명이 없는 경우
이 예제에서는 `Sales` 데이터베이스가 현재 서버에 없습니다.
1. **추가** 를 클릭하면 **Microsoft 구독에 연결** 대화 상자가 열립니다.  
1. **Microsoft 구독에 연결** 대화 상자를 완성하고 **확인** 을 클릭하여 **백업 파일 위치 선택** 대화 상자로 돌아갑니다.  자세한 내용은 [Microsoft Azure 구독에 연결](../../relational-databases/backup-restore/connect-to-a-microsoft-azure-subscription.md) 을 참조하세요.
1. **백업 파일 위치 선택** 대화 상자에서 **확인** 을 클릭하면 **Microsoft Azure에서 백업 파일 찾기** 대화 상자가 열립니다.
1. **컨테이너** 를 확장하고 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`로 이동합니다.
1. 백업 파일을 선택한 다음 **확인**을 클릭합니다.
1. **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.
1. **확인**을 클릭합니다.

#### <a name="f-restore-local-backup-to-microsoft-azure-storage-url"></a>F. Microsoft Azure Storage(URL)에 로컬 백업 복원
`Sales` 데이터베이스가 `https://mystorageaccount.blob.core.windows.net/myfirstcontainer` 에 있는 백업에서 Microsoft Azure Storage 컨테이너 `E:\MSSQL\BAK`로 복원됩니다.  Azure 컨테이너에 대한 SQL Server 자격 증명이 이미 생성되었습니다.  **복원** 태스크를 통해 만들 수 없으므로 대상 컨테이너에 대한 SQL Server 자격 증명이 이미 있어야 합니다.  `Sales` 데이터베이스가 현재 서버에 없습니다.
1.  **개체 탐색기**에서 SQL Server 데이터베이스 엔진의 인스턴스에 연결한 다음 해당 인스턴스를 확장합니다.
2.  **데이터베이스** 를 마우스 오른쪽 단추로 클릭하고 **데이터베이스 복원...** 을 선택합니다.
3.  **일반** 페이지의 **원본** 섹션에서 **디바이스** 를 선택합니다.
4.  찾아보기(...) 단추를 클릭하여 **백업 디바이스 선택** 대화 상자를 엽니다.  
5.  **백업 미디어 유형:** 드롭다운 목록에서 **파일** 을 선택합니다.
6.  **추가** 를 클릭하면 **백업 파일 찾기** 대화 상자가 열립니다.
7.  `E:\MSSQL\BAK`로 이동하고 백업 파일을 선택한 다음 **확인**을 클릭합니다.
8.  **확인** 을 클릭하여 **일반** 페이지로 돌아갑니다.
9.  **페이지 선택** 창에서 **파일** 을 클릭합니다.
10. **모든 폴더를 파일에 다시 배치**확인란을 선택합니다.
11. `https://mystorageaccount.blob.core.windows.net/myfirstcontainer`데이터 파일 폴더: **및** 로그 파일 폴더: **텍스트 상자에**컨테이너를 입력합니다.
12. **확인**을 클릭합니다.

## <a name="see-also"></a>참고 항목    
 [트랜잭션 로그 백업&#40;SQL Server&#41;](../../relational-databases/backup-restore/back-up-a-transaction-log-sql-server.md)     
 [전체 데이터베이스 백업 만들기&#40;SQL Server&#41;](../../relational-databases/backup-restore/create-a-full-database-backup-sql-server.md)     
 [데이터베이스를 새 위치로 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-database-to-a-new-location-sql-server.md)     
 [트랜잭션 로그 백업 복원&#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-a-transaction-log-backup-sql-server.md)     
 [RESTORE&#40;Transact-SQL&#41;](../../t-sql/statements/restore-statements-transact-sql.md)     
 [데이터베이스 복원&#40;옵션 페이지&#41;](../../relational-databases/backup-restore/restore-database-options-page.md)     
 [데이터베이스 복원&#40;일반 페이지&#41;](../../relational-databases/backup-restore/restore-database-general-page.md)    
    
  
