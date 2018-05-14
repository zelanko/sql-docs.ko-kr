---
title: Azure SQL Database 및 데이터 웨어하우스의 투명한 데이터 암호화 | Microsoft Docs
description: SQL Database 및 데이터 웨어하우스의 투명한 데이터 암호화에 대해 간략히 설명합니다. 이 문서에서는 서비스 관리 투명한 데이터 암호화 및 Bring Your Own Key를 비롯하여 구성에 대한 장점과 옵션에 대해 설명합니다.
keywords: ''
author: becczhang
manager: craigg
editor: ''
ms.prod: ''
ms.reviewer: ''
ms.suite: sql
ms.prod_service: sql-database, sql-data-warehouse
ms.service: sql-database
ms.component: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.date: 04/10/2018
ms.author: rebeccaz
monikerRange: = azuresqldb-current || = sqlallproducts-allversions
ms.openlocfilehash: bc007f1021c68c782d8a3e2e426cad3c43f3047a
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 05/03/2018
---
# <a name="transparent-data-encryption-for-sql-database-and-data-warehouse"></a>SQL Database 및 데이터 웨어하우스의 투명한 데이터 암호화
[!INCLUDE[appliesto-xx-asdb-xxxx-xxx-md](../../../includes/appliesto-xx-asdb-xxxx-xxx-md.md)]

투명한 데이터 암호화를 통해 악의적인 활동의 위협으로부터 Azure SQL Database 및 Azure 데이터 웨어하우스를 보호할 수 있습니다. 이 기능은 응용 프로그램을 변경할 필요 없이 미사용 데이터베이스, 연결된 백업 및 트랜잭션 로그 파일의 실시간 암호화 및 암호 해독을 수행합니다.

투명한 데이터 암호화는 데이터베이스 암호화 키라는 대칭 키를 사용하여 전체 데이터베이스의 저장소를 암호화합니다. 이 데이터베이스 암호화 키는 투명한 데이터 암호화 보호기에 의해 보호됩니다. 보호기는 서비스 관리 인증서(서비스 관리 투명한 데이터 암호화) 또는 Azure Key Vault에 저장된 비대칭 키(Bring Your Own Key) 중 하나입니다. 서버 수준에서 투명한 데이터 암호화 보호기를 설정합니다. 

데이터베이스 시작 시 암호화된 데이터베이스 암호화 키는 암호 해독된 후 SQL Server 데이터베이스 엔진 프로세스의 데이터베이스 파일을 암호 해독 및 재암호화하는 데 사용됩니다. 투명한 데이터 암호화를 통해 페이지 수준에서 데이터의 실시간 I/O 암호화 및 암호 해독을 수행합니다. 각 페이지는 메모리로 읽어올 때 암호 해독되며 디스크에 기록하기 전에 암호화됩니다. 투명한 데이터 암호화에 대한 일반적인 설명은 [투명한 데이터 암호화](transparent-data-encryption.md)를 참조하세요.

Azure 가상 머신에서 실행되는 SQL Server는 Key Vault의 비대칭 키를 사용할 수도 있습니다. 구성 단계는 SQL Database에서 비대칭 키를 사용하는 것과 다릅니다. 자세한 내용은 [Azure Key Vault를 사용하여 확장 가능 키 관리(SQL Server)](extensible-key-management-using-azure-key-vault-sql-server.md)를 참조하세요.

## <a name="service-managed-transparent-data-encryption"></a>서비스 관리 투명한 데이터 암호화

Azure의 투명한 데이터 암호화에서 데이터베이스 암호화 키가 기본 제공 서버 인증서로 보호되도록 기본 설정됩니다. 기본 제공 서버 인증서는 각 서버에 대해 고유합니다. 데이터베이스가 지리적 복제 관계에 있는 경우 주 및 지역 보조 데이터베이스는 주 데이터베이스의 부모 서버 키로 보호됩니다. 두 개의 데이터베이스가 동일한 서버에 연결된 경우에는 동일한 기본 제공 인증서를 공유합니다. Microsoft는 적어도 90일마다 이러한 인증서를 자동으로 회전시킵니다.

Microsoft는 지역 복제 및 복원에 필요한 대로 원활하게 키를 이동하고 관리합니다. 

> [!IMPORTANT]
> 새로 만든 모든 SQL 데이터베이스는 서비스 관리 투명한 데이터 암호화를 사용하여 기본적으로 암호화됩니다. 2017년 5월 이전의 기존 데이터베이스와 복원, 지리적 복제 및 데이터베이스 복사를 통해 만든 데이터베이스는 기본적으로 암호화되지 않습니다.
>

## <a name="bring-your-own-key"></a>Bring Your Own Key

Bring Your Own Key 지원을 통해 투명한 데이터 암호화 키를 제어하고 이 키에 액세스할 수 있는 사용자 및 시기를 제어할 수 있습니다. Key Vault는 Azure 클라우드 기반 외부 키 관리 시스템으로 투명한 데이터 암호화가 Bring Your Own Key 지원과 통합된 최초의 키 관리 서비스입니다. Bring Your Own Key를 통해 데이터베이스 암호화 키는 Key Vault에 저장된 비대칭 키로 보호됩니다. 비대칭 키는 Key Vault를 벗어나지 않습니다. 서버에 키 자격 증명 모음에 대한 권한이 있으면 서버는 Key Vault를 통해 여기에 기본 키 작업 요청을 보냅니다. 비대칭 키는 서버 수준에서 설정되고 해당 서버 아래의 모든 데이터베이스는 해당 키를 상속합니다.

이제 Bring Your Own Key 지원을 통해 키 회전 및 키 자격 증명 모음 사용 권한과 같은 키 관리 작업을 제어할 수 있습니다. 키를 삭제하고 모든 암호화 키에 대해 감사/보고 기능을 사용할 수도 있습니다. Key Vault는 중앙 집중식 키 관리를 제공하고 밀접하게 모니터링된 하드웨어 보안 모듈을 사용합니다. Key Vault는 규정 준수를 충족하도록 키와 데이터의 관리를 분리하는 기능을 제공합니다. Key Vault에 대한 자세한 내용은 [Key Vault 설명서 페이지](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)를 참조하세요.

SQL Database 및 데이터 웨어하우스에 대한 Bring Your Own Key 지원에서 투명한 데이터 암호화에 대해 자세히 알아보려면 [Bring Your Own Key 지원에서 투명한 데이터 암호화](transparent-data-encryption-byok-azure-sql.md)를 참조하세요.

Bring Your Own Key 지원에서 투명한 데이터 암호화를 사용하기 시작하려면 [PowerShell을 사용하는 Key Vault에서 사용자 고유 키를 사용하여 투명한 데이터 암호화 설정](transparent-data-encryption-byok-azure-sql-configure.md) 방법 가이드를 참조하세요.

## <a name="move-a-transparent-data-encryption-protected-database"></a>투명한 데이터 암호화로 보호되는 데이터베이스 이동

Azure 내에서의 작업을 위해 데이터베이스 암호를 해독할 필요는 없습니다. 원본 데이터베이스 또는 주 데이터베이스에서 투명한 데이터 암호화 설정은 대상에서 투명하게 상속됩니다. 포함된 작업에는 다음이 포함됩니다.
- 지역 복원
- 셀프 서비스 특정 시점 복원
- 삭제된 데이터베이스 복원
- 활성 지역 복제
- 데이터베이스 복사본 만들기

투명한 데이터 암호화로 보호된 데이터베이스를 내보내면 데이터베이스의 내보낸 콘텐츠는 암호화되지 않습니다. 내보낸 이 콘텐츠는 암호화되지 않은 BACPAC 파일에 저장됩니다. 새 데이터베이스 가져오기를 마친 후에 BACPAC 파일을 적절하게 보호하고 투명한 데이터 암호화를 사용하도록 설정해야 합니다.

예를 들어 BACPAC 파일을 온-프레미스 SQL Server 인스턴스에서 내보낼 경우 새 데이터베이스의 가져온 콘텐츠는 자동으로 암호화되지 않습니다. 마찬가지로 온-프레미스 SQL Server 인스턴스로 BACPAC 파일을 내보낸 경우 새 데이터베이스도 자동으로 암호화되지 않습니다.

한 가지 예외는 SQL 데이터베이스 간에 내보내는 경우입니다. 새 데이터베이스에서 투명한 데이터 암호화가 사용되지만 PACPAC 파일 자체는 암호화되지 않습니다.

## <a name="manage-transparent-data-encryption-in-the-azure-portal"></a>Azure Portal에서 투명한 데이터 암호화 관리

Azure Portal을 통해 투명한 데이터 암호화를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다. 

데이터베이스 수준에서 투명한 데이터 암호화를 설정합니다. 데이터베이스에서 투명한 데이터 암호화를 사용하려면 [Azure Portal](https://portal.azure.com)로 이동하고 Azure 관리자 또는 참가자 계정으로 로그인합니다. 사용자 데이터베이스에서 투명한 데이터 암호화 설정을 찾습니다. 기본적으로 서비스 관리 투명한 데이터 암호화가 사용됩니다. 데이터베이스를 포함하는 서버에서 투명한 데이터 암호화 인증서가 자동으로 생성됩니다. 

![서비스 관리 투명한 데이터 암호화](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

서버 수준에서 투명한 데이터 암호화 보호기로도 알려져 있는 투명한 데이터 암호화 마스터 키를 설정합니다. Bring Your Own Key 지원에서 투명한 데이터 암호화를 사용하고 Key Vault에서 키를 사용하여 데이터베이스를 보호하려면 서버에서 투명한 데이터 암호화 설정을 참조하세요. 

![Bring Your Own Key 지원에서 투명한 데이터 암호화](./media/transparent-data-encryption-azure-sql/tde-byok-support.png) 

## <a name="manage-transparent-data-encryption-by-using-powershell"></a>PowerShell을 사용하여 투명한 데이터 암호화 관리

PowerShell을 통해 투명한 데이터 암호화를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다. 

| Cmdlet | Description |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |데이터베이스에서 투명한 데이터 암호화 활성화 또는 비활성화|
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |데이터베이스에서 투명한 데이터 암호화 상태 가져오기 |
| [Get-Azure-Rm-Sql-Database-Transparent-Data-Encryption-Activity](/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |데이터베이스에 대한 암호화 진행률 확인 |
| [Add-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |SQL Server 인스턴스에 Key Vault 키 추가 |
| [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |SQL Server 인스턴스의 Key Vault 키 가져오기  |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |SQL Server 인스턴스의 투명한 데이터 암호화 보호기 설정 |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |투명한 데이터 암호화 보호기 가져오기 |
| [Remove-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |SQL Server 인스턴스에서 Key Vault 키 제거 |
|  | |

## <a name="manage-transparent-data-encryption-by-using-transact-sql"></a>Transact-SQL을 사용하여 투명한 데이터 암호화 관리

마스터 데이터베이스의 **dbmanager** 역할 관리자 또는 멤버인 로그인을 사용하여 데이터베이스에 연결합니다.

| Command | Description |
| --- | --- |
| [ALTER DATABASE(Azure SQL Database)](/sql/t-sql/statements/alter-database-azure-sql-database) | SET ENCRYPTION ON/OFF는 데이터베이스를 암호화 또는 암호 해독합니다. |
| [sys.dm_database_encryption_keys](/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |연결된 데이터베이스 암호화 키 및 데이터베이스의 암호화 상태에 대한 정보를 반환합니다. |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |연결된 데이터베이스 암호화 키 및 각 데이터 웨어하우스 노드의 암호화 상태에 대한 정보를 반환합니다. | 
|  | |

Transact-SQL을 사용하여 Key Vault에서 키를 투명한 데이터 암호화 보호기를 전환할 수 없습니다. PowerShell 또는 Azure Portal을 사용합니다.

## <a name="manage-transparent-data-encryption-by-using-the-rest-api"></a>REST API를 사용하여 투명한 데이터 암호화 관리
 
REST API를 통해 투명한 데이터 암호화를 구성하려면 Azure 소유자, 참가자 또는 SQL 보안 관리자로 연결되어 있어야 합니다. 

| Command | Description |
| --- | --- |
|[서버 만들기 또는 업데이트](/rest/api/sql/servers/createorupdate)|SQL Server 인스턴스에 Azure Active Directory ID 추가(Key Vault에 액세스 권한을 부여하는 데 사용됨)|
|[서버 키 만들기 또는 업데이트](/rest/api/sql/serverkeys/createorupdate)|SQL Server 인스턴스에 Key Vault 키 추가|
|[서버 키 삭제](/rest/api/sql/serverkeys/delete)|SQL Server 인스턴스에서 Key Vault 키 제거|
|[서버 키 가져오기](/rest/api/sql/serverkeys/get)|SQL Server 인스턴스에서 특정 Key Vault 키 가져오기|
|[서버별 서버 키 나열](/rest/api/sql/serverkeys/listbyserver)|SQL Server 인스턴스의 Key Vault 키 가져오기 |
|[암호화 보호기 만들기 또는 업데이트](/rest/api/sql/encryptionprotectors/createorupdate)|SQL Server 인스턴스의 투명한 데이터 암호화 보호기 설정|
|[암호화 보호기 가져오기](/rest/api/sql/encryptionprotectors/get)|SQL Server 인스턴스의 투명한 데이터 암호화 보호기 가져오기|
|[서버별 암호화 보호기 나열](/rest/api/sql/encryptionprotectors/listbyserver)|SQL Server 인스턴스의 투명한 데이터 암호화 보호기 가져오기 |
|[투명한 데이터 암호화 구성 만들기 또는 업데이트](/rest/api/sql/transparentdataencryptions/createorupdate)|데이터베이스에서 투명한 데이터 암호화 활성화 또는 비활성화|
|[투명한 데이터 암호화 구성 가져오기](/rest/api/sql/transparentdataencryptions/get)|데이터베이스에서 투명한 데이터 암호화 구성 가져오기|
|[투명한 데이터 암호화 구성 결과 나열](/rest/api/sql/transparentdataencryptionactivities/ListByConfiguration)|데이터베이스에 대한 암호화 결과 가져오기|

## <a name="next-steps"></a>다음 단계

- 투명한 데이터 암호화에 대한 일반적인 설명은 [투명한 데이터 암호화](transparent-data-encryption.md)를 참조하세요.
- SQL Database 및 데이터 웨어하우스에 대한 Bring Your Own Key 지원에서 투명한 데이터 암호화에 대해 자세히 알아보려면 [Bring Your Own Key 지원에서 투명한 데이터 암호화](transparent-data-encryption-byok-azure-sql.md)를 참조하세요.
- Bring Your Own Key 지원에서 투명한 데이터 암호화를 사용하기 시작하려면 [PowerShell을 사용하는 Key Vault에서 사용자 고유 키를 사용하여 투명한 데이터 암호화 설정](transparent-data-encryption-byok-azure-sql-configure.md) 방법 가이드를 참조하세요.
- Key Vault에 대한 자세한 내용은 [Key Vault 설명서 페이지](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault)를 참조하세요.
