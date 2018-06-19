---
title: PowerShell - TDE 보호기 회전 - Azure SQL | Microsoft Docs
description: Azure SQL Server에 대해 TDE(투명한 데이터 암호화) 보호기를 회전하는 방법을 알아봅니다.
keywords: ''
services: sql-database
documentationcenter: ''
author: becczhang
manager: jhubbard
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.custom: ''
ms.tgt_pltfrm: ''
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: ryzhang26
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 45dc9d4d9f4681fde06f75e8fa666c6584bcf863
ms.sourcegitcommit: a78fa85609a82e905de9db8b75d2e83257831ad9
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 06/18/2018
ms.locfileid: "35696744"
---
# <a name="rotate-the-transparent-data-encryption-tde-protector-using-powershell"></a>PowerShell을 사용하여 TDE(투명한 데이터 암호화) 보호기 회전 
[!INCLUDE[appliesto-xx-asdb-asdw-xxx-md](../../../includes/appliesto-xx-asdb-asdw-xxx-md.md)]

이 방법 가이드에서는 Azure Key Vault에서 TDE 보호기를 사용하여 Azure SQL Server에 대한 키 회전을 설명합니다. Azure SQL Server의 TDE 보호기를 회전한다는 것은 서버에서 데이터베이스를 보호하는 새 비대칭 키로 전환한다는 것을 의미합니다. 키 회전은 온라인 작업이며 전체 데이터베이스가 아니라 데이터베이스의 데이터 암호화 키만 암호 해독 및 다시 암호화하므로 불과 몇 분 안에 완료됩니다.

이 가이드에서는 서버에서 TDE 보호기를 회전하는 두 가지 옵션을 설명합니다.

> [!NOTE]
> 키 회전을 수행하기 전에 일시 중지된 SQL Data Warehouse를 다시 시작해야 합니다.
>

> [!IMPORTANT]
> 롤오버 후에는 키의 이전 버전을 **삭제하지 마세요**.  키가 롤오버되면 이전 데이터베이스 백업처럼 일부 데이터가 이전 키로 암호화됩니다. 
>

## <a name="prerequisites"></a>사전 요구 사항

- 이 방법 가이드는 Azure Key Vault의 키를 Azure SQL Database 또는 데이터 웨어하우스에 대한 TDE 보호기로 이미 사용 중이라고 가정합니다. [BYOK를 사용하는 투명한 데이터 암호화 지원](transparent-data-encryption-byok-azure-sql.md)을 참조하세요.
- Azure PowerShell 버전 3.7.0 이상이 설치되어 실행 중이어야 합니다. 
- [권장되지만 선택 사항임] HSM(하드웨어 보안 모듈) 또는 로컬 키 저장소에서 TDE 보호기에 대한 키 자료를 먼저 만들고 키 자료를 Azure Key Vault로 가져옵니다. 자세히 알아보려면 [HSM(하드웨어 보안 모듈) 및 Key Vault 사용에 대한 지침](https://docs.microsoft.com/azure/key-vault/key-vault-get-started)을 따르세요.

## <a name="option-1-auto-rotation"></a>옵션 1: 자동 회전

동일한 키 이름 및 키 자격 증명 모음 아래에 새 버전의 기존 TDE 보호기 키를 Key Vault에 생성합니다. Azure SQL 서비스는 이 새 버전을 사용하여 24시간 이내 시작됩니다. 

[Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey) cmdlet을 사용하여 새 버전의 TDE 보호기를 만들려면

   ```powershell
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>
   ```

## <a name="option-2-manual-rotation"></a>옵션 2: 수동 회전

이 옵션은 [Add-AzureKeyVaultKey](/powershell/module/azurerm.keyvault/add-azurekeyvaultkey), [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) 및 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet을 사용하여 새 키 이름 또는 다른 키 자격 증명 모음 아래에 있을 수 있는 완전히 새로운 키를 추가합니다. 

>[!NOTE]
>키 자격 증명 모음 이름 및 키 이름의 조합된 길이는 94자를 초과할 수 없습니다.
>

   ```powershell
   # Add a new key to Key Vault
   Add-AzureKeyVaultKey `
   -VaultName <KeyVaultName> `
   -Name <KeyVaultKeyName> `
   -Destination <HardwareOrSoftware>

   # Add the new key from Key Vault to the server
   Add-AzureRmSqlServerKeyVaultKey `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>   
  
   <# Set the key as the TDE protector for all resources 
   under the server #>
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```
  
## <a name="other-useful-powershell-cmdlets"></a>다른 유용한 PowerShell cmdlet

- TDE 보호기를 Microsoft 관리에서 BYOK 모드로 전환하려면 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet을 사용합니다.

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type AzureKeyVault `
   -KeyId <KeyVaultKeyId> `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName>
   ```

- TDE 보호기를 BYOK 모드에서 Microsoft 관리로 전환하려면 [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) cmdlet을 사용합니다.

   ```powershell
   Set-AzureRmSqlServerTransparentDataEncryptionProtector `
   -Type ServiceManaged `
   -ServerName <LogicalServerName> `
   -ResourceGroup <SQLDatabaseResourceGroupName> 
   ``` 

## <a name="next-steps"></a>다음 단계

- 보안 위험이 발생할 경우 잠재적으로 손상된 TDE 보호기를 제거하는 방법 알아보기: [잠재적으로 손상된 키 제거](transparent-data-encryption-byok-azure-sql-remove-tde-protector.md) 

- TDE에 대한 Bring Your Own Key 지원 시작: [PowerShell을 사용하고 Key Vault에서 사용자 고유 키를 사용하여 TDE 설정](transparent-data-encryption-byok-azure-sql-configure.md)
