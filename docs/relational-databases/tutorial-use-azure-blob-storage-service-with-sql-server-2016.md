---
title: '자습서: SQL Server 2016에서 Azure Blob 스토리지 서비스 사용'
ms.custom: seo-dt-2019
ms.date: 01/10/2019
ms.prod: sql
ms.technology: ''
ms.prod_service: database-engine
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: e69be67d-da1c-41ae-8c9a-6b12c8c2fb61
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: aba8d7e3dc7aaf48523303ad6f63682c888b3c46
ms.sourcegitcommit: 4baa8d3c13dd290068885aea914845ede58aa840
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 03/13/2020
ms.locfileid: "79286977"
---
# <a name="tutorial-use-azure-blob-storage-service-with-sql-server-2016"></a>자습서: SQL Server 2016에서 Azure Blob 스토리지 서비스 사용

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
Microsoft Azure Blob Storage 서비스에서 SQL Server 2016 사용 자습서를 시작합니다. 이 자습서는 SQL Server 데이터 파일 및 SQL Server 백업에 Microsoft Azure Blob Storage 서비스를 사용하는 방법을 이해하는 데 도움이 됩니다.  
  
Microsoft Azure Blob Storage 서비스에 대한 SQL Server 통합 지원은 SQL Server 2012 서비스 팩 1 CU2 향상된 기능으로 시작되었으며, SQL Server 2014 및 SQL Server 2016에서 더욱 개선되었습니다. 이 기능에 대한 개요 및 사용할 경우의 이점은 [Microsoft Azure의 SQL Server 데이터 파일](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)을 참조하세요. 라이브 데모는 [지정 시간 복원 데모](https://channel9.msdn.com/Blogs/Windows-Azure/File-Snapshot-Backups-Demo)를 참조하세요.  

이 자습서에서는 여러 섹션을 통해 Microsoft Azure Blob Storage 서비스에서 SQL Server 데이터 파일을 사용하는 방법을 보여 줍니다. 각 섹션은 특정 작업을 중심으로 하며, 섹션을 순서대로 완료해야 합니다. 먼저 저장된 액세스 정책과 공유 액세스 서명을 사용하여 Blob Storage에 새 컨테이너를 만드는 방법을 알아봅니다. 그런 다음 SQL Server 자격 증명을 만들어 Azure Blob Storage에 SQL Server를 통합하는 방법을 살펴봅니다. 데이터베이스를 Blob 스토리지에 백업하고 Azure 가상 머신에 복원합니다. SQL Server 2016 파일-스냅샷 트랜잭션 로그 백업을 사용하여 특정 시점 및 새 데이터베이스로 복원합니다. 최종적으로, 이 자습서에서는 파일-스냅샷 백업 이해와 작업에 도움이 되도록 메타데이터 시스템 저장 프로시저 및 함수를 사용하는 방법을 보여 줍니다.
  
## <a name="prerequisites"></a>사전 요구 사항

이 자습서를 완료하려면 [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] 백업 및 복원 개념과 T-SQL 구문에 대해 잘 알고 있어야 합니다. 이 자습서를 사용하려면 Azure Storage 계정, SSMS(SQL Server Management Studio), SQL Server 온-프레미스의 인스턴스에 대한 액세스, SQL Server 2016을 실행하는 Azure VM(가상 머신)에 대한 액세스 및 AdventureWorks2016 데이터베이스가 필요합니다. 또한 BACKUP 및 RESTORE 명령을 실행하는 데 사용하는 계정은 **모든 자격 증명 변경** 권한이 있는 **db_backup operator** 데이터베이스 역할에 있어야 합니다. 

- 체험 [Azure 계정](https://azure.microsoft.com/offers/ms-azr-0044p/)을 받습니다.
- [Azure Storage 계정](https://docs.microsoft.com/azure/storage/common/storage-quickstart-create-account?tabs=portal)을 만듭니다.
- [SQL Server 2017 Developer Edition](https://www.microsoft.com/sql-server/sql-server-downloads)을 설치합니다.
- [SQL Server를 실행하는 Azure VM](https://azure.microsoft.com/documentation/articles/virtual-machines-provision-sql-server/) 프로비전
- [SQL Server Management Studio](https://docs.microsoft.com/sql/ssms/download-sql-server-management-studio-ssms)를 설치합니다.
- [AdventureWorks2016 샘플 데이터베이스](https://docs.microsoft.com/sql/samples/adventureworks-install-configure)를 다운로드합니다.
- 사용자 계정에 [db_backupoperator](https://docs.microsoft.com/sql/relational-databases/security/authentication-access/database-level-roles) 역할을 할당하고 [모든 자격 증명 변경](https://docs.microsoft.com/sql/t-sql/statements/alter-credential-transact-sql) 권한을 부여합니다. 

## <a name="1---create-stored-access-policy-and-shared-access-storage"></a>1 - 저장된 액세스 정책 및 공유 액세스 스토리지 만들기

이 섹션에서는 [Azure PowerShell](https://azure.microsoft.com/documentation/articles/powershell-install-configure/) 스크립트를 사용하여 저장된 액세스 정책을 통해 Azure Blob 컨테이너에 공유 액세스 서명을 만듭니다.  
  
> [!NOTE]  
> 이 스크립트는 Azure PowerShell 5.0.10586을 사용하여 작성되었습니다.  
  
공유 액세스 서명은 컨테이너, Blob, 큐 또는 테이블에 대한 제한된 액세스 권한을 부여하는 URI입니다. 저장된 액세스 정책은 액세스 해지, 만료, 연장을 포함하여 서버 쪽에서 공유 액세스 서명에 대한 제어 수준을 추가로 제공합니다. 이 새로운 향상된 기능을 사용하는 경우 최소한 읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들어야 합니다.  
  
Azure PowerShell, Azure Storage SDK, Azure REST API 또는 타사 유틸리티를 사용하여 저장된 액세스 정책과 공유 액세스 서명을 만들 수 있습니다. 이 자습서에서는 Azure PowerShell 스크립트를 사용하여 이 작업을 완료하는 방법을 보여 줍니다. 스크립트는 리소스 관리자 배포 모델을 사용하며 다음과 같은 새 리소스를 만듭니다.  
  
-   Resource group   
-   스토리지 계정  
-   Azure Blob 컨테이너   
-   SAS 정책    

이 스크립트는 먼저 여러 변수를 선언하여 위 리소스의 이름 및 다음 필수 입력 값의 이름을 지정합니다.  
  
-   기타 리소스 개체의 이름 지정에 사용되는 접두사 이름    
-   구독 이름    
-   데이터 센터 위치  

  
스크립트는 [2 - 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](#2---create-a-sql-server-credential-using-a-shared-access-signature)에서 사용할 적절한 CREATE CREDENTIAL 문을 생성하여 작업을 완료합니다. 이 문은 클립보드에 복사되며 확인할 수 있도록 콘솔에 출력됩니다.  
  
컨테이너에 정책을 만들고 SAS(공유 액세스 서명) 키를 생성하려면 다음 단계를 따르세요.  
  
1.  Windows PowerShell 또는 Windows PowerShell ISE를 엽니다(위의 버전 요구 사항 참조).  
  
2.  아래 스크립트를 편집한 후 실행합니다.  
  
    ```powershell
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionID = '<your subscription ID>'   # the ID  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy 

    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # Add an authenticated Azure account for use in the session   
    Connect-AzAccount    
  
    # Set the tenant, subscription and environment for use in the rest of   
    Set-AzContext -SubscriptionId $subscriptionID   
  
    # Create a new resource group - comment out this line to use an existing resource group  
    New-AzResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new Azure Resource Manager storage account - comment out this line to use an existing Azure Resource Manager storage account  
    New-AzStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the Azure Resource Manager storage account  
    $accountKeys = Get-AzStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an Azure Resource Manager storage account  
    $storageContext = New-AzStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value

    # Creates a new container in blob storage  
    $container = New-AzStorageContainer -Context $storageContext -Name $containerName  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $policy = New-AzStorageContainerStoredAccessPolicy -Container $containerName -Policy $policyName -Context $storageContext -StartTime $(Get-Date).ToUniversalTime().AddMinutes(-5) -ExpiryTime $(Get-Date).ToUniversalTime().AddYears(10) -Permission rwld

    # Gets the Shared Access Signature for the policy  
    $sas = New-AzStorageContainerSASToken -name $containerName -Policy $policyName -Context $storageContext
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  

    # Sets the variables for the new container you just created
    $container = Get-AzStorageContainer -Context $storageContext -Name $containerName
    $cbc = $container.CloudBlobContainer 
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql 

    # Once you're done with the tutorial, remove the resource group to clean up the resources. 
    # Remove-AzResourceGroup -Name $resourceGroupName  
    ```  

3.  스크립트가 완료되면 다음 섹션에서 사용할 수 있도록 클립보드에 CREATE CREDENTIAL 문이 있습니다.  


## <a name="2---create-a-sql-server-credential-using-a-shared-access-signature"></a>2 - 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기

이 섹션에서는 SQL Server가 이전 단계에서 만든 Azure 컨테이너에 쓰고 읽을 때 사용할 보안 정보를 저장하기 위한 자격 증명을 만듭니다.  
  
SQL Server 자격 증명은 SQL Server 외부의 리소스에 연결하는 데 필요한 인증 정보를 저장하는 데 사용되는 개체입니다. 자격 증명에는 스토리지 컨테이너의 URI 경로와 이 컨테이너에 대한 공유 액세스 서명이 저장됩니다.  

SQL Server 자격 증명을 만들려면 다음 단계를 수행합니다.  
  
1.  SQL Server Management Studio에 연결합니다.  
2.  새 쿼리 창을 열고 온-프레미스 환경에 있는 데이터베이스 엔진의 SQL Server 인스턴스에 연결합니다.  
  
3.  새 쿼리 창에서 섹션 1의 공유 액세스 서명을 사용하는 CREATE CREDENTIAL 문을 붙여넣고 해당 스크립트를 실행합니다.  
  
    스크립트는 다음 코드와 같습니다.  
  
    ```sql   
    /* Example:
    USE master  
    CREATE CREDENTIAL [https://msfttutorial.blob.core.windows.net/containername] 
    WITH IDENTITY='SHARED ACCESS SIGNATURE'   
    , SECRET = 'sharedaccesssignature' 
    GO */
    
    USE master  
    CREATE CREDENTIAL [https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>] 
      -- this name must match the container path, start with https and must not contain a forward slash at the end
    WITH IDENTITY='SHARED ACCESS SIGNATURE' 
      -- this is a mandatory string and should not be changed   
     , SECRET = 'sharedaccesssignature' 
       -- this is the shared access signature key that you obtained in section 1.   
    GO    
    ```  
  
4.  사용할 수 있는 모든 자격 증명을 보려면 인스턴스에 연결된 쿼리 창에서 다음 문을 실행합니다.  
  
    ```sql  
    SELECT * from sys.credentials  
    ```  
  
5.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 인스턴스에 연결합니다.  
  
6.  새 쿼리 창에서 섹션 1의 공유 액세스 서명을 사용하는 CREATE CREDENTIAL 문을 붙여넣고 해당 스크립트를 실행합니다.  
  
7.  Azure 컨테이너에 액세스할 수 있게 하려는 추가 SQL Server 인스턴스에 대해 5단계와 6단계를 반복합니다.  

## <a name="3---database-backup-to-url"></a>3 - URL에 데이터베이스 백업

이 섹션에서는 온-프레미스 SQL Server 2016 인스턴스의 AdventureWorks2016 데이터베이스를 [섹션 1](#1---create-stored-access-policy-and-shared-access-storage)에서 만든 Azure 컨테이너로 백업합니다.
  
> [!NOTE]  
> SQL Server 2012 SP1 CU2 이상 데이터베이스 또는 SQL Server 2014 데이터베이스를 이 Azure 컨테이너에 백업하려는 경우 [여기](https://docs.microsoft.com/sql/relational-databases/backup-restore/sql-server-backup-to-url?view=sql-server-2014) 에 문서화된 사용되지 않는 구문을 통해 WITH CREDENTIAL 구문을 사용하여 URL에 백업할 수 있습니다.  
  
Blob Storage에 데이터베이스를 백업하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
2.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 섹션 1에서 지정한 컨테이너 및 스토리지 계정 이름에 맞게 URL을 수정한 다음, 이 스크립트를 실행합니다.  
  
    ```sql  
  
    -- To permit log backups, before the full database backup, modify the database to use the full recovery model.  
    USE master;  
    ALTER DATABASE AdventureWorks2016  
       SET RECOVERY FULL;  
  
    -- Back up the full AdventureWorks2016 database to the container that you created in section 1  
    BACKUP DATABASE AdventureWorks2016   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_onprem.bak'  
  
    ```  
  
4.  개체 탐색기를 열고 스토리지 계정 및 계정 키를 사용하여 Azure Storage에 연결합니다. 
    1.  컨테이너를 확장하고 섹션 1에서 만든 컨테이너를 확장한 다음, 위 3단계의 백업이 이 컨테이너에 표시되는지 확인합니다.  
  
   ![Azure Storage 계정에 연결](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/connect-to-azure-storage.png)


## <a name="4----restore-database-to-virtual-machine-from-url"></a>4 - URL에서 가상 머신으로 데이터베이스 복원

이 섹션에서는 Azure 가상 머신의 SQL Server 2016 인스턴스로 AdventureWorks2016 데이터베이스를 복원합니다.
  
> [!NOTE]  
> 이 자습서에서는 간단한 설명을 위해 데이터베이스 백업에 사용한 것과 동일한 컨테이너를 데이터 및 로그 파일에 사용합니다. 프로덕션 환경에서는 여러 컨테이너를 사용할 가능성이 크며, 여러 데이터 파일을 사용하는 경우도 많습니다. SQL Server 2016에서는 큰 데이터베이스를 백업할 때 백업 성능을 향상시키기 위해 여러 blob에 백업을 스트라이핑할 수도 있습니다.  
  
Azure Blob 스토리지에서 Azure 가상 머신의 SQL Server 2016 인스턴스로 AdventureWorks2016 데이터베이스를 복원하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.   
2.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.   
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 섹션 1에서 지정한 컨테이너 및 스토리지 계정 이름에 맞게 URL을 수정한 다음, 이 스크립트를 실행합니다.  
  
    ```sql  
    -- Restore AdventureWorks2016 from URL to SQL Server instance using Azure blob storage for database files  
    RESTORE DATABASE AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_onprem.bak'   
       WITH  
          MOVE 'AdventureWorks2016_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Data.mdf'  
         ,MOVE 'AdventureWorks2016_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Log.ldf'  
    --, REPLACE  
  
    ```  
  
4.  개체 탐색기를 열고 Azure SQL Server 2016 인스턴스에 연결합니다.   
5.  개체 탐색기에서 데이터베이스 노드를 확장하고 AdventureWorks2016 데이터베이스가 복원되었는지 확인합니다(필요에 따라 노드 새로 고침).    
    1. AdventureWorks2016을 마우스 오른쪽 단추로 클릭하고 속성을 선택합니다.
    1. 파일을 선택하고 두 데이터베이스 파일의 경로가 Azure 블로그 컨테이너의 blob을 가리키는 URL인지 확인합니다(완료되면 취소 선택).
    
     ![Azure VM의 AdventureWorks 데이터베이스](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/adventureworks-on-azure-vm.png)

    
8.  개체 탐색기에서 Azure Storage에 연결합니다.
    1. 컨테이너를 확장하고 섹션 1에서 만든 컨테이너를 확장한 다음, 위 3단계의 AdventureWorks2016_Data.mdf 및 AdventureWorks2016_Log.ldf가 섹션 3의 백업 파일과 함께 이 컨테이너에 표시되는지 확인합니다(필요에 따라 노드 새로 고침).  
  
   ![Azure의 컨테이너 내 데이터 파일](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/data-files-in-container.png)

## <a name="5---backup-database-using-file-snapshot-backup"></a>5 - 파일-스냅샷 백업을 사용하여 데이터베이스 백업

이 섹션에서는 Azure 스냅샷을 사용하여 거의 즉시 백업을 수행하기 위해 파일-스냅샷 백업을 사용하여 Azure 가상 머신에서 AdventureWorks2016 데이터베이스를 백업합니다. 파일-스냅샷 백업에 대한 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅샷 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
파일-스냅샷 백업을 사용하여 AdventureWorks2016 데이터베이스를 백업하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.   
2.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
3.  다음 TRANSACT-SQL 스크립트를 복사하여 쿼리 창에 붙여넣고 실행합니다. 이 쿼리 창을 닫지 마세요. 5단계에서 이 스크립트를 다시 실행합니다. 이 시스템 저장 프로시저를 사용하면 지정된 데이터베이스를 구성하는 각 파일에 대한 기존 파일 스냅샷 백업을 볼 수 있습니다. 이 데이터베이스에 대한 파일 스냅샷 백업이 없는 것을 확인할 수 있습니다.  
  
    ```sql  
    -- Verify that no file snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
    ```  
  
4.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 섹션 1에서 지정한 컨테이너 및 스토리지 계정 이름에 맞게 URL을 수정한 다음, 이 스크립트를 실행합니다. 이 백업이 얼마나 빨리 수행되는지 확인합니다.  
  
    ```sql  
    -- Backup the AdventureWorks2016 database with FILE_SNAPSHOT  
    BACKUP DATABASE AdventureWorks2016   
       TO URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2016_Azure.bak'   
       WITH FILE_SNAPSHOT;    
    ```  
  
5.  4단계의 스크립트가 성공적으로 실행되었는지 확인한 후 다음 스크립트를 다시 실행합니다. 4단계의 파일-스냅샷 백업 작업은 데이터와 로그 파일 둘 다의 파일-스냅샷을 생성했습니다.  
  
    ```sql  
    -- Verify that two file-snapshot backups exist  
    SELECT * FROM sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
  
    ```  
  
    ![스냅샷을 표시하는 fn_db_backup_file_snapshots의 결과](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/results-showing-snapshot.png) 
  
6.  개체 탐색기에서 Azure 가상 머신의 SQL Server 2016 인스턴스에 있는 데이터베이스 노드를 확장하고 AdventureWorks2016 데이터베이스가 이 인스턴스로 복원되었는지 확인합니다(필요에 따라 노드 새로 고침).  
7.  개체 탐색기에서 Azure Storage에 연결합니다.   
8.  컨테이너를 확장하고 섹션 1에서 만든 컨테이너를 확장한 다음, 위 4단계의 AdventureWorks2016_Azure.bak가 섹션 3의 백업 파일 및 섹션 4의 데이터베이스 파일과 함께 이 컨테이너에 표시되는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![Azure에서 스냅샷 백업](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/snapshot-backup-on-azure.PNG)

## <a name="6----generate-activity-and-backup-log-using-file-snapshot-backup"></a>6 - 파일-스냅샷 백업을 사용하여 작업 및 백업 로그 생성

이 섹션에서는 AdventureWorks2016 데이터베이스에 작업을 생성하고 파일-스냅샷 백업을 사용하여 정기적으로 트랜잭션 로그 백업을 만듭니다. 파일 스냅샷 백업 사용 방법에 대한 자세한 내용은 [Azure의 데이터베이스 파일에 대한 파일-스냅샷 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
AdventureWorks2016 데이터베이스에 작업을 생성하고 파일-스냅샷 백업을 사용하여 정기적으로 트랜잭션 로그 백업을 만들려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.   
2.  두 개의 새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 각각 연결합니다.   
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창의 하나에 붙여넣은 다음 실행합니다. 4단계에서 새 행을 추가하기 전에는 Production.Location 테이블에 14개의 행이 있습니다.  
  
    ```sql 
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2016.Production.Location;    
    ```  
  
4.  다음 Transact-SQL 스크립트 두 개를 복사하여 두 개의 개별 쿼리 창에 붙여넣습니다. 섹션 1에서 지정한 컨테이너 및 스토리지 계정 이름에 맞게 URL을 수정한 다음, 개별 쿼리 창에서 두 스크립트를 동시에 실행합니다. 두 스크립트를 완료하는 데 약 7분 정도 걸립니다.  
  
    ```sql  
    -- Insert 30,000 new rows into the Production.Location table in the AdventureWorks2014 database in batches of 75  
    DECLARE @count INT=1, @inner INT;  
    WHILE @count < 400  
       BEGIN  
          BEGIN TRAN;  
             SET @inner =1;  
                WHILE @inner <= 75  
                   BEGIN;  
                      INSERT INTO AdventureWorks2016.Production.Location    
                         (Name, CostRate, Availability, ModifiedDate)   
                            VALUES (NEWID(), .5, 5.2, GETDATE());  
                      SET @inner = @inner + 1;  
                   END;  
          COMMIT;  
       WAITFOR DELAY '00:00:01';   
       SET @count = @count + 1;  
       END;  
    SELECT COUNT (*) from AdventureWorks2014.Production.Location;    
    ```  
  
    ```sql  
    --take 7 transaction log backups with FILE_SNAPSHOT, one per minute, and include the row count and the execution time in the backup file name   
    DECLARE @count INT=1, @device NVARCHAR(120), @numrows INT;  
    WHILE @count <= 7  
       BEGIN  
             SET @numrows = (SELECT COUNT (*) FROM AdventureWorks2016.Production.Location);  
             SET @device = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-' + CONVERT (varchar(10),@numrows) + '-' + FORMAT(GETDATE(), 'yyyyMMddHHmmss') + '.bak';  
             BACKUP LOG AdventureWorks2016 TO URL = @device WITH FILE_SNAPSHOT;  
             SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016');  
          WAITFOR DELAY '00:1:00';   
             SET @count = @count + 1;  
       END;  
    ```  
  
5.  첫 번째 스크립트의 출력을 검토하여 최종 행 개수가 29,939개인 것을 확인합니다.  
  
    ![행 수 29,939가 표시됨](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/29-thousand-rows.png)
  
6.  두 번째 스크립트의 출력을 검토하여 BACKUP LOG 문을 실행할 때마다 두 개의 새 파일 스냅샷이 생성되는 것을 확인합니다.로그 파일의 파일 스냅샷 하나와 데이터 파일의 파일 스냅샷 하나 등 총 두 개의 파일 스냅샷이 각 데이터베이스 파일마다 생성됩니다. 두 번째 스크립트가 완료되면 각 데이터베이스 파일마다 8개씩, 총 16개의 파일 스냅샷이 있습니다. BACKUP DATABASE 문에서 하나가 생성되고 BACKUP LOG 문을 실행할 때마다 하나가 생성되었습니다.  
  
   ![스냅샷 결과 백업](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/snapshot-back-results.png)
  
7.  개체 탐색기에서 Azure Storage에 연결합니다.  
  
8.  컨테이너를 확장하고 섹션 1에서 만든 컨테이너를 확장한 다음, 이전 섹션의 데이터 파일과 함께 7개의 새 백업 파일이 나타나는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![Azure 컨테이너 여러 스냅샷](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/tutorial-snapshots-in-container.png)

## <a name="7---restore-a-database-to-a-point-in-time"></a>7 - 데이터베이스를 지정 시간으로 복원

이 섹션에서는 두 트랜잭션 로그 백업 사이의 특정 시점으로 AdventureWorks2016 데이터베이스를 복원합니다.  
  
기존의 백업에서 특정 시점 복원을 수행하려면 전체 데이터베이스 백업, 차등 백업 및 복원하려는 시점 바로 다음까지의 모든 트랜잭션 로그 파일을 사용해야 합니다. 파일-스냅샷 백업을 사용할 경우 복원하려는 시간을 프레이밍하는 골대를 제공하는 두 개의 인접한 로그 백업 파일만 있으면 됩니다. 각 로그 백업이 각 데이터베이스 파일(각 데이터 파일 및 로그 파일)의 파일 스냅샷을 만들기 때문에 두 개의 로그 파일 스냅샷 백업 세트만 있으면 됩니다.  
  
파일 스냅샷 백업 세트에서 지정한 특정 시점으로 데이터베이스를 복원하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
2.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.   
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣은 다음 실행합니다. 5단계에서 더 적은 수의 행이 있는 특정 시점으로 복원하기 전에 Production.Location 테이블에 29,939개의 행이 있는지 확인합니다.  
  
    ```sql
    -- Verify row count at start  
    SELECT COUNT (*) from AdventureWorks2016.Production.Location   
    ```  
  
    ![행 수 29,939가 표시됨](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/29-thousand-rows.png) 
  
4.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 인접한 두 개의 로그 백업 파일을 선택하고 파일 이름을 이 스크립트에 필요한 날짜 및 시간으로 변환합니다. 섹션 1에서 지정한 컨테이너 및 스토리지 계정 이름에 맞게 URL을 수정하고 첫 번째 및 두 번째 백업 파일 이름을 제공한 다음, “June 26, 2018 01:48 PM”의 형식으로 STOPAT 시간을 제공하고 이 스크립트를 실행합니다. 이 스크립트를 완료하려면 몇 분 정도 걸립니다.  
  
    ```sql  
    -- restore and recover to a point in time between the times of two transaction log backups, and then verify the row count  
    ALTER DATABASE AdventureWorks2016 SET SINGLE_USER WITH ROLLBACK IMMEDIATE;  
    RESTORE DATABASE AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<firstbackupfile>.bak'   
       WITH NORECOVERY,REPLACE;  
    RESTORE LOG AdventureWorks2016   
       FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<secondbackupfile>.bak'    
       WITH RECOVERY, STOPAT = 'June 26, 2018 01:48 PM';  
    ALTER DATABASE AdventureWorks2016 set multi_user;  
    -- get new count  
    SELECT COUNT (*) FROM AdventureWorks2016.Production.Location ;
    ```  
  
5.  출력을 검토합니다. 복원 후 행 개수는 18,389개로, 로그 백업 5와 6 사이의 행 개수입니다(사용자 행 개수는 다를 수 있음).  
  
    ![18-thousand-rows.JPG](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/18-thousand-rows.png)

## <a name="8----restore-as-new-database-from-log-backup"></a>8 - 로그 백업에서 새 데이터베이스로 복원

이 섹션에서는 파일-스냅샷 트랜잭션 로그 백업에서 AdventureWorks2016 데이터베이스를 새 데이터베이스로 복원합니다.  
  
이 시나리오에서는 비즈니스 분석 및 보고를 위해 다른 가상 머신의 SQL Server 인스턴스로 복원을 수행합니다. 다른 가상 머신의 다른 인스턴스로 복원할 경우 이 목적을 위한 큰 전용 가상 머신에 작업이 오프로드되므로 트랜잭션 시스템의 리소스를 사용할 필요가 없습니다.  
  
트랜잭션 로그 백업에서 파일-스냅샷 백업을 사용한 복원은 매우 빠르며, 기존의 스트리밍 백업보다 훨씬 더 빠릅니다. 기존의 스트리밍 백업의 경우 전체 데이터베이스 백업, 차등 백업 및 일부 또는 전체 트랜잭션 로그 백업(또는 새로운 전체 데이터베이스 백업)을 사용해야 합니다. 그러나 파일-스냅샷 로그 백업의 경우 가장 최근 로그 백업(또는 다른 로그 백업이나 두 로그 백업 시간 사이의 지점으로 특정 시점 복원을 위한 두 개의 인접한 로그 백업)만 있으면 됩니다. 즉, 각 파일-스냅샷 로그 백업이 각 데이터베이스 파일(각 데이터 파일 및 로그 파일)의 파일 스냅샷을 만들기 때문에 하나의 로그 파일-스냅샷 백업 세트만 있으면 됩니다.  
  
파일 스냅샷 백업을 사용하여 트랜잭션 로그 백업에서 새 데이터베이스로 데이터베이스를 복원하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.   
2.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스에 연결합니다.  
  
    > [!NOTE]  
    > 이전 섹션에 사용한 것과 다른 Azure 가상 머신인 경우 [2 - 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](#2---create-a-sql-server-credential-using-a-shared-access-signature)의 단계를 수행한 상태여야 합니다. 다른 컨테이너로 복원하려면 새 컨테이너에 대해 [1 - 저장된 액세스 정책 및 공유 액세스 스토리지 만들기](#1---create-stored-access-policy-and-shared-access-storage)를 수행하세요.  
  
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 사용할 로그 백업 파일을 선택합니다. 섹션 1에서 지정한 컨테이너 및 스토리지 계정 이름에 맞게 URL을 수정하고 로그 백업 파일 이름을 제공한 다음, 이 스크립트를 실행합니다.  
  
    ```sql  
    -- restore as a new database from a transaction log backup file  
    RESTORE DATABASE AdventureWorks2016_EOM   
        FROM URL = 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/<logbackupfile.bak'    
        WITH MOVE 'AdventureWorks2016_data' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Data.mdf'  
       , MOVE 'AdventureWorks2016_log' to 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/AdventureWorks2014_EOM_Log.ldf'  
       , RECOVERY  
    --, REPLACE   
    ```  
  
4.  출력을 검토하여 복원이 성공했는지 확인합니다.   
5.  개체 탐색기에서 Azure Storage에 연결합니다.    
6.  컨테이너를 확장하고, 섹션 1에서 만든 컨테이너를 확장한 다음(필요한 경우 새로 고침), 새 데이터 및 로그 파일이 이전 섹션의 Blob과 함께 컨테이너에 나타나는지 확인합니다.  
  
    ![새 데이터베이스에 대한 데이터 및 로그 파일을 보여 주는 Azure 컨테이너](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/new-db-in-azure-container.png)

## <a name="9---manage-backup-sets-and-file-snapshot-backups"></a>9 - 백업 세트 및 파일-스냅샷 백업 관리

이 섹션에서는 [sp_delete_backup &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md) 시스템 저장 프로시저를 사용하여 백업 세트를 삭제합니다. 이 시스템 저장 프로시저는 이 백업 세트와 연결된 각 데이터베이스 파일에서 백업 파일 및 파일 스냅샷을 삭제합니다.  
  
> [!NOTE]  
> Azure Blob 컨테이너에서 백업 파일을 삭제하여 백업 세트를 삭제하려고 하면 백업 파일 자체만 삭제되고 연결된 파일 스냅샷은 유지됩니다. 이 시나리오에서는 [sys.fn_db_backup_file_snapshots &#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md) 시스템 함수를 사용하여 분리된 파일 스냅샷의 URL을 확인하고 [sp_delete_backup_file_snapshot &#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) 시스템 저장 프로시저를 사용하여 각 분리된 파일 스냅샷을 삭제합니다. 자세한 내용은  [Azure의 데이터베이스 파일에 대한 파일-스냅샷 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)을 참조하세요.  
  
파일-스냅샷 백업 세트를 삭제하려면 다음 단계를 따르세요.  
  
1.  SQL Server Management Studio에 연결합니다.  
2.  새 쿼리 창을 열고 Azure 가상 머신에 있는 데이터베이스 엔진의 SQL Server 2016 인스턴스(또는 이 컨테이너에 대한 읽기 및 쓰기 권한이 있는 모든 SQL Server 2016 인스턴스)에 연결합니다.   
3.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣습니다. 연결된 파일 스냅샷과 함께 삭제할 로그 백업을 선택합니다. 섹션 1에서 지정한 컨테이너 및 스토리지 계정 이름에 맞게 URL을 수정하고 로그 백업 파일 이름을 제공한 다음, 이 스크립트를 실행합니다.  
  
  ```sql
  sys.sp_delete_backup 'https://<mystorageaccountname>.blob.core.windows.net/<mystorageaccountcontainername>/tutorial-21764-20181003205236.bak';  
  ```  
  
4.  개체 탐색기에서 Azure Storage에 연결합니다.  
5.  컨테이너를 확장하고 섹션 1에서 만든 컨테이너를 확장한 다음, 3단계에서 사용한 백업 파일이 이 컨테이너에 더 이상 표시되지 않는지 확인합니다(필요에 따라 노드 새로 고침).  
  
    ![로그 백업 Blob 삭제를 보여 주는 Azure 컨테이너](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/deleted-backup-snapshot.png)
  
6.  다음 Transact-SQL 스크립트를 복사하여 쿼리 창에 붙여넣은 다음 실행하여 두 개의 파일 스냅샷이 삭제되었는지 확인합니다.  
  
    ```sql  
    -- verify that two file snapshots have been removed  
    SELECT * from sys.fn_db_backup_file_snapshots ('AdventureWorks2016');   
    ```  
    ![2개의 파일 스냅샷이 삭제되었음을 보여 주는 결과 창](media/tutorial-use-azure-blob-storage-service-with-sql-server-2016/results-of-two-deleted-snapshot-files.png)

## <a name="10---remove-resources"></a>10 - 리소스 제거

이 자습서를 완료하고 리소스를 보존하려면 이 자습서에서 생성된 리소스 그룹을 삭제해야 합니다. 

리소스 그룹을 삭제하려면 다음 powershell 코드를 실행합니다.

  ```powershell
  # Define global variables for the script  
  $prefixName = '<prefix name>'  # should be the same as the beginning of the tutorial
  
  # Set a variable for the name of the resource group you will create or use  
  $resourceGroupName=$prefixName + 'rg'   
  
  # Adds an authenticated Azure account for use in the session   
  Connect-AzAccount    
  
  # Set the tenant, subscription and environment for use in the rest of   
  Set-AzContext -SubscriptionId $subscriptionID    
    
  # Remove the resource group
  Remove-AzResourceGroup -Name $resourceGroupName   
  ```


  
## <a name="see-also"></a>참고 항목

[Microsoft Azure의 SQL Server 데이터 파일](../relational-databases/databases/sql-server-data-files-in-microsoft-azure.md)  
[Azure의 데이터베이스 파일에 대한 파일-스냅샷 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
[URL에 SQL Server 백업](../relational-databases/backup-restore/sql-server-backup-to-url.md) 
[공유 액세스 서명, 1부: SAS 모델 이해](https://azure.microsoft.com/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[컨테이너 만들기](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[컨테이너 ACL 설정](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[컨테이너 ACL 가져오기](https://msdn.microsoft.com/library/azure/dd179469.aspx)
[자격 증명&#40;데이터베이스 엔진&#41;](../relational-databases/security/authentication-access/credentials-database-engine.md)  
[CREATE CREDENTIAL &#40;Transact-SQL&#41;](../t-sql/statements/create-credential-transact-sql.md)  
[sys.credentials&#40;Transact-SQL&#41;](../relational-databases/system-catalog-views/sys-credentials-transact-sql.md)  
[sp_delete_backup&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup.md)  
[sys.fn_db_backup_file_snapshots&#40;Transact-SQL&#41;](../relational-databases/system-functions/sys-fn-db-backup-file-snapshots-transact-sql.md)  
[sp_delete_backup_file_snapshot&#40;Transact-SQL&#41;](../relational-databases/system-stored-procedures/snapshot-backup-sp-delete-backup-file-snapshot.md) [Azure의 데이터베이스 파일에 대한 파일-스냅샷 백업](../relational-databases/backup-restore/file-snapshot-backups-for-database-files-in-azure.md)  
