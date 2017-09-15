---
title: "Azure SQL Database 및 데이터 웨어하우스에 대한 TDE | Microsoft Docs"
description: "SQL Database 및 데이터 웨어하우스의 투명한 데이터 암호화에 대해 간략히 설명합니다. 이 문서에서는 서비스 관리 TDE 및 Bring Your Own Key를 비롯하여 구성에 대한 옵션과 장점에 대해 설명합니다."
keywords: 
services: sql-database
documentationcenter: 
author: becczhang
manager: jhubbard
editor: 
ms.assetid: 
ms.service: sql-database
ms.custom: security
ms.workload: 
ms.tgt_pltfrm: 
ms.devlang: na
ms.topic: article
ms.date: 08/07/2017
ms.author: rebeccaz
ms.translationtype: HT
ms.sourcegitcommit: 46b16dcf147dbd863eec0330e87511b4ced6c4ce
ms.openlocfilehash: 35c94a39989fda76ea023588b2d7a3aa4e463262
ms.contentlocale: ko-kr
ms.lasthandoff: 09/05/2017

---


# <a name="transparent-data-encryption-for-azure-sql-database-and-data-warehouse"></a>Azure SQL Database 및 데이터 웨어하우스의 투명한 데이터 암호화

[!INCLUDE[tsql-appliesto-xxxxxx-asdb-asdw-xxx-md](../../../includes/tsql-appliesto-xxxxxx-asdb-asdw-xxx-md.md)]

TDE(투명한 데이터 암호화)를 사용하면 응용 프로그램을 변경할 필요 없이 사용하지 않는 데이터베이스, 연결된 백업 및 트랜잭션 로그 파일에 대한 실시간 암호화 및 암호 해독을 수행하여 악의적인 활동의 위협에 대해 Azure SQL Database 및 데이터 웨어하우스를 보호할 수 있습니다.

TDE는 DEK(데이터베이스 암호화 키)라는 대칭 키를 사용하여 전체 데이터베이스의 저장소를 암호화합니다. 이 데이터베이스 암호화 키는 서비스 관리 인증서(“Service-Managed TDE”) 또는 Azure Key Vault에 저장된 비대칭 키(“Bring Your Own Key”) 중 하나인 TDE 보호기로 보호됩니다. TDE 보호기는 서버 수준에서 설정됩니다. 

데이터베이스 시작 시 암호화된 DEK는 암호 해독된 후 SQL 엔진 프로세스의 데이터베이스 파일을 암호 해독 및 재암호화하는 데 사용됩니다. TDE를 통해 페이지 수준에서 데이터의 실시간 I/O 암호화 및 암호 해독을 수행합니다. 각 페이지는 메모리로 읽어올 때 암호 해독되며 디스크에 기록하기 전에 암호화됩니다. TDE에 대한 일반적인 설명은 [TDE(투명한 데이터 암호화)](transparent-data-encryption.md)를 참조하세요.

Azure 가상 컴퓨터에서 실행되는 SQL Server는 Key Vault의 비대칭 키를 사용할 수도 있습니다. 구성 단계는 Azure SQL Database에서 비대칭 키를 사용하는 것과 다릅니다. 자세한 내용은 [Azure Key Vault를 사용한 확장 가능 키 관리(SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)를 참조하세요.

## <a name="service-managed-tde"></a>서비스 관리 TDE

Azure에서 TDE에 대한 기본 설정은 데이터베이스 암호화 키가 기본 제공 서버 인증서로 보호되는 것입니다. 기본 제공 서버 인증서는 각 서버에 대해 고유합니다. 데이터베이스가 지리적 복제 관계에 있는 경우 주 및 지리적 보조 데이터베이스는 주 데이터베이스의 부모 서버 키로 보호됩니다. 두 개의 데이터베이스가 동일한 서버에 연결된 경우에는 동일한 기본 제공 인증서를 공유합니다. Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전시킵니다.

Microsoft는 지리적 복제 및 복원에 필요한 대로 원활하게 키를 이동 및 관리합니다. 

> [!IMPORTANT]
> 새로 만든 모든 SQL 데이터베이스는 서비스 관리 TDE를 사용하여 기본적으로 암호화됩니다. 2017년 5월 이전의 기존 데이터베이스와 복원, 지리적 복제 및 데이터베이스 복사를 통해 만든 데이터베이스는 기본적으로 암호화되지 않습니다.
>

## <a name="bring-your-own-key"></a>Bring Your Own Key

BYOK(Bring Your Own Key) 지원을 통해 사용자는 TDE 암호화 키를 제어하고 이 키에 액세스할 수 있는 사용자 및 시기를 제어할 수 있습니다. AKV(Azure Key Vault)는 Azure의 클라우드 기반 외부 키 관리 시스템으로, TDE가 BYOK 지원을 통합한 최초의 키 관리 서비스입니다. BYOK를 통해 데이터베이스 암호화 키는 AKV에 저장된 비대칭 키로 보호됩니다. 비대칭 키는 Key Vault에서 비밀로 유지됩니다. 서버에 키 자격 증명 모음에 대한 권한이 있으면 서버는 Key Vault 서비스를 통해 키 자격 증명 모음에 기본 키 작업 요청을 보냅니다. 비대칭 키는 서버 수준에서 설정되고 해당 서버 아래 모든 데이터베이스에 의해 상속됩니다. BYOK 지원을 통해 사용자는 키 회전, 키 자격 증명 모음 권한, 키 삭제, 모든 암호화 키에 감사/보고 사용 등의 키 관리 작업을 제어할 수 있습니다. Key Vault는 중앙 키 관리를 제공하고, 엄격하게 모니터링되는 HSM(하드웨어 보안 모듈)을 활용하며, 키 및 데이터 관리의 분리를 유도하여 규정 준수를 충족하도록 합니다. Key Vault에 대한 자세한 내용은 [Key Vault 설명서 페이지](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)를 방문하세요.

Azure SQL Database 및 데이터 웨어하우스에 대한 BYOK 기반 TDE 지원에 대해 자세히 알아보려면 [Bring Your Own Key 지원으로 투명한 데이터 암호화](transparent-data-encryption-byok-azure-sql.md)를 참조하세요.

BYOK 기반 TDE 지원 사용을 시작하려면 [PowerShell을 사용하고 Key Vault에서 사용자 고유 키를 사용하여 투명한 데이터 암호화 설정](transparent-data-encryption-byok-azure-sql-configure.md) 방법 가이드를 방문하세요.

## <a name="moving-a-tde-protected-database"></a>TDE로 보호되는 데이터베이스 이동

Azure 내에서의 작업을 위해 데이터베이스 암호를 해독할 필요는 없습니다. 원본 데이터베이스 또는 주 데이터베이스의 TDE 설정은 대상에서 투명하게 상속됩니다. 여기에는 다음과 관련된 작업이 포함됩니다.
- 지리적 복원
- 셀프 서비스 특정 시점 복원
- 삭제된 데이터베이스 복원
- 활성 지리적 복제
- 데이터베이스 복사본 만들기

TDE로 보호된 데이터베이스를 내보낼 때 데이터베이스의 내보낸 콘텐츠는 암호화되지 않습니다. 내보낸 이 콘텐츠는 암호화되지 않은 BACPAC 파일에 저장됩니다. 새 데이터베이스 가져오기가 완료되면 BACPAC 파일을 적절하게 보호하고 TDE를 사용하도록 설정해야 합니다.

예를 들어 BACPAC 파일을 온-프레미스 SQL Server에서 내보낼 경우 새 데이터베이스의 가져온 콘텐츠는 자동으로 암호화되지 않습니다. 마찬가지로 온-프레미스 SQL Server로 BACPAC 파일을 내보낸 경우 새 데이터베이스도 자동으로 암호화되지 않습니다.

한 가지 예외는 Azure SQL Database에서(로) 내보낼 경우입니다. 새 데이터베이스에서 TDE가 사용되지만 PACPAC 파일 자체는 암호화되지 않습니다.

## <a name="managing-transparent-data-encryption-in-the-azure-portal"></a>Azure Portal에서 투명한 데이터 암호화 관리

Azure Portal을 통해 TDE를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다. 

데이터베이스 수준에서 투명한 데이터 암호화가 설정됩니다. 데이터베이스에서 TDE를 사용하려면 [Azure Portal](https://portal.azure.com)을 방문하고 Azure 관리자 또는 참가자 계정으로 로그인합니다. 사용자 데이터베이스에서 TDE 설정을 찾습니다. 기본적으로 서비스 관리 TDE가 사용되며 데이터베이스를 포함하는 서버에 대해 TDE 인증서가 자동으로 생성됩니다. 

![서비스 관리 TDE](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

TDE 마스터 키라고도 하는 *TDE 보호기*는 서버 수준에서 설정됩니다. Bring Your Own Key 기반 TDE 지원을 사용하고 Azure Key Vault의 키를 사용하여 데이터베이스를 보호하려면 서버의 TDE 설정으로 이동하세요. 

![BYOK 기반 TDE 지원](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="managing-transparent-data-encryption-using-powershell"></a>PowerShell을 사용하여 투명한 데이터 암호화 관리

PowerShell을 통해 TDE를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다. 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |데이터베이스에 대해 TDE를 사용하거나 사용하지 않도록 설정합니다.|
| [Get-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |데이터베이스에 대한 TDE 상태를 가져옵니다. |
| [Get-AzureRmSqlDatabaseTransparentDataEncryptionActivity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |데이터베이스에 대한 암호화 진행률을 확인합니다. |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |SQL Server에 Key Vault 키를 추가합니다. |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |SQL Server의 Key Vault 키를 가져옵니다. |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |SQL Server에 대 한 TDE 보호기를 설정합니다. |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |TDE(투명한 데이터 암호화) 보호기를 가져옵니다. |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |SQL Server에 Key Vault 키를 제거합니다. |
|  | |

## <a name="managing-transparent-data-encryption-using-transact-sql"></a>Transact-SQL을 사용하여 투명한 데이터 암호화 관리

관리자 또는 master 데이터베이스의 **dbmanager** 역할 구성원인 로그인을 사용하여 데이터베이스에 연결합니다.

| Command | Description |
| --- | --- |
| [ALTER DATABASE(Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) | SET ENCRYPTION ON/OFF를 사용하여 데이터베이스를 암호화 또는 암호 해독합니다. |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |연결된 데이터베이스 암호화 키 및 데이터베이스의 암호화 상태에 대한 정보를 반환합니다. |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |연결된 데이터베이스 암호화 키 및 각 데이터 웨어하우스 노드의 암호화 상태에 대한 정보를 반환합니다. | 
|  | |

Transact-SQL을 사용하여 TDE 보호기를 Azure Key Vault의 키로 전환할 수 없습니다. PowerShell 또는 Azure Portal을 사용하세요.

## <a name="managing-transparent-data-encryption-using-rest-api"></a>REST API를 사용하여 투명한 데이터 암호화 관리
 
REST API를 통해 TDE를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다. 

| Command | Description |
| --- | --- |
|[서버 만들기 또는 업데이트](/rest/api/sql/servers/createorupdate)|AAD ID를 SQL Server에 추가합니다(Key Vault에 액세스 권한을 부여하는 데 사용됨).|
|[서버 키 만들기 또는 업데이트](/rest/api/sql/serverkeys/createorupdate)|SQL Server에 Key Vault 키를 추가합니다.|
|[서버 키 삭제](/rest/api/sql/serverkeys/delete)|SQL Server에 Key Vault 키를 제거합니다.|
|[서버 키 가져오기](/rest/api/sql/serverkeys/get)|SQL Server에서 특정 Key Vault 키를 가져옵니다.|
|[서버별 서버 키 나열](/rest/api/sql/serverkeys/listbyserver)|SQL Server의 Key Vault 키를 가져옵니다.|
|[암호화 보호기 만들기 또는 업데이트](/rest/api/sql/encryptionprotectors/createorupdate)|SQL Server에 대 한 TDE 보호기를 설정합니다.|
|[암호화 보호기 가져오기](/rest/api/sql/encryptionprotectors/get)|SQL Server에 대한 TDE 보호기를 가져옵니다.|
|[서버별 암호화 보호기 나열](/rest/api/sql/encryptionprotectors/listbyserver)|SQL Server의 TDE 보호기를 가져옵니다.|
|[투명한 데이터 암호화 구성 만들기 또는 업데이트](/rest/api/sql/transparentdataencryptions/createorupdate)|데이터베이스에 대해 TDE를 사용하거나 사용하지 않도록 설정합니다.|
|[투명한 데이터 암호화 구성 가져오기](/rest/api/sql/transparentdataencryptions/get)|데이터베이스에 대한 TDE 구성을 가져옵니다.|
|[투명한 데이터 암호화 구성 결과 나열](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|데이터베이스에 대한 암호화 결과를 가져옵니다.|

## <a name="next-steps"></a>다음 단계

- TDE에 대한 일반적인 설명은 [TDE(투명한 데이터 암호화)](transparent-data-encryption.md)를 참조하세요.

- Azure SQL Database 및 데이터 웨어하우스에 대한 BYOK 기반 TDE 지원에 대해 자세히 알아보려면 [Bring Your Own Key 지원으로 투명한 데이터 암호화](transparent-data-encryption-byok-azure-sql.md)를 방문하세요.

- BYOK 기반 TDE 지원 사용을 시작하려면 [PowerShell을 사용하고 Key Vault에서 사용자 고유 키를 사용하여 투명한 데이터 암호화 설정](transparent-data-encryption-byok-azure-sql-configure.md) 방법 가이드를 방문하세요.

- Key Vault에 대한 자세한 내용은 [Key Vault 설명서 페이지](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)를 참조하세요.

