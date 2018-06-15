---
title: '1단원: 저장된 액세스 정책 및 공유 액세스 서명 만들기 | Microsoft 문서'
ms.custom: ''
ms.date: 06/02/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: tutorial
ms.reviewer: ''
ms.suite: sql
ms.technology: backup-restore
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- SQL Server 2016
ms.assetid: 41674d9d-8132-4bff-be4d-85a861419f3d
caps.latest.revision: 22
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 721f9245ff8057c54cef5facdf4a4de423e53961
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32942008"
---
# <a name="lesson-1-create-stored-access-policy-and-shared-access-signature"></a>1단원: 저장된 액세스 정책 및 공유 액세스 서명 만들기
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
이 단원에서는 [Azure PowerShell](https://azure.microsoft.com/en-us/documentation/articles/powershell-install-configure/) 스크립트를 사용하여 저장된 액세스 정책을 통해 Azure Blob 컨테이너에 공유 액세스 서명을 만듭니다.  
  
> [!NOTE]  
> 이 스크립트는 Azure PowerShell 5.0.10586을 사용하여 작성되었습니다.  
  
공유 액세스 서명은 컨테이너, Blob, 큐 또는 테이블에 대한 제한된 액세스 권한을 부여하는 URI입니다. 저장된 액세스 정책은 액세스 해지, 만료, 연장을 포함하여 서버 쪽에서 공유 액세스 서명에 대한 제어 수준을 추가로 제공합니다. 이 새로운 향상된 기능을 사용하는 경우 최소한 읽기, 쓰기 및 나열 권한이 있는 컨테이너에 정책을 만들어야 합니다.  
  
Azure PowerShell, Azure Storage SDK, Azure REST API 또는 타사 유틸리티를 사용하여 저장된 액세스 정책과 공유 액세스 서명을 만들 수 있습니다. 이 자습서에서는 Azure PowerShell 스크립트를 사용하여 이 작업을 완료하는 방법을 보여 줍니다. 스크립트는 리소스 관리자 배포 모델을 사용하며 다음과 같은 새 리소스를 만듭니다.  
  
-   리소스 그룹  
  
-   저장소 계정  
  
-   Azure Blob 컨테이너  
  
-   SAS 정책  
  
이 스크립트는 먼저 여러 변수를 선언하여 위 리소스의 이름 및 다음 필수 입력 값의 이름을 지정합니다.  
  
-   기타 리소스 개체의 이름 지정에 사용되는 접두사 이름  
  
-   구독 이름  
  
-   데이터 센터 위치  
  
> [!NOTE]  
> 이 스크립트는 기존 ARM 또는 클래식 배포 모델 리소스 중 하나를 사용할 수 있도록 작성되었습니다.  
  
스크립트는 [2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)에서 사용할 적절한 CREATE CREDENTIAL 문을 생성하여 작업을 완료합니다. 이 문은 클립보드에 복사되며 확인할 수 있도록 콘솔에 출력됩니다.  
  
컨테이너에 정책을 만들고 SAS(공유 액세스 서명) 키를 생성하려면 다음 단계를 따르세요.  
  
1.  Windows PowerShell 또는 Windows PowerShell ISE를 엽니다(위의 버전 요구 사항 참조).  
  
2.  다음 스크립트를 편집한 후 실행합니다.  
  
    ```  
    <#   
    This script uses the Azure Resource model and creates a new ARM storage account.  
    Modify this script to use an existing ARM or classic storage account   
    using the instructions in comments within this script  
    #>  
    # Define global variables for the script  
    $prefixName = '<a prefix name>'  # used as the prefix for the name for various objects  
    $subscriptionName='<your subscription name>'   # the name  of subscription name you will use  
    $locationName = '<a data center location>'  # the data center region you will use  
    $storageAccountName= $prefixName + 'storage' # the storage account name you will create or use  
    $containerName= $prefixName + 'container'  # the storage container name to which you will attach the SAS policy with its SAS token  
    $policyName = $prefixName + 'policy' # the name of the SAS policy  
  
    <#   
    Using Azure Resource Manager deployment model  
    Comment out this entire section and use the classic storage account name to use an existing classic storage account  
    #>  
  
    # Set a variable for the name of the resource group you will create or use  
    $resourceGroupName=$prefixName + 'rg'   
  
    # adds an authenticated Azure account for use in the session   
    Login-AzureRmAccount    
  
    # set the tenant, subscription and environment for use in the rest of   
    Set-AzureRmContext -SubscriptionName $subscriptionName   
  
    # create a new resource group - comment out this line to use an existing resource group  
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $locationName   
  
    # Create a new ARM storage account - comment out this line to use an existing ARM storage account  
    New-AzureRmStorageAccount -Name $storageAccountName -ResourceGroupName $resourceGroupName -Type Standard_RAGRS -Location $locationName   
  
    # Get the access keys for the ARM storage account  
    $accountKeys = Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $storageAccountName  
  
    # Create a new storage account context using an ARM storage account  
    $storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys[0].Value 
  
    <#  
    Using the Classic deployment model  
    Use the following four lines to use an existing classic storage account  
    #>  
    #Classic storage account name  
    #Add-AzureAccount  
    #Select-AzureSubscription -SubscriptionName $subscriptionName #provide an existing classic storage account  
    #$accountKeys = Get-AzureStorageKey -StorageAccountName $storageAccountName  
    #$storageContext = New-AzureStorageContext -StorageAccountName $storageAccountName -StorageAccountKey $accountKeys.Primary  
  
    # The remainder of this script works with either the ARM or classic sections of code above  
  
    # Creates a new container in blob storage  
    $container = New-AzureStorageContainer -Context $storageContext -Name $containerName  
  
    # Sets up a Stored Access Policy and a Shared Access Signature for the new container  
    $policy = New-AzureStorageContainerStoredAccessPolicy -Container $containerName -Policy $policyName -Context $storageContext -StartTime $(Get-Date).ToUniversalTime().AddMinutes(-5) -ExpiryTime $(Get-Date).ToUniversalTime().AddYears(10) -Permission rwld

    # Gets the Shared Access Signature for the policy  
    $sas = New-AzureStorageContainerSASToken -name $containerName -Policy $policyName -Context $storageContext
    Write-Host 'Shared Access Signature= '$($sas.Substring(1))''  
  
    # Outputs the Transact SQL to the clipboard and to the screen to create the credential using the Shared Access Signature  
    Write-Host 'Credential T-SQL'  
    $tSql = "CREATE CREDENTIAL [{0}] WITH IDENTITY='Shared Access Signature', SECRET='{1}'" -f $cbc.Uri,$sas.Substring(1)   
    $tSql | clip  
    Write-Host $tSql  
  
    ```  
  
3.  스크립트가 완료되면 다음 단원에서 사용할 수 있도록 클립보드에 CREATE CREDENTIAL 문이 있습니다.  
  
**다음 단원:**  
  
[2단원: 공유 액세스 서명을 사용하여 SQL Server 자격 증명 만들기](../relational-databases/lesson-2-create-a-sql-server-credential-using-a-shared-access-signature.md)  
  
## <a name="see-also"></a>참고 항목  
[공유 액세스 서명, 1부: SAS 모델 이해](https://azure.microsoft.com/en-us/documentation/articles/storage-dotnet-shared-access-signature-part-1/)  
[컨테이너 만들기](https://msdn.microsoft.com/library/azure/dd179468.aspx)  
[컨테이너 ACL 설정](https://msdn.microsoft.com/library/azure/dd179391.aspx)  
[컨테이너 ACL 가져오기](https://msdn.microsoft.com/library/azure/dd179469.aspx)  
  
  
  

