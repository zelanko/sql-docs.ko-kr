---
title: '여러 데이터베이스 백업: Azure Blob Storage'
description: 이 문서에서는 PowerShell cmdlet을 사용하여 Azure Blob Storage 서비스로의 SQL Server 백업을 자동화하는 데 사용할 수 있는 예제 스크립트를 제공합니다.
titleSuffix: PowerShell
ms.custom: seo-lt-2019
ms.date: 12/17/2019
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: e79840f828a7891ac3e01cd52721eb5755a97c7b
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91809249"
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>Azure Blob Storage에 여러 데이터베이스 백업 - PowerShell

 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

이 항목에서는 PowerShell cmdlet을 사용하여 Azure Blob Storage 서비스로의 백업을 자동화하는 데 사용할 수 있는 예제 스크립트를 제공합니다.  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>백업 및 복원에 대한 PowerShell cmdlet 개요

**Backup-SqlDatabase** 및 **Restore-SqlDatabase** 는 백업 및 복원 작업을 수행하는 데 사용할 수 있는 두 가지 주요 cmdlet입니다.

또한 **SqlCredential** cmdlet 세트와 같이 Windows Azure Blob Storage에 대한 백업을 자동화하는 데 필요할 수 있는 다른 cmdlet도 있습니다.

사용 가능한 모든 cmdlet 목록은 [SqlServer cmdlet](/powershell/module/sqlserver)을 참조하세요.
  
> [!TIP]  
> **SqlCredential** cmdlet은 Azure Blob Storage로의 백업 및 복원 시나리오에서 사용됩니다. 자격 증명과 해당 사용에 관한 자세한 내용은 [Microsoft Azure Blob Storage 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>다중 데이터베이스, 다중 인스턴스 백업 작업에 대한 PowerShell

아래의 섹션에는 여러 SQL Server 인스턴스에서 SQL 자격 증명을 만들고, 한 SQL Server 인스턴스의 모든 사용자 데이터베이스를 백업하는 등의 다양한 작업에 대한 스크립트가 포함되어 있습니다. 이러한 스크립트를 사용하여 사용자 환경의 요구 사항에 따라 백업 작업을 자동화하거나 예약할 수 있습니다. 여기에 있는 스크립트는 예로 제공되었으며 사용자 환경에 맞게 수정하거나 확장할 수 있습니다.  
  
예제 스크립트에 대한 고려 사항은 다음과 같습니다.  
  
- SQL Server PowerShell은 cmdlet을 구현하여 PowerShell 공급자가 지원하는 개체의 계층 구조를 나타내는 경로 구조를 탐색합니다. 경로의 노드를 탐색한 후 다른 cmdlet을 사용하여 현재 개체에 대한 기본 작업을 수행할 수 있습니다.

  자세한 내용은 [Navigate SQL Server PowerShell Paths](../../powershell/navigate-sql-server-powershell-paths.md)을 참조하세요.

- **Get-ChildItem** cmdlet: **Get-ChildItem**이 반환하는 정보는 SQL Server PowerShell 경로에서의 위치에 따라 달라집니다. 예를 들어 위치가 컴퓨터 수준에 있는 경우 이 cmdlet은 컴퓨터에 설치된 모든 SQL Server 데이터베이스 엔진 인스턴스를 반환합니다. 또는 위치가 데이터베이스와 같은 개체 수준에 있으면 데이터베이스 개체의 목록을 반환합니다. 기본적으로 **Get-ChildItem** cmdlet은 시스템 개체를 반환하지 않습니다. `–Force` 매개 변수를 사용하여 시스템 개체를 확인합니다.

- Azure Storage 계정 및 SQL 자격 증명은 필수 구성 요소이며 Azure Blob Storage 서비스에 대한 모든 백업 및 복원 작업에 필요합니다.
  
### <a name="create-a-sql-credential-on-all-instances-of-sql-server"></a>모든 SQL Server 인스턴스에서 SQL 자격 증명 만들기

다음 스크립트를 사용하여 컴퓨터의 모든 SQL Server 인스턴스에 대해 일반 SQL 자격 증명을 만들 수 있습니다. 컴퓨터의 인스턴스 중 하나에 동일한 이름의 기존 자격 증명이 이미 있는 경우 스크립트는 오류를 표시하고 계속됩니다.  
  
```powershell
# load the sqlps module
import-module sqlps  
  
# set parameters
$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$storageKey = "<myStorageAccessKey>"  
$secureString = ConvertTo-SecureString $storageKey -AsPlainText -Force  
$credentialName = "myCredential-$(Get-Random)"

Write-Host "Generate credential: " $credentialName
  
#cd to sql server and get instances  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and create a SQL credential, output any errors
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials"
        New-SqlCredential -Name $credentialName -Identity $storageAccount -Secret $secureString -Path $path -ea Stop | Out-Null
        Write-Host "...generated credential $($path)\$($credentialName)."  }
    catch { Write-Host $_.Exception.Message } }
```

> [!NOTE]
> `-ea Stop | Out-Null` 문은 사용자 정의 예외 출력에 사용됩니다. 기본 PowerShell 오류 메시지를 선호하는 경우 이 문을 제거해도 됩니다. 

### <a name="remove-a-sql-credential-from-all-instances-of-sql-server"></a>모든 SQL Server 인스턴스에서 SQL 자격 증명 제거

다음 스크립트를 사용하여 컴퓨터에 설치된 모든 SQL Server 인스턴스에서 특정 자격 증명을 제거할 수 있습니다. 자격 증명이 특정 인스턴스에 없는 경우 오류 메시지가 표시되고 모든 인스턴스가 확인될 때까지 스크립트가 계속 실행됩니다.  
  
```powershell
import-module sqlps

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$credentialName = "<myCredential>"

Write-Host "Delete credential: " $credentialName

cd $sqlPath
$instances = Get-ChildItem

#loop through instances and delete a SQL credential
foreach ($instance in $instances)  {
    try {
        $path = "$($sqlPath)\$($instance.DisplayName)\credentials\$($credentialName)"
        Remove-SqlCredential -Path $path -ea Stop | Out-Null
        Write-Host "...deleted credential $($path)."  }
    catch { Write-Host $_.Exception.Message } }
```  
  
### <a name="full-backup-for-all-databases"></a>모든 데이터베이스에 대한 전체 백업

다음 스크립트에서는 컴퓨터에 있는 모든 데이터베이스의 백업을 만듭니다. 여기에는 사용자 데이터베이스뿐만 아니라 **msdb** 시스템 데이터베이스도 포함됩니다. 이 스크립트에서는 **tempdb** 및 **model** 시스템 데이터베이스를 필터링합니다.  
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $backupUrlContainer
  
cd $sqlPath
$instances = Get-ChildItem

#loop through instances and backup all databases (excluding tempdb and model)
foreach ($instance in $instances)  {
    $path = "$($sqlPath)\$($instance.DisplayName)\databases"
    $databases = Get-ChildItem -Force -Path $path | Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}

    foreach ($database in $databases) {
        try {
            $databasePath = "$($path)\$($database.Name)"
            Write-Host "...starting backup: " $databasePath
            Backup-SqlDatabase -Database $database.Name -Path $path -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
            Write-Host "...backup complete."  }
        catch { Write-Host $_.Exception.Message } } }
```  
  
### <a name="full-backup-for-system-databases-only-on-a-specific-instance-of-sql-server"></a>특정 SQL Server 인스턴스에서만 시스템 데이터베이스의 전체 백업

전체 스크립트를 사용하여 SQL Server의 명명된 인스턴스에서 **master** 및 **msdb** 데이터베이스를 백업할 수 있습니다. 인스턴스 매개 변수 값을 변경하여 모든 인스턴스에 대해 동일한 스크립트를 사용할 수 있습니다. SQL Server의 기본 인스턴스 이름은 `DEFAULT`입니다.
  
```powershell
import-module sqlps  

$sqlPath = "sqlserver:\sql\$($env:COMPUTERNAME)"
$instanceName = "DEFAULT"
$storageAccount = "<myStorageAccount>"  
$blobContainer = "<myBlobContainer>"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "<myCredential>"

Write-Host "Backup database: " $instanceName " to " $backupUrlContainer
  
cd "$($sqlPath)\$($instanceName)"

#loop through instance and backup specific databases
$databases = "master", "msdb"  
foreach ($database in $databases) {
    try {
        Write-Host "...starting backup: " $database
        Backup-SqlDatabase -Database $database -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On
        Write-Host "...backup complete." }
    catch { Write-Host $_.Exception.Message } }
```  
  
## <a name="see-also"></a>참고 항목

[Azure Blob Storage Service로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)

[URL에 SQL Server 백업 모범 사례 및 문제 해결](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)