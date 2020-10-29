---
title: Azure Key Vault의 고객 관리형 키와 관련된 일반적인 오류
description: Azure Key Vault에서 TDE(투명한 데이터 암호화) 및 고객 관리형 키를 사용하여 액세스 문제 및 일반 오류를 식별하고 해결하는 방법에 대해 알아봅니다.
ms.custom: seo-lt-2019
helpviewer_keywords:
- troublshooting, tde akv
- tde akv configuration, troubleshooting
- tde troubleshooting
author: jaszymas
ms.prod: sql
ms.technology: security
ms.reviewer: vanto
ms.topic: conceptual
ms.date: 11/06/2019
ms.author: jaszymas
monikerRange: = azuresqldb-current || = azure-sqldw-latest || = sqlallproducts-allversions
ms.openlocfilehash: 2eb908b1d63b70453aeff0e650f93b7c4e794520
ms.sourcegitcommit: 22e97435c8b692f7612c4a6d3fe9e9baeaecbb94
ms.translationtype: HT
ms.contentlocale: ko-KR
ms.lasthandoff: 10/27/2020
ms.locfileid: "92679255"
---
# <a name="common-errors-for-transparent-data-encryption-with-customer-managed-keys-in-azure-key-vault"></a>Azure Key Vault의 고객 관리 키를 통한 투명한 데이터 암호화의 일반적인 오류

[!INCLUDE[asdb-asdbmi-asa](../../../includes/applies-to-version/asdb-asdbmi-asa.md)]

이 문서에서는 [Azure Key Vault에서 고객 관리 키와 함께 TDE(투명한 데이터 암호화)](/azure/sql-database/transparent-data-encryption-byok-azure-sql)를 사용하도록 구성된 데이터베이스에 액세스할 수 없는 Azure Key Vault 키 액세스 문제를 파악하고 해결하는 방법을 설명합니다.

## <a name="introduction"></a>소개
TDE가 Azure Key Vault에서 고객 관리 키를 사용하도록 구성된 경우 데이터베이스를 온라인 상태로 유지하려면 이 TDE 보호기에 지속적으로 액세스할 수 있어야 합니다.  논리 SQL 서버가 Azure Key Vault의 고객 관리형 TDE 보호기에 대한 액세스 권한을 잃게 되면 데이터베이스는 적절한 오류 메시지와 함께 모든 연결을 거부하고 Azure Portal에서 해당 상태를 ‘액세스할 수 없음’으로 변경합니다.

처음 8시간 동안 기본 Azure Key Vault 키 액세스 문제가 해결되면 데이터베이스가 자동으로 복구되고 온라인 상태가 됩니다. 즉, 일시적인 모든 네트워크 중단 시나리오의 경우 사용자 작업이 필요하지 않으며 데이터베이스는 자동으로 온라인 상태가 됩니다. 대부분의 경우 기본 Key Vault 키 액세스 문제를 해결하려면 사용자 작업이 필요합니다. 

액세스할 수 없는 데이터베이스가 더 이상 필요 하지 않은 경우 즉시 삭제하여 비용 발생을 중지할 수 있습니다. Azure Key Vault 키에 대한 액세스가 복원되고 데이터베이스가 다시 온라인 상태가 될 때까지 데이터베이스에 대한 기타 모든 작업은 허용되지 않습니다. 고객 관리 키로 암호화된 데이터베이스에 액세스할 수 없는 동안에는 서버에서 고객 관리 키에서 서비스 관리 키로 TDE 옵션을 변경할 수도 없습니다. 이 기능은 TDE 보호기에 대한 권한이 해지된 상태에서 무단 액세스로부터 데이터를 보호하는 데 필요합니다. 

데이터베이스가 8시간 넘게 액세스할 수 없게 된 후에는 더 이상 자동으로 복구되지 않습니다. 해당 기간 후에 필요한 Azure Key Vault 키 액세스가 복원된 경우 데이터베이스를 다시 온라인 상태로 전환하려면 수동으로 키 액세스의 유효성을 다시 검사해야 합니다. 이 경우 데이터베이스를 다시 온라인 상태로 만들려면 데이터베이스 크기에 따라 상당한 시간이 소요될 수 있습니다. 데이터베이스가 다시 온라인 상태가 되면 [장애 조치(failover) 그룹](/azure/sql-database/sql-database-auto-failover-group), PITR 기록, 태그 등 이전에 구성한 설정이 모두 **손실됩니다** . 따라서 가능한 한 빨리 기본 Key Vault 문제를 인식하고 해결할 수 있는 [작업 그룹](/azure/azure-monitor/platform/action-groups)을 사용하여 알림 시스템을 구현하는 것이 좋습니다. 

## <a name="common-errors-causing-databases-to-become-inaccessible"></a>데이터베이스에 액세스할 수 없는 일반적인 오류

Key Vault로 TDE를 사용할 때 발생하는 문제는 대부분 다음 구성 오류 중 하나 때문에 발생합니다.

### <a name="the-key-vault-is-unavailable-or-doesnt-exist"></a>Key Vault를 사용할 수 없거나 존재하지 않습니다.

- Key Vault를 실수로 삭제되었습니다.
- Azure Key Vault에 대해 방화벽이 구성되었지만 이 방화벽에서 Microsoft 서비스에 대한 액세스를 허용하지 않습니다.
- 일시적인 네트워크 오류로 인해 Key Vault를 사용할 수 없습니다.

### <a name="no-permissions-to-access-the-key-vault-or-the-key-doesnt-exist"></a>Key Vault 또는 키에 액세스할 수 있는 권한이 없습니다.

- 키가 실수로 삭제되었거나, 사용하지 않도록 설정되었거나, 키가 만료되었습니다.
- 논리 SQL Server 인스턴스 APPID를 실수로 삭제했습니다.
- 논리 SQL Server 인스턴스를 다른 구독으로 이동했습니다. 논리 서버를 다른 구독으로 이동했으면 새 APPID를 만들어야 합니다.
- 키의 APPID에 부여된 권한이 부족합니다(가져오기, 래핑 및 래핑 해제를 포함하지 않음).
- 논리 SQL Server 인스턴스 APPID에 대한 권한이 철회되었습니다.

## <a name="identify-and-resolve-common-errors"></a>일반적인 오류 식별 및 해결

이 섹션에서는 가장 일반적인 오류의 문제 해결 단계를 설명합니다.

### <a name="missing-server-identity"></a>누락된 서버 ID

**오류 메시지**

_401 AzureKeyVaultNoServerIdentity - 서버 ID가 서버에 올바르게 구성되어 있지 않습니다. 지원 담당자에게 문의하세요._

**검색**

다음 cmdlet 또는 명령을 사용하여 ID가 논리 SQL Server 인스턴스에 할당되었는지 확인합니다.

- Azure PowerShell: [Get-AzureRMSqlServer](/powershell/module/AzureRM.Sql/Get-AzureRmSqlServer?view=azurermps-6.13.0) 

- Azure CLI: [az-sql-server-show](/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-show)

**마이그레이션**

다음 cmdlet 또는 명령을 사용하여 논리 SQL Server 인스턴스의 Azure AD ID(APPID)를 구성합니다.

- Azure PowerShell: [Set-AzureRmSqlServer](/powershell/module/azurerm.sql/set-azurermsqlserver?view=azurermps-6.13.0)(`-AssignIdentity` 옵션 사용)

- Azure CLI: [az sql server 업데이트](/cli/azure/sql/server?view=azure-cli-latest#az-sql-server-update)(`--assign_identity` 옵션 사용)

Azure Portal에서 Key Vault로 이동한 다음 **액세스 정책** 으로 이동합니다. 다음 단계를 완료합니다. 

 1. **새로 추가** 단추를 사용하여 이전 단계에서 만든 서버의 APPID를 추가합니다. 
 1. 다음 키 사용 권한을 할당합니다. Get, 래핑 및 래핑 해제 

자세한 내용은 [Assign an Azure AD identity to your server](/azure/sql-database/transparent-data-encryption-byok-azure-sql-configure#assign-an-azure-ad-identity-to-your-server)(서버에 Azure AD ID 할당)를 참조하세요.

> [!IMPORTANT]
> Key Vault로 TDE의 초기 구성 후에 논리 SQL Server 인스턴스를 새 테넌트로 이동한 경우 Azure AD ID를 구성하는 단계를 반복하여 새 APPID를 만듭니다. 그런 다음 Key Vault에 APPID를 추가하고 키에 올바른 권한을 할당합니다. 
>

### <a name="missing-key-vault"></a>누락된 Key Vault

**오류 메시지**

_503 AzureKeyVaultConnectionFailed - Azure Key Vault에 연결하려는 시도가 실패했으므로 서버에서 작업을 완료할 수 없습니다._

**검색**

키 URI 및 Key Vault를 식별하려면:

1. 다음 cmdlet 또는 명령을 사용하여 특정 논리 SQL Server 인스턴스의 키 URI를 가져옵니다.

    - Azure PowerShell: [Get-AzureRmSqlServerKeyVaultKey](/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey?view=azurermps-6.13.0)

    - Azure CLI: [az-sql-server-tde-key-show](/cli/azure/sql/server/tde-key?view=azure-cli-latest#az-sql-server-tde-key-show) 

1. 키 URI를 사용하여 Key Vault 식별:

    - Azure PowerShell: $MyServerKeyVaultKey 변수의 속성을 검사하여 Key Vault에 대한 세부 정보를 가져올 수 있습니다.

    - Azure CLI: Key Vault에 대한 자세한 내용은 반환된 서버 암호화 보호기를 검사합니다.

**마이그레이션**

Key Vault 사용 가능 여부 확인:

- Key Vault를 사용할 수 있고 논리 SQL Server 인스턴스에서 액세스할 수 있는지 확인합니다.
- Key Vault가 방화벽 뒤에 있는 경우 Microsoft 서비스에서 Key Vault에 액세스할 수 있도록 확인란이 선택되어 있는지 확인합니다.
- Key Vault를 실수로 삭제한 경우 구성을 처음부터 완료해야 합니다.


### <a name="missing-key"></a>누락된 키

**오류 메시지**

_404 ServerKeyNotFound - 요청된 서버 키를 현재 구독에서 찾을 수 없습니다._ 

_409 ServerKeyDoesNotExists - 서버 키가 없습니다._

**검색**

키 URI 및 Key Vault를 식별하려면:

- [누락된 Key Vault](#missing-key-vault)의 cmdlet 또는 명령을 사용하여 논리 SQL Server 인스턴스에 추가된 키 URI를 식별합니다. 명령을 실행하면 키 목록이 반환됩니다.

**마이그레이션**

TDE 보호기가 Key Vault에 있는지 확인합니다.

1. Key Vault를 식별하고 Azure Portal의 Key Vault로 이동합니다.
1. 키 URI로 식별되는 키가 있는지 확인합니다.

### <a name="missing-permissions"></a>누락된 권한

**오류 메시지**

_401 AzureKeyVaultMissingPermissions - 서버에서 Azure Key Vault에 필요한 사용 권한이 누락되었습니다._

**검색**

키 URI 및 Key Vault를 식별하려면: 

- [누락된 Key Vault](#missing-key-vault)의 cmdlet 또는 명령을 사용하여 논리 SQL Server 인스턴스에서 사용하는 Key Vault를 식별합니다.

**마이그레이션**

논리 SQL Server 인스턴스에 Key Vault에 대한 사용 권한 및 키에 액세스할 수 있는 권한이 있는지 확인:

- Azure Portal에서 Key Vault > **액세스 정책** 으로 이동합니다. 논리 SQL Server 인스턴스 APPID를 찾습니다.  
- APPID가 있는 경우 APPID에 다음 키 사용 권한이 있는지 확인합니다. Get, 래핑 및 래핑 해제.
- APPID가 없는 경우 **새로 추가** 단추를 사용하여 추가합니다. 

## <a name="getting-tde-status-from-the-activity-log"></a>활동 로그에서 TDE 상태 가져오기

Azure Key Vault 키 액세스 이슈로 인한 데이터베이스 상태를 모니터링할 수 있도록 Azure Resource Manager URL 및 Subscription+Resourcegroup+ServerName+DatabaseName을 기반으로 리소스 ID에 대한 [활동 로그](/azure/service-health/alerts-activity-log-service-notifications)에 다음 이벤트가 로그됩니다. 

**서비스가 Azure Key Vault 키에 대한 액세스 권한을 잃은 경우 발생하는 이벤트**

EventName: MakeDatabaseInaccessible 

상태: 시작됨 

설명: 데이터베이스에서 Azure Key Vault 키에 대한 액세스 권한을 잃어 현재 액세스할 수 없음: <error message>   

 

**자동 복구를 위한 8시간 대기 시간이 시작되는 경우 발생하는 이벤트** 

EventName: MakeDatabaseInaccessible 

상태: InProgress 

설명: 데이터베이스에서 Azure Key Vault 키 액세스 권한이 8시간 이내에 사용자에 의해 다시 설정될 때까지 대기 중입니다.   

 

**데이터베이스가 자동으로 다시 온라인 상태가 되는 경우 발생하는 이벤트**

EventName: MakeDatabaseAccessible 

상태: 성공 

설명: Azure Key Vault 키에 대한 데이터베이스 액세스 권한이 다시 설정되었으며 현재 데이터베이스가 온라인 상태입니다. 

 

**8시간 이내에 문제가 해결되지 않고 Azure Key Vault 키 액세스의 유효성을 수동으로 검사해야 하는 경우 발생하는 이벤트** 

EventName: MakeDatabaseInaccessible 

상태: 성공 

설명: 데이터베이스에 액세스할 수 없으므로 사용자가 Azure Key Vault 오류를 확인하고 키 유효성 검사를 다시 사용하여 Azure Key Vault 키에 대한 액세스를 다시 설정해야 합니다. 

 

**키 유효성 검사를 수동으로 수행한 후 db가 온라인 상태가 되는 경우 발생하는 이벤트**

EventName: MakeDatabaseAccessible 

상태: 성공 

설명: Azure Key Vault 키에 대한 데이터베이스 액세스 권한이 다시 설정되었으며 현재 데이터베이스가 온라인 상태입니다. 

 

**Azure Key Vault 키 액세스의 유효성 다시 검사가 성공하고 db를 다시 온라인 상태로 전환하는 경우 발생하는 이벤트**

EventName: MakeDatabaseAccessible 

상태: 시작됨 

설명: Azure Key Vault 키에 대한 데이터베이스 액세스 권한을 복원하는 중입니다. 

 

**Azure Key Vault 키 액세스의 유효성을 다시 검사하지 못한 경우 발생하는 이벤트**

EventName: MakeDatabaseAccessible 

상태: 실패 

설명: Azure Key Vault 키에 대한 데이터베이스 액세스 권한을 복원하지 못했습니다. 


## <a name="next-steps"></a>다음 단계

- [Azure Resource Health](/azure/service-health/resource-health-overview)를 확인하세요.
- 이메일/SMS/푸시/음성, 논리 앱, 웹후크, ITSM 또는 Automation Runbook과 같은 기본 설정에 따라 알림 및 경고를 받도록 [작업 그룹](/azure/azure-monitor/platform/action-groups)을 설정합니다.