---
title: "PowerShell - TDE 보호기 제거 - Azure SQL | Microsoft Docs"
description: "BYOK(Bring Your Own Key) 기반 TDE를 사용하여 Azure SQL Database 또는 데이터 웨어하우스에 대해 잠재적으로 손상된 TDE 보호기에 대응하는 방법 가이드입니다."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: craigg
ms.prod: 
ms.reviewer: 
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: 
ms.component: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.openlocfilehash: 30b08c760eff3bdeb6d264d1c9d79c375f0a09ec
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 12/21/2017
---
# <a name="remove-a-transparent-data-encryption-tde-protector-using-powershell"></a>PowerShell을 사용하여 TDE(투명한 데이터 암호화) 보호기 제거
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

## <a name="prerequisites"></a>사전 요구 사항
- Azure 구독이 있고 해당 구독의 관리자여야 합니다.
- Azure PowerShell 버전 4.2.0 이상이 설치되어 실행 중이어야 합니다. 
- 이 방법 가이드는 Azure Key Vault의 키를 Azure SQL Database 또는 데이터 웨어하우스에 대한 TDE 보호기로 이미 사용 중이라고 가정합니다. 자세한 내용은 [BYOK를 사용하는 투명한 데이터 암호화 지원](transparent-data-encryption-byok-azure-sql.md)을 참조하세요.

## <a name="overview"></a>개요
이 방법 가이드는 BYOK(Bring Your Own Key) 기반 TDE를 사용하여 Azure SQL Database 또는 데이터 웨어하우스에 대해 잠재적으로 손상된 TDE 보호기에 대응하는 방법을 설명합니다. TDE에 대한 BYOK 지원에 대한 자세한 내용은 [개요 페이지](transparent-data-encryption-byok-azure-sql.md)를 참조하세요. 

극단적인 상황이나 테스트 환경에서만 다음 절차를 수행해야 합니다. Azure Key Vault에서 실제로 사용된 TDE 보호기를 삭제하면 **데이터 손실**이 발생할 수 있으므로 방법 가이드를 주의 깊게 검토합니다. 

키가 손상되어 서비스 또는 사용자가 키에 대한 무단 액세스를 하는 것으로 의심되는 경우 키를 삭제하는 것이 가장 좋습니다.

Key Vault에서 TDE 보호기가 삭제된 후에는 **서버에서 암호화된 데이터베이스에 대한 모든 연결이 차단되고 해당 데이터베이스는 오프라인으로 전환되며 24시간 이내 삭제됩니다.** 손상된 키를 사용하여 암호화된 오래된 백업은 더 이상 액세스할 수 없습니다.

이 방법 가이드는 인시던트 대응 후 원하는 결과에 따라 두 가지 접근 방법을 통해 진행됩니다.
- Azure SQL Database / 데이터 웨어하우스에 **액세스 가능하도록** 유지하려면
- Azure SQL Database / 데이터 웨어하우스에 **액세스 불가능하도록**하려면

## <a name="to-keep-the-encrypted-resources-accessible"></a>암호화된 리소스를 액세스 가능하게 유지하려면
1. [Key Vault에서 새 키](https://docs.microsoft.com/powershell/module/azurerm.keyvault/add-azurekeyvaultkey?view=azurermps-4.1.0)를 만듭니다. 액세스 제어가 자격 증명 모음 수준에서 프로비전되므로 잠재적으로 손상된 TDE 보호기와는 별도의 키 자격 증명 모음에 새 키가 만들어지는지 확인합니다. 
2. [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) 및 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet을 사용하여 서버에 새 키를 추가하고 서버의 새 TDE 보호기로 업데이트합니다.

   ```powershell
   # Add the key from Key Vault to the server  
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>
   
   # Set the key as the TDE protector for all resources under the server
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault -KeyId <KeyVaultKeyId> 
   ```

3. [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) cmdlet을 사용하여 서버 및 모든 복제본이 새 TDE 보호기로 업데이트되었는지 확인합니다. 

   >[!NOTE]
   > 새로운 TDE 보호기가 서버 아래의 모든 데이터베이스와 보조 데이터베이스로 전파되는 데 몇 분이 걸릴 수 있습니다.
   >

   ```powershell
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```

4. Key Vault에서 [새 키의 백업](/powershell/module/azurerm.keyvault/backup-azurekeyvaultkey)을 가져옵니다.

   ```powershell
   <# -OutputFile parameter is optional; 
   if removed, a file name is automatically generated. #>
   Backup-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -OutputFile <DesiredBackupFilePath>
   ```
 
5. [Remove-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/remove-azurekeyvaultkey) cmdlet을 사용하여 Key Vault에서 손상된 키를 삭제합니다. 

   ```powershell
   Remove-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName>
   ```
 
6. [Restore-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/restore-azurekeyvaultkey) cmdlet을 사용하여 향후 Key Vault에 키를 복원하려면
   ```powershell
   Restore-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -InputFile <BackupFilePath>
   ```
 
## <a name="to-make-the-encrypted-resources-inaccessible"></a>암호화된 리소스를 액세스할 수 없도록 하려면
1. 잠재적으로 손상된 키로 암호화된 데이터베이스를 삭제합니다.
데이터베이스 및 로그 파일은 자동으로 백업되므로 모든 지점에서 데이터베이스의 특정 시점 복원을 수행할 수 있습니다(키를 제공하는 한). 최신 트랜잭션의 최대 10분 동안 잠재적인 데이터 손실을 방지하기 위해 활성 TDE 보호기를 삭제하기 전에 데이터베이스를 삭제해야 합니다. 
2. Key Vault에서 TDE 보호기의 키 자료를 백업합니다.
3. Key Vault에서 잠재적으로 손상된 키 제거

## <a name="next-steps"></a>다음 단계

- 보안 요구 사항을 준수하는 서버의 TDE 보호기를 회전하는 방법 알아보기: [PowerShell을 사용하여 투명한 데이터 암호화 보호기 회전](transparent-data-encryption-byok-azure-sql-key-rotation.md)

- TDE에 대한 Bring Your Own Key 지원 시작: [PowerShell을 사용하고 Key Vault에서 사용자 고유 키를 사용하여 TDE 설정](transparent-data-encryption-byok-azure-sql-configure.md)
