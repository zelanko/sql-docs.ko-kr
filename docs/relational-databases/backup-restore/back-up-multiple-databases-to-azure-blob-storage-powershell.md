---
title: Azure Blob Storage에 여러 데이터베이스 백업 - PowerShell | Microsoft 문서
ms.custom: ''
ms.date: 05/20/2016
ms.prod: sql
ms.prod_service: backup-restore
ms.reviewer: ''
ms.technology: backup-restore
ms.topic: conceptual
ms.assetid: f7008339-e69d-4e20-9265-d649da670460
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 67d2b66ac05562741958b6fb7e439b0685f80458
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47855659"
---
# <a name="back-up-multiple-databases-to-azure-blob-storage---powershell"></a>Azure Blob Storage에 여러 데이터베이스 백업 - PowerShell
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  이 항목에서는 PowerShell cmdlet을 사용하여 Windows Azure Blob 저장소 서비스에 대한 백업을 자동화하는 데 사용할 수 있는 예제 스크립트를 제공합니다.  
  
## <a name="overview-of-powershell-cmdlets-for-backup-and-restore"></a>백업 및 복원에 대한 PowerShell cmdlet 개요  
 **Backup-SqlDatabase** 및 **Restore-SqlDatabase** 는 백업 및 복원 작업을 수행하는 데 사용할 수 있는 두 가지 주요 cmdlet입니다. 또한 **SqlCredential** cmdlet 집합과 같이 Windows Azure Blob 저장소에 대한 백업을 자동화하는 데 필요할 수 있는 다른 cmdlet도 있습니다. 백업 및 복원 작업에서 사용되는, [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] 에서 사용할 수 있는 PowerShell cmdlet의 목록은 다음과 같습니다.  
  
 Backup-SqlDatabase  
 이 cmdlet은 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 백업을 만드는 데 사용됩니다.  
  
 Restore-SqlDatabase  
 데이터베이스를 복원하는 데 사용됩니다.  
  
 New-SqlCredential  
 이 cmdlet은 Windows Azure 저장소에 대한 SQL Server 백업에 사용할 SQL 자격 증명을 만드는 데 사용됩니다. 자격 증명과 SQL Server 백업 및 복원에서 자격 증명의 사용에 대한 자세한 내용은 [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)을 참조하세요.  
  
 Get-SqlCredential  
 이 cmdlet은 자격 증명 개체와 해당 속성을 검색하는 데 사용됩니다.  
  
 Remove-SqlCredential  
 SQL 자격 증명 개체를 삭제합니다.  
  
 Set-SqlCredential  
 이 cmdlet은 SQL 자격 증명 개체의 속성을 변경하거나 설정하는 데 사용됩니다.  
  
> [!TIP]  
>  Credential cmdlet은 Windows Azure Blob 저장소에 대한 백업 및 복원 시나리오에서 사용됩니다.  
  
### <a name="powershell-for-multi-database-multi-instance-backup-operations"></a>다중 데이터베이스, 다중 인스턴스 백업 작업에 대한 PowerShell  
 아래의 섹션들에는 여러 SQL Server 인스턴스에서 SQL 자격 증명을 만들고, 한 SQL Server 인스턴스의 모든 사용자 데이터베이스를 백업하는 등의 다양한 작업에 대한 스크립트가 포함되어 있습니다. 이러한 스크립트를 사용하여 사용자 환경의 요구 사항에 따라 백업 작업을 자동화하거나 예약할 수 있습니다. 여기에 있는 스크립트는 예로 제공되었으며 사용자 환경에 맞게 수정하거나 확장할 수 있습니다.  
  
 예제 스크립트에 대한 고려 사항은 다음과 같습니다.  
  
1.  **SQL Server PowerShell 경로 탐색:** Windows PowerShell은 cmdlet을 구현하여 PowerShell 공급자가 지원하는 개체의 계층 구조를 나타내는 경로 구조를 탐색합니다. 경로의 노드를 탐색한 후 다른 cmdlet을 사용하여 현재 개체에 대한 기본 작업을 수행할 수 있습니다.  
  
2.  **Get-ChildItem** cmdlet: **Get-ChildItem** 이 반환하는 정보는 SQL Server PowerShell 경로에서의 위치에 따라 달라집니다. 예를 들어 위치가 컴퓨터 수준에 있는 경우 이 cmdlet은 컴퓨터에 설치된 모든 SQL Server 데이터베이스 엔진 인스턴스를 반환합니다. 또 다른 예로, 위치가 데이터베이스와 같은 개체 수준에 있으면 이 cmdlet은 데이터베이스 개체의 목록을 반환합니다.  기본적으로 **Get-ChildItem** cmdlet은 시스템 개체를 반환하지 않습니다.  –Force 매개 변수를 사용하면 시스템 개체를 표시할 수 있습니다.  
  
     자세한 내용은 [Navigate SQL Server PowerShell Paths](../../relational-databases/scripting/navigate-sql-server-powershell-paths.md)을 참조하세요.  
  
3.  변수 값을 변경하여 각 코드 예제를 독립적으로 시도할 수 있지만, Windows Azure 저장소 계정과 SQL 자격 증명을 만드는 것은 사전 전제 조건이며 Windows Azure Blob 저장소 서비스에 대한 모든 백업 및 복원 작업에 필요합니다.  
  
### <a name="create-a-sql-credential-on-all-the-instances-of-sql-server"></a>모든 SQL Server 인스턴스에서 SQL 자격 증명 만들기  
 두 가지 예제 스크립트가 있으며 둘 모두 컴퓨터의 모든 SQL Server 인스턴스에서 SQL 자격 증명 "mybackupToURL"을 만듭니다. 간단한 첫 번째 예에서는 자격 증명을 만들고 예외를 트래핑하지 않습니다.  예를 들어 컴퓨터의 인스턴스 중 하나에 동일한 이름의 기존 자격 증명이 이미 있는 경우 스크립트가 실패합니다. 두 번째 예에서는 오류를 트래핑하여 스크립트가 계속 실행될 수 있도록 합니다.  
  
```  
  
import-module sqlps  
  
# create variables  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#pipe the instances to new-sqlcredentail cmdlet to create SQL credential  
$instances | new-sqlcredential -Name $credentialName  -Identity $storageAccount -Secret $secureString  
```  
  
```  
  
import-module sqlps  
  
# set the parameter values  
  
$storageAccount = "mystorageaccount"  
$storageKey = "<storageaccesskeyvalue>"  
$secureString = convertto-securestring $storageKey  -asplaintext -force  
$credentialName = "mybackuptoURL"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
# get the list of instances  
$instances = Get-childitem  
#loop through instances and create a SQL credential, output any errors  
foreach ($instance in $instances)  
{  
    Try  
{  
     new-sqlcredential -Name $credentialName -path "SQLServer:\SQL\$($instance.name)" -Identity $storageAccount -Secret $secureString -ea Stop   
}  
Catch [Exception]  
    {  
  
            write-host "instance - $($instance.name): "$_.Exception.Message  
  
    }  
  
 }  
  
```  
  
### <a name="remove-a-sql-credential-from-all-the-instances-of-sql-server"></a>모든 SQL Server 인스턴스에서 SQL 자격 증명 제거  
 이 스크립트를 사용하여 컴퓨터에 설치된 모든 SQL Server 인스턴스에서 특정 자격 증명을 제거할 수 있습니다. 자격 증명 개체가 특정 인스턴스에 없는 경우 오류 메시지가 표시되고 모든 인스턴스가 확인될 때까지 스크립트가 계속 실행됩니다.  
  
```  
  
import-module sqlps  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$credentialName = "mybackuptoURL"  
  
$instances = Get-childitem  
  
foreach ($instance in $instances)  
   {   
    try  
        {  
            $path = "SQLServer:\SQL\$($instance.name)\credentials\$credentialName"   
            Remove-sqlCredential -path $path -ea stop   
         }  
         catch [Exception]  
         {  
            write-host $_.Exception.Message  
  
        }  
  
    }  
```  
  
### <a name="full-database-backup-for-all-databases-including-system-databases"></a>시스템 데이터베이스를 비롯한 모든 데이터베이스에 대한 전체 데이터베이스 백업  
 다음 스크립트에서는 컴퓨터에 있는 모든 데이터베이스의 백업을 만듭니다. 여기에는 사용자 데이터베이스뿐만 아니라 **msdb** 시스템 데이터베이스도 포함됩니다. 이 스크립트에서는 **tempdb** 및 **model** 시스템 데이터베이스를 필터링합니다.  
  
```  
  
import-module sqlps  
# set the parameter values  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the  databases -filter out tempdb and model databases  
  
 foreach ($instance in $instances)  
 {  
   $path = "sqlserver:\sql\$($instance.name)\databases"  
   $alldatabases = get-childitem -Force -path $path |Where-object {$_.name -ne "tempdb" -and $_.name -ne "model"}   
  
   $alldatabases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On -script   
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases"></a>모든 사용자 데이터베이스에 대한 전체 데이터베이스 백업  
 다음 스크립트를 사용하여 컴퓨터의 모든 SQL Server 인스턴스에서 모든 사용자 데이터베이스를 백업할 수 있습니다.  
  
```  
  
import-module sqlps   
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackuptoURL"  
  
# cd to computer level  
  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
# loop through each instances and backup up all the user databases  
 foreach ($instance in $instances)  
 {  
    $databases = dir "sqlserver:\sql\$($instance.name)\databases"  
   $databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On   
 }  
```  
  
### <a name="full-database-backup-for-master-and-msdb-system-databases-on-all-the-instances-of-sql-server"></a>모든 SQL Server 인스턴스의 MASTER 및 MSDB(시스템 데이터베이스)에 대한 전체 데이터베이스 백업  
 다음 스크립트를 사용하여 컴퓨터에 설치된 모든 SQL Server 인스턴스에서 **master** 및 **msdb** 데이터베이스를 백업할 수 있습니다.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$credentialName = "mybackupToUrl"  
$sysDbs = "master", "msdb"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
$instances = Get-childitem   
foreach ($instance in $instances)  
 {  
      foreach ($s in $sysdbs)  
     {  
Backup-SqlDatabase -Database $s -path "sqlserver:\sql\$($instance.name)" -BackupContainer  $backupUrlContainer -SqlCredential $credentialName -Compression On   
}    
 }  
  
```  
  
### <a name="full-database-backup-for-all-user-databases-on-an-instance-of-sql-server"></a>한 SQL Server 인스턴스의 모든 사용자 데이터베이스에 대한 전체 데이터베이스 백업  
 다음 스크립트는 SQL Server의 명명된 인스턴스에서 사용할 수 있는 사용자 데이터베이스만 백업하는 데 사용됩니다. $srvPath 매개 변수 값을 변경하여 같은 스크립트를 컴퓨터의 기본 인스턴스에 사용할 수 있습니다.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME"  # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#cd to computer level  
cd SQLServer:\SQL\$env:COMPUTERNAME  
  
#retrieves the database objects for a specific instance  
$databases = dir $srvPath\databases  
  
#backup all the user databases  
$databases | Backup-SqlDatabase -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
```  
  
### <a name="full-database-backup-for-only-system-databases-master-and-msdb-on-an-instance-of-sql-server"></a>한 SQL Server 인스턴스의 시스템 데이터베이스(MASTER 및 MSDB)에 대한 전체 데이터베이스 백업  
 전체 스크립트를 사용하여 SQL Server의 명명된 인스턴스에서 **master** 및 **msdb** 데이터베이스를 백업할 수 있습니다. $srvPath 매개 변수 값을 변경하여 같은 스크립트를 컴퓨터의 기본 인스턴스에 사용할 수 있습니다.  
  
```  
  
import-module sqlps  
  
$storageAccount = "mystorageaccount"  
$blobContainer = "privatecontainertest"  
$backupUrlContainer = "https://$storageAccount.blob.core.windows.net/$blobContainer/"  
$srvPath = "SQLServer:\SQL\$env:COMPUTERNAME\INSTANCENAME" # for default instance, the $srvpath variable is "SQLServer:\SQL\$env:COMPUTERNAME\DEFAULT"  
$credentialName = "mybackupToUrl"  
  
#navigate to instance level  
cd $srvPath  
  
$sysDbs = "master", "msdb"  
foreach ($s in $sysDbs)   
{  
Backup-SqlDatabase -Database $s -BackupContainer $backupUrlContainer -SqlCredential $credentialName -Compression On  
}  
  
```  
  
## <a name="see-also"></a>참고 항목  
 [Microsoft Azure Blob 저장소 서비스로 SQL Server 백업 및 복원](../../relational-databases/backup-restore/sql-server-backup-and-restore-with-microsoft-azure-blob-storage-service.md)   
 [URL에 대한 SQL Server 백업 - 최상의 방법 및 문제 해결](../../relational-databases/backup-restore/sql-server-backup-to-url-best-practices-and-troubleshooting.md)  
  
  
