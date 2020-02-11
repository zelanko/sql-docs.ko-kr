---
title: 활성 임대가 있는 백업 Blob 파일 삭제 | Microsoft 문서
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: 13a8f879-274f-4934-a722-b4677fc9a782
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 663bab775aff9a04a4a9d93f2bcbd0e193b18f37
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: ko-KR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72783061"
---
# <a name="deleting-backup-blob-files-with-active-leases"></a>활성 임대가 있는 백업 Blob 파일 삭제
  Azure storage에 백업 하거나 복원 하는 경우 SQL Server는 blob에 대 한 단독 액세스를 잠그기 위해 무한 임대를 획득 합니다. 백업 또는 복원 프로세스가 성공적으로 완료되면 임대가 해제됩니다. 백업 또는 복원에 실패하면 백업 프로세스에서는 잘못된 모든 blob을 정리하려고 합니다. 하지만 오랫동안 지속된 네트워크 연결 오류로 인해 백업이 실패한 경우에는 백업 프로세스에서 blob에 액세스할 수 없으므로 blob이 분리됩니다. 즉, 임대가 해제될 때까지 blob을 쓰거나 삭제할 수 없습니다. 이 항목에서는 임대를 해제하고 blob을 삭제하는 방법에 대해 설명합니다.  
  
 임대 유형에 대한 자세한 내용은 이 [문서](https://go.microsoft.com/fwlink/?LinkId=275664)를 참조하십시오.  
  
 백업 작업이 실패하는 경우 잘못된 백업 파일이 만들어질 수 있습니다.  백업 blob 파일에 활성 임대도 있어 해당 blob을 삭제하거나 덮어쓸 수 없습니다.  이러한 blob을 삭제하거나 덮어쓰려면 먼저 임대를 해제해야 합니다. 백업 실패 시 임대를 정리하고 blob을 삭제하는 것이 좋습니다. 스토리지 관리 작업의 일부로 주기적으로 정리를 선택할 수도 있습니다.  
  
 복원 실패 시 후속 복원이 차단되지 않으므로 활성 임대는 문제가 되지 않을 수 있습니다. blob을 덮어쓰거나 삭제해야 할 때만 임대 해제가 필요합니다.  
  
## <a name="managing-orphaned-blobs"></a>분리된 Blob 관리  
 다음 단계에서는 백업 또는 복원 작업 실패 후 정리하는 방법을 설명합니다. 모든 단계는 PowerShell 스크립트를 사용하여 수행할 수 있습니다. 코드 예제는 다음 섹션에서 제공됩니다.  
  
1.  **임대가 있는 Blob 식별:** 백업 프로세스를 실행 하는 스크립트나 프로세스가 있는 경우 스크립트나 프로세스 내에서 오류를 캡처하여 blob 정리에 사용할 수 있습니다.   또한 LeaseStats 및 LeastState 속성을 사용하여 임대가 있는 blob을 식별할 수 있습니다. blob 식별 후에는 blob 삭제 전에 목록을 검토하고 백업 파일이 유효한지 확인하는 것이 좋습니다.  
  
2.  **임대 중단:** 권한 있는 요청은 임대 ID를 제공 하지 않고 임대를 중단할 수 있습니다. 자세한 내용은 [여기](https://go.microsoft.com/fwlink/?LinkID=275664) 를 참조하십시오.  
  
    > [!TIP]  
    >  SQL Server는 복원 작업 중 임대 ID를 실행하여 단독 액세스를 설정합니다. 복원 임대 ID는 BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2입니다.  
  
3.  **Blob 삭제:** 활성 임대가 있는 blob을 삭제 하려면 먼저 임대를 해제 해야 합니다.  
  
###  <a name="Code_Example"></a>PowerShell 스크립트 예제  
 ** \* 중요 \* \* ** PowerShell 2.0을 실행 하는 경우 Microsoft Windowsazure.servicebus 어셈블리를 로드 하는 데 문제가 있을 수 있습니다. 문제 해결을 위해 Powershell 3.0으로 업그레이드하는 것이 좋습니다. PowerShell 2.0에 대한 다음 해결 방법을 사용할 수도 있습니다.  
  
-   다음과 같이 powershell.exe.config 파일을 만들거나 수정하여 런타임에 .NET 2.0 및 .NET 4.0 어셈블리를 로드합니다.  
  
    ```xml
    <?xml version="1.0"?>
    <configuration>
        <startup useLegacyV2RuntimeActivationPolicy="true">
            <supportedRuntime version="v4.0.30319"/>
            <supportedRuntime version="v2.0.50727"/>
        </startup>
    </configuration>
    ```  
  
 다음 예에서는 활성 임대가 있는 blob을 식별한 다음 해제합니다. 임대 ID를 필터링하는 방법도 보여 줍니다.  
  
 이 스크립트 실행 팁  
  
> [!WARNING]  
>  Azure Blob storage 서비스에 대 한 백업이이 스크립트와 동시에 실행 되는 경우이 스크립트는 백업에서 동시에 얻으려고 시도 하는 임대를 중단 하므로 백업이 실패할 수 있습니다. 이 스크립트는 유지 관리 기간이나 백업이 실행되지 않을 때 실행하는 것이 좋습니다.  
  
1.  이 스크립트를 실행 하면 저장소 계정, 저장소 키, 컨테이너 및 Azure storage 어셈블리 경로와 이름 매개 변수 값을 제공 하 라는 메시지가 표시 됩니다. 스토리지 어셈블리의 경로는 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]인스턴스의 설치 디렉터리입니다. 스토리지 어셈블리의 파일 이름은 Microsoft.WindowsAzure.Storage.dll입니다. 다음은 프롬프트 및 입력 값의 예입니다.  
  
    ```  
    cmdlet  at command pipeline position 1  
    Supply values for the following parameters:  
    storageAccount: mycloudstorageaccount  
    storageKey: 0BopKY7eEha3gBnistYk+904nf  
    blobContainer: mycontainer   
    storageAssemblyPath: C:\Program Files\Microsoft SQL Server\MSSQL12.MSSQLSERVER\MSSQL\Binn\Microsoft.WindowsAzure.Storage.dll  
    ```  
  
2.  잠긴 임대를 가진 blob이 없는 경우 다음과 같은 메시지가 나타납니다.  
  
     **잠긴 임대 상태의 blob이 없습니다.**  
  
     잠긴 임대를 가진 blob이 있는 경우 다음과 같은 메시지가 나타납니다.  
  
     **임대 중단**  
  
     **Blob>의 \<URL에 대 한 임대가 복원 임대입니다. 아직 활성 상태인 복원 임대가 있는 blob이 있는 경우에만이 메시지가 표시 됩니다.**  
  
     **Blob>의 \<url에 대 한 임대가> Bob의 url에 대 \<한 복원 임대 중단 임대가 아닙니다.**  
  
```powershell
param(  
       [Parameter(Mandatory=$true)]  
       [string]$storageAccount,  
       [Parameter(Mandatory=$true)]  
       [string]$storageKey,  
       [Parameter(Mandatory=$true)]  
       [string]$blobContainer,  
       [Parameter(Mandatory=$true)]  
       [string]$storageAssemblyPath  
)  
  
# Well known Restore Lease ID  
$restoreLeaseId = "BAC2BAC2BAC2BAC2BAC2BAC2BAC2BAC2"  
  
# Load the storage assembly without locking the file for the duration of the PowerShell session  
$bytes = [System.IO.File]::ReadAllBytes($storageAssemblyPath)  
[System.Reflection.Assembly]::Load($bytes)  
  
$cred = New-Object 'Microsoft.WindowsAzure.Storage.Auth.StorageCredentials' $storageAccount, $storageKey  
$client = New-Object 'Microsoft.WindowsAzure.Storage.Blob.CloudBlobClient' "https://$storageAccount.blob.core.windows.net", $cred  
$container = $client.GetContainerReference($blobContainer)  
  
#list all the blobs  
$allBlobs = $container.ListBlobs()
  
$lockedBlobs = @()  
# filter blobs that are have Lease Status as "locked"  
foreach($blob in $allBlobs)  
{  
    $blobProperties = $blob.Properties
    if($blobProperties.LeaseStatus -eq "Locked")  
    {  
        $lockedBlobs += $blob  
    }  
}  
  
if ($lockedBlobs.Count -eq 0)  
{
    Write-Host " There are no blobs with locked lease status"  
}

if($lockedBlobs.Count -gt 0)  
{  
    Write-Host "Breaking leases"  
    foreach($blob in $lockedBlobs )
    {  
        try  
        {  
            $blob.AcquireLease($null, $restoreLeaseId, $null, $null, $null)  
            Write-Host "The lease on $($blob.Uri) is a restore lease"  
        }  
        catch [Microsoft.WindowsAzure.Storage.StorageException]  
        {  
            if($_.Exception.RequestInformation.HttpStatusCode -eq 409)  
            {  
                Write-Host "The lease on $($blob.Uri) is not a restore lease"  
            }  
        }  
  
        Write-Host "Breaking lease on $($blob.Uri)"  
        $blob.BreakLease($(New-TimeSpan), $null, $null, $null) | Out-Null  
    }  
}
```  
  
## <a name="see-also"></a>참고 항목  
 [URL에 SQL Server 백업 모범 사례 및 문제 해결](sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
