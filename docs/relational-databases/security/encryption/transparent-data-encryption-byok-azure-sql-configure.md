---
title: 'PowerShell 및 CLI: Azure Key Vault 키를 사용하여 SQL TDE 설정 | Microsoft Docs'
description: PowerShell 또는 CLI를 사용하여 미사용 암호화를 위해 TDE(투명한 데이터 암호화)를 사용하도록 Azure SQL Database 및 데이터 웨어하우스를 구성하는 방법에 대해 알아봅니다.
keywords: ''
documentationcenter: ''
author: aliceku
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.workload: On Demand
ms.tgt_pltfrm: ''
ms.devlang: azurecli, powershell
ms.topic: article
ms.date: 04/24/2018
ms.author: aliceku
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: b86f427c1efe7ef36eef3be7944bd1ecd3ec8ed1
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 04/26/2018
---
# <a name="powershell-and-cli-enable-transparent-data-encryption-using-your-own-key-from-azure-key-vault"></a>PowerShell 및 CLI: Azure Key Vault에서 사용자 고유 키를 사용하여 투명한 데이터 암호화 사용

[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

이 방법 가이드는 SQL Database 또는 데이터 웨어하우스에서 TDE(투명한 데이터 암호화)를 위해 Azure Key Vault의 키를 사용하는 방법을 안내합니다. BYOK(Bring Your Own Key) 기반 TDE 지원에 대해 자세히 알아보려면 [Azure SQL에 대한 Bring Your Own Key 기반 TDE](transparent-data-encryption-byok-azure-sql.md)를 방문하세요. 

## <a name="prerequisites-for-powershell"></a>PowerShell에 대한 필수 구성 요소

- Azure 구독이 있고 해당 구독의 관리자여야 합니다.
- [권장되지만 선택 사항임] TDE 보호기 키 자료의 로컬 복사본을 만들기 위해 HSM(하드웨어 보안 모듈) 또는 로컬 키 저장소를 포함합니다.
- Azure PowerShell 버전 4.2.0 이상이 설치되어 실행 중이어야 합니다. 
- TDE에 사용할 Azure Key Vault 및 키를 만듭니다.
   - [Key Vault에서 PowerShell 지침](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)
   - [HSM(하드웨어 보안 모듈) 및 Key Vault 사용에 대한 지침](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - 키 자격 증명 모음은 TDE에 사용할 다음과 같은 속성을 포함해야 합니다.
   - [일시 삭제](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-soft-delete)
   - [PowerShell을 사용한 키 자격 증명 모음 일시 삭제를 사용하는 방법](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-powershell) 
- 키는 TDE에 사용할 다음과 같은 특성을 포함해야 합니다.
   - 만료 날짜 없음
   - 비활성화되지 않음
   - *가져오기*, *키 래핑*, *키 래핑 해제* 작업을 수행할 수 있습니다.

## <a name="step-1-assign-an-azure-ad-identity-to-your-server"></a>1단계. 서버에 Azure AD ID 할당 

기존 서버가 있는 경우 다음을 사용하여 Azure AD ID를 서버에 추가합니다.

   ```powershell
   $server = Set-AzureRmSqlServer `
   -ResourceGroupName <SQLDatabaseResourceGroupName> `
   -ServerName <LogicalServerName> `
   -AssignIdentity
   ```

서버를 만드는 경우 -Identity 태그와 함께 [New-AzureRmSqlServer](/powershell/module/azurerm.sql/new-azurermsqlserver) cmdlet을 사용하여 서버 생성 중에 Azure AD ID를 추가합니다.

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

[Set-AzureRmKeyVaultAccessPolicy](/powershell/module/azurerm.keyvault/set-azurermkeyvaultaccesspolicy) cmdlet을 사용하여 TDE에 대해 키를 사용하기 전에 키 자격 증명 모음에 서버 액세스 권한을 부여합니다.

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
>Key Vault에서 예제 KeyId: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
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

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>5단계. 암호화 상태 및 암호화 작업 확인

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

## <a name="prerequisites-for-cli"></a>CLI에 대한 필수 구성 요소

- Azure 구독이 있고 해당 구독의 관리자여야 합니다.
- [권장되지만 선택 사항임] TDE 보호기 키 자료의 로컬 복사본을 만들기 위해 HSM(하드웨어 보안 모듈) 또는 로컬 키 저장소를 포함합니다.
- 명령줄 인터페이스 버전 2.0 이상입니다. 최신 버전을 설치하고 Azure 구독에 연결하려면 [Azure 플랫폼 간 명령줄 인터페이스 2.0 설치 및 구성](https://docs.microsoft.com/en-us/cli/azure/install-azure-cli?view=azure-cli-latest)을 참조하세요. 
- TDE에 사용할 Azure Key Vault 및 키를 만듭니다.
   - [CLI 2.0을 사용하여 Key Vault 관리](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-manage-with-cli2)
   - [HSM(하드웨어 보안 모듈) 및 Key Vault 사용에 대한 지침](https://docs.microsoft.com/azure/key-vault/key-vault-get-started#a-idhsmaif-you-want-to-use-a-hardware-security-module-hsm)
 - 키 자격 증명 모음은 TDE에 사용할 다음과 같은 속성을 포함해야 합니다.
   - [일시 삭제](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-ovw-soft-delete)
   - [CLI를 사용한 키 자격 증명 모음 일시 삭제를 사용하는 방법](https://docs.microsoft.com/en-us/azure/key-vault/key-vault-soft-delete-cli) 
- 키는 TDE에 사용할 다음과 같은 특성을 포함해야 합니다.
   - 만료 날짜 없음
   - 비활성화되지 않음
   - *가져오기*, *키 래핑*, *키 래핑 해제* 작업을 수행할 수 있습니다.
   
## <a name="step-1-create-a-server-and-assign-an-azure-ad-identity-to-your-server"></a>1단계. 서버 만들기 및 서버에 Azure AD ID 할당
      cli
      # create server (with identity) and database
      az sql server create -n "ServerName" -g "ResourceGroupName" -l "westus" -u "cloudsa" -p "YourFavoritePassWord99@34" -I 
      az sql db create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 
      

 
## <a name="step-2-grant-key-vault-permissions-to-your-server"></a>2단계. 서버에 Key Vault 권한 부여
      cli
      # create key vault, key and grant permission
      az keyvault create -n "VaultName" -g "ResourceGroupName" 
      az keyvault key create -n myKey -p software --vault-name "VaultName" 
      az keyvault set-policy -n "VaultName" --object-id "ServerIdentityObjectId" -g "ResourceGroupName" --key-permissions wrapKey unwrapKey get list 
      

 
## <a name="step-3-add-the-key-vault-key-to-the-server-and-set-the-tde-protector"></a>3단계. Key Vault 키를 서버에 추가하고 TDE 보호기 설정
  
     cli
     # add server key and update encryption protector
      az sql server key create -g "ResourceGroupName" -s "ServerName" -t "AzureKeyVault" -u "FullVersionedKeyUri 
      az sql server tde-key update -g "ResourceGroupName" -s "ServerName" -t AzureKeyVault -u "FullVersionedKeyUri" 
      
  
  > [!Note]
> 키 자격 증명 모음 이름 및 키 이름의 조합된 길이는 94자를 초과할 수 없습니다.
> 

>[!Tip]
>Key Vault에서 예제 KeyId: https://contosokeyvault.vault.azure.net/keys/Key1/1a1a2b2b3c3c4d4d5e5e6f6f7g7g8h8h
>
  
## <a name="step-4-turn-on-tde"></a>4단계. TDE 설정 
      cli
      # enable encryption
      az sql db tde create -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" --status Enabled 
      

이제 데이터베이스 또는 데이터 웨어하우스에는 Key Vault의 암호화 키로 TDE가 설정됩니다.

## <a name="step-5-check-the-encryption-state-and-encryption-activity"></a>5단계. 암호화 상태 및 암호화 작업 확인

     cli
      # get encryption scan progress
      az sql db tde show-activity -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

      # get whether encryption is on or off
      az sql db tde show-configuration -n "DatabaseName" -g "ResourceGroupName" -s "ServerName" 

