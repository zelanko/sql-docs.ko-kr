---
title: 활성 임대가 있는 백업 Blob 파일 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 08/17/2017
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: cdc58884e65fb243bbb75f257e19ccef3faa2b9f
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/01/2020
ms.locfileid: "72908941"
---
# <a name="delete-backup-blob-files-with-active-leases"></a>활성 임대가 있는 백업 Blob 파일 삭제

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

Microsoft Azure Storage로 백업하거나 Microsoft Azure Storage에서 복원할 때 SQL Server는 Blob에 대한 단독 액세스를 잠그기 위해 무한 임대를 획득합니다. 백업 또는 복원 프로세스가 성공적으로 완료되면 임대가 해제됩니다. 백업 또는 복원에 실패하면 백업 프로세스에서는 잘못된 모든 Blob을 정리하려고 합니다. 하지만 오랫동안 지속된 네트워크 연결 오류로 인해 백업이 실패한 경우에는 백업 프로세스에서 blob에 액세스할 수 없으므로 blob이 분리됩니다. 즉, 임대가 해제될 때까지 Blob을 쓰거나 삭제할 수 없습니다. 이 항목에서는 임대를 해제(중단)하고 Blob을 삭제하는 방법을 설명합니다.
  
임대 유형에 대한 자세한 내용은 이 [문서](https://go.microsoft.com/fwlink/?LinkId=275664)를 참조하세요.  
  
백업 작업이 실패하는 경우 잘못된 백업 파일이 만들어질 수 있습니다. 백업 blob 파일에 활성 임대도 있어 해당 blob을 삭제하거나 덮어쓸 수 없습니다. 이러한 Blob을 삭제하거나 덮어쓰려면 먼저 임대를 해제(중단)해야 합니다. 백업 실패가 있는 경우 임대를 정리하고 Blob을 삭제하는 것이 좋습니다. 스토리지 관리 작업의 일부로 주기적으로 임대를 정리하고 Blob을 삭제할 수도 있습니다.  
  
복원 실패가 있는 경우 후속 복원이 차단되지 않으므로 활성 임대는 문제가 되지 않을 수 있습니다. blob을 덮어쓰거나 삭제해야 할 때만 임대 해제가 필요합니다.  
  
## <a name="manage-orphaned-blobs"></a>분리된 Blob 관리

다음 단계에서는 백업 또는 복원 작업 실패 후 정리하는 방법을 설명합니다. PowerShell 스크립트를 사용하여 모든 단계를 수행할 수 있습니다. 다음 섹션에는 예제 PowerShell 스크립트가 포함되어 있습니다.  
  
1. **임대가 있는 Blob 식별:** 백업 프로세스를 실행하는 스크립트나 프로세스가 있는 경우 해당 스크립트나 프로세스 내에서 오류를 캡처하여 Blob 정리에 사용할 수 있습니다.  LeaseStats 및 LeastState 속성을 사용하여 임대가 있는 Blob을 식별할 수도 있습니다. Blob을 식별하고 나서 목록을 검토하고 백업 파일의 유효성을 확인한 후 Blob을 삭제합니다.  
  
1. **임대 중단:** 권한 있는 요청은 임대 ID를 제공하지 않고 임대를 중단할 수 있습니다. 자세한 내용은 [여기](https://go.microsoft.com/fwlink/?LinkID=275664) 를 참조하십시오.  
  
    > [!TIP]  
    > SQL Server는 복원 작업 중 임대 ID를 실행하여 단독 액세스를 설정합니다. 복원 임대 ID는 BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2입니다.  
  
1. **Blob 삭제:** 활성 임대가 있는 Blob을 삭제하려면 먼저 임대를 중단해야 합니다.  

###  <a name="Code_Example"></a> PowerShell 스크립트 예  
  
> [!IMPORTANT]
> PowerShell 2.0을 실행하는 경우 Microsoft WindowsAzure.Storage.dll 어셈블리를 로드하는 데 문제가 있을 수 있습니다. 문제 해결을 위해 [PowerShell](https://docs.microsoft.com/powershell/)을 업그레이드하는 것이 좋습니다. 다음 해결 방법을 사용하여 다음과 같이 powershell.exe.config 파일을 만들거나 수정하여 런타임에 .NET 2.0 및 .NET 4.0 어셈블리를 로드할 수도 있습니다.  
>
> ```xml
> <?xml version="1.0"?>
>     <configuration>
>         <startup useLegacyV2RuntimeActivationPolicy="true">
>             <supportedRuntime version="v4.0.30319"/>
>             <supportedRuntime version="v2.0.50727"/>
>         </startup>
>     </configuration>  
> ```  
  
 다음 예제 스크립트에서는 활성 임대가 있는 Blob을 식별한 다음 중단합니다. 임대 ID를 필터링하는 방법도 보여 줍니다.  
  
#### <a name="tips-on-running-this-script"></a>이 스크립트 실행 팁
  
> [!WARNING]  
> 이 스크립트는 백업에서 동시에 획득하려고 하는 임대를 중단하므로 이 스크립트와 동시에 Azure Blob Storage 서비스로의 백업을 실행할 경우 백업이 실패할 수 있습니다. 이 스크립트는 유지 관리 기간에 실행하거나, 실행되고 있거나 실행될 예정인 백업이 없을 때 실행하세요.  
  
- 이 스크립트를 실행하려면 먼저 스토리지 계정, 스토리지 키, 컨테이너 및 Azure Storage 어셈블리 경로와 이름 매개 변수의 값을 추가해야 합니다. 스토리지 어셈블리의 경로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리입니다. 스토리지 어셈블리의 파일 이름은 Microsoft.WindowsAzure.Storage.dll입니다.
  
- 잠긴 임대가 있는 Blob이 없는 경우 다음 메시지가 나타납니다. `There are no blobs with locked lease status`
  
- 잠긴 임대를 가진 blob이 있는 경우 다음과 같은 메시지가 나타납니다. `Breaking Leases`, `The lease on <URL of the Blob> is a restore lease: You will see this message only if you have a blob with a restore lease that is still active.` 및 `The lease on <URL of the Blob> is not a restore lease Breaking lease on <URL of the Bob>.`
  
```powershell
$storageAccount = "<myStorageAccount>"
$storageKey = "<myStorageKey>"
$blobContainer = "<myBlobContainer>"
$storageAssemblyPathName = "<myStorageAssemblyPathName>"
  
# well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
$container = $client.GetContainerReference($blobContainer)  
  
# list all the blobs  
$blobs = $container.ListBlobs($null,$true)
  
# filter blobs that are have Lease Status as "locked"
$lockedBlobs = @()  
foreach($blob in $blobs)  
{  
    $blobProperties = $blob.Properties
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
    }  
}  

if($lockedBlobs.Count -gt 0)  
{  
    Write-Host "Breaking leases..."
    foreach($blob in $lockedBlobs )
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease."  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease."  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)."  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
} else { Write-Host " There are no blobs with locked lease status." }
```  
  
## <a name="see-also"></a>참고 항목

[URL에 SQL Server 백업 모범 사례 및 문제 해결](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
