---
title: "PowerShell: TDE using your own Azure Key Vault 키를 사용하여 TDE 설정 | Microsoft Docs"
description: "PowerShell을 사용하여 미사용 암호화를 위해 TDE(투명한 데이터 암호화)를 사용하도록 Azure SQL Database 및 데이터 웨어하우스를 구성하는 방법에 대해 알아봅니다."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: cguyer
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: Inactive
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: cf8f46ab01c08e68fa22f65a4f86f4ff16f16ba3
ms.contentlocale: ko-kr
ms.lasthandoff: 09/05/2017

---


# <a name="powershell-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell: Azure Key Vault에서 사용자 고유 키를 사용하여 투명한 데이터 암호화 사용

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

이 방법 가이드는 SQL Database 또는 데이터 웨어하우스에서 TDE(투명한 데이터 암호화)를 위해 Azure Key Vault의 키를 사용하는 방법을 안내합니다. BYOK(Bring Your Own Key) 기반 TDE 지원에 대해 자세히 알아보려면 [Azure SQL에 대한 Bring Your Own Key 기반 TDE](transparent-data-encryption-byok-azure-sql.md)를 방문하세요. 

## <a name="prerequisites"></a>필수 구성 요소

- Azure 구독이 있고 해당 구독의 관리자여야 합니다.
- [권장되지만 선택 사항임] TDE 보호기 키 자료의 로컬 복사본을 만들기 위해 HSM(하드웨어 보안 모듈) 또는 로컬 키 저장소를 포함합니다.
- Azure PowerShell 버전 4.2.0 이상이 설치되어 실행 중이어야 합니다. 
- TDE에 사용할 Azure Key Vault 및 키를 만듭니다.
   - [Key Vault에서 PowerShell 지침](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [HSM(하드웨어 보안 모듈) 및 Key Vault 사용에 대한 지침](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
- 키는 TDE에 사용할 다음과 같은 특성을 포함해야 합니다.
   - 만료 날짜 없음
   - 비활성화되지 않음
   - *가져오기*, *키 래핑*, *키 래핑 해제* 작업을 수행할 수 있습니다.

## <a name="step-1-assign-an-aad-identity-to-your-server"></a>1단계. 서버에 AAD ID 할당 

기존 서버가 있는 경우 다음을 사용하여 AAD ID를 서버에 추가합니다.

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

서버를 만드는 경우 -Identity 태그와 함께 [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) cmdlet을 사용하여 서버 생성 중에 AAD ID를 추가합니다.

   ```powershell
   $server = New-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -Location <RegionName> `
   -ServerName <LogicalServerName> `
   -ServerVersion "12.0" `
   -SqlAdministratorCredentials <PSCredential> `
   -AssignIdentity 
   ```

## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>2단계. 서버에 Key Vault 권한 부여

[Set-AzureRmKeyValutAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet을 사용하여 TDE에 대해 키를 사용하기 전에 키 자격 증명 모음에 서버 액세스 권한을 부여합니다.

   ```powershell
   Set-AzureRmKeyVaultAccessPolicy  `
   -VaultName <KeyVaultName> `
   -ObjectId $server.Identity.PrincipalId `
   -PermissionsToKeys get, wrapKey, unwrapKey
   ```

## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>3단계. Key Vault 키를 서버에 추가하고 TDE 보호기 설정

- [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) cmdlet을 사용하여 Key Vault에서 서버로 키를 추가합니다.
- [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet을 사용하여 모든 서버 리소스에 대한 TDE 보호기로 키를 설정합니다.
- [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) cmdlet을 사용하여 TDE 보호기가 원하는 대로 구성되었는지 확인합니다.

> [!Note]
> 키 자격 증명 모음 이름 및 키 이름의 조합된 길이는 94자를 초과할 수 없습니다.
> 

>[!Tip]
>Key Vault의 KeyId 예: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>

   ```powershell
   <# Add the key from Key Vault to the server #>
   Add-AzureRmSqlServerKeyVaultKey `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -KeyId <KeyVaultKeyId>

   <# Set the key as the TDE protector for all resources under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> 

   <# To confirm that the TDE protector was configured as intended: #>
   Get-AzureRmSqlServerTransparentDataEncryptionProtector `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> 
   ```

## <a name="step-4-turn-on-tde"></a>4단계. TDE 설정 

[Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) cmdlet을 사용하여 TDE를 설정합니다.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `
   -State "Enabled"
   ```

이제 데이터베이스 또는 데이터 웨어하우스에는 Key Vault의 암호화 키로 TDE가 설정됩니다.

## <a name="step-5-check-the-encryption-state-and-encryption-activity-of-the-database-or-data-warehouse"></a>5단계. 데이터베이스 또는 데이터 웨어하우스의 암호화 상태 및 암호화 작업 확인

[Get-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption)을 사용하여 암호화 상태를 가져오고 [Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity)를 사용하여 데이터베이스 또는 데이터 웨어하우스에 대한 암호화 진행 상태를 확인합니다.

   ```powershell
   # Get the encryption state
   Get-AzureRMSqlDatabaseTransparentDataEncryption `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName> `

   <# Check the encryption progress for a database or data warehouse #>
   Get-AzureRMSqlDatabaseTransparentDataEncryptionActivity `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -DatabaseName <DatabaseName>  
   ```

## <a name="other-useful-powershell-cmdlets"></a>다른 유용한 PowerShell cmdlet

- [Set-AzureRMSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) cmdlet을 사용하여 TDE를 해제합니다.

   ```powershell
   Set-AzureRMSqlDatabaseTransparentDataEncryption `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -DatabaseName <DatabaseName> `
   -State "Disabled”
   ```
 
- [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) cmdlet을 사용하여 서버에 추가된 Key Vault의 키 목록을 반환합니다.

   ```powershell
   <# KeyId is an optional parameter, to return a specific key version #>
   Get-AzureRmSqlServerKeyVaultKey `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>
   ```
 
- [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey)를 사용하여 서버에서 Key Vault 키를 제거합니다.

   ```powershell
   <# The key set as the TDE Protector cannot be removed. #>
   Remove-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroupName <SQLDatabaseResourceGroupName>   
   ```
 
## <a name="troubleshooting"></a>문제 해결

문제가 발생하는 경우 다음 사항을 확인합니다.
- 키 자격 증명 모음을 찾을 수 없는 경우 [Get-AzureRmSubscription](/powershell/module/azurerm.profile/get-azurermsubscription) cmdlet을 사용하여 올바른 구독이 있는지 확인합니다.

   ```powershell
   Get-AzureRmSubscription `
   -SubscriptionId <SubscriptionId>
   ```

- 서버에 새 키를 추가할 수 없거나 새 키를 TDE 보호기로 업데이트할 수 없는 경우 다음 사항을 확인합니다.
   - 키의 만료 날짜가 없어야 합니다.
   - 키에 *가져오기*, *키 래핑* 및 *키 래핑 해제* 작업이 사용하도록 설정되어야 합니다.

## <a name="next-steps"></a>다음 단계

- 보안 요구 사항을 준수하는 서버의 TDE 보호기를 회전하는 방법 알아보기: [PowerShell을 사용하여 투명한 데이터 암호화 보호기 회전](transparent-data-encryption-byok-azure-sql-key-rotation.md)
- 보안 위험이 발생할 경우 잠재적으로 손상된 TDE 보호기를 제거하는 방법 알아보기: [잠재적으로 손상된 키 제거](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) 



